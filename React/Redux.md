# Redux

## Redux LC

Component -> Dispatches -> Action -> Reducers -> Central Store -> triggers Subscription -> Components


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
