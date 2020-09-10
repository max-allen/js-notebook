
Not sure of it's exact origin. I've found a source that says Doug Crockford in 2001, and another that says it was developed by a number of people including
[Richard Cornford](https://groups.google.com/g/comp.lang.javascript/c/eTzWVa1W_pE/m/N9lnvRG9WJ8J) in 2003.

The simplest way of organizing your data and behavior into a single unit:

```js
var dealership = {
  manufacturer: 'ford',
  sell(car) {
    console.log(`Would you like this ${car} by ${this.manufacturer}?`)
  }
}
```

This is unofficially known as the **namespace pattern**. Not a syntactic feature of the language, but an idiom. It isn't a module, because the module pattern requires **encapsulation** (hiding data and behavior).

The state of a module is held by its methods via closure.

```js
var dealership = (function Module(manufacturer) {
  var publicAPI = { sell, };
  return publicAPI;

  function sell(car) {
    console.log(`Would you like this ${car} by ${this.manufacturer}?`)
  }
})('ford');

dealership.sell('2009 Taurus') // Would you like this 2009 Taurus by ford?
```

This usage of closure is closing over variables that are designed to change state over time. The purpose of a module is to track state over time.

```js
function DealershipModule(manufacturer) {
  var publicAPI = { sell, };
  return publicAPI;

  function sell(car) {
    console.log(`Would you like this ${car} by ${this.manufacturer}?`)
  }
};

var dealership = DealershipModule('2009 Taurus');
```

In the above, `DealershipModule` is a factory function, capable of creating many instances with their own states, and exposes the minimum api necessary for its purpose.

The module pattern isn't an example of first class support for modules – it's a prevalant idiom that's emerged from tools provided by the language.

**Enter ES6**

ES6 modules provide first class support for modules. TC39 and Node.js didn't coordinate their respective specs
well. As a result, ES6 modules had support in browers long before their server-side counterpart (approx. 5 years).

```js
var manufacturer = 'ford';

export default function sell(car) {
  console.log(`Would you like this ${car} by ${manufacturer}?`)
}
```
These modules are file-based, so it's _impossible_ to have more than one ES6 module in the same file. Without a build
process, if you wanted to ship each of these to the browser, the browser would need to load each file. Modern JS apps
are composed of _thousands_ of modules. People work around this with build tools like Webpack that'll compile their
ES6-authored modules to the old syntax.

These modules are also *singletons* (see IIFE example): they're only invoked once, and each subsequent import is a
reference to that instance. If you wanted to support creating multiple instances of your module, your API would need
to expose a factory function for this.