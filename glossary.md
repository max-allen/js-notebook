**Indentifiers** are sequences of of characters that identify a variable, function, or property.
```javascript
let bar = 10; // bar is the identifier here
```

**Statements** are any groups of words, numbers, and operators that peform a specific task.

**Expressions** are any reference to variables or values, or sets of variables and values combined with operators.
  - literal value expression: `2`
  - variable expression: `foo`
  - arithmetic expression: `foo + 2`
  - assignment expression: `baz = foo + 2`

```javascript
/*
this statement assigns the value returned by the length function
to the variable noResults
*/
const noResults = shipments && !shipments.length
```

**Undeclared indentifiers** have no formal declaration at any scope. No memory allocation.

**Undefined indentifiers** have been formally declared and a location in memory, but no associated value.

**Lexical scope** is the name for the type of scope javascript determines at compile time. The name _lexical_ refers to the lexing stage of compilation. Scopes are fixed at authortime and are not affected by runtime conditions.

**Hoisting** is a term used to describe the behavior of execution contexts in JavaScript. It suggests variable and function declarations are moved to the top of your code. This isn't what actually happens though – declarations are put into memory during the compile phase.

**Closure** describes the ability of a function to remember and access its lexical scope despite being executed in a different scope.