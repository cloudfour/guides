[About HTML Semantics and Front-end Architecture]: http://nicolasgallagher.com/about-html-semantics-front-end-architecture
[Modular CSS BEM/OOCSS Naming]: http://benfrain.com/modular-css-bem-oocss-naming/
[The Specificity Graph]: http://csswizardry.com/2014/10/the-specificity-graph/
[CSS Guidelines]: http://cssguidelin.es
[CSS Guidelines: Architectural Principles]: http://cssguidelin.es/#architectural-principles
[Atomic CSS and Lobotomized Owls]: http://alistapart.com/article/axiomatic-css-and-lobotomized-owls
[CSScomb]: http://csscomb.com
[CSScomb config]: http://
[CSS Property Order]: http://markdotto.com/2011/11/29/css-property-order/
[Code Guide by @mdo]: http://codeguide.co/#css
[Outside In]: http://webdesign.tutsplus.com/articles/outside-in-ordering-css-properties-by-importance--cms-21685
[SUIT CSS Naming Conventions]: https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md
[SUIT CSS Linter]: https://github.com/necolas/postcss-bem-linter
[ARIA Role, State, and Property Quick Reference]: http://rawgit.com/w3c/aria-in-html/master/index.html#recommendations-table

<!--
TODO: table of contents
-->

Organization
============

## Directory Structure

