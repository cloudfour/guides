Today I learned a bit about CSS `filter`, which is a *property* that allows you to do a bunch of annoying things, but I find that the `grayscale` filter value is not terrible. I played around in a [codepen](http://codepen.io/lyzadanger/pen/vEpxMy) and noted:

* You can transition on `filter`, at least in some browsers
* You can listen for `transitionend` just like with any transition
* `grayscale` can take a percentage argument which operates something like the "opacity" of the filter, e.g. `grayscale(50%)`

I do not however know the performance impacts of filters and those transitions and anticipate they could be significant issues.

## Events

`transitionend` events are useful but supported inconsistently, no surprise there. [Bootstrap's transition.js](https://github.com/twbs/bootstrap/blob/master/js/transition.js) does a decent job of wrapping that up. I adapted a slightly boiled-down variant of this for my own use. Intriguingly the feature test involves checking for a `style` property on a given element.
