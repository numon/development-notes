# React Hooks 

## UseState
 ```javascript
 import {useState} from 'react';
 const [inputState, setInputState] = useState({count:0, title:'test'});
 ```
 use multiple useState to separate state and do not update all filds in one state

## UseEffect
 ```javascript
  import {useEffect} from 'react';
  useeffect(()=> {fetch()}, []);
  
  // clean function
  useeffect(()=> {
  fetch()
  return () => console.log('run unmount');
  }, [someData]);
   ```
  first arg - function run after render
  second arg - componentDidMount
  
  can use multiple times 
  useeffect(()=> {}); - will run every time when render function run
  
   If your effect returns a function, React will run it when it is time to clean up:
  
## useCallBack
  useCallback returns a memoized callback
  
  ```javascript
  const Counter = () => {
  const [count, setCount] = useState(0)
  const [otherCounter, setOtherCounter] = useState(0)
  
  const increment = useCallback(() => {
    setCount(count + 1)
  }, [count])
  const decrement = useCallback(() => {
    setCount(count - 1)
  }, [count])
  const incrementOtherCounter = useCallback(() => {
    setOtherCounter(otherCounter + 1)
  }, [otherCounter])

  /*
  const increment = (() => {
    setCount(count + 1)
  })
  const decrement = (() => {
    setCount(count - 1)
  })
  const incrementOtherCounter = (() => {
    setOtherCounter(otherCounter + 1)
  })
  */
  return (
    <>
      Count: {count}
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={incrementOtherCounter}>incrementOtherCounter</button>
    </>
  )
}
  ```
  if you try to click one of the counters, only the functions related to the state that changes are going to be re-instantiated.
  
  
## useRef 
 This hook allows us to access a DOM element imperatively.
 
## useReducer
This hook is used to manage state
```javascript
const reducer = (state, action) => {
  switch (action) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      throw new Error()
  }
}
const Counter = () => {
  const [count, dispatch] = useReducer(reducer, 0)
  return (
    <>
      Counter: {count}
      <button onClick={() => dispatch('INCREMENT')}>+</button>
      <button onClick={() => dispatch('DECREMENT')}>-</button>
    </>
  )
}
```

## useContext

## useMemo
 useMemo returns a memoized value
 ```javascript 
 const App = () => {
    const fooFunction = () => {
        return 'Foo is just Food without D'
    }

    const useMemoResult = React.useMemo(fooFunction, [])
    const useCallbackResult = React.useCallback(fooFunction, [])

    console.log('useMemoResult: ', useMemoResult)
    console.log('useCallbackResult: ', useCallbackResult)

    return <p>Foo is just food without D</p>
}
// RESULT -> React.useMemo runs the fooFunction which returns a string Foo is just Food without D while React.useCallback just returns a fooFunction without calling it
```


## Custom Hooks

all custom hooks can be found here - https://nikgraf.github.io/react-hooks/
