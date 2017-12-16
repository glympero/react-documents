## package.JSON

### install scripts

when we want to add custom code to run like babel, or live-server, we need
to define a new key-value pair with key name: "scripts" like:

"scripts": {
  "name to run from cmd": "the command to run",
  "serve": "live-server public/",
}

- yarn run serve -> runs the serve script from package.json

example with webpack watching changes :

"scripts": {
  "serve": "live-server public/",
  "build": "webpack --watch",
  "build-babel": "babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch"
},
