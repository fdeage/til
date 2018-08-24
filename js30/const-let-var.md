# `var`, `const` & `let`

## `var`

`var` has been in JS since the beginning of JS. It's, historically, THE way to declare a variable.

`var` is not lexically bound (=not scoped to a block):

```
function fn() {
  let foo = "bar";
  var foo2 = "bar";
  if (true) {
    let foo; // no Error, foo === undefined
    var foo2;
    // foo2 has been rewritten!
    foo = "qux";
    foo2 = "qux";
    console.log(foo);
    // "qux", the variable belongs to its block
    console.log(foo2);
    // "qux"
  }
  console.log(foo);
  // "bar", the variable belongs to its block ("fn" function)
  console.log(foo2);
  // "qux"
}
```

Basically `var` has a global (if declared outside) or *function* scope (while `let` has a *block* scope).

```
var x = "outside";
function foo() {
  var x = "inside"; // x is redefined: it's another one
  console.log(x);
}
foo(); // inside
console.log(x); // outside
```

```
var x = "outside";
function foo() {
  x = "inside"; //same global x
  console.log(x);
}
foo(); // inside
console.log(x); // inside
```


`var` variables are hoisted (cf. below): declarations are read at the beginngin (but not the assignation!).

`var` is implicit: `myVar = 3` is equivalent to `var myVar = 3` *in a global context* (if used for the first time). Note that the global object in a browser is `window`.

Now that `let` and `const` are here, `var` should be used only with `try/catch` (sometimes).

## `const`

New. `const` is the right choice 99% of the time (the other 1% being `let`, if we need to modify the reference)

`const`: unique assignation lexically bound (scoped to the block).

A `const` can't be reassigned (that would trigger a `TypeError: Assignment to constant variable`), but can be mutated: the reference cannot change, but the objet the `const` is refering to can change (cf. `freeze`).

Array mutation:

```
const a = [1];
const b = a;
console.log(a === b); // true
b.push(2);
console.log(a === b); // true
console.log(a); /// [ 1, 2 ]
```

Object mutation:

```
const obj = {};
obj.i = 1;
console.log(obj); // { i: 1 }
```

```
function fn() {
  const foo = "bar"
  if (true) {
    const foo // SyntaxError, a `const` needs to be assigned
    const foo = "qux"
    foo = "norf" // SyntaxError, can't be reassigned
    console.log(foo)
    // "qux", the variable belongs to its block's scope ("if")

    const CONFIG = [];
    CONFIG.push(12);
    console.log(CONFIG); // [12]
}
  console.log(foo)
  // "bar", the variable belongs to the `fn` function
}
```

## `let`

The other 'new' declaration of ES6 (the other one being `const`)
> "`let` is the new `var`"

Scoped to the current block -> to be used in loops to avoid conflicts with other variables

## Hoisting

All `var` variables declarations behave as if they were made at the beginning of the scope (declarations only, not assignations):

```
console.log(a); // ReferenceError: a is not defined
console.log(b); // undefined
var b = 0;

console.log(c); // ReferenceError: c is not defined
let c = 2;
```

becomes

```
console.log(a);
var b;

console.log(b);
b = 0;

console.log(c);
let c = 2;
```

`let` and `const` don't have this, which can lead to potential *temporal dead zones*:

```
function fn() {
  console.log(foo); // ReferenceError, TDZ!
  let foo = "bar";
}
```
