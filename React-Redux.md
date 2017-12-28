## Redux
React-Redux is a state management library, a javascript library that
integrates nicely with react and it allows us to track changing data.

Redux store is just an object which contains app state

### Why need Redux

All components can interact with this GLOBAL redux state container. Can get VALUES or
set values and they can be trully resuable.

With redux each component can define two things:
- what data it NEEDS
- what data it needs to be able to change

### Installation
- yarn add redux@3.7.2
- import { createStore } from 'redux';

createStore is called once to create the store

const store = createStore((state = { count: 0 }) => {
  return state;
});

- state is the current state and since we dont have a constructor function
  we instantiate the default state there.

- store.getState() -> return the current state

### Recap
- to use redux we have to access createStore
- we call this function to actually create store and this store is that thing
  that tracks our changing data over time.
- we have to pass a function in the createStore and that function gets called right
  away and instantiates our state.
- to fetch the current state, we use the store.getState() method

### change data inside redux store

- we change data inside store using a tool called actions.

#### Actions
- action is nothing more than an object that gets sent to the store
- this object describes the type of action we'd like to take

For a calculator, we might have actions like increment, decrement, reset

- In action object, we have to provide a single property : the action type

{
  type: 'INCREMENT'
}

the UPPER case for action name is a convention.

- Then we sent this action (which is an object) to the store by using store.dispatch

store.dispatch({
    type: 'INCREMENT'
});

- Everytime we dispatch an action, the store runs and this action is passed to
  the store as a second parameter called action.

const store = createStore((state = { count: 0 }, action) => {
  switch(action.type) {
    case 'INCREMENT' :
      return {
        count: state.count + 1
      }
    default :
      return state;
  }
});

#### How to watch for changes in the store
store.subscribe is a function and we pass a single function which  gets called
every single time the store changes. A fantastic way to do something when STATE
changes.

store.subscribe(() => {
  console.log(store.getState());
});

#### stop watching for changes (unsubscribe)

const unsubscribe = store.subscribe(() => {
  console.log(store.getState());
});

some action dispatches...

unsubscribe(); //stop listening to further dispatches.


#### How to dispatch an action and pass some data along (dynamic actions)

Pass more than the action.type. Inside dispatch object, except from type we can
pass whatever key-value we want.

store.dispatch({
  type: 'INCREMENT',
  incrementBy: 5
});

### action generators
Action generators are functions that return action objects. So the action.dispatch
calls will be created once and we'll have a function to generate the action objects

### reducer

The function after the createStore is called a reducer. The reducer determines
what to do in the state based of an action.

Key attributes of a reducer:
- 1. Reducers are pure functions
  Pure function have certain qualities:
    A. The output is only determined by the input
      //return new state based on old state and action and dont interact with things outside
    B. Never directly change state and modify actions. Just return a new state


import { combineReducers } from 'redux';

combineReducers will allows us to create multiple functions that define how
a redux application changes

const store = createStore(
    combineReducers({
        expenses: nameOfExpensesReducer,
        filters: nameOfFiltersReducer
    });
);

### multiple reducers
// ADD_EXPENSE
// REMOVE_EXPENSE
// EDIT_EXPENSE
// SET_TEXT_FILTER
// SORT_BY_DATE
// SORT_BY_AMOUNT
// SET_START_DATE
// SET_END_DATE

const demoState = {
    expenses: [{
        id: '212121212',
        description: 'January Rent',
        note: 'This was the last rent paid',
        amount: 54500,
        createdAt: 0
    }],
    filters: {
        text: 'rent',
        sortBy: 'amount',  //date or amount
        startDate: undefined,
        endDate: undefined
    }
};

- Use a single reducer for each root property in our redux store (expenses and filters)
- Then combine those reducers to create the complete store.

### connected components
- they can read the store
- they can dispatch actions to the store

### Organising Redux
Inside src /folder we need the following directories:

- actions -> setup our actions - create our action generators
- reducers -> create Reducers
- store -> configure store
- selectors -> they refer to things that actually query the data (like the function getVisibleExpenses)

- Connect React-Redux in app.js

### High order components
- HOC is a component that renders another component

Let's say we want to take any component we might render and add an admin message just above it!!
We could add this info in every component, but the goal of high order components is to REUSE CODE

Advantages:
- Reuse Code
- Render hijacking
- Prop manipulation
- Abstract state

How to create:
This is a regular component :

const Info = (props) => {
    return (
        <div>
            <h1>Info</h1>
            <p>The info is: {props.info}</p>
        </div>
    );
}

ReactDOM.render(<Info info='Flying next week' />, document.getElementById('app'));

- Step 1: Create a regular function (not a react component)

const withAdminWarning = () => {

}

This function will be called with the component(s) we want to wrap and we'll get
back an alternative version of the passed component, which will be the HOC (AdminInfo)

const AdminInfo = withAdminWarning(Info);

The component (Info) is passed as an argument to the function above like:

//WrappedComponent is in UpperCase as it is a component

const withAdminWarning = (WrappedComponent) => { // WrappedComponent in this case is <Info />
  return (props) => {
    <div>
          <p>This is private info, plese do not share!</p>
          <WrappedComponent {...props}/>
      </div>
  }
}

{..props} : Taking every key value pair on that object and passing them down as props

- We can pass a special prop into the high order component (isAdmin):
ReactDOM.render(<AdminInfo isAdmin={true} info='Flying next week' />, document.getElementById('app'));


## React - redux

Connect store to various components.

It really needs two things:
- A Provider component used once at the root of the application
- A function (connect) that will be used on components that need to connect to redux store

INSTALLATION
- yarn add react-redux@5.0.5

USAGE
- import them to app.js import { Provider } from 'react-redux';
- Wrap the components with a provider component which passed the store to the whole
  application
  <Provider store={store}>
        <AppRouter />
    </Provider>
- To component:
  - import { connect } from 'react-redux'; //connect connects component to store
  - Create a new const for high order component:
    - const ConnectedComponentName = connect(Here Provide info about what we want to connect)(PassComponentToConnectToStore)
    - So we define a function inside connect which let us determine what info from
      the store we want our component to be able to access

      connect((state) => {
          return { //returns an object with key-value pairs from state.
            name: 'George'
          };
      })(ComponentToConnect) // Now name can be used as prop in the component.
      - Export the new High Order Component
