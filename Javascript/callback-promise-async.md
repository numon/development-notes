## What is a Callback?
### Why do we even need Callback in JavaScript?
- Web Browser is a playground for JavaScript. JavaScript enables interactive web pages along with best friend HTML & CSS
- They are many events in the web browser and JavaScript’s role 
to response to the events and show something in action. Events could be user-generated like mouse click or typing
- The fundamental reason for a callback is to run code in response to an event. 
To register a callback function for an event, you need to be able to pass it to another function, 
which is responsible for binding the event and callback together

We use callback everyday. For example, the example below print Hello in response to clicking event to the body of a webpage

```javascript

const body = document.getElementsByTagName('body')[0];

function callback() {
  console.log('Hello');
}

body.addEventListener('click', callback);

```

## Why Callback
Let’s make a function called loadScript which loads scripts and modules asynchronously

```javascript
function loadScript(src) {
  // creates a <script> tag and append it to the page
  // this causes the script with given src to start loading and run when complete
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}

loadScript('/my/script.js');
```
### problem:
- The script is executed “asynchronously”, as it starts loading now, but runs laters, when the function has already finished
- If there is any code below loadScript(...), it does not wait until the script loading finish and would NOT work

### SOLUTION
Let’s add a callback function as a second argument to loadScript that should execute when the script loads

```javascript
// define function loadScript
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(script);

  document.head.append(script);
}

// call function

loadScript('/my/script.js', function() {
  // the callback runs after the script is loaded
  newFunction(); // so now it works
  ...
});
```

## Callback in Callback
```javascript
loadScript('/my/script.js', function(script) {

  loadScript('/my/script2.js', function(script) {

    loadScript('/my/script3.js', function(script) {
      // ...continue after all scripts are loaded
    });

  })

});

## Promise
Promise is introduced in ES6 to resolve the callback hell issue and handle asynchronous operations
```javascript
function loadScript(src) {
  return new Promise(function(resolve, reject) {
    let script = document.createElement('script');
    script.src = src;

    script.onload = () => resolve(script);
    script.onerror = () => reject(new Error(`Script load error for ${src}`));

    document.head.append(script);
  });
}

// USAGE
let promise = loadScript("https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js");

promise.then(
  script => alert(`${script.src} is loaded!`),
  error => alert(`Error: ${error.message}`)
);

promise.then(script => alert('Another handler...'));
```

## printString function 

### using Callback
First, make a printString function that print (console.log) the string and callback parameterized function with interval (setTimeout) of 1 seconds (1000 ms)
```javascript
function printString(string, callback) {
  setTimeout(
    () => {
      console.log(string)
      callback()
    },
    1 * 1000 // 1s
   )
}
```
Let’s try to print the letter A, B , C in the order
```javascript
function printAll() {
  printString("A", () => {
    printString("B", () => {
      printString("C", () => {})
    })
  })
}

printAll()
```
### printString function to print string in Promise way
```javascript
function printString(string) {
  return new Promise((resolve, reject) => {
    setTimeout(
      () => {
        console.log(string)
        resolve()
      },
      1 * 1000
      )
  })
}

function printAll() {
  printString("A")
  .then(() => {
    return printString("B")
  })
  .then(() => {
    return printString("C")
  })
}

printAll()
```
