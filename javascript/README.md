<!-- General link aliases -->
[Airbnb JavaScript Style Guide]: https://github.com/airbnb/javascript

<!-- MDN link aliases -->
[Array Literal Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_array_literals
[Array.from]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from
[Array.prototype.push]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push
[NodeList]: https://developer.mozilla.org/en-US/docs/Web/API/NodeList
[Object.assign]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
[Object Literal Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_object_literals

<!-- JSPerf link aliases -->
[Adding Array Items]: https://jsperf.com/adding-array-items
[Arrays from Array-Like Objects]: https://jsperf.com/array-like-object-to-array
[Arrays From Iterables]: https://jsperf.com/arrays-from-iterables
[Mapping Over Iterables]: https://jsperf.com/array-from-vs-spread-vs-array-from-map
[Shallow Copy Objects]: https://jsperf.com/shallow-copy-objects
[Shallow Copy Arrays]: https://jsperf.com/shallow-copy-arrays

<!-- ESLint link aliases -->
[array-bracket-newline]: https://eslint.org/docs/rules/array-bracket-newline
[array-callback-return]: https://eslint.org/docs/rules/array-callback-return
[array-element-newline]: https://eslint.org/docs/rules/array-element-newline
[no-array-constructor]: https://eslint.org/docs/rules/no-array-constructor.html
[no-const-assign]: https://eslint.org/docs/rules/no-const-assign.html
[no-new-object]: https://eslint.org/docs/rules/no-new-object.html
[no-prototype-builtins]: https://eslint.org/docs/rules/no-prototype-builtins
[no-var]: https://eslint.org/docs/rules/no-var.html
[object-shorthand]: https://eslint.org/docs/rules/object-shorthand.html
[prefer-const]: https://eslint.org/docs/rules/prefer-const.html
[prefer-object-spread]: https://eslint.org/docs/rules/prefer-object-spread
[prefer-spread]: https://github.com/sindresorhus/eslint-plugin-unicorn/blob/master/docs/rules/prefer-spread.md
[quote-props]: https://eslint.org/docs/rules/quote-props.html

# JavaScript Guide

*A mostly reasonable approach to JavaScript, inspired by the [Airbnb JavaScript Style Guide].*

## Table of Contents

1. [Variables](#variables)
2. [Objects](#objects)
3. [Arrays](#arrays)

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

### 3.8 Array Line Breaks

Use line breaks after open and before close array brackets if an array has multiple lines.

#### Examples

🚫 Nope. 🚫

```js
const a = [1
];

const b = [
  1];

const c = [function foo() {
  dosomething();
}
];

const d = [
  function foo() {
    dosomething();
  }];
```

🎉 Yep! 🎉

```js
const a = [];

const b = [
];

const c = [1];

const d = [
  1
];

const e = [function foo() {
  dosomething();
}];

const f = [
  function foo() {
    dosomething();
  }
];
```

#### Resources

- ESLint: 
  - [array-bracket-newline]
  - [array-element-newline]

[⇧ top](#javascript-guide)
