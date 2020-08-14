Lexical Scope
- We need to understand lexical scope so we can understand closure.
- We need to understand closure so we can understand the module pattern.

Scope is where we look for things. What are we looking for? Identifiers. All variables fall into two roles:
receiving assignment, or you're retreiving a value from the variable.

JS engine sorting variables into scopes.

Syntax error on line 10, but you receive an error message prior to execution of lines 1 through 9. It's because JS goes through a processing step first.

4 Stages to Compiler Theory:
- Lexing
- Tokenization
- Parsing
- Code Generation

_*(lexing & tokenization are ocasssionally done together)_

Interpreted v Compiled not the distribution model for the binary, but is the code processed prior to being executed

In a true scripting language (e.g bash script), if you have a syntax error on line 5, you may need to worry about / undo what happened on lines 1-4 because they've actually been executed.

During compilation / parsing step, develops plan for lexical environment. Where each of the lexical scopes are, and which indentifiers belong to each scope. This is the executable code handed off to be executed by another part of the engine (JVM). During execution, whenever it reaches a scope, it generates the indentifiers that should belong to that scope based on the given instructions.

So JS is a two pass system, not a single pass

Units of scope are:
 - functions
 - blocks (es6)

Two variables belonging to different scopes with the same name is called `shadowing`

```javascript
var foo = 'bar'

function fooLogger() {
  let foo = 'baz'
  console.log('FOO', foo)
}

fooLogger();
```

Example above will parse and execute just fine, but because there's an identifier with the name foo belonging to fooLogger's scope, there's no way for us to lexically access foo belonging to the global scope.

In a lexically scoped language, all scopes are determined at compile-time, not runtime.
More efficient.

During compiliation step, compiler also determines whether identifier is `target` (receiving assignment), or 
`source` (having value retrieved)

Post Compilation (Code Execution)
&ndash; variable declarations are gone

```javascript
foo = 'bar';

// fooLogger function declaration no longer exists now that we're at runtime

fooLogger();
```
JVM requests information about each identifier from Scope Manager (SM).
  - JVM asks SM for access to `foo` in global scope, assigns `'bar'` (`foo` is an area in-memory that requires assignment).
  - JVM asks for access to `fooLogger` and invokes function returned by SM. During invocation, JVM asks SM for `foo` identifier via `fooLogger` scope, assigns `baz`. JVM asks for access to `console` via `fooLogger` scope, but it doesn't exist, so it checks one level up at global scope.

```javascript

let foo = 'baz';

function fooLogger() {
  foo = 'bar';
  qux = 10;
  console.log('foo');
};

fooLogger();

foo;
qux;
```
Compilation
- JVM processes formal declaration of foo. Asks SM for existence of identifier foo in global scope. foo doesn't exist, so location in memory is created for foo.
- JVM repeats this process for fooLogger function declaration and additionally creates fooLogger scope. the statements within `fooLogger` aren't formal function declarations, so compliation is finished.

Execution
- JVM processes target reference for `foo`. `foo` exists in global scope, so value `bar` is assigned to it.
- JVM processes source reference for `fooLogger`. `fooLogger` is present in scope, retrieved, and executed. Execution moves to body of
  `fooLogger`.
- target reference for foo is processed. JVM checks `fooLogger` scope for existence of `foo` identifier. It doesn't exist so checks one
  level up at global scope. location is retrieved and assignment `bar` is made.
- target reference for qux is processed. Not found in the scope of `fooLogger`. Check is made globally,`qux` is not found, so location
  in memory is created for `qux` and returned to JVM for assignment of value `10`.

  This is one of the bad parts of JavaScript: **auto globals**. If you try to assign to a variable that hasn't been formally declared,
  once you arrive at the global scope, the global scope will create the variable for you. auto globals aren't suppported in `strict mode`.

- The final two lines source references to `foo` and `qux`, respectively. Both identifiers exist within global scope, so values are
  retrieved. Because of the invocation of `fooLogger`, `qux` exists within the global scope.

```javascript
let foo = 'baz';

function fooLogger() {
  foo = 'bar';

  function say(something) {
    console.log(foo, something);
  };
  say('here');
};

fooLogger();
say('where are you');
```

- in the above, it's important to note that the identifier `something` belogs to the scope of `say`. a function parameter formally
  declares a variable in that scope. The literal `here` is assigned to `something` during execution.
-  the source reference when say is invoked globally results in a reference error being thrown.
