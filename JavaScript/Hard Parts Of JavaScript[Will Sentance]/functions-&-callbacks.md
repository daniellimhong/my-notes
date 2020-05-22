# Functions & Callbacks (& Higher Order Function)

## Key Takeaways

- Functions, under the hood, are first class objects. Which is why they can be assigned to variables and properties of other objects
- **Higher Order Function:** the outer function that accepts a function as a parameter
  - Any function that takes in a function or returns a function is automatically a higher order function
- **Callback:** the function we insert as a parameter
- Callbacks and Higher Order Functions Simplify our code and keep it DRY.

## Notes

### Generalized Functions

- We have functions to make them reusable (DRY: Don't repeat yourself)
- Parameters (placeholders) mean we don't need to decide what data to run our functionality on until we run the function
- Higher order functions follow this same principle.
  - We may not want to decide exactly what some of our functionality is until we run our function.

### Repeating Functionality

Example #1

```javascript
function copyArrayAndMultiplyBy2(array) {
  const output = [];
  for (let i = 0; i < array.length; i++) {
    output.push(array[i] * 2);
  }
  return output;
}

const myArray = [1, 2, 3];
const result = copyArrayAndMultiplyBy2(myArray);

/* 

// Global Execution Context:
    # memory:
        copyArrayAndMultiplyBy2: function
        myArray: [1,2,3]
        result : 
    //

    **Executing** result = copyArrayAndMultiplyBy2(myArray);
    // copyArrayAndMultiplyBy2 Execution Context:
    # local memory:
        array : [1,2,3];
        output: [2,4,6]
        
    # thread of execution:
        what function is doing 
    //

    Call Stack:
    1. copyArrayAndMultiplyBy2
    2. global()
*/
```

- imagine having to repeat this for adding by 3 or dividing by 2
- we can insert functionality to GENERALIZE our code.

Example #2

```javascript
// Example of generalizing the above code to make it more reusable

function copyArrayAndManipulate(array, instructions) {
  const output = [];
  for (let i = 0; i < array.length; i++) {
    output.push(instructions(array[i]));
  }
  return output;
}

function multiplyBy2(input) {
  return input * 2;
}

const result = copyArrayAndManipulate([1, 2, 3], multiplyBy2);
```

### Higher Order Function Examples

Example #1

```javascript
function copyArrayAndManipulate(array, instructions) {
  const output = [];
  for (let i = 0; i < array.length; i++) {
    output.push(instructions(array[i]));
  }
  return output;
}

function multiplyBy2(input) {
  return input * 2;
}

const result = copyArrayAndManipulate([1, 2, 3], multiplyBy2);

/* 
    // Global Execution Context:
    # memory:
        copyArrayAndManipulate: function
        multiplyBy2: function
        result : 
    //

    **Executing** result = copyArrayAndManipulate([[1,2,3], multiplyBy2);
    // copyArrayAndManipulate Execution Context:
    # local memory:
        array : [1,2,3];
        instructions : function (multiplyBy2)
        output: [ ]
        
    # thread of execution:
        what function is doing 
    //


    **Executing** multiplyBy2(array[i])
    // multiplyBy2 Execution Context:
    # local memory:
        input : 1
        return: 2
        
    # thread of execution:
        what function is doing 
    //

    Call Stack:
    1. multiplyBy2(1) 
    2. copyArrayAndManipulate
    4. global()
*/
```

### Callbacks & Higher Order Functions

- Functions in javascript = first class objects
- They can co-exist with and can be treated like any other javascript objs
- Behind the scenes, functions are objects
  1. assigned to variables and properties of other objects
  2. passed as arguments into functions
  3. returned as values from functions

**The Higher Order Function:**

- The outer function that takes in a function is our higher-order function

**Callback function:**

- The function we insert is our callback function

I.E: previous example

- Higher order function: copyArrayAndManiulate
- Callback: multiplyBy2

#### Note on Arrow Functions

Arrow functions - a shorthand way to save functions
anonymous & arrow function:

- improve immediate legibility of the code
- syntactic sugar
- understanding how they work under-the-hood is vital to avoid confusion
- certain reasons to not use, involving objects and prototypes
