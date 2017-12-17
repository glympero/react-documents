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
  module: {
      rules: [{
          loader: 'babel-loader',   //define the loader
          test: /\.js$/,            //files that end with .js
          exclude: /node_modules/   //dont run babel inside node_modules
      }]
  }
- tell babel to use env and react presets by creating a separate .babelrc file
  in the root of project. This is a json file

#### Source Maps
- add devtool inside webpack as a sibling to module to track errors inside our code
- development setup: cheap-module-eval-source-map

module: {
    rules: [{
        ...
    }]
},
devtool: 'cheap-module-eval-source-map'

#### webpack dev server (live-server alternative)

- installation : yarn add webpack-dev-server@2.5.1
- Lots of options but only one is needed 'contentbase' : which tells the dev server
  where to find our public files.
- add devServer inside webpack as a sibling to module. devServer is an object
  and we configure inside the contentBase which is the absolute path to public folder

  *module: {
      rules: [{
          ...
      }]
  },
  devtool: 'cheap-module-eval-source-map',
  devServer: path_join(__dirname, "public")*
- add a script to package.json in order to run it. Inside scripts:
  "dev-server": "webpack-dev-server",

Now with only
yarn run dev-server, we can watch our changes and use babel for
transforming JSX.

IMPORTANT!
Does not use bundle.js file in the public folder, but from the file which
is generated from dev-server and keeps it in memory

### SCSS vs SASS
(SCSS uses semi-colomns and curly braces, SASS does not)

- Create a new folder in src directory : /styles
- Add file inside styles : styles.css
- Add new rule to webpack with two loaders: css-loader, style-loader
- add loaders locally : yarn add style-loader css-loader
- configure rule by adding an array of loaders with 'use': use: [ 'style-loader', 'css-loader' ]
module: {
    rules: [{
        loader: 'babel-loader',
        test: /\.js$/,
        exclude: /node_modules/
    },{
        test:/\.css$/,
        use: [ 'style-loader', 'css-loader' ]
    }]
},
- Go to app.js and import the css file from styles folder
import './styles/styles.css';

- To use scss we need two new loaders to transform scss to css that browsers understand
- yarn add sass-loader
