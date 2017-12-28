## React Router

### installation

- react-router includes both web and native
- react-router-dom only for web
- react-router-native only for native

### Web installation

- yarn add react-router-dom@4.2.2

### Named parameters from react-router-dom

- BrowserRouter will be used once to create the new Router
- Route for every single page by providing the matching path and what to do then

### import to app.js
- import { BrowserRouter, Route } from 'react-router-dom';
- create a JSX const and create the router

const routes = (
  <BrowserRouter>

  </BrowserRouter>
);

- Define the various Routes by adding a Route component and providing two props:
- 1. the path (path="/")
- 2. The component to render which is an component

### historyApiFallback: true
prevent server side rendering by always serving index.html page with webpack

- adjust webpack

*devServer: {
    contentBase: path.join(__dirname, "public"),
    historyApiFallback: true
}*

We tell the dev-server that we're going to be handling routing via client side
code and that it should return this page for all 404 routes like /create

Process:
- go to a page which via server-side rendering will return a 404 (/create)
- the dev-server will see that (the 404) and since we have set the historyApiFallback: true,
  it will return the index.html page.
- index.html will load the bundle.js file which loads for every single page
- the bundle.js will run the router code, determine that the url is /create
  and will show the correct component

### not showing all components that match all paths ("/", "/create")
pass another prop to Route
- exact={true}

### 404 page
Render a component for a route that has not been defined
import Switch from react-router-dom
- When react-router sees Switch, it's going to move through the routes defined
  and it's going to stop when it finds a match
- if it does not found any matching routes, it will go to the final (NotFound)
  which always match as it does not provide a path

### Linking between routes

- Link : <Link to="/routeToGo">Go to This Route</Link> //basic links
- NavLink: <NavLink to="/routeToGo" activeClassName="is-active" exact={true}>Dashboard</NavLink>
  exact only for the first route (to exact math route)
  Declare an is-active class to specify what to apply to link when is active

### React-Router to separate file
- in src /folder create a new folder named : routers /
- create a new file inside routers / AppRouter.js
- AppRouter.js will export a React Component

### Query Strings and URL parameters
React-router passes various props to component:

- history: This is an object and it contains a bunch of properties, most of which
  are method and these allows us to manipulate the history. They allow us to for
  example, redirect the user programmatically via javascript.
- match: Contains params object and why current route is a match.
- location: Contains info about the current url, also shows hash values and query strings

hash is when using url/edit#contact-us, the page will scroll down to the content
which has an id of contact-us

### dynamic urls

- <Route path="/edit/:id" component={EditExpensePage} />
- :id means that it matches everything after / and it gives us access to this value
