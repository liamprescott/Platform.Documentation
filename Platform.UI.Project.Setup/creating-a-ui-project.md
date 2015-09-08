# Creating a UI project
Instructions about setting up a simple project based on using:

- npm as the pipeline tool
- node-sass for Sass compilation
- autoprefixer to post process Sass generated CSS
- rimraf to clean distribution folders as part of a 'distribute' build
- nodemon to watch for 'production' file updates and automatically run compilation tasks
- browser-sync to watch for 'distribution' file updates and automatically reload any connected browsers
- parallelshell to run multiple tasks at the same time (nodemon & browser-sync)

### Main steps:
1. Create package.json
2. Install core packages
3. Author npm scripts


## 1. package.json

A package.json contains:
- Standard project properties (name etc)
- An index of dependencies (utilities/packages) required for development
- An index of dependencies required to run a project. We don't need any of these as all our packages are used during build and deployment only.
- A collection of custom scripts that can be run from the CLI (Command Line Interface)

For more information see:
- https://docs.npmjs.com/files/package.json
- http://stackoverflow.com/questions/18875674/whats-the-difference-between-dependencies-devdependencies-and-peerdependencies

### To create
Do one of the following:

1. Copy an existing one and modify
2. Create from scratch
3. Run ```npm init``` via CLI in the root directory and follow the wizard prompts

*Note: may wish to manually add '''private:"true"'''*

This creates the following file:
```
/ project
  - package.json
```


## 2. Install core packages
Next we install the core npm packages.

##### Install options

- Always install with the ```---save-dev``` flag to ensure that they are added to the ```devDependencies```
- Always install locally (via CLI within the project directory) do not add the ```-g``` flag

For more info see: https://docs.npmjs.com/cli/install

##### Accessing a project specific package when not installed globally (without -g)**

For example to check the version number or view the help.

This can be done by running the bin from a **relative path** e.g. on windows ```.\node_modules\.bin\node-sass --version```

- https://lostechies.com/derickbailey/2012/04/24/executing-a-project-specific-nodenpm-package-a-la-bundle-exec/
- http://superuser.com/questions/547446/start-program-from-relative-path


##### Packages:
1. node-sass
2. autoprefixer
3. nodemon
4. browser-sync
5. parrallelshell

### 1. node-sass
```npm install node-sass --save-dev```


### 2. autoprefixer
Autoprefixer requires 2 packages which can be installed simultaneously:

```npm install postcss-cli autoprefixer --save-dev```


- https://github.com/postcss/autoprefixer
- https://github.com/code42day/postcss-cli


### 3. nodemon
Whilst mainly used to automatically restart node applications during development when files change, it can also be used to automatically run build scripts when files change in 'watched' directories.
- https://github.com/remy/nodemon

```npm install nodemon --save-dev```

**To stop** when running (in CLI) enter ```CTRL + C```


### 4. browser-sync
A live reload server & client that will sync connected devices / browsers

```npm install browser-sync --save-dev```

### 5. parallelshell
Runs shell commands in parallel

```npm install parallelshell --save-dev```

See: https://github.com/keithamus/parallelshell


## 3. Author npm scripts
See: [authoring-packagejson-scripts.md](/authoring-packagejson-scripts.md)
