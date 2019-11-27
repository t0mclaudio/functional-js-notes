# Functional Programming in Javascript

## What is Functional Programming?
Functional programming is a way to organise and write code like a mathematical function. This minimizes bugs and improve maintanability by making code small, self-contained, and testable.

## Imperative vs Declarative
Imperative is written like a recipe and answers the question how things are done.
Declarative is in your face and defines what a function does written like a mathematical equation.

### Three concepts of functional programming
1. Immutabality
* Constants instead of variables
* Defining instead of assigning to variables
* We say x IS 3 instead of saying x IS EQUAL to 3
2. Separating functions and data
* Functions are separate from data unlike in OOP where often grouped together
* Functions do not modify data instead they return a new modified data
* Data are passed to functions and processed
3. First-class functions
* Allows us to treat function like how strings, objects, arrays can be handles
* Can be passed as arguments to other functions
* Functions work in isolation (Pure functions)


### Passing functions as arguments
### Function Creators -> Returning functions
``` js
  const createPrinter = () => () => console.log('hello');
  // is the same as it is written below

  const createPrinter = function() {
    return function() {
      console.log('hello');
    }
  }
```
```js
  const double = x => x * 2;
  const triple = x => x * 3;
  const quad = x => x * 4;

  // As implemented First Order Function
  const createMultiplier = y => x => x * y;
  const double = createMultiplier(2);
  const triple = createMultiplier(3);
  const quad = createMultiplier(4);

  double(3)
```

### Closure
Variable set in the parent is still accessible to child function

```js
  const createPriner = () => {
    const myFave = 42;
    return () => console.log(`Fav num is ${myFave}`);
  }

  const printer = createPrinter()
  printer() 
  // returns Fav num is 42
```

### Higher-Order Functions
```js
  const divide = (x, y) => x/y;

  const secondArgumentIsntZero = func => 
    (...args) => {
      if (args[1] === 0) {
        console.log('Error: dividing by zero');
        return null;
      }

      return func(...args);
    }
  const divideSafe = secondArgumentIsntZero(divide);
  console.log(divideSafe(7,0));  
```

### Spread Operator
```js
  const newObject = {
    ...object1,
    ...object2
  }

  const newObj = {
    ...obj1.name,
    ...obj2
  }
  const nArray = [1,2,3]
  const newArray = [
    ...nArray,
    4
  ]
// newArray will be [1,2,3,4]
```

### Map function
```js
  const numbers = [1,2,3];
  const double = x => x * 2;
  const doubledNumbers = numbers.map(double);
```
### Filter function
```js
  // function pass as parameter should return boolean
  const numbers  = [1,2,3,4,5];
  const isEven = x => x % 2 === 0;
  const evenNumbers = numbers.filter(isEven)
```
### Every/Some function
  Every function Returns True if everything condition is true 
  Some function return true if one element is true for condition

### Slice
  To return a new array for functions that mutate the array
  ```js
    const numbers = [1,2,3,4,5]
    numbers.slice().reverse() // slice returns new array while reverse mutates the new array
  ```
### Sorting
Sort is a mutating functions
It means use slice
Sort requires a comparative function
```js
  const mixNumbers = [9,8,2,6,7,3,4]
  const ascending = (a, b) => {
    if (a < b) return -1;
    if (a > b) return 1;
    return 0;
  }
  const sortedNumbers = mixNumbers.slice().sort(ascending);
```

### Recursion
```js
  const countDown = x => {
    if (x < 0) return;
    console.log(x);
    countDown(x-1)
  }
```