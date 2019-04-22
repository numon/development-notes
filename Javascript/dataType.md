# Data type
There are 7 basic types in JavaScript.

- `number` for numbers of any kind: integer or floating-point.
- `string` for strings. A string may have one or more characters, there’s no separate single-character type.
- `boolean` for true/false.
- `null` for unknown values – a standalone type that has a single value null.
- `undefined` for unassigned values – a standalone type that has a single value undefined.
- `object` for more complex data structures.
- `symbol` for unique identifiers.

The `typeof` operator allows us to see which type is stored in a variable.
- Two forms: `typeof x` or `typeof(x)`.
- Returns a string with the name of the type, like "string".
- For null returns "object" – this is an error in the language, it’s not actually an object.

## Number
Besides regular numbers, there are so-called “special numeric values” which also belong to this data type: Infinity, -Infinity and NaN.

Infinity represents the mathematical Infinity ∞. It is a special value that’s greater than any number.

We can get it as a result of division by zero:

```javascript
 alert( 1 / 0 ); // Infinity
 ```
Or just reference it directly:

```javascript
 alert( Infinity ); // Infinity
```

## String
A string in JavaScript must be surrounded by quotes.

let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed ${str}`;
In JavaScript, there are 3 types of quotes.

Double quotes: "Hello".
Single quotes: 'Hello'.
Backticks: `Hello`.
Double and single quotes are “simple” quotes. There’s no difference between them in JavaScript.

Backticks are “extended functionality” quotes. They allow us to embed variables and expressions into a string by wrapping them in ${…}, for example:

// embed a variable
```javascript
alert( `Hello, ${name}!` ); // Hello, John!
```

// embed an expression
```javascript
alert( `the result is ${1 + 2}` ); // the result is 3
```

## Boolean
The boolean type has only two values: `true` and `false`.

## Null
The special null value does not belong to any of the types described above.
In JavaScript, null is not a “reference to a non-existing object” or a “null pointer” like in some other languages.
It’s just a special value which represents “nothing”, “empty” or “value unknown”.

## undefined
The special value undefined also stands apart. It makes a type of its own, just like null.
The meaning of undefined is “value is not assigned”.
If a variable is declared, but not assigned, then its value is undefined:
```javascript
let x;
alert(x); // shows "undefined"
```


## Objects


## Link to read
https://developer.mozilla.org/uk/docs/Web/JavaScript/Data_structures
https://learn.javascript.ru/types-intro
https://habr.com/sandbox/19108/
https://javascript.info/types#a-boolean-logical-type
