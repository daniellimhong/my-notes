# JavaScript Principles
- Thread Of Execution, Functions, Call Stack

## Key Takeaways
- Every Execution Context is made up of two parts: Thread of execution & Memory
- Every program will have a Global Execution Context and for every function call (in the order of the Thread of Execution), a new execution context will be created for each of them.
    - Execution Context for functions are deleted after it's finished running except for the return value
- Call Stack: a stack data structure that the javascript engine runs to keep track of the function that is currently running. global() will always be at the bottom when functions are running and current function running will always be at the top.

## Notes

### Thread of Execution
JavaScript code runs, it:
- Goes through the code line-by-line/ 'executes' each line -  known as thread of execution
- Saves 'data' like strings and arrays so that we can use that data later - in its memory

### Functions
- Code we save ('define') functions & can use (call/invoke/execute/run) later with the function's name & ()

Execution context
- Created to run the code of a function - has 2 parts
    - Thread of execution
    - Memory

### Call Stack
- JavaScript keeps track of what function is currently running (where's the thread of execution)
- When a function is ran -  the engine adds it to the call stack
- When it finishes running , it is removed from the call stack
- Whatever is top of the call stack, thats the function currently running
- Global() always at the bottom.

Example:

```javascript
const num = 3; 
function multiplyBy2(inputNumber){
	const result = inputNumber*2;
	return result;
}

const output = multiplyBy2(num);
const newOutput = multiplyBy2(10);
```

```javascript
/* 

// Global Execution Context:
# memory:
	num : 3
	multiplyBy2: function
	output: 6 {before multiplyBy2 Execution Context, it is empty} / { after, it is 6}
//

**Executing** output = multiplyBy2(3);
// multiplyBy2 Execution Context:
# local memory:
	input number : 3 (also known as the argument)
	result : 6
# execution context:
	return result 
//
note: since "output = multipleBy2(3), output is set to the return value of the 
function call, which will be 6"

**Executing** newOutput = multiplyBy2(10);
// multiplyBy2 Execution Context:
# local memory:
	input number : 10
	result : 20
# execution context:
	return result 
//
*/
```

```javascript
// Call Stack

/* 
	1. multiplyBy2(10)
	2. global()
*/
```