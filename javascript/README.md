<!-- General link aliases -->
[Airbnb JavaScript Style Guide]: https://github.com/airbnb/javascript

<!-- MDN link aliases -->
[Array Destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring
[Array Literal Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_array_literals
[Array.from]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from
[Array.prototype.push]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push
[Function Arguments Object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments
[Function Expression]: https://developer.mozilla.org/en-US/docs/web/JavaScript/Reference/Operators/function
[Function Declaration]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function
[NodeList]: https://developer.mozilla.org/en-US/docs/Web/API/NodeList
[Object.assign]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
[Object Destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Object_destructuring
[Object Literal Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_object_literals

<!-- JSPerf link aliases -->
[Adding Array Items]: https://jsperf.com/adding-array-items
[Arrays from Array-Like Objects]: https://jsperf.com/array-like-object-to-array
[Array Destructuring vs Not]: https://jsperf.com/array-destructuring
[Arrays From Iterables]: https://jsperf.com/arrays-from-iterables
[Mapping Over Iterables]: https://jsperf.com/array-from-vs-spread-vs-array-from-map
[Object Destructuring vs Not]: https://jsperf.com/destructure-vs-not
[Shallow Copy Objects]: https://jsperf.com/shallow-copy-objects
[Shallow Copy Arrays]: https://jsperf.com/shallow-copy-arrays

<!-- ESLint link aliases -->
[array-callback-return]: https://eslint.org/docs/rules/array-callback-return
[no-array-constructor]: https://eslint.org/docs/rules/no-array-constructor.html
[no-const-assign]: https://eslint.org/docs/rules/no-const-assign.html
[no-new-object]: https://eslint.org/docs/rules/no-new-object.html
[no-prototype-builtins]: https://eslint.org/docs/rules/no-prototype-builtins
[no-var]: https://eslint.org/docs/rules/no-var.html
[object-shorthand]: https://eslint.org/docs/rules/object-shorthand.html
[prefer-const]: https://eslint.org/docs/rules/prefer-const.html
[prefer-destructuring]: https://eslint.org/docs/rules/prefer-destructuring
[prefer-object-spread]: https://eslint.org/docs/rules/prefer-object-spread
[prefer-rest-params]: https://eslint.org/docs/rules/prefer-rest-params
[prefer-spread]: https://github.com/sindresorhus/eslint-plugin-unicorn/blob/master/docs/rules/prefer-spread.md
[quote-props]: https://eslint.org/docs/rules/quote-props.html

<!-- Babel link aliases -->
[@babel/plugin-transform-destructuring]: https://babeljs.io/docs/en/next/babel-plugin-transform-destructuring.html

# JavaScript Guide

*A mostly reasonable approach to JavaScript, inspired by the [Airbnb JavaScript Style Guide].*

## Table of Contents

1. [Variables](#variables)
2. [Objects](#objects)
3. [Arrays](#arrays)
4. [Destructring](#destructuring)

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

## Functions

### 6.1 Function Style

Understand the difference between **function declarations** and **function expressions**.

> The primary difference between function declarations and function expressions is that declarations are hoisted to the top of the scope in which they are defined, which allows you to write code that uses the function before its declaration.

It can be argued that using function expressions will result in more a structured code base. We do not have a strict rule of using function declarations vs function expressions but wanted to document the difference between the two.

#### Examples

> Function declarations in JavaScript are hoisted to the top of the enclosing function or global scope. You can use the function before you declared it:
>
> ```js
> hoisted(); // logs "foo"
>
> function hoisted() {
>   console.log('foo');
> }
> ```

> Although this code might seem like an error, it actually works fine because JavaScript engines hoist the function declarations to the top of the scope. That means this code is treated as if the declaration came before the invocation.

> Note that function expressions are not hoisted:
>
> ```js
> notHoisted(); // TypeError: notHoisted is not a function
> 
> var notHoisted = function() {
>    console.log('bar');
> };
> ```


### Resources

- MDN Web Docs
  - [Function Declaration]
  - [Function Expression]

### 6.2 Arguments Parameter

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

### 6.3 Use Rest Syntax for Arguments Object

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








<a name="es6-default-parameters"></a><a name="7.7"></a>
[7.7](#es6-default-parameters) Use default parameter syntax rather than mutating function arguments.

```js
// really bad
function handleThings(opts) {
  // No! We shouldn’t mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}
```

<a name="functions--default-side-effects"></a><a name="7.8"></a>
- [7.8](#functions--default-side-effects) Avoid side effects with default parameters.

> Why? They are confusing to reason about.

```js
var b = 1;
// bad
function count(a = b++) {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

<a name="functions--defaults-last"></a><a name="7.9"></a>
- [7.9](#functions--defaults-last) Always put default parameters last.

```js
// bad
function handleThings(opts = {}, name) {
  // ...
}

// good
function handleThings(name, opts = {}) {
  // ...
}
```

<a name="functions--constructor"></a><a name="7.10"></a>
- [7.10](#functions--constructor) Never use the Function constructor to create a new function. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

> Why? Creating a function in this way evaluates a string similarly to `eval()`, which opens vulnerabilities.

```js
// bad
var add = new Function('a', 'b', 'return a + b');

// still bad
var subtract = Function('a', 'b', 'return a - b');
```

<a name="functions--signature-spacing"></a><a name="7.11"></a>
- [7.11](#functions--signature-spacing) Spacing in a function signature. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

> Why? Consistency is good, and you shouldn’t have to add or remove a space when adding or removing a name.

```js
// bad
const f = function(){};
const g = function (){};
const h = function() {};

// good
const x = function () {};
const y = function a() {};
```

<a name="functions--mutate-params"></a><a name="7.12"></a>
- [7.12](#functions--mutate-params) Never mutate parameters. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

> Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

```js
// bad
function f1(obj) {
  obj.key = 1;
}

// good
function f2(obj) {
  const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
}
```

<a name="functions--reassign-params"></a><a name="7.13"></a>
- [7.13](#functions--reassign-params) Never reassign parameters. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

> Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

```js
// bad
function f1(a) {
  a = 1;
  // ...
}

function f2(a) {
  if (!a) { a = 1; }
  // ...
}

// good
function f3(a) {
  const b = a || 1;
  // ...
}

function f4(a = 1) {
  // ...
}
```

<a name="functions--spread-vs-apply"></a><a name="7.14"></a>
- [7.14](#functions--spread-vs-apply) Prefer the use of the spread operator `...` to call variadic functions. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

> Why? It’s cleaner, you don’t need to supply a context, and you can not easily compose `new` with `apply`.

```js
// bad
const x = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// good
const x = [1, 2, 3, 4, 5];
console.log(...x);

// bad
new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

// good
new Date(...[2016, 8, 5]);
```

<a name="functions--signature-invocation-indentation"></a>
- [7.15](#functions--signature-invocation-indentation) Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

```js
// bad
function foo(bar,
              baz,
              quux) {
  // ...
}

// good
function foo(
  bar,
  baz,
  quux,
) {
  // ...
}

// bad
console.log(foo,
  bar,
  baz);

// good
console.log(
  foo,
  bar,
  baz,
);
```

[⇧ top](#javascript-guide)
