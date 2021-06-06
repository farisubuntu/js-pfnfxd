

// Ch5: Closures:

_**closure is all around you in JavaScript, you just have to recognize and embrace it.** Closures are not a special opt-in tool that you must learn new syntax and patterns for. No, closures are not even a weapon that you must learn to wield and master as Luke trained in The Force.

> **From MDN**: A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

> closures enables us to create stateful functions.

> Stateful functions are functions that can “remember” data from previous executions.

**Notes**: 

- When we start our program, the engine will create a **global execution** context for us and this "context" will Never _die_.

- Every time we invoke a function, a new **execution context** is created, and each execution context has it’s own “Variable Environment” or “scope”. _This local variable environment is holding all arguments that got passed to it and all declarations made inside the body of the function_,

For example lets create a function that “remembers” and count how many times it got executed:

**First: this will not work well, because we recreating the numOfExecutions variable every time we invoke "counter()"**

```js
function counter(){
  let numOfExecutions = 0;//function executing context
  numOfExecutions++;
  console.log(numOfExecutions);
}
counter() // 1
counter() // 1

```
**Second, change the 'numOfExecutions' to be global will working but it _bad practice_**

```js
let numOfExecutions = 0;//Global execution context

function counter() {
  numOfExecutions++;
  console.log(numOfExecutions);
}
function someFunc() {
  numOfExecutions = 100;
}
someFunc()
counter() // 101
counter() // 102

```

**Third: Usinbg Lexical Scope**

```js
function createCounter() {
  // creating a wrapping execution context
  // so we won't pollute the global environment
  let numOfExecutions = 0;

  // creating and returning an inner function that closes over the lexical environment
  function counter() {
    numOfExecutions++;
    console.log(numOfExecutions);
  }
  return counter;
}
const counter = createCounter();
counter() // 1
counter() // 2
```_