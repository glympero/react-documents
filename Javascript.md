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

### map
array.map((element, index) => {
  access to elements and index
});

### get typeof a value

- typeof value === 'number'

### ES6 Object destructuring

With object destructuring, we are able to take an object and rip it apart.

const person = {
    name: 'George',
    age: 40,
    location: {
        city: 'Athens',
        temp: 8
    }
};

const {name, age} = person; //Matches name = person.name, age = person.age

Renaming:
const {temp: temperature, city } = person.location; //matches and renames
                                                  //temp as temperature = person.location.temp

Default values if value name does not exists:
const {name = 'Anonymous', age} = person;

Default values and renaming:
const {name: firstName = 'Anonymous', age} = person;

### ES6 Array destructuring

const address = [
    'Zarra 23',
    'Arta',
    'Epirus',
    '47100'
];

//inside brackets goes an ordered list of variable names
const [] = address;

const [streetName, cityName, stateName, zipCode] = address;

console.log(`You are in ${streetName}, state ${stateName}`);

We can destruct as many items as we want.

const [, cityName, stateName] = address; //only 2,3 items

const [streetName] = address; //only first item

Default values:
const [streetName = 'No City', cityName, stateName, zipCode] = address;

### ES6 spread operator array

const names = ['George', 'Maria'];

names.push('Danai'); //This does change our arrays
names.concat('Danai'); //This returns a new array and names does not changes
ES6:
  [...names, 'Danai'];

### ES6  Operator Objects

- first need to adjust babel.
- Installation: yarn add babel-plugin-transform-object-rest-spread
- babelrc:
{
  "presets": [
    "env",
    "react"
  ],
  "plugins": [
    "transform-class-properties",
    "transform-object-rest-spread" //Add this plugin
  ]
}

- usage
const user = {
    name: 'Jen',
    age: 24
};

console.log({
    ...user,
    name: "George"
});

New object now has name = George and age = 24

#### Edit an object with Spread Object

- Pass the id as separate parameter and all the parameters we want to change as object

store.dispatch(editExpense(secondExpense.expense.id, {
    note: 'We have to learn it fastttt'
}));

- In the action pass them as they are to the reducer:

//id is the id passed, and updates is the object passed
const editExpense = (id, updates) => ({
    type: 'EDIT_EXPENSE',
    id,
    updates
});

- In the reducer, map the state and just return state if id not matching, and
  if id matches then return the state (...state) along with the updates (...action.updates)
  THIS ALLOWS US TO PASS AS MANY PARAMS AS WE WANT WITHOUT HAVING TO CHECK WHICH
  PARAMS ARE PASSED!!!!!!

*NO need to set a default value to undefined as if we dont set something it's set to undefined!*

### Timestamps
- timestamps are counted in milliseconds and we count the time front or backwards in time
  compared to zero spot.
- Zero spot is January 1st 1970 (unix epoch)
- So positive number come afterwards and negative before

### array sort

function(a,b) {
  if(we want a to come first return)
    return -1
  if(we want b to come first)
    return 1
  if(they want to leave untouched)
    return 0
}
