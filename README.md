## Operator Overloading

This adds operator overloading in a standardized and logical way.

----

methods can be descibed as 

\[ operator literal \](operand) {}  
Example: `+(y) {}`

or

~\[ operator literal \]() {}  
Example: `~+() {}`

----

*here we assume `X` is an object with the addition operator overridden*

The first is called when the operator is called from the *left hand side* of the operation.  
`X + 7` would call the `+() {}` method.

The second takes place when the operator is called from the *right hand side* of the operator.  
`7 + X` would call the `~+() {}` method.

----

```js
class Overloader {
  constructor(x) {
    this.x = x;
  }

  +(y) {
    return this.x + y;
  }

  // notice this takes no arguments
  ~+() {
    return this.x;
  }
}

const x = new Overloader(7);
console.log(x + 7) // 14;
console.log(7 + x) // 14;
```

----

#### Things to be decided:
- How to add this behavior to an existing function/class
  ```js
  function Overloader(x) {
    this.x = x;
  }
  // perhaps
  Object.defineProperty(Overloader.prototype, +, { value: (y) => this.x + y });
  // or maybe
  Object.defineOverload(Overloader.prototype, +, (y) => this.x + y);
  ```

----

#### Current issues with this proposal:
