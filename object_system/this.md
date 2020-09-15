```js
var dealership = {
  manufacturer: 'ford',
  sell(car) {
    console.log(`Would you like this ${car} by ${this.manufacturer}?`)
  }
}

// here ask is invoked with the this context of dealership (implicit binding)
dealership.ask('What is implicit binding?')
```

Unlike lexical scope, where the scopes are determined at authortime, with `this`
the context is determined dynamically at runtime. This tradeoff is intentional: flexibility
of `this` versus the predictability of lexical scoping.

```js
function sell(car) {
    console.log(`Would you like this ${car} by ${this.manufacturer}?`)
  }

var dealershipOne = {
  manufacturer: 'ford',
  sell
}

var dealershipTwo = {
  manufacturer: 'mazda',
  sell
}

// in this case there is just one function, ask, that's shared across objects and invoked in different contexts.

dealershipOne.sell('How do I share a method?')

dealershipTwo.sell('How do I share a method?')
```

the `this` context can be explicitly bound via the `.call` or `.apply` methods:

```js
var dealershipOne = {
  manufacturer: 'ford',
  sell
}

sell.call(dealershipOne, 'Can I explicitly set context?')
```

### Function context

Here, the value of `this` is not set by call, so `this` will default to the global object, `window` (assumes non-strict mode and in browser).

```js
function startEngine() {
  return this
}

startEngine() === window // true
```




