## javascript

### try - catch

try {
  //the block of code we want to execute
} catch (e) {
  console.log(e)''
}

### arrow Functions
Arrow functions use whatever this binding is in the parent scope for the classes
which for classes is the class instance

my_function = (arguments) => {
  this. //works without binding
}

### parse

const num = '12';

parseInt(num, 10) return 12

### ES6 import - export

All files running with webpack maintain their local scope

There are two types of exports

- default export (one)
- named exports (multiple)

- utils.js
  const add = (a, b) => a + b;
  const square = (x) => x * x;

  export default add;
  export { square, add as default };

- app.js
  import square from './utils.js'
  import add, { square } from './utils.js'
  console.log(square(3));

#### why use default
- we dont have to use the same name (as named exports)

### import third party dependencies (npm)

- install -> import -> use

### ES6 class properties
Avoid the need to create a constructor for just adding this.state
Avoid the need to manually bind all of our handler methods

All that can be done by setting up the babelrc file in order to support new syntax

The babel plugin is : 'transform-class properties' plugin

Installation
- yarn add babel-plugin-transform-class-properties@6.24.
- configure .babelrc file by adding a new key-value pair "plugins"

{
  "presets": [
    "env",
    "react"
  ],
  "plugins": [
    "transform-class-properties"
  ]
}

Now constructor is not necessary and we can declare properties like
class NewClass {
  state = {
    ......
  }
}
