## 2015-02-25

Neat little trick that'll work in IE9+:

```javascript
var print = console.log.bind(console, '>');
print('Hello, World'); // > Hello, World
```
