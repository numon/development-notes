
## Curry pattern

### What is currying?

Currying is the process of transforming a function that takes multiple arguments into a series of functions that take one argument at a time. Well that’s the theory.

```javascript
const sum = x => y => x + y;
// returns the number 3
sum (2)(1);
// returns a function y => 2 + y
sum (2);
```
### Functional composition
In functional composition you have a sequence of functions applied all on the same single argument as f(g(x)). This would be your example:
```javascript


// Object oriented approach
const getUglyFirstCharacterAsLower = str
  => str.substr (0, 1).toLowerCase ();
// Functional approach
const curriedSubstring = start => length => str
  => str.substr(start, length);
const curriedLowerCase = str => str.toLowerCase ();
const getComposedFirstCharacterAsLower = str
  => curriedLowerCase (curriedSubstring (0) (1) (str));
```
It is also very popular to use a compose function to compose your functions::
```javascript
const compose = (...fns) =>
  fns.reduce((f, g) => (...args) => f(g(...args)));
```
Using the above-defined functions curriedSubstring and curriedLowerCase you can then use compose to do this:
```javascript
const getNewComposedFirstCharacterAsLower
  = compose (curriedLowerCase, curriedSubstring (0) (1));
if (getComposedFirstCharacterAsLower ('Martin') ===       
    getNewComposedFirstCharacterAsLower ('Martin') {
  console.log ('These two provide equal results.');
}
```
### Practical use in an example project
I have used curried functions when I was developing my NPM package conditional-expression. You can read more about it in my post: How to replace switch and ternaries in functional JavaScript.

You can see the actual code here: https://github.com/MartinGentleman/conditional-expression/blob/master/src/index.js

Using currying led to a better code. I chose syntax:
```javascript
match(something).equals(something).then(result).else(default);
```
instead of:
```javascript
match(something).equals(something, result).else(default);
```

more read hear https://medium.com/front-end-weekly/javascript-es6-curry-functions-with-practical-examples-6ba2ced003b1
