<!-- Link aliases -->

[ARIA Role, State, and Property Quick Reference]: https://www.w3.org/TR/html-aria/#aria-table
[About HTML Semantics and Front-end Architecture]: http://nicolasgallagher.com/about-html-semantics-front-end-architecture
[Atom]: http://atom.io
[Atomic CSS and Lobotomized Owls]: http://alistapart.com/article/axiomatic-css-and-lobotomized-owls
[Autoprefixer]: https://github.com/postcss/autoprefixer
[CSS Dig]: https://css-tricks.com/starting-a-refactor-with-css-dig/
[CSS Guidelines: Architectural Principles]: http://cssguidelin.es/#architectural-principles
[CSS Guidelines: JavaScript Hooks]: http://cssguidelin.es/#javascript-hooks
[CSS Guidelines]: http://cssguidelin.es
[CSS Property Order]: http://markdotto.com/2011/11/29/css-property-order/
[CSS Reset]: http://meyerweb.com/eric/tools/css/reset/
[CSScomb config]: http://
[CSScomb]: http://csscomb.com
[Code Guide by @mdo]: http://codeguide.co/#css
[KSS]: https://github.com/kss-node/kss-node
[Modular CSS BEM/OOCSS Naming]: http://benfrain.com/modular-css-bem-oocss-naming/
[Naming CSS Stuff Is Really Hard]:http://seesparkbox.com/foundry/naming_css_stuff_is_really_hard
[normalize.css]: http://necolas.github.io/normalize.css/
[Outside In]: http://webdesign.tutsplus.com/articles/outside-in-ordering-css-properties-by-importance--cms-21685
[PostCSS]: https://github.com/postcss/postcss
[Rework]: https://github.com/reworkcss/rework
[SUIT CSS Linter]: https://github.com/necolas/postcss-bem-linter
[SUIT CSS Naming Conventions]: https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md
[SUIT CSS Utils]: https://github.com/suitcss/utils
[Sass Guidelines: The 7-1 Pattern]: http://sass-guidelin.es/#the-7-1-pattern
[stylelint]: https://stylelint.io/
[stylefmt]: https://github.com/morishitter/stylefmt
[Sublime Text]: http://sublimetext.com
[The CSS Specificity Graph]: http://csswizardry.com/2014/10/the-specificity-graph/

# JavaScript Guide

*A mostly reasonable approach to JavaScript, inspired by the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript).*

## Table of Contents

  1. [References](#references) (Variables, Constants, etc.)

## References

### 1.1 Prefer Constants

Use `const` for all of your references; avoid using `var`. 

> Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

Nope.

```js
var a = 1;
var b = 2;
```

Yep!

```js
const a = 1;
const b = 2;
```

### 1.2 Reassigning References

If you must reassign references, use `let` instead of `var`. 

> Why? `let` is block-scoped rather than function-scoped like `var`. Function-scoped variables are hoisted which can lead to bugs if you are not careful. Using block-scoped variables makes our code more predictable by giving the variable an explicit scope.

eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

Nope.

```js
var count = 1;
if (true) {
  count += 1;
}
```

Yep!

```js
let count = 1;
if (true) {
  count += 1;
}
```

### 1.3 Block Scope

Note that both `let` and `const` are block-scoped.

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
