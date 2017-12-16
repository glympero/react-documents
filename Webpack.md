## webpack

webpack is an asset bundler, combines our app with third party libraries and
returns a single javascript file

- allows us to organize our javascript by returning a single javascript file (bundle)
  which contains everything our application needs, including our dependencies and
  our application code.
- Instead of calling multiple javascript files, which can slow down the APPLICATION
  we just make a single request to a single javascript file
- webpack breaks the files to small 'island' which they can communicate using the
  ES6 import/export syntax
- install third party dependencies and import them to different files

### structure

- public/
  -> index.html
  -> bundle.js (the result after running webpack)
- src/
  -> app.js, util.js
- node_modules/
  -> react.js, react-dom.js

### install

yarn add webpack@3.1.0

### configure

- add a script to package.json - "build": "webpack" or "build": "webpack --watch" for continuous watching
- create the configuration file for webpack - webpack.config.js which is a node script
  and we have access to what we would have inside a node.js application


### inside webpack.config.js

- Setup our entry point where application kick off for us
- Tell webpack where to output the final bundle file
- create a module which is an object which contains all of the configuration
  details

  *module.exports is a node thing. its a way to expose something (in this case an object) to another file*


  module.exports = {
    entry: './path to src/appjs',
    output: {
      path: 'THIS NEEDS TO BE ABSOLUTE PATH',
      'filename': 'the name which is common to be bundle.js'
    }
  }

  *__dirname -> contails the path to our project folder*

  *we are going to use path from node to join the __dirname with the public folder*

- Join path to project folder + public folder : *path.join(__dirname, 'public')*

### minimum webpack configuration

const path = require('path');

*module.exports = {
    entry: './src/app.js',
    output: {
        path: path.join(__dirname, 'public'),
        filename: 'bundle.js'
    }
}*

### loaders

A loader lets you customise the behaviour of webpack when it loads a given file

#### Convert JSX to regular javascript using babel
- install necessary dependencies - yarn add babel-core@6.25.0 babel-loader@7.1.1
  babel-core allows to run babel from webpack, babel-loader allows us to teach webpack
  how to load babel
- configure the module object inside webpack module
  *module.exports = {
      entry: './src/app.js',
      output: {
          path: path.join(__dirname, 'public'),
          filename: 'bundle.js'
      },
      module: {

      }
  }*
- define rules which can be how to convert JSX to JS, SCSS to CSS etc
