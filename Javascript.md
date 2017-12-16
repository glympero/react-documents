## javascript

### try - catch

try {
  //the block of code we want to execute
} catch (e) {
  console.log(e)''
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
