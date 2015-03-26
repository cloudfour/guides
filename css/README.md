<!-- Link aliases -->

[ARIA Role, State, and Property Quick Reference]: http://rawgit.com/w3c/aria-in-html/master/index.html#recommendations-table
[About HTML Semantics and Front-end Architecture]: http://nicolasgallagher.com/about-html-semantics-front-end-architecture
[Atom]: http://atom.io
[Atomic CSS and Lobotomized Owls]: http://alistapart.com/article/axiomatic-css-and-lobotomized-owls
[CSS Guidelines: Architectural Principles]: http://cssguidelin.es/#architectural-principles
[CSS Guidelines]: http://cssguidelin.es
[CSS Property Order]: http://markdotto.com/2011/11/29/css-property-order/
[CSScomb config]: http://
[CSScomb]: http://csscomb.com
[Code Guide by @mdo]: http://codeguide.co/#css
[KSS]: https://github.com/kss-node/kss-node
[Modular CSS BEM/OOCSS Naming]: http://benfrain.com/modular-css-bem-oocss-naming/
[Outside In]: http://webdesign.tutsplus.com/articles/outside-in-ordering-css-properties-by-importance--cms-21685
[PostCSS]: https://github.com/postcss/postcss
[Rework]: https://github.com/reworkcss/rework
[SUIT CSS Linter]: https://github.com/necolas/postcss-bem-linter
[SUIT CSS Naming Conventions]: https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md
[SUIT CSS Utils]: https://github.com/suitcss/utils
[Sass Guidelines: The 7-1 Pattern]: http://sass-guidelin.es/#the-7-1-pattern
[Sublime Text]: http://sublimetext.com
[The CSS Specificity Graph]: http://csswizardry.com/2014/10/the-specificity-graph/

# CSS Guide

