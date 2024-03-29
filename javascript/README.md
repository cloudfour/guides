<!-- General link aliases -->
[Airbnb JavaScript Style Guide]: https://github.com/airbnb/javascript

<!-- MDN link aliases -->
[Array Destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring
[Array Literal Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_array_literals
[Array.from]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from
[Array.prototype.push]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push
[Function Arguments Object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments
[Function Declaration]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function
[Function Default Parameters]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters
[Function Expression]: https://developer.mozilla.org/en-US/docs/web/JavaScript/Reference/Operators/function
[No eval]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval#Do_not_ever_use_eval!
[NodeList]: https://developer.mozilla.org/en-US/docs/Web/API/NodeList
[Object.assign]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
[Object Destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Object_destructuring
[Object Literal Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_object_literals
[Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax
[Template Literals]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals

<!-- JSPerf link aliases -->
[Adding Array Items]: https://jsperf.com/adding-array-items
[Arrays from Array-Like Objects]: https://jsperf.com/array-like-object-to-array
[Array Destructuring vs Not]: https://jsperf.com/array-destructuring
[Arrays From Iterables]: https://jsperf.com/arrays-from-iterables
[Mapping Over Iterables]: https://jsperf.com/array-from-vs-spread-vs-array-from-map
[Object Destructuring vs Not]: https://jsperf.com/destructure-vs-not
[Shallow Copy Objects]: https://jsperf.com/shallow-copy-objects
[Shallow Copy Arrays]: https://jsperf.com/shallow-copy-arrays
[Spread Syntax for Variadic Functions]: https://jsperf.com/spread-syntax-for-variadic-functions

<!-- ESLint link aliases -->
[array-callback-return]: https://eslint.org/docs/rules/array-callback-return
[function-paren-newline]: https://eslint.org/docs/rules/function-paren-newline
[no-array-constructor]: https://eslint.org/docs/rules/no-array-constructor.html
[no-const-assign]: https://eslint.org/docs/rules/no-const-assign.html
[no-eval]: https://eslint.org/docs/rules/no-eval
[no-new-func]: https://eslint.org/docs/rules/no-new-func
[no-new-object]: https://eslint.org/docs/rules/no-new-object.html
[no-param-reassign]: https://eslint.org/docs/rules/no-param-reassign.html
[no-prototype-builtins]: https://eslint.org/docs/rules/no-prototype-builtins
[no-var]: https://eslint.org/docs/rules/no-var.html
[object-shorthand]: https://eslint.org/docs/rules/object-shorthand.html
[prefer-const]: https://eslint.org/docs/rules/prefer-const.html
[prefer-destructuring]: https://eslint.org/docs/rules/prefer-destructuring
[prefer-object-spread]: https://eslint.org/docs/rules/prefer-object-spread
[prefer-rest-params]: https://eslint.org/docs/rules/prefer-rest-params
[prefer-spread]: https://eslint.org/docs/rules/prefer-spread
[prefer-template]: https://eslint.org/docs/rules/prefer-template.html
[quotes]: https://eslint.org/docs/rules/quotes.html
[quote-props]: https://eslint.org/docs/rules/quote-props.html

<!-- Babel link aliases -->
[@babel/plugin-transform-destructuring]: https://babeljs.io/docs/en/next/babel-plugin-transform-destructuring.html

# JavaScript Guide

*A mostly reasonable approach to JavaScript, inspired by the [Airbnb JavaScript Style Guide].*

## A note on performance vs readability

The end-user experience always come first which means performance should always be top-of-mind. The JSPerf examples used in this guide do not use large datasets. If you find yourself working with large datasets and the suggested approach based on this guide performs slower, don't be afraid to push back on a per-project basis (see [Performance vs Readability](https://blog.usejournal.com/performance-vs-readability-2e9332730790)).

## Table of Contents

1. [Variables](#variables)
2. [Objects](#objects)
3. [Arrays](#arrays)
4. [Destructring](#destructuring)
5. [Strings](#strings)
6. [Functions](#functions)

---

## Variables

### 1.1 Prefer Constants

Use `const` for all of your references; avoid using `var`. 

> Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

#### Examples

🚫 Nope. 🚫

```js
var a = 1;
var b = 2;
```

🎉 Yep! 🎉

```js
const a = 1;
const b = 2;
```

#### Resources

- ESLint:
  - [prefer-const]
  - [no-const-assign]

### 1.2 Reassigning References

If you must reassign references, use `let` instead of `var`. 

> Why? `let` is block-scoped rather than function-scoped like `var`. Function-scoped variables are hoisted which can lead to bugs if you are not careful. Using block-scoped variables makes our code more predictable by giving the variable an explicit scope.

#### Examples

🚫 Nope. 🚫

```js
var count = 1;
if (true) {
  count += 1;
}
```

🎉 Yep! 🎉

```js
let count = 1;
if (true) {
  count += 1;
}
```

#### Resources

- ESLint: [no-var]

### 1.3 Block Scope

Note that both `let` and `const` are block-scoped.

#### Examples

```js
// Both `const` and `let` only exist in the blocks they are defined in.
{
  let a = 1;
  const b = 1;
}
console.log(a); // ReferenceError: a is not defined
console.log(b); // ReferenceError: b is not defined
```

[⇧ top](#javascript-guide)

---

## Objects

### 2.1 Object Creation 

Use the literal syntax for object creation.

> Why? While there are no performance differences between the two approaches, the byte savings and conciseness of the object literal form is what has made it the de facto way of creating new objects.

#### Examples

🚫 Nope. 🚫

```js
const item = new Object();
````

🎉 Yep! 🎉

```js
const item = {};
```

#### Resources

- ESLint: [no-new-object]

### 2.2 Object Shorthand Syntax

Use object shorthand syntax for both methods and property values.

> Why? ECMAScript 6 provides a concise form for defining object literal methods and properties. This syntax can make defining complex object literals much cleaner.

#### Object Method

🚫 Nope. 🚫

```js
const atom = {
  value: 1,
  addValue: function (value) {
    return atom.value + value;
  },
};
```

🎉 Yep! 🎉

```js
const atom = {
  value: 1,
  addValue(value) {
    return atom.value + value;
  },
};
```

#### Object Property

🚫 Nope. 🚫

```js
const generalLeiaOrgana = 'General Leia Organa';

const obj = {
  generalLeiaOrgana: generalLeiaOrgana,
};
```

🎉 Yep! 🎉

```js
const generalLeiaOrgana = 'General Leia Organa';

const obj = {
  generalLeiaOrgana,
};
```

#### Resources

- ESLint: [object-shorthand]

### 2.3 Object Quoted Properties

Only quote properties that are invalid identifiers.

> Why? In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.

#### Examples

🚫 Nope. 🚫

```js
const obj = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};
```

🎉 Yep! 🎉

```js
const obj = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

#### Resources

- ESLint: [quote-props]

### 2.4 Object Prototype Methods

Do not call `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`. 

> Why? In ECMAScript 5.1, `Object.create` was added, which enables the creation of objects with a specified `[[Prototype]]`. `Object.create(null)` is a common pattern used to create objects that will be used as a Map. This can lead to errors when it is assumed that objects will have properties from `Object.prototype`.

#### Examples

🚫 Nope. 🚫

```js
console.log(object.hasOwnProperty(key));
```

🎉 Yep! 🎉

```js
// Good
console.log(Object.prototype.hasOwnProperty.call(object, key));

// Best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
console.log(has.call(object, key));
```

#### Resources

- ESLint: [no-prototype-builtins]

### 2.5 Object Shallow-Copy
  
Prefer the [object spread][Object Literal Spread Syntax] operator over [`Object.assign`][Object.assign] to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

> Why? Object spread is a declarative alternative which may perform better than the more dynamic, imperative Object.assign.

#### Examples

🚫 Nope. 🚫

```js
// This mutates `original` ಠ_ಠ
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 });
delete copy.a; // So does this!

// Works but not preferred
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }
```

🎉 Yep! 🎉

```js
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

#### Resources

- ESLint: [prefer-object-spread]
- JSPerf: [Shallow Copy Objects]

[⇧ top](#javascript-guide)

---

## Arrays

### 3.1 Array Creation

Use the literal syntax for array creation.

> Why? Use of the `Array` constructor to construct a new array is generally discouraged in favor of array literal notation because of the single-argument pitfall and because the `Array` global may be redefined.

#### Examples

🚫 Nope. 🚫

```js
const items = new Array();
```

🎉 Yep! 🎉

```js
const items = [];
```

#### Resources

- ESLint: [no-array-constructor]


### 3.2 Adding Items To Arrays

Use [Array.prototype.push()][Array.prototype.push] instead of direct assignment to add items to an array.

#### Examples

🚫 Nope. 🚫

```js
const someStack = [];
someStack[someStack.length] = 'abracadabra';
```

🎉 Yep! 🎉

```js
const someStack = [];
someStack.push('abracadabra');
```

#### Resources

- JSPerf: [Adding Array Items]

### 3.3 Array Shallow-Copy

Use [array spread syntax][Array Literal Spread Syntax] `...` to shallow-copy arrays.

> Why? Better overall performance.

#### Examples

🚫 Nope. 🚫

```js
// Too slow
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
const len = animals.length;
const animalsCopy = [];
let i;

for (i = 0; i < len; i ++) {
  animalsCopy[i] = animals[i];
}

// Works but is not preferred
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
const animalsCopy = animals.slice();
```

🎉 Yep! 🎉

```js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
const animalsCopy = [...animals];
```

#### Resources:

- JSPerf: [Shallow Copy Arrays]

### 3.4 Arrays From Iterables

To convert an iterable object (e.g. [NodeList]) to an array, use [array spread syntax][Array Literal Spread Syntax] `...` instead of [Array.from].

> Why? Better performance.

#### Examples

🚫 Nope. 🚫

```js
const paragraphs = document.querySelectorAll('p');
const nodes = Array.from(paragraphs);
```

🎉 Yep! 🎉

```js
const paragraphs = document.querySelectorAll('p');
const nodes = [...paragraphs];
```
#### Note

If using Babel with `@babel/preset-env` with option `loose:true`, and are transpiling to older targets in a `.browserlistrc`, you may need to add the following to your Babel config (e.g., `babel.config.js`):

```js
plugins: [
  ...,
  '@babel/plugin-transform-spread',
  ...
]
```

(The default option for this plugin is `loose:false`, which will override the global setting)

#### Resources

- ESLint: [prefer-spread]
- JSPerf: [Arrays From Iterables]

### 3.5 Arrays from Array-Like Objects

Use [`Array.from`][Array.from] for converting an array-like object to an array.

> Why? Not only is it easier to read/type but it also performs better.

#### Examples

🚫 Nope. 🚫

```js
const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };
const arr = Array.prototype.slice.call(arrLike);
```

🎉 Yep! 🎉

```js
const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };
const arr = Array.from(arrLike);
```

#### Resources

- JSPerf: [Arrays from Array-Like Objects]

### 3.6 Mapping Over Iterables

Use [array spread syntax][Array Literal Spread Syntax] `...` instead of [`Array.from`][Array.from] for mapping over iterables.

> Why? Overall better performance.

#### Examples

🚫 Nope. 🚫

```js
const iterable = 'Hello there!';
const upperCase = letter => letter.toUpperCase();
const upperCaseLetters = Array.from(iterable, upperCase);
```

🎉 Yep! 🎉

```js
const iterable = 'Hello there!';
const upperCase = letter => letter.toUpperCase();
const upperCaseLetters = [...iterable].map(upperCase);
```

#### Resources

- JSPerf: [Mapping Over Iterables]

### 3.7 Array Callback Return

Use `return` statements in array method callbacks. It’s okay to omit the `return` if the function body consists of a single statement returning an expression without side effects.
<!-- @TODO: Link later: following [8.2](#arrows--implicit-return).  -->

#### Examples

🚫 Nope. 🚫

```js
inbox.filter(msg => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});
```

🎉 Yep! 🎉

```js
inbox.filter(msg => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});
```

🎉 Also good! 🎉

```js
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// The return can be omitted here.
[1, 2, 3].map(x => x + 1);
```

#### Resources

- ESLint: [array-callback-return]

[⇧ top](#javascript-guide)

---

## Destructuring

### 4.1 Object Destructuring

Use [object destructuring][Object Destructuring] when accessing and using multiple properties of an object.

> Why? Destructuring saves you from creating temporary references for those properties.

#### Examples

🚫 Nope. 🚫

```js
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}
```

🎉 Yep! 🎉

```js
// Good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// Best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

#### Resources

- ESLint: [prefer-destructuring]
- JSPerf: [Object Destructuring vs Not]
- MDN Web Docs: [Object Destructuring]

### 4.2 Array Destructuring

How you destructure an array depends on your situation. Below are a couple of ways to complete the same task.

#### Examples

```js
// This works!
const arr = [1, 2, 3, 4];
const first = arr[0];
const second = arr[1];
const rest = arr.slice(2);

console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4]

// This works great also!
const arr = [1, 2, 3, 4];
const [first, second, ...rest] = arr;

console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4]
```

_**Note:** For performance reasons, strongly consider use of the [@babel/plugin-transform-destructuring] plugin when using [array destructuring][Array Destructuring]._

#### Resources

- Babel Plugin: [@babel/plugin-transform-destructuring]
- JSPerf: [Array Destructuring vs Not]
- MDN Web Docs: [Array Destructuring]

### 4.3 Destructuring for Multiple Return Values

Use [object destructuring][Object Destructuring] for multiple return values, not [array destructuring][Array Destructuring].

> Why? You can add new properties over time or change the order of things without breaking call sites.

#### Examples

🚫 Nope. 🚫

```js
function processInput(input) {
  return [left, right, top, bottom];
}

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);
```

🎉 Yep! 🎉

```js
function processInput(input) {
  return { left, right, top, bottom };
}

// the caller selects only the data they need
const { left, top } = processInput(input);
```

[⇧ top](#javascript-guide)

---

## Strings

### 5.1 Quotes

Use single quotes `''` for strings. The exception is if a string includes a literal `'` single quote, use double quotes `"` instead.

#### Examples

🚫 Nope. 🚫

```js
// Should be single quote.
const name = "Cloud Four";

// Template literals should contain interpolation or newlines.
const name = `Cloud Four`;

// This string has a literal single quote!
const foo = 'What\'s for dinner?';
```

🎉 Yep! 🎉

```js
const name = 'Cloud Four';

// It's okay to use double quotes here.
const foo = "What's for dinner?";
```

#### Resources

- ESLint: [quotes]

### 5.2 Template Literals

When programmatically building up strings, use [template literals][Template Literals] instead of concatenation.

> Why? Template literals (template strings) give you a readable, concise syntax with proper newlines and string interpolation features.

#### Examples

🚫 Nope. 🚫

```js
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}
```

🎉 Yep! 🎉

```js
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

#### Resources

- ESLint: [prefer-template]

### 5.3 Eval

[Never use `eval()`][No eval] on a string, it opens too many vulnerabilities.

#### Resources

- ESLint: [no-eval]

[⇧ top](#javascript-guide)

---

## Functions

### 6.1 Avoid Function Hoisting

Although it is possible to call functions before they are defined via [hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) we prefer to avoid this pattern in our code as it can be confusing.

#### Examples

Although this code works properly it may be more confusing and we generally avoid it:

```js
logFoo();

function logFoo() {
  console.log("foo");
}
```

We would prefer one of the following patterns:

```js
// Define the function before calling
function logFoo() {
  console.log("foo");
}

logFoo();
```

```js
// Import the function
import {logFoo} from './log-foo.js';

logFoo();
```

In files that call a number of helper functions it can be helpful to move those functions to modules, or start the file with a main function that provides a summary of the steps taken in the file. For example:

```js
// The `main` function contains an overview of the file's logic.
// (`main` could be switched to a more meaningful name in context.)
function main() {
  thing1();
  thing2();
  thing3();
  thing4();
}

function thing1() {}
function thing2() {}
function thing3() {}
function thing4() {}

main();
```

Another option is to move helper functions to modules:

```js
// Import helpers so they're defined up front
import {thing1, thing2, thing3, thing4} from './helpers.js';

thing1();
thing2();
thing3();
thing4();
```

### 6.2 Function Arguments Parameter

Never name a function parameter `arguments`.

> Why? This will take precedence over the [`arguments` object][Function Arguments Object] that is given to every function scope.

#### Examples

🚫 Nope. 🚫

```js
function foo(name, options, arguments) {
  // ...
}
```

🎉 Yep! 🎉

```js
function foo(name, options, args) {
  // ...
}
```

#### Resources

- MDN: [Function Arguments Object]

### 6.3 Use Rest Syntax for Function Arguments Object

Use the rest syntax `...args` instead of the `arguments` object.

> Why? Rest arguments are a real Array, and not merely Array-like as the `arguments` object is.

#### Examples

🚫 Nope. 🚫

```js
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// Slow performance
function concatenateAll() {
  const args = Array.from(arguments);
  return args.join('');
}
```

🎉 Yep! 🎉

```js
function concatenateAll(...args) {
  return args.join('');
}
```

#### Resources

- ESLint: [prefer-rest-params]

### 6.4 Function Default Parameters

Use [function default parameter syntax][Function Default Parameters] rather than mutating function arguments.

#### Examples

🚫 Nope. 🚫

```js
function doThings(opts) {
  // If opts is falsey it can introduce bugs.
  opts = opts || {};
  // ...
}

function doThings(opts) {
  if (opts === undefined) {
    opts = {};
  }
  // ...
}
```

🎉 Yep! 🎉

```js
function doThings(opts = {}) {
  // ...
}
```

#### Resources

- MDN: [Function Default Parameters]

### 6.5 Function Default Parameter Side Effects

Avoid side effects with [function default parameters][Function Default Parameters].

> Why? They are confusing to reason about.

#### Examples

🚫 Nope. 🚫

```js
let b = 1;

// Eek!
function count(a = b++) {
  console.log(a);
}

count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

### 6.6 Function Constructor

Never use the `Function` constructor to create a new function.

> Why? Creating a function in this way evaluates a string similarly to `eval()`, which [opens vulnerabilities](#53-eval).

#### Examples

🚫 Nope. 🚫

```js
var add = new Function('a', 'b', 'return a + b');

var subtract = Function('a', 'b', 'return a - b');
```

🎉 Yep! 🎉

```js
var x = function (a, b) {
    return a + b;
};
```

#### Resources

- ESLint: [no-new-func]

### 6.7 Mutating Function Parameters

Never mutate function parameters.

> Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

#### Examples

🚫 Nope. 🚫

```js
function foo(bar) {
    bar = 13;
}

function foo(bar) {
    bar++;
}
```

🎉 Yep! 🎉

```js
function foo(bar) {
    var baz = bar;
}
```

#### Resources

- ESLint: [no-param-reassign]


### 6.8 Spread Syntax for Variadic Functions

Prefer the use of the [spread syntax operator `...`][Spread Syntax] to call variadic functions (a function that accepts a variable number of arguments).

> Why? It’s cleaner, you don’t need to supply a context, and it's easier to compose `new` when compared to using `apply`.

#### Examples

🚫 Nope. 🚫

```js
const args = [1, 2, 3, 4];
Math.max.apply(Math, args);

new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));
```

🎉 Yep! 🎉

```js
const args = [1, 2, 3, 4];
Math.max(...args);

new Date(...[2016, 8, 5]);
```

#### Resources

- ESLint: [prefer-spread]
- JSPerf: [Spread Syntax for Variadic Functions]

[⇧ top](#javascript-guide)

---

## Arrow Functions

TBD...

[⇧ top](#javascript-guide)

---

## Classes & Constructors

TBD...

[⇧ top](#javascript-guide)

---

## Modules

TBD...

[⇧ top](#javascript-guide)

---

## Iterators and Generators

TBD...

[⇧ top](#javascript-guide)

---

## Properties

TBD...

[⇧ top](#javascript-guide)

---

## Variables

TBD...

[⇧ top](#javascript-guide)

---

## Hoisting

TBD...

[⇧ top](#javascript-guide)

---

## Comparison Operators & Equality

TBD...

[⇧ top](#javascript-guide)

---

## Blocks

TBD...

[⇧ top](#javascript-guide)

---

## Control Statements

TBD...

[⇧ top](#javascript-guide)

---

## Comments

TBD...

[⇧ top](#javascript-guide)

---

## Whitespace

TBD...

[⇧ top](#javascript-guide)

---

## Commas

TBD...

[⇧ top](#javascript-guide)

---

## Semicolons

TBD...

[⇧ top](#javascript-guide)

---

## Type Casting & Coercion

TBD...

[⇧ top](#javascript-guide)

---

## Naming Conventions

TBD...

[⇧ top](#javascript-guide)

---

## Accessors

TBD...

[⇧ top](#javascript-guide)

---

## Events

TBD...

[⇧ top](#javascript-guide)

---

## jQuery

TBD...

[⇧ top](#javascript-guide)

---

## ECMAScript 5 Compatibility

TBD...

[⇧ top](#javascript-guide)

---

## ECMAScript 6+ (ES 2015+) Styles

TBD...

[⇧ top](#javascript-guide)

---

## Standard Library

TBD...

[⇧ top](#javascript-guide)

---

## Testing

TBD...

[⇧ top](#javascript-guide)

---

## Performance

TBD...

[⇧ top](#javascript-guide)

---

## Resources

TBD...

[⇧ top](#javascript-guide)

---

## In the Wild

TBD...

[⇧ top](#javascript-guide)

---

## Translation

TBD...

[⇧ top](#javascript-guide)

---

## The JavaScript Style Guide Guide

TBD...

[⇧ top](#javascript-guide)

---

## Contributors

TBD...

[⇧ top](#javascript-guide)

---

## License

TBD...

[⇧ top](#javascript-guide)
