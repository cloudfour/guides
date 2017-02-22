<!-- Link aliases -->

[ARIA Role, State, and Property Quick Reference]: http://rawgit.com/w3c/aria-in-html/master/index.html#recommendations-table
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
[Sublime Text]: http://sublimetext.com
[The CSS Specificity Graph]: http://csswizardry.com/2014/10/the-specificity-graph/

# CSS Guide

Clean, consistent and understandable CSS is paramount to a successful project. It sets the tone, both visually and architecturally, for the entire front-end. These are our collected (and evolving) best practices for writing styles with some _style_. 😎

- [Organization](#organization)
    - [Directory Structure](#directory-structure)
    - [Base Styles](#base-styles)
    - [Components](#components)
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
    - [Compatibility](#compatibility)
- [Tools](#tools)
    - [Processors](#processors)
    - [Formatters](#formatters)
    - [Validators](#validators)
    - [Analyzers](#analyzers)

## Organization

### Directory Structure

This structure is an adaptation of [Sass Guidelines: The 7-1 Pattern]. It represents the organization of different types of style sheets, and the order they should follow. Unless specific project requirements dictate otherwise, the directory structure should look _something_ like this:

<pre>
├── base/
│   ├── forms.css
│   ├── typography.css
│   └── variables.css
├── components/
│   ├── alert.css
│   ├── button.css
│   └── grid.css
├── utils/
│   ├── display.css
│   ├── position.css
│   └── text.css
├── vendor/
│   └── ...
└── main.css
</pre>

### Base Styles

The `base/` directory should contain foundational styles and other global dependencies. There should be few (if any) class definitions within this directory. In addition to common variables, this would also be an appropriate place to put mixins or functions if a preprocessor is in use.

- Variables, mixins and functions should be organized in their own separate files.

    ```css
    /* base/variables.css */

    :root {
      --font-family-sans: popular-sans, "Helvetica Neue", sans-serif;
      --font-size-base: 22px;
      --transition-duration: 360ms;
    }

    @custom-media --width-min-md screen and (min-width: 30em);
    @custom-media --width-min-lg screen and (min-width: 60em);
    ```

- Each file should only be responsible for providing base styles for a designated group of related elements.

    ```css
    /* base/scaffolding.css */

    * {/*...*/}

    html {/*...*/}

    body {/*...*/}
    ```

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

The `components/` directory should have the largest number of files, because most of the CSS should be written as small, reusable components.

- Each file should contain only one component and, if possible, only class selectors with a common namespace for that component:

    ```css
    /* components/alert.css */

    .Alert {/*...*/}

    .Alert--fixed {/*...*/}

    .Alert-header {/*...*/}

    .Alert-closeButton {/*...*/}
    ```

    ```css
    /* components/button.css */

    .Button {/*...*/}

    .Button--large {/*...*/}

    .Button--small {/*...*/}
    ```

### Utilities

The `utilities/` directory is where definitions for utility classes (or "helpers") should occur. Unlike components, there may be many of these class definitions per file. Their organization should be according to what kind of properties they affect. See [SUIT CSS Utils] for a nice example of this organization.

- Each file should contain only classes prefixed with `u-` to identity them as utilities.

    ```css
    /* utilities/margin.css */

    .u-marginAbove {
      margin-top: var(--vspace) !important;
    }

    .u-marginBelow {
      margin-bottom: var(--vspace) !important;
    }
    ```

- To ensure dominance over conflicting declarations, **utilities should come last after all other styles** in `main.css`.

    ```css
    /* main.css */

    @import "base";
    @import "components";
    @import "sections";
    @import "utils";
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

1. Combined selectors should be on separate lines, and the opening brace should be on the same line as the last selector.
2. Variables and preprocessor cruft should come before any properties, separated with blank line below.
3. One space should be after each colon, and each line should end with a semicolon.
4. Values of zero should be unit-less.
5. Strings within values should use double quotes.
6. Comma-delimited numbers inside of values with parenthesis (e.g. `rgb(0,0,0)`) should have no spaces between them.
7. Decimal values should include a leading `0`.
8. Time values should be represented with the millisecond (`ms`) unit.
9. Nested pseudo element blocks should come after all property declarations.
10. Nested pseudo class blocks should come after all pseudo element blocks.
11. Nested class or attribute blocks should come after all pseudo class blocks.
12. Nested media queries should come after all combined class or attribute blocks.
13. Closing braces should be on a new line.
14. A blank line should come after each declaration block.

### Property Sorting

Until recently, we followed Guy Routledge's [Outside In] method of property sorting. Over time, we discovered most property sorting methodologies require maintenance as new properties (for example, `flex-*` or `grid-*`) are introduced. This makes them inherently fragile and difficult to enforce.

We now recommend properties are sorted alphabetically. This technique will scale to accommodate any new properties, and requires no learning curve for new project contributors.

```css
/* Do */

selector {
  display: flex;
  font-size: 2em;
  left: 0;
  position: absolute;
  top: 0;
}
```

```css
/* Don't */

selector {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  font-size: 2em;
}
```

[CSScomb] is a tool that will automate the process of formatting and organizing CSS properties. It is available as a package for [Atom] and [Sublime Text], and can be executed manually or upon saving your file.

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

Naming stuff can be hilariously difficult. To minimize future confusion, try to pick names that are less likely to change (or become inaccurate). For example, a component name of `.FormGroup` might be better than `.RegistrationShipping`, since it describes a _function_ rather than a _context_. See [Naming CSS Stuff Is Really Hard] for more examples.

The following conventions were adapted from the [SUIT CSS Naming Conventions].

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

#### States

Syntax: `<ComponentName>.is-stateOfComponent`

State classes should reflect changes to a component's state. As such, it's important to resist the temptation to apply direct styles to these classes. Scoping states to associated component classes insures the use of consistent cross-component terminology.

```css
/* Component Name */
.Tweet {}

/* State of component */
.Tweet.is-expanded {}
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

#### JavaScript Hooks

See [CSS Guidelines: JavaScript Hooks]

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

Use the following properties with care. They should occur in reusable utilities most of the time, and not repeated across a wide variety of components.

- `margin`
- `float`
- `width`
- `height`
- `font-*`
- `line-height`
- `text-align`
- `white-space`

### Encapsulation

When writing base styles for a component, assume that the component is unaware of everything outside of its box. Add styles that depend on surrounding elements with care (or instead use more utility classes in your HTML.)

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

When combining components for specific overrides, do this in a context-specific style sheet:

```css
/* sections/search.css */

.Section--search .Button {/*...*/}
```

If this combination reoccurs, consider creating a new component to abstract the needed pieces:

```css
/* components/searchbar.css */

.SearchBar {/*...*/}

.SearchBar-button {/*...*/}
```

### Compatibility

Vendor prefixes or other non-standard fallbacks make CSS difficult to read and maintain. Even mixins require documentation and maintenance. [Autoprefixer] will handle prefixes and other fallbacks based on your project's actual support requirements. This allows us to write styles in a standard and predictable way:

```scss
/* Don't */
.Component {
  -webkit-transform: translateX(-50%);
  -ms-transform: translateX(-50%);
  transform: translateX(-50%);
}

/* Don't */
.Component {
  @include translateX(-50%);
}

/* Do */
.Component {
  transform: translateX(50%);
}
```

[⇧ top](#css-guide)
<!---------------->

## Tools

### Processors

- **[PostCSS]**

### Formatters

- **[CSScomb]** CSScomb is a coding style formatter for CSS. You can easily write your own configuration to make your style sheets beautiful and consistent.

### Validators

- **[stylelint]** With this plugin, you can check the validity of stylesheets against a set of project-specific conventions. The plugin will throw an error if it finds CSS that violates these rules.

### Analyzers

- **[The CSS Specificity Graph]** A very simple model for diagrammatically assessing the overall health of your codebase in terms of specificity—a way of looking at an entire project’s CSS and highlighting any potentially troublesome areas of higher-than-ideal specificity. 
- **[CSS Dig]** A Chrome extension that summarizes selector and propery usage for any given page. Particularly useful for identifying areas of needless repetition (see [Dryness](#dryness)).

[⇧ top](#css-guide)
<!---------------->
