# Learning JavaScript

*Note*: Right now this is just a catch-all place for some JavaScript learning resources and scribbly notes. I may continue to organize this more formally as we go.

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

## Questions for Thought

* Is there a difference between JavaScript and ECMAScript? Why do both exist?
* Explore: What's the relationship between JavaScript and node?

## Exercises

These let you try out a couple of places that you can go to test JavaScript and inspect the state of the browser environment.

### Web Inspector, the `window` object

In Chrome, open the Web Inspector (`Option-Cmd-I` on a Mac) and go to the `console` tab.

Type

```javascript
window
```

and hit enter.

What this does is display (print out) a representation of the value for the identifier `window`. `window` is a JavaScript `Object` that is made available by the `environment` in the browser (if "Object" and "environment" are mysterious concepts as of yet, don't fret, they'll come up later). 

Expand the `window` object and explore it a bit, especially the stuff under the `document` property (itself another object...it's objects all the way down!). The `document` object contains representations of a lot of stuff about the web document in the browser window and you may start seeing some items that look familiar here.

### ScratchPad, `window` object redux

In Firefox, go to `Tools -> Web Developer -> Scratchpad...`. You can [read more about it here](https://developer.mozilla.org/en-US/docs/Tools/Scratchpad) if you like.

The console in Web Inspector or the Console in Firefox are useful for quick, one-line things (in the previous example, `window` gets evaluated as soon as you hit enter), but ScratchPad gives you the ability to run longer chunks of JavaScript code in the browser environment. 

Type

```javascript```
window
```

and hit enter. 

Now click the `Run` button. Nothing happens. That's because we're not _in_ the console, the way we were when we were in the Web Inspector console above. This isn't a console, so things aren't logging out (displaying their values). But what if we wanted to examine the `window` object? There are two options. One is to right-click the `window` text and choose `Inspect` from the pop-up menu (this lets you explore the current state of the `window` object on that line).

#### Thinking Points

* What happens if you modify the code in the ScratchPad to read: `console.log(window);` and click `Run`? Can you find the output?
* What is the value of the `window.document.URL` property? What does it refer to?
