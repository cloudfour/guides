# Utility Class Name Conventions

An ideal utility class name should resemble an abbreviated set of instructions. It should favor verbs over adjectives and nouns, and limit its use of abbreviations. It should represent behavioral traits, and be succinct without sacrificing its clarity.

## 1. Prefixes

You should prefix all class names with `u-` to identify them as utilities. Classes intended to apply only at certain media queries should include a _viewport prefix_ for that query.

```css
.u-sm-floatLeft {}
   |
   viewport prefix
```

You should consider the likelihood of needing to apply a utility based on the viewport size before using viewport prefixes.

## 2. Choosing functional base names

If CSS components are comparable to the class constructs of OOP, then you should compare CSS utilities to basic functions. Like functions, their names should imply what they affect.

A class name of `.u-floatLeft` implies that its effect is to float something to the left. "Float" is the _function_, and "Left" is an _argument_ for the float direction parameter. Expressed in JavaScript, it would look like this:

```js
function float (direction) {
  // Logic and magic
}

float('left');
```

Using the function and argument structure for utilities will result in names that are easy to remember and comprehend in the context of HTML.

```
.u-floatLeft
   |    |
   |    argument
   function
```

In some cases, the functionality implied by the class name only makes sense in the context of a specific type of element. You can prepend subject _namespaces_ to clarify the type of element that applies.

```
.u-textGrow
   |   |
   |   function
   namespace
```

In other cases, this convention may be totally convoluted, and can be ignored if it makes sense to.

```css
/* This is kind of verbose and silly. */
.u-textPreventWrapping {}

/* This is an acceptable compromise. */
.u-textNoWrap {}
```

## 3. Directional descriptors

Names featuring directional descriptors (e.g. "top", "bottom", "left", "right") as arguments should include them in full instead of abbreviating.

```css
.u-padTop {}
.u-spaceLeft {}
.u-offsetRight {}
```

If a name needs to imply that two directions on the same axis are relevant to the behavior of the class, use a common alias to represent each axis.

```css
/* x-axis (left and right) */
.u-padSides {}
.u-padLateral {}
.u-padHorizontal {}

/* y-axis (top and bottom) */
.u-padEnds {}
.u-padLongitudinal {}
.u-padVertical {}
```

If a name needs to imply that two directions on opposing axis are relevant to the behavior of the class, combine the two with the Y axis leading.

```css
.u-roundCornersTopLeft {}
.u-posAbsoluteBottomRight {}
```

## 4. Incremental permutations

Names often need variations where the amount or degree of change differs in an incremental fashion.

### 4.1. Using a "clothing size" scale

"Clothing sizes" ranging typically from extra-small to extra-large can be used to imply a scale.

```css
.u-padXs /* extra-small */
.u-padSm /* small */
.u-pad   /* default */
.u-padMd /* medium */
.u-padLg /* large */
.u-PadXl /* extra-large */
```

**Pros:**
- It's familiar and easy to comprehend.

**Cons:**
- It doesn't make sense for negative values.
- The relationship between "default" and "medium" is unclear.
- It's concrete in nature, opposed to abstract.
- It doesn't scale well outside the bounds of "xs" and "xl".

### 4.2. Using a numeric scale

You can also use numeric ranges to imply a scale, and unlike clothing sizes, they're logical for both positive and negative values. You should consider how to best represent "negatives", since the minus sign can be mistaken for a delimiter. One solution (inspired by [the Solarized color scheme](http://ethanschoonover.com/solarized)) is to prefix negatives with a leading zero.

```css
.u-pad02 /* -2 below default */
.u-pad01 /* -1 below default */
.u-pad   /* default */
.u-pad1  /* +1 above default */
.u-pad2  /* +2 above default */
```

**Pros:**
- It's terse and relatively clear.
- It's abstract in nature, opposed to concrete.
- It scales as well as numbers do.

**Cons:**
- Leading zeros for "smaller" can be confusing.

### 4.3 Zero and below

Classes that apply `0` values or negative lengths should not be permutations of classes that apply positive values. The functionality is different enough to warrant a unique name.

```css
/* These apply positive margins by "spacing". */
.u-space02 {}
.u-space01 {}
.u-space {}
.u-space1 {}
.u-space2 {}

/* This removes margins by "unspacing". */
.u-unspace {}

/* These apply negative margins by "pulling". */
.u-pullLeft {}
.u-pullRight {}
.u-pullSides {}
.u-pullEnds {}
```
