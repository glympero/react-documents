# react-documents

## live-server
liver-server folder-to-run(which containts the index.html file)

## babel

yarn global add babel-cli@6.24.1

npm install -g babel-cli@6.24.1

### babel-presets

yarn add babel-preset-react@6.24.1 babel-preset-env@1.5.2

### run babel from cmd

babel src/app.js --out-file=public/scripts/app.js --presets=env,react

#### To check changes real time
babel src/app.js --out-file=public/scripts/app.js --presets=env,react —-watch


## JSX

JSX ignores undefined, null, booleans

JSX does not support objects


## ES6

### let + const

let cannot be redefinded but can reassigned

let name = 'george'; //Ok
name = 'Maria'       //Ok

let name = 'unknown'   //Error

const cannot be redefinded and cannot be reassigned

let and const are function scoped and block level scoped

### arrow functions

all arrow functions are anonymous

#### arguments objects

console.log(arguments) inside arrow function not works
no longer bound with arrow functions

####  this keyword - no longer bound
this keyword - no longer bound

es6 arrow functions no longer bind their own 'this' value, instead they use
the 'this' value of the context they were created in

## Data binding

jsx does not have built in data binding
we have to re-render page in order to see results

## Forms

e.preventDefault() -> prevents full page submit

### to get value
e.target.elements.{name of input}.value

## Validations

!!undefined = false

!!valid = true
