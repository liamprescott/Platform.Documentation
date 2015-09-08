# Authoring package.json scripts
Defining some simple tasks to run:

These are defined within the 'scripts' object in *package.json*.

```javascript
{
  "name": "",
  "version": "1.0.0",
  "description": "",
  "main": "",
  "author": "",
  "license": "ISC",
  "private": true,
  "config": {},
  "devDependencies": {},
  "scripts": {
    /* Tasks are defined here */
  }
}
```
## npm Scripts basics
#### Windows command prompt syntax
- **&&** for chaining tasks
- **&** for running tasks simaltaneously
- **<** for inputting the contents (stdin) of a file to a command
- **>** or redirecting output (stdout) of a command and dumping it to a file
- **|** for redirecting output (stdout) of a command and sending it to another command

#### To silence the output of a package
- Add ```-s``` to an ```npm run $package``` command [silences the output from the package](https://docs.npmjs.com/misc/config#default-configs)


## Tasks / Steps
1. Compile main CSS for development
2. Autoprefix CSS
3. Sequence tasks together
4. Automatically run tasks when files change (watching)
5. Setting up synchronised browser testing
6. Create main 'entry point' task
7. Running the project


### 1. Compiling CSS from Sass
This involves use of 3 scripts (to aid reuse later on).
1. ```"compile:css:main"``` is the core task that compiles 'main.scss' to 'main.css'
2. ```"compile:css:deploy"``` calls core with configuration options for development
2. ```"compile:css:dev"``` calls core with configuration options for deployment

```javascript
"scripts": {
  "css:compile:deploy": "npm run css:compile:main -- --source-map false --output-style compressed",
  "css:compile:dev": "npm run css:compile:main -- --source-map true --output-style expanded",
  "css:compile:main": "node-sass style/scss/main.scss style/css/main.css",
}

```


### 2. Autoprefix CSS

Ensure that the caniuse database (added as part of the **autoprefixer** installation) is up to date:
```npm update caniuse-db```

This shows an autoprefixer configured to run via postcss.

```javascript
"scripts": {
  //...Other tasks
  "css:autoprefix": "postcss --use autoprefixer -c postcss-options.json -o style/css/main.css style/css/main.css",
}

```

Please note that this config includes configuring the settings via an options.json located in the project root directory.
```javascript
{
  "autoprefixer": {
    "browsers": "last 2 versions"
  }
}
```

Autoprefixer uses Browserlist to specify target browsers, see:
https://github.com/ai/browserslist#queries


### 3. Sequence tasks together
Sequence together the various tasks into workflows e.g. create CSS 'build' and 'deploy' workflows

```javascript
"scripts": {
  //...Other tasks
  "css:build:deploy": "npm run css:compile:deploy && npm run css:autoprefix",
  "css:build:dev": "npm run css:compile:dev && npm run css:autoprefix",
}

```


### 4. Automatically run tasks when files change (watching)
Watch the file system for changes to files and trigger tasks to run automatically when changes happen.

```javascript
// In this example: watching for changes to .scss files within the style/scss directory
// and running 'npm run build:css' when any file is updated
"scripts": {
  //...Other tasks
  "dev:watch:scss": "nodemon -e scss -w style/scss -x \"npm run css:build:dev\"",
}

```

**Important:**

- To run, the script **must** be enclosed in double quotes("") not single('').
- Therefore these must be **escaped** within the json object (\"...\")  


### 5. Setting up synchronised browser testing

```javascript
// In this example:
// - Trigger browsers to automatically reload any changes are made to the CSS files within the '/styles/css/' folder
// - Proxy URL is configured to local.Platform.UI.Template
"scripts": {
  //...Other tasks
  "dev:browsersync": "browser-sync start --files \"style/css/*.css\" --proxy local.Platform.UI.Template",
}

```

For more info / options see: http://www.browsersync.io/docs/command-line/


### 6. Create main 'entry point' task
Create a single run script that will set up the project to run the following tasks at the same time (in parallel):
- Sass => CSS automatic compilation (dev mode)
- Synchronised browser testing

```javascript
// This
"scripts": {
  //...Other tasks
  "development": "parallelshell \"npm run dev:browsersync\" \"npm run dev:watch:scss\""
}

```

### 7. Running the project
Now simply running ```npm run development``` sets everything going.

**To stop** (a nodemon task) when running (in CLI) ```CTRL + C```
