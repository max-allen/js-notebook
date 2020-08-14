```javascript
function getCars() {}

// Get another car is a function expression

var nextCar = function getAnotherCar() {
  console.log(getAnotherCar)
}

getCars
nextCar
getAnotherCar
```

- the source reference to `getAnotherCar` within itself is fine, because its identifier has
  been added to its scope, but the source reference that occurs globally will result in a
  reference error.

**function declarations** add their identifier to the enclosing scope, while **function expressions** create
a new scope, and add their identifier to it; this identifier is read-only.

```javascript
  const pressHandler = function() {}
  const blurHandler = function handleBlur() {}
```

- `blurHandler` is a **named function expression**. `pressHandler` is an **anonymous
  function expression**.
  - named function expressions allow self-reference
  - names for function expressions appear in stack traces

```javascript
const ids = people.map(person => person.id)

const ids = people.map(function getId(person) {
  return person.id
})
```

```javascript
getPerson()
  .then(person => getData(person.id))
  .then(renderData);

getPerson()
  .then(function getDataFrom(person) {
    return getData(person.id);
  })
  .then(renderData);
```

Immediately Invoked Function Expression (IIFE)
- Able to run without polluting enclosing scope
  - use can help avoid naming collisions

```javascript
let foo = 'baz';

(function fooLogger() {
  let foo = 'bar';
  console.log(foo);
})();

console.log(foo)
```