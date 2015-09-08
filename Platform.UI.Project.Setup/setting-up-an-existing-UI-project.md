# Setting up an existing UI project
These instructions relate to setting up a UI project that has already been configured to do the following:

- Sass based CSS preprocessing using the C/C++ port of Sass called **LibSass** which is implemented via **Node-Sass**
- Implementing basic **npm** (Node Package Manager) based task running to facilitate the following:
  - Automatic node-sass based Sass compilation as files are updated
  - Automatic post-processing of CSS to autoprefix browser prefixes as CSS files are updated
  - Automatic reloading of connected browsers
  - Synchronised browsing of connected browsers

## The setup will involve:
1. Installing the basic environment required
2. Installing the required packages
3. Preparing to go
4. Running tasks

## 1. Installing the basic environment

The core platform is Nodejs. **Skip this step** if it is already installed although you may wish to upgrade.

### Nodejs

Node.js® is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications.

It is required for it's **Node Package Manager (npm)** which installs, publishes and manages node programs.

The majority of the build workflow utilities and plugins are Node.js packages.

#### Installing Nodejs
1. Go to https://nodejs.org/ and click 'install'

#### Updating Nodejs
1. Follow these instructions: http://exponential.io/blog/install-or-upgrade-nodejs-on-windows/

### Links
- https://nodejs.org/


## 2. Installing required packages
**Assumption:** All required files are source controlled as part of the project.

1. In command prompt navigate into the project folder
2. ```npm install```


## 3. Preparing to go
1. In command prompt navigate into the project folder
2. Update the **caniuse** database which is used by **Autoprefixer**

  ```npm update caniuse-db```


## 4. Running tasks
- In command prompt navigate into the project folder

### During Development
- ```npm run <TASK-NAME>``` e.g. ```npm run development```

### For Deployment
- ```npm run <TASK-NAME>``` e.g. ```npm run deploy```
