<!-- General Link aliases -->
[Airbnb JavaScript Style Guide]: https://github.com/airbnb/javascript
[MDN: Object.assign]: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
[MDN: Object Literal Spread Syntax]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#Spread_in_object_literals
[Object Destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Object_destructuring
[Array Destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring

<!-- JSPerf aliases -->
[JSPerf: Shallow Copy Objects]: https://jsperf.com/shallow-copy-objects
[Object Destructuring vs Not]: https://jsperf.com/destructure-vs-not
[Array Destructuring vs Not]: https://jsperf.com/array-destructuring

<!-- ESLint link aliases -->
[no-const-assign]: https://eslint.org/docs/rules/no-const-assign.html
[no-new-object]: https://eslint.org/docs/rules/no-new-object.html
[no-prototype-builtins]: https://eslint.org/docs/rules/no-prototype-builtins
[no-var]: https://eslint.org/docs/rules/no-var.html
[object-shorthand]: https://eslint.org/docs/rules/object-shorthand.html
[prefer-const]: https://eslint.org/docs/rules/prefer-const.html
[prefer-destructuring]: https://eslint.org/docs/rules/prefer-destructuring
[prefer-object-spread]: https://eslint.org/docs/rules/prefer-object-spread
[quote-props]: https://eslint.org/docs/rules/quote-props.html

<!-- Babel link aliases -->
[@babel/plugin-transform-destructuring]: https://babeljs.io/docs/en/next/babel-plugin-transform-destructuring.html

# JavaScript Guide

*A mostly reasonable approach to JavaScript, inspired by the [Airbnb JavaScript Style Guide].*

## Table of Contents

1. [Variables](#variables)
2. [Objects](#objects)
4. [Destructring](#destructuring)

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

### 2.5 Object Spread over Object.assign
  
Prefer the [object spread][MDN: Object Literal Spread Syntax] operator over [`Object.assign`][MDN: Object.assign] to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

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
- JSPerf: [Shallow Copy Objects][JSPerf: Shallow Copy Objects]

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
