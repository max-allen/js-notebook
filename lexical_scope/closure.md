The concept of closure comes from lambda calculus and predates computer programming. The linkage between a function and scope it was defined in.

```js
function ask(question) {
  setTimeout(function waitASec() {
    console.log(question);
  }, 100)
}

ask('What is closure?') // what is closure?
```

The `waitASec` function is closed over the variable `question`.

Academically, closure is on a per-variable basis, but modern JS engines implement closure as a linkage to the entire scope (therefore a scope-based operation).

```js
function ask(question) {
  return function holdYourQuestion() {
    console.log(question);
  };
}

var myQuestion = ask('What is closure?')

myQuestion(); // what is closure?
```

`holdYourQuestion` is closed over the variable `question`. 

Closure doesn't preserve a snapshot of the variable, but the actual variable itself. It preserves a linkage to that variable allowing access during execution.

```js
  var foo = 10;

  var logFoo = function() {
    console.log(foo);
  };

  foo = 2;

  logFoo(); // 2
```

```js
  for (var i = 1; i <= 3; i++) {
    setTimeout(function() {
      console.log(`i ${i}`);
    }, i * 1000);
  }
  // i: 4
  // i: 4
  // i: 4
```

```js
  for (var i = 1; i <= 3; i++) {
    let j = i;
    setTimeout(function() {
      console.log(`i ${i}`);
    }, i * 1000);
  }
  // i: 1
  // i: 2
  // i: 3
```

```js
  for (let i = 1; i <= 3; i++) { // treated as a new declaration of i for each iteration
    setTimeout(function() {
      console.log(`i ${i}`);
    }, i * 1000);
  }
  // i: 1
  // i: 2
  // i: 3
```