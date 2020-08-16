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

```js
var manufacturer = 'ford';

export default function sell(car) {
  console.log(`Would you like this ${car} by ${manufacturer}?`)
}
```