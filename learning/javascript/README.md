# Learning JavaScript

*Note*: Right now this is just a catch-all place for some JavaScript learning resources and scribbly notes. I may continue to organize this more formally as we go. The sections will be based roughly on the excellent [_Eloquent JavaScript_](http://eloquentjavascript.net/) by Martijn Haverbeke.

# JavaScript, Introduction

Read the [Introduction chapter of _Eloquent JavaScript_](http://eloquentjavascript.net/00_intro.html).

## *What is JavaScript?* and Terminology

### ECMA

The chapter makes mention of ECMA and ECMAScript. These are terms you’ll hear a lot. Developers often abbreviate “ECMAScript”  to _ES_, as in _ES5_ and _ES6_ (both in written and spoken forms).

ES6 (ECMAScript 6, also known as “Harmony”) is a big, hot topic right now. We’ll be talking more about that as we go.

For now, most of what you’ll see is ES5, the flavor of JavaScript supported by [basically every browser](http://kangax.github.io/compat-table/es5/).

### Platforms and Engines

JavaScript is a language, but it needs a place to be executed. There are several leading JavaScript *engines* ("virtual environments that interpret and execute JavaScript", thanks, Wikipedia!), including:

* V8 (Chrome, node)
* SpiderMonkey (first JS engine ever; now in Firefox)
* Nitro (Safari)


## An Aside: Matters of Style and Opinion

Toward the end of the introduction for _Eloquent JavaScript_ is a code block like this:

```javascript
function fac(n) {
  if (n == 0)
    return 1;
  else
    return fac(n - 1) * n;
}
```

Coding style is like writing style and punctuation: different people do it differently. At Cloud Four, we have our own set of conventions for writing JavaScript (and other things, like CSS!) that we try to stick to. In fact, this code block violates one of them.

We define JavaScript coding conventions at Cloud Four using two tools, [JSHint](http://jshint.com/) and [JSCS](http://jscs.info/).

JSHint conventions are tuned toward preventing you from making actual programming mistakes, while JSCS conventions are stylistic.

Configuration files for both JSHint and JSCS are installed automatically on Cloud Four laptops using boxen, and the appropriate plugins/packages for enforcing them are installed for either Atom or SublimeText. In case you are curious, you can [find our current conventions here](https://github.com/cloudfour/cloudfour-boxen/tree/master/modules/cloudfour_potions/files/dotfiles) (`jscsrc` and `jshintrc`).

## Exercises

These let you try out a couple of places that you can go to test JavaScript and inspect the state of the browser environment.

### Exercise 1: Web Inspector, the `window` object

In Chrome, open the Web Inspector (`Option-Cmd-I` on a Mac) and go to the `console` tab.

Type

```javascript
window
```

and hit enter.

What this does is display (print out) a representation of the value for the identifier `window`. `window` is a JavaScript `Object` that is made available by the `environment` in the browser (if "Object" and "environment" are mysterious concepts as of yet, don't fret, they'll come up later). 

Expand the `window` object and explore it a bit, especially the stuff under the `document` property (itself another object...it's objects all the way down!). The `document` object contains representations of a lot of stuff about the web document in the browser window and you may start seeing some items that look familiar here.

### Exercise 2: ScratchPad, `window` object redux

In Firefox, go to `Tools -> Web Developer -> Scratchpad...`. You can [read more about it here](https://developer.mozilla.org/en-US/docs/Tools/Scratchpad) if you like.

The console in Web Inspector or the Console in Firefox are useful for quick, one-line things (in the previous example, `window` gets evaluated as soon as you hit enter), but ScratchPad gives you the ability to run longer chunks of JavaScript code in the browser environment. 

Type

```javascript```
window
```

and hit enter. 

Now click the `Run` button. Nothing happens. That's because we're not _in_ the console, the way we were when we were in the Web Inspector console above. This isn't a console, so things aren't logging out (displaying their values). But what if we wanted to examine the `window` object? There are two options. One is to right-click the `window` text and choose `Inspect` from the pop-up menu (this lets you explore the current state of the `window` object on that line).

#### Exercise Thinking Points

* What happens if you modify the code in the ScratchPad to read: `console.log(window);` and click `Run`? Can you find the output?
* What is the value of the `window.document.URL` property? What does it refer to?

## Questions for Thought

* Is there a difference between JavaScript and ECMAScript? Why do both exist?
* Explore: What's the relationship between JavaScript and node?