- [Organization](#organization)
    - [Directory Structure](#directory-structure)
    - [Base Styles](#base-styles)
    - [Components](#components)
    - [Page Styles](#page-styles)
    - [Utilities](#utilities)
- [Conventions](#conventions)
    - [General Rules](#general-rules)
    - [Property Sorting](#property-sorting)
    - [Selectors](#selectors)
    - [Class Naming](#class-naming)
    - [Comments](#comments)
- [Architecture](#architecture)
    - [Dryness](#dryness)
    - [Encapsulation](#encapsulation)
    - [Composition](#composition)
- [Tools](#tools)
    - [Processors](#processors)
    - [Formatters](#formatters)
    - [Validators](#validators)
    - [Analyzers](#analyzers)

## Organization

### Directory Structure

This structure was adapted from [Sass Guidelines: The 7-1 Pattern], and represents the organization of different types of style sheets, and also the sequential order in which they should be applied.

<pre>
├── base
│   ├── normalize.css
│   ├── reset.css
│   ├── typography.css
│   └── variables.css
│   └── ...
├── components
│   ├── alert.css
│   ├── button.css
│   ├── dropdown.css
│   └── tabs.css
│   └── ...
├── pages
│   ├── contact.css
│   └── home.css
│   └── ...
├── utils
│   ├── u-align.css
│   ├── u-display.css
│   └── u-position.css
│   └── ...
├── vendor
│   └── ...
└── main.css
</pre>

The exact naming of folders and files (extensions included) will vary depending on what processing tools are being used, but unless specific project requirements dictate otherwise, the directory structure should look something like this.

### Base Styles

The `base/` directory should contain mostly foundational element styles and any core dependencies (mixins, variables, functions, etc.) that need to be globally available. There should be few (if any) class definitions within this directory. Some examples of what you might place here include:

- `reset.css` or `normalize.css` (or _both_)
- `variables.css`
- `mixins.css`
- `scaffolding.css`
- `forms.css`
- `typography.css`

Each file should only be responsible for providing base styles for designated group of related elements.

```css
/* base/forms.css */

label {/*...*/}

input {/*...*/}

button {/*...*/}
```

```css
/* base/typography.css */

h1,
h2,
h3 {/*...*/}

pre,
code {/*...*/}
```

### Components

The `components/` directory should be the largest, as most of the CSS should be written as small, reusable components. Some examples of what you might place here include:

- `alert.css`
- `button.css`
- `grid.css`
- `arrange.css`
- `dropdown.css`
- `tablist.css`
- `well.css`

Each file should contain only one component, and if possible, only class selectors with a common namespace for that component:

```css
/* components/button.css */

.Button {/*...*/}

.Button--large {/*...*/}

.Button--small {/*...*/}
```

### Page Styles

The `pages/` directory is where page-specific styling and contextual use-case overrides for components should occur. If a page requires specific modifications to a component, they should be placed in a style sheet for that page:

- `home.css`
- `listing.css`
- `error.css`

```css
/* pages/home.css */

.Page--home .Page-welcome .Button {
  font-size: 3em;
}
```

### Utilities

The `utilities/` directory is where utility classes (or "helpers") should be defined. Unlike components, there may be multiple class definitions within each file, though they should be organized according to what kind of properties they affect. [SUIT CSS Utils] is nice example of this kind of organization. Some examples of what you might place here include:

- `display.css`
- `position.css`
- `text.css`

Each file should contain nothing but class definitions prefixed with `u-` to identity them as utility classes. To ensure that they always override conflicting declarations, **utilities should be included after all other styles** in `main.css`.

```css
/* utilities/display.css */

.u-displayBlock {
  display: block !important;
}

.u-displayInline {
  display: inline !important;
}
```

[⇧ top](#css-guide)
<!---------------->

## Conventions

### General Rules

These rules were adapted from [CSS Guidelines]. This is an example of how declaration block syntax should be formatted (Sass syntax used to illustrate nesting):

```sass
.Selector-1,
.Selector-2 { /* 1 */
  @include some-mixin(); /* 2 */

  display: block; /* 3 */
  padding: 0; /* 4 */
  background-image: url("image.png"); /* 5 */
  background-color: rgba(0,0,0,0.1); /* 6 */
  opacity: 0.8; /* 7 */
  transition-duration: 300ms; /* 8 */

  &::before { /* 9 */
    content: "Foo";
  }

  &:hover,
  &:focus { /* 10 */
    color: green;
  }

  &.is-disabled,
  &[disabled] { /* 11 */
    pointer-events: none;
  }

  @media (min-width: 40em) { /* 12 */
    width: auto;
  }
} /* 13 */
/* 14 */
```

1. Combined selectors should be on separate lines; the opening brace (`{`) should be on the same line as the last selector
2. Variables and preprocessor cruft should be placed before any properties, with a blank line below
3. One space should be after each colon (`:`); each line should end with a semicolon (`;`)
4. Values of `0` should be unit-less
5. Strings within values should use double quotes (`""`)
6. Comma-delimited numerical values inside of parenthesis should have no spaces
7. Decimal values should include a leading `0`
8. Time values should be represented in milliseconds (`ms`)
9. Nested pseudo element blocks should be placed after all property declarations
10. Nested pseudo class blocks should be placed after all pseudo element blocks
11. Nested class or attribute blocks should be placed after all pseudo class blocks
12. Nested media queries should be placed after all combining class blocks
13. Closing braces (`}`) should be on a new line
14. A blank line should be after each declaration block

### Property Sorting

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

### Selectors

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

### Class Naming

Adapted from the [SUIT CSS Naming Conventions].

#### Utility Classes

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

#### Component Classes

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

#### Micro-semantics

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

### Comments

Comments are a good idea. There is no standardized CSS documentation tool ([KSS] for example) currently in use. For comments that explain declarations, this formatting is nice:

From https://github.com/suitcss/components-arrange/blob/master/lib/arrange.css

```css
/**
 * 1. Protect against the component expanding beyond the confines of its
 *    container if properties affecting the box-model are applied to the
 *    component. Mainly necessary because of (5).
 * 2. Rely on table layout.
 * 3. Zero out the default spacing that might be on an element (e.g., `ul`).
 * 4. Make sure the component fills at least the full width of its parent.
 * 5. Reset the table-layout algorithm in case a component is nested.
 */

.Arrange {
  box-sizing: border-box; /* 1 */
  display: table; /* 2 */
  margin: 0; /* 3 */
  min-width: 100%; /* 4 */
  padding: 0; /* 3 */
  table-layout: auto; /* 5 */
}
```

<!-- TODO: More content -->

[⇧ top](#css-guide)
<!---------------->

## Architecture

See [CSS Guidelines: Architectural Principles]

### Dryness

Use the following properties with care. Ideally, they should mostly be found in reusable utilities, and not be repeated across a wide variety of components.

- `margin`
- `float`
- `width`
- `height`
- `font-*`
- `line-height`
- `text-align`
- `white-space`

### Encapsulation

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

### Composition

If two components need to be combined in order to define overriding styles for a specific use case, then this should be done within a context-specific style sheet:

```css
/* pages/search.css */

.Page--search .Button {/*...*/}
```

If this combination is reoccurring, then a better solution is to create a new components that abstracts the needed pieces:

```css
/* components/searchbar.css */

.SearchBar {/*...*/}

.SearchBar-button {/*...*/}
```

[⇧ top](#css-guide)
<!---------------->

## Tools

### Processors

- **[PostCSS]**
- **[Rework]**

### Formatters

- **[CSScomb]**
    CSScomb is a coding style formatter for CSS. You can easily write your own configuration to make your style sheets beautiful and consistent.

### Validators

- **[SUIT CSS Linter]**
    With this plugin, you can check the validity of stylesheets against a set of BEM-style conventions. You can use preset patterns (SUIT and BEM, currently) or insert your own. The plugin will throw an error if it finds CSS that does not follow the specified conventions.

### Analyzers

- **[The CSS Specificity Graph]**

[⇧ top](#css-guide)
<!---------------->
