# Redux

## Redux LC

Component -> Dispatches -> Action -> Reducers -> Central Store -> triggers Subscription -> Components

Immutable Update Patterns on reduxjs.org: http://redux.js.org/docs/recipes/reducers/ImmutableUpdatePatterns.html


## Redux example

```jsx harmony
const redux =require('redux');
const createStore = redux.createStore;
const initialState = {
  counter: 0
}

// reducer

const rootReducer = (state = initialState, action) => {
  if(action.type === 'INC_COUNTER') {
  return {
    ...state,
    counter: state.counter +1
  }
}

//Store
cont store = createStore(rootReducer);
console.log(store.getStore();

//Subscription
store.subscribe(()=> {
  console.log('Subscribe', store.getState())
})


//Dispatching

store.dispatch({
  type: 'INC_COUNTER'
});

store.dispatch({
  type: 'ADD_COUNTER',
  payload: 10
});


```

## React-redux 

```jsx harmony
import { Provider } from 'react-redux'
  <Provider store=store>
    <App />
  </Provider>
  
const mapStateToProps = (state) => {
  return {
    globalState: state
    }
}

const mapDispatchToProps = dispatch => {
  return {
    incCount: () => dispatch({type: 'INCREMENT'})
  }
}

export defautl connect(mapStateToProps, mapDispatchToProps)(Counter)

// merge reducer

import { createStore, combineReducers } from 'redux';

const rootReducer = combineReducers({
  one: firstReducer,
  two: secondReducer
});

const state = createStore(rootReducer);

```
## Update nested state element
```jsx harmony

function updateVeryNestedField(state, action) {
    return {
        ...state,
        first : {
            ...state.first,
            second : {
                ...state.first.second,
                [action.someId] : {
                    ...state.first.second[action.someId],
                    fourth : action.someValue
                }
            }
        }
    }
}