Adapted from [Sass Guidelines: The 7-1 Pattern](http://sass-guidelin.es/#the-7-1-pattern)

Unless project requirements dictate otherwise, the directory structure for CSS source code should look something like this:

<pre>
├── base
│   ├── normalize.css
│   ├── reset.css
│   ├── typography.css
│   └── variables.css
├── components
│   ├── alert.css
│   ├── button.css
│   ├── dropdown.css
│   └── tabs.css
├── pages
│   ├── contact.css
│   └── home.css
├── themes
│   ├── admin.css
│   └── default.css
├── utils
│   ├── u-align.css
│   ├── u-display.css
│   └── u-position.css
├── vendor
└── main.css
</pre>

<!--
TODO: breakdown of each folder
-->

<!--
TODO: ## File Separation
-->

Formatting
==========

## General Rules

These rules were adapted from [CSS Guidelines].

0. Closely related selectors should be on the same line

    ```css
    h1, .h1 {
      font-size: 2em;
    }
    ```

0. All other selectors should be on new lines

    ```css
    .Component-header,
    .Component-footer {
      display: block;
    }
    ```

0. One space should be before each opening brace (`{`)

    ```css
    /* Do */

    selector {
      property: value;
    }
    ```

    ```css
    /* Don't */

    selector{
      property: value;
    }
    ```

0. One space should be after each property–value delimiting colon (`:`)

    ```css
    /* Do */

    selector {
      property: value;
    }
    ```

    ```css
    /* Don't */

    selector {
      property:value;
    }
    ```

0. Each declaration should be on its own line

    ```css
    /* Do */

    selector {
      width: 100%;
      height: 100%;
    }
    ```

    ```css
    /* Don't */

    selector {
      width: 100%; height: 100%;
    }
    ```

0. The opening brace (`{`) should be on the same line as the last selector

    ```css
    /* Do */

    .Selector-a,
    .Selector-b {
      property: value;
    }
    ```

    ```css
    /* Don't */

    .Selector-a,
    .Selector-b
    {
      property: value;
    }
    ```

0. The closing brace (`}`) should be on its own new line

    ```css
    /* Do */

    selector {
      property: value;
    }
    ```

    ```css
    /* Don't */

    selector {
      property: value; }
    ```

0. A trailing semi-colon (`;`) should be on all declarations

    ```css
    /* Do */

    selector {
      width: 100%;
      height: 100%;
      opacity: 1;
    }

    ```

    ```css
    /* Don't */

    selector {
      width: 100%;
      height: 100%;
      opacity: 0
    }
    ```

## Property Organization

It is recommended to order all property declarations categorically rather than randomly or alphabetically. The high-level categories that determine this property order are loosely based on the [Outside In] method described by Guy Routledge:

>The gist of the technique is to start with big-picture properties which impact stuff outside the element and work in towards the finer details. This is why I call it the “Outside In” method.

0. Layout Properties
0. Box Model Properties
0. Visual Properties
0. Typography Properties
0. Misc Properties

<!--
TODO: Make this a table

- Positioning
    - `position`
    - `z-index`
    - `top`
    - `right`
    - `bottom`
    - `left`
    - `margin`
    - `...`
- Box
    - `float`
    - `clear`
    - `display`
    - `width`
    - `height`
    - `padding`
    - `flex`
    - `vertical-align`
    - `...`
- Contents
    - `content`
    - `overflow`
    - `visibility`
    - `text-align`
    - `...`
- Typography
    - `font`
    - `line-height`
    - `letter-spacing`
    - `white-space`
    - `text-overflow`
    - `...`
- Surfaces
    - `outline`
    - `border`
    - `background`
    - `color`
    - `...`
- Effects
    - `opacity`
    - `filter`
    - `box-shadow`
    - `text-shadow`
    - `transform`
    - `...`
- Behaviors
    - `transition`
    - `animation`
    - `pointer-events`
    - `...`

-->

```css
/* Do */

selector {
  position: absolute;    /* Position */
  top: 0;                /* Position */
  left: 0;               /* Position */

  display: inline-block; /* Box model */
  width: 100%;           /* Box model */
  height: 2em;           /* Box model */
  padding: 3px 7px;      /* Box model */

  font-size: 11px;       /* Typography */
  line-height: 1;        /* Typography */
  white-space: nowrap;   /* Typography */
  text-align: center;    /* Typography */
}
```

```css
/* Don't */

selector {
  display: inline-block; /* Box model */
  font-size: 11px;       /* Typography */
  height: 2em;           /* Box model */
  left: 0;               /* Position */
  line-height: 1;        /* Typography */
  padding: 3px 7px;      /* Box model */
  position: absolute;    /* Position */
  text-align: center;    /* Typography */
  top: 0;                /* Position */
  white-space: nowrap;   /* Typography */
  width: 100%;           /* Box model */
}
```

[CSScomb] is a tool that will automate the otherwise difficult process of maintaining organized CSS properties. It is available as a package for [Atom] and [Sublime Text], and can be executed manually or upon saving your file.

Selectors
=========

## General Rules

- ID selectors should be avoided

    ```css
    /* Don't */

    #some-id {}
    ```

    ```css
    /* Don't even */

    element#some-id {}
    ```

- Element selectors should be avoided outside of defining base styles

    ```css
    /* Don't */

    .Component ul {}
    ```

    ```css
    /* Don't */

    .Component > span {}
    ```

    ```css
    /* Don't */

    li.Component-item {}
    ```

- Nesting should be avoided unless the resulting specificity is actually needed

    ```css
    /* Do */

    .Component {}

    .Component-element {}
    ```

    ```css
    /* Don't */

    .Component {}

    .Component .Component-element {}
    ```

    **Note:** It is also acceptable to "nest" pseudo classes and pseudo elements when using a preprocessor, since doing this has no unintentional effect on specificity.

- Nested selectors may only be two levels deep and must consist of a modifier class followed by an element class

    ```css
    .Component--modifier .Component-element {}
    ```

- Unrelated selectors should not be combined

    ```css
    /* Do */

    h1,
    h2,
    h3 {
      font-weight: bold;
      letter-spacing: -0.1em;
    }
    ```

    ```css
    /* Don't */

    .Component-header,
    .OtherComponent-header,
    .AnotherComponent--extended {
      margin-top: 0;
    }
    ```

    **Note:** If using a preprocessor like Sass, the `@extend` feature should be used with great care to avoid the unintentional combining of unrelated selectors.

## Class Naming Syntax

Adapted from the [SUIT CSS Naming Conventions].

### Naming Utilities

Syntax: `u-[sm|md|lg-]<utilityName>`

```css
.u-floatLeft {
  float: left !important;
}

@media (--sm) {
  .u-sm-floatLeft {
    float: left !important;
  }
}
```

<!--
TODO: ### States
-->

### Naming Components

Syntax: `<ComponentName>[--modifierName|-descendentName`

```css
/* Component Name */
.Alert {}

/* Modifier */
.Alert--dismissable {}

/* Descendent */
.Alert-closeButton {}

/* Modifying descendants */
.Alert--dismissable .Alert-closeButton {}
```

### Micro-semantics

When deciding how to construct complex class names with multiple delimited pieces, look at existing HTML specifications for inspiration before deciding on something arbitrary.

The [ARIA Role, State, and Property Quick Reference] is a good resource for common element and state names.

```css
/* Elements */

.Component-body {}
.Component-header {}
.Component-button {}
.Component-dialog {}
.Component-img {}
```

```css
/* Modifiers */

.Component--labelled {}
.Component--hasPopop {}
```

```css
/* States */

.Component.is-busy {}
.Component.is-expanded {}
.Component.is-checked {}
.Component.is-selected {}
```

Encapsulation
=============

When writing base styles for a component, assume that the component is entirely unaware of everything outside of its box. If styles that depend on other sibling or parent elements are needed, add them prescriptively (or consider using an additional utility class in your HTML.)

```css
/* Do */

.Component {
  display: block;
}

.Component--withMargin {
  margin-top: 1em;
}

.Component--size1of2 {
  width: 50%;
}
```

```css
/* Don't */

.Component {
  margin-top: 1em;
  display: block;
  width: 50%;
}
```

<!--
TODO: more examples of encapsulation
-->

Specificity
===========

## Special Considerations

Use the following properties with care. Ideally, they should mostly be found in reusable utilities, and not be repeated across a wide variety of components.

```css
/*
margin
float
width
height
font-*
line-height
text-align
white-space
*/
```

Architecture
============

See [CSS Guidelines: Architectural Principles]

<!--
TODO: more content
-->

Tools
=====

- **[CSScomb]**
    CSScomb is a coding style formatter for CSS. You can easily write your own configuration to make your style sheets beautiful and consistent.

- **[SUIT CSS Linter]**
    With this plugin, you can check the validity of stylesheets against a set of BEM-style conventions. You can use preset patterns (SUIT and BEM, currently) or insert your own. The plugin will throw an error if it finds CSS that does not follow the specified conventions.
