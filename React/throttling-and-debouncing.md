## Throttling
Throttling enforces a maximum number of times a function can be called over time. 


```javascript
function throttle(func, ms) {

  let isThrottled = false,
    savedArgs,
    savedThis;

  function wrapper() {

    if (isThrottled) { // (2)
      savedArgs = arguments;
      savedThis = this;
      return;
    }

    func.apply(this, arguments); // (1)

    isThrottled = true;

    setTimeout(function() {
      isThrottled = false; // (3)
      if (savedArgs) {
        wrapper.apply(savedThis, savedArgs);
        savedArgs = savedThis = null;
      }
    }, ms);
  }

  return wrapper;
}
```

## Debouncing
Debouncing enforces that a function will not be called again until a certain amount of time has passed since its last call.

```javascript
  function debounce(f, ms) {
  
    let isCooldown = false;
  
    return function() {
      if (isCooldown) return;
  
      f.apply(this, arguments);
  
      isCooldown = true;
  
      setTimeout(() => isCooldown = false, ms);
    };
  
  }
  ```
  
  ```javascript
  import { useMemo, useState } from 'react'

/**
 * Debounce a function by time
 * @param {Function} func
 * @param {Number} delay
 */

export default function useDebounce(func, delay) {
    const [id, setId] = useState(null)

    return useMemo(
        (...args) => {
            if (id) {
                clearTimeout(id)
            } else {
                setId(
                    setTimeout(() => {
                        setId(null)
                        func(...args)
                    }, delay)
                )
            }
        },
        [func]
    )
}
```
