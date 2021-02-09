
### run saga midlware
```javascript

import createSagaMiddleware from 'redux-saga';
import sagas from './sagas/index';

const sagaMiddleware = createSagaMiddleware();
const middleware = [sagaMiddleware];
const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(...middleware)));
sagaMiddleware.run(sagas);
```


### example saga

```javascript
import {takeEvery, call, put} from "redux-saga/effects";
import {addData, FETCH_DATA} from "./action";
import { takeLatest } from 'redux-saga/effects'

function fetchDataFrom() {
  return fetch('https://swapi.co/api/people/1/')
    .then(response => response.json())
}

function* workerLoadData() {
  const data = yield call(fetchDataFrom);
  yield put(addData(data));
}

export function* watchLoadData() {
  yield takeLatest(FETCH_DATA, workerLoadData)
}
```

In the above example, `takeEvery` allows multiple fetchData instances to be started concurrently.
At a given moment, we can start a new fetchData task while there are still one or more previous fetchData tasks which have not yet terminated.

### handle error

```javascript
function* fetchProducts() {
  const { response, error } = yield call(fetchProductsApi)
  if (response)
    yield put({ type: 'PRODUCTS_RECEIVED', products: response })
  else
    yield put({ type: 'PRODUCTS_REQUEST_FAILED', error })
}
```

Sometimes we start multiple tasks in parallel but we don't want to wait for all of them, we just need to get the winner: the first one that resolves (or rejects). 
The race Effect offers a way of triggering a race between multiple Effects.

```javascript
import { race, call, put, delay } from 'redux-saga/effects'

function* fetchPostsWithTimeout() {
  const {posts, timeout} = yield race({
    posts: call(fetchApi, '/posts'),
    timeout: delay(1000)
  })

  if (posts)
    yield put({type: 'POSTS_RECEIVED', posts})
  else
    yield put({type: 'TIMEOUT_ERROR'})
}

export function* watchAndLog() {
  while (true) {
    const action = yield take('*');
    const state = yield select();

    console.log('action', action);
    console.log('state after', state);
  }
}

export function* loginFlow() {
  while (true) {
    yield take('LOGIN');
    console.log('take FETCH_DATA');
    yield take('LOGOUT');
    console.log('take ADD_DATA');

  }
```
