## react

A component is an ES6 class that extends React.component

Each React class must implement one method -> render

class Header extends React.Component {
  render() {
    return (
        <div>
          <h1>Hello</h1>
        </div>
    );
  }
}


### props

pass data inside the component when initialise an instance of a component is known as props

data is passed by using key-value pairs.

key can be anything we like.

### this

inside of react components, we have access to this.

it is a reference to the current instance of the component

React gives access to the props by an object -> this.props

### methods

Add methods inside a class component above render function. access function with this.functionToReference

### method binding

In a component, we can call the constructor method along with the props variables,
initialise them with super(props) and then bind the (this) to the method we want

constructor(props){
  super(props);
  this.method = this.method.bind(this);
}

Now the (this) is available inside our method and is not undefined anymore.

### props vs STATE
props come from above (parent component)
state is defined in the component itself

props cannot be changed by the component itself
state can be changed by component (setState)
### component state

component state allows our components to manage some data. If we have an object with various key-value pairs and when data changes the component will automatically re-render to
reflect those changes.

State is just an object with key-value pairs. We define our initial data and that allows us
to get that rendered to the screen.
State object can be changed by us so we can change it based off of some event, whether
it is a button click, a form submission or something else like the finishing of an
HTTP request that got some JSON data from an API.

WHEN WE DO CHANGE THE STATE THE APPLICATION WILL AUTOMATICALLY GOIND TO RENDER ITSELF
SO REACT IS GOING TO WORK TO GET THE UI UP TO DATE WITH THE NEW STATE VALUES.

IF STATE CHANGES APP WILL RE-RENDER, IF NOT APP WILL STAY THE SAME

#### how to set up state
- <Counter />

- step 1 - come up with some default set of values (Setup default state object)
  this.state = {
    count: 0
  }



- step 2 - The component is rendered with default state values *happens automatically*
  render will called -> Count: 0

- step 3 - call a function to add one to Counter (Change state based on event)

  handleAddOne() {
    //Increase 'count' state by 1
  }
  this.setState(() => {
    return {
      count: this.state.count +1
    }
  });

  if we add prevState as an argument to anonymous function, we have access to current state.
  prevState is our state object before applied changes.

  this.setState((prevState) => {
    return {
      count: prevState.count +1
    }
  });

  call setState, create an anonymous function and return an object
  *the returned object from setState DOES NOT overwrites whole state, just updates certain values*
  *calls to this.setState are asynchronous*


- step 4 - application re-renders *happens automatically*
  render will called -> Count: 1

- step 5.... - Repeat from step 3

#### how to manipulate state from children?

props are one way street. props can get passed from a parent to a child.
Parent -> props -> child YES.
child -> props -> parent NO.

To reverse that one-way dataflow, we need to pass functions in as props !!!!

We define a method in parent class that has all the logic for doing something using this.setState
Then pass that function to the child component, which can call this function that gets passed
down as a prop to actually take that action.

#### manipulate array STATE

this.setState((prevState) => {
  return {
    array: [...prevState.array, new_array_element]
  }
});

this.setState((prevState) => {
  return {
    array: prevState.array.concat([new_array_element])
  }
});

### Stateless functional component
Faster - Easier to test
simple presentational components
cant have state but have props
Also dont have access to this.

const User = (props) => {
  return {
    <div>
      <p>Name: {props.name}</p>
    </div>
  }
}

### class based components

components that manage state

*React Components can be function or can be classes that extend React.Component*

### Default props values

Default props values can be added to components by adding. Can be used when not
passing a prop to component, then default value for prop is used

const Header = (props) => {
  return {
    <div>
      <h1>{props.title}</h1>
      <h2>{props.subtitle}</h1>
    </div
  }
};

Header.defaultProps = {
  title: 'Default value for title'
}


### Way to configure default STATE

class User extends React.Component {
  constructor(props){
    super(props);

    this.state = {
      role: props.role
    }
  }
}

User.defaultProps = {
  role: 'Admin'
}

ReactDOM.render(<User />, document.getElementById('app')); //Role = Admin

ReactDOM.render(<User role="Customer"/>, document.getElementById('app')); //Role = Customer

## React Dev Tools
$r -> shows details about the selected component.

### return function from event handler

<button onClick={(e) => { props.myFunction(withArgument)}}>Click</button>

### filter array

array.filter((element) => {
  return element !== something;
})

## Functions available only to class based components

Lifecycle methods

componentDidMount - Fires when the component first gets mounted to the DOM
- used for fetching data

componentDidUpdate - Fires after the state values change or after the prop values change
- has access to arguments: prevProps and prevState
- used for saving data

componentWillUnmount - Fires before a component goes away
- NO access to arguments: prevProps and prevState

Inside them we have access to this.state and this.props

## passing children to props
What if we had a layout component and we wanted to render a header and a footer
and we wanted some stuff in the middle to be dynamic specific to each individual
page
We pass the JSX through the component

One way is to create our template and pass it via pros to component and then render it
- Create the layout
const Layout = (props) => {
  return (
    <div>
      <p>Header</p>
      {props.content}
      <p>Footer</p>
    </div>
  );
}

- Create the template
const template = (
  <div>
    <h1>Page Title</h1>
    <p>This is my page</p>
  </div>
);

- Pass it via props and render it to component
ReactDOM.render(<Layout content={template}/>, document.getElementById('app'));


Another way: Break the Component to <Layout><p>This is inline</p></Layout> and pass inside the JSX
When you pass something in to a component like this, you have access to it via
the children prop:
const Layout = (props) => {
  return (
    <div>
      <p>Header</p>
      {props.children}
      <p>Footer</p>
    </div>
  );
}

## Server vs Client Routing

### Server Side Routing
Browser detects a URL change and communicates with the server. So browser makes an HTTP
request and the server responds with the HTML and browser goes ahead and renders things.
It completely removes what was shows in the browser and completely replaces it with the
new HTML. This takes time...request-responses-latency-network performance.

### Client Side Routing
Client side handles the re-rendering of the application using client side javascript.
Server request happens only the first time.
We use the HTML history API to watch for url changes and run javascript to implement
those changes.

- 1. Find matching component (/ -> App, /help -> Help, /about -> About)
- 2. Render with javascript function call
