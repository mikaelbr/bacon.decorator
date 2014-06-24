# Bacon.decorate

> Unify your API and abstract time using Functional Reactive Programming and [Bacon.js](https://github.com/baconjs/bacon.js)

APIs are hard. Sometimes they can have you provide a callback,
other times they return a promise or not even be async. You
can unify the usage of your API and abstract consepts like
sync or async, by using Functional Reactive Programming
and the help of a implementation called [Bacon.js](https://github.com/baconjs/bacon.js).

The result of function calls will be reactive data types
from [Bacon.js](https://github.com/baconjs/bacon.js). If you
are unsure how to use Bacon, the [Bacon.js README](https://github.com/baconjs/bacon.js)
is very helpful and comprehensive.

## Example

```javascript
var decorate = require('./');
var Q = require('q');

var m = {

  // Async values using promises
  get: decorate.promise(function (arg1, arg2) {
    // Could be something like $.ajax aswell
    var def = Q.defer();
    setTimeout(function () {
      def.resolve("Async?");
    }, 1000);

    return def.promise;
  }),

  // Async values using callbacks
  getAnother: decorate.callback(function (a, b, callback) {
    setTimeout(function () {
      callback(a + ", " + b)
    }, 1000);
  }),


  // Regular sync values
  sync: decorate.value(function (a, b) {
    return a + ", " + b;
  }),

  // Or using events
  // This is an Event Stream of body content
  // triggered on click
  event: decorate.event('click', function () {
    return document.body;
  }, '.currentTarget.innerHTML')
};
```

By adding decorator to all methods, we can access them
without thinking about if it's async or sync and we
can easily combine them in different ways.

### Example of waiting for multiple data inputs:

```javascript
// Waiting for multiple values (example)
m.get('foo', 'bar')
  .combine(m.getAnother('Foo', 'Bar'), function (a, b) {
    return a + ": " + b;
  })
  .combine(m.sync('Baz', 'Qux'), function (a, b) {
    return a + ", " + b;
  })
  .onValue(function (value) {
    console.log('val', value);
    //=> val Async?: Foo, Bar, Baz, Qux
  });
```

## API

### ```decorate.callback```
More info soon

### ```decorate.event```
More info soon

### ```decorate.promise```
More info soon

### ```decorate.value```
More info soon

### ```decorate.array```
More info soon

### ```decorate.interval```
More info soon

### ```decorate.sequentially```
More info soon

### ```decorate.repeatedly```
More info soon

### ```decorate.later```
More info soon

### ```decorate.poll```
More info soon


## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)



