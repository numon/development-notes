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

// Action Type
export const FETCH_INIT = 'FETCH_INIT';
export const FETCH_SUCCESS = 'FETCH_SUCCESS';

// Action Creators 
export const fetchInit = () => ({ type: actionType.FETCH_INIT });

export const addArtsObject = (data) => ({
  type: actionType.FETCH_SUCCESS,
  artObjects: data.artObjects,
  total: data.count,
});

export const fetchError = () => ({
  type: actionType.FETCH_SUCCESS,
});

export const fetchArts = (sortConfig) => (dispatch) => {
  const fetchData = async () => {
    dispatch(fetchInit());
    try {
      const result = await axios(generateURL(sortConfig));
      console.log(result.data);
      dispatch(addArtsObject(result.data));
    } catch (error) {
      dispatch(fetchError());
    }
  };
  fetchData();
};


// Reducer
const initialState = {
  isLoading: true,
  isError: false,
  artObjects: [],
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case actionType.FETCH_INIT:
      return {
        ...state,
        isLoading: true,
        isError: false,
      };
    case actionType.FETCH_SUCCESS:
      return {
        ...state,
        isLoading: false,
        isError: false,
        artObjects: action.artObjects,
        total: action.total,
      };
    case actionType.FETCH_FAILURE:
      return {
        ...state,
        isError: true,
      };
    default:
      return state;
  }
};
}

// Store
import { createStore, applyMiddleware, compose } from 'redux';
import { Provider } from 'react-redux';
import thunk from 'redux-thunk';
import reducer from './store/reducer';

/* eslint-disable no-underscore-dangle */
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
/* eslint-enable */
const middleware = [thunk];
const store = createStore(reducer, composeEnhancers(applyMiddleware(...middleware)));

 
//Subscription and Dispatching

const mapStateToProps = (state) => ({
  artObjects: state.artObjects,
  isError: state.isError,
  isLoading: state.isLoading,
  sortConfig: state.sortConfig,
});

const mapDispatchToProps = (dispatch) => ({
  getArtObjects: (sortConfig) => dispatch(fetchArts(sortConfig)),
});

export default connect(mapStateToProps, mapDispatchToProps)(ItemList);


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

