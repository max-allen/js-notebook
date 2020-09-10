```javascript
foo;
bar;

var foo = 10;
var teacher = 15;
```

**let dosen't hoist**

`var` will initialize with the value `undefined`, but `let` isn't initialized until the definition is evaluated, so any attempt to access the variable prior to initialization will result in a reference error. This is referred to as the _Temporal Dead Zone_. This exists for academic reasons vis-a-vis `const`. If `const` were initialized at declaration with the value `undefined` and assigned a different value at execution, it would technically have had different values at different points in time. Academically, this would violate the concept of a `const`, which is why TDZ exists for block scoped variables.

Due to this behavior, it may seem that _let doesn't hoist_. But that is incorrect:

```javascript
var foo = 'garden';
{
  console.log(foo); // this similarly results in a reference error
  let foo;
}
```

If `let` didn't hoist, the source reference of `foo` should log `garden`. The declaration is handled at compile time.