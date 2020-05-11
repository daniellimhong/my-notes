## Key Takeaways

- Closure ('the backpack') is the instance of functions holding on to data from an outside scope in between execution by returning functions from another function.

```javascript
function outer(){
	let counter = 0;
	function incrementCounter(){
		counter ++;
	}
	return incrementCounter;
}

const myNewFunction = outer();
```

- console.dir(myNewFunction) reveals:
    - that the hidden property of '[[Scope]]' contains the backpack/closure holding the live data of counter.
    - because incrementCounter accesses 'counter', outside of its function scope, JavaScript creates a closure so that incrementCounter can continue to access that variable.
    - This is necessary because after a function's execution context is finished running, normally all memory and variables are to be deleted. The closure or backpack will allow functions to continue accessing variables that should be deleted after the function continues executing.

---

## Notes

- Intro
    - Closure is the most esoteric of JavaScript concepts
    - Enables pro-level functions like 'once' and 'memoize;
    - Many JS design pattern including the module pattern use closure
    - Functions get a new memory every run/invocation
    - Functions with memories
        - when our functions get called, it creates a live store of data (local memory/variable env/state) for that function's execution context
            - when is finished executing, the local memory is deleted (except return value)
        - **What if our functions could hold on to live data between executions?**
            - Would let our function definitions have an associated cache/persistent memory
            - It all starts with **us returning a function from another function**

- Returning Functions
    - Functions can be return from other functions in JavaScript 

    ```javascript
    function createFunction(){
    	function multiplyBy2(num){
    		return num*2;
    	}
    	return multiplyBy2;
    }

    const generatedFunc = createFunction();
    const result = generatedFunc(3);
    /* 
    	// Global Execution Context:
    	# memory:
    		createFunction: function
    		generatedFunc: multiplyBy2 (function declaration)
    		result : 6
    	//
    	
    	**Executing** generatedFunc = createFunc();
    	// createdFunc Execution Context:
    	# local memory:
    		multiplyBy2 : function
    		output: multiplyBy2 (returning the function)
    		
    	# thread of execution:
    		what function is doing 
    	//
    	
    	**Executing** result = generatedFunc(3);
    	// generatedFunc(3) Execution Context:
    	# local memory:
    		num : 3
    		output: 6
    		
    	# thread of execution:
    		what function is doing 
    	//
    */
    ```

- Nested Function Scope
    - Calling a function in the same function call as it was defined

    ```jsx
    function outer(){
    	let counter = 0;
    	function incrementCoutner(){
    		counter ++;
    	}
    	incrementerCounter();
    }

    outer();
     /* 

    	// Global Execution Context:
    	# memory:
    		outer: function
    	//
    	
    	**Executing** outer();
    	// outer() Execution Context:
    	# local memory:
    		counter : 0
    		incrementCounter: function
    		
    	# thread of execution:
    		incrementCounter()

    			**Executing** outer();
    		// incrementCounter() Execution Context:
    		# local memory:
    			
    		# thread of execution:
    			counter++
    	//

    	

    call stack
    incrementCoutner()
    outer()
    global()
    */
    ```

- Retaining Function Memory

    ```jsx
    function outer(){
    	let counter = 0;
    	function incrementCounter(){
    		counter ++;
    	}
    	return incrementCounter;
    }

    const myNewFunction = outer();
    myNewFunction();
    myNewFunction();

    /* 

    	// Global Execution Context:
    	# memory:
    		function outer : incrementCounter
    		const myNewFunction : outer()
    	//
    	
    	**Executing** myNewFunction = outer();
    	// outer() Execution Context:
    	# local memory:
    		- counter : 0
    		- incrementCounter: function
    		returns output : incrementCounter
    		
    	# thread of execution:
    		none
    	//

    	**Executing** myNewFunction()
    	// myNewFunction() Execution Context:
    	# local memory:
    		- counter : 0
    		
    	# thread of execution:
    		counter ++
    	//
    			

    */
    ```

- Function Closure
    - a backpack of data carried over
    - hidden property/hidden square bracket [[Scope]] property
    - it can only be accessed by running the function, not dot notation.
    - this is considered private data/variables.

- Closure Technical Definitions & Review

    C.O.V.E 
    - Closed over variable environment

    P.L.S.R.D
    - Persistent, lexical-scoped, static, reference data

    Closure
    - the main term!
    - called P.L.S.R.D/Backpack
    - the 'backpack' (or 'closure') of live data is attached to incrementCounter (then to myNewFunction) thorugh a hidden property known as [[scope]]] which persists when the inner function is returned out

    Scope
    - rules of at what given line, what data is available to me?

- Closure Applications
    - Closure gives our functions persistent memories and entirely new toolkit for writing professional code
        - **Helper functions:** everyday professional helper functions like 'once' and 'memoize'
        - **Iterators and generators:** Which use lexical scoping and closure to achieve the most contemporary patterns for handling data in JavaScript
        - **Module pattern:** Preserved state for the life of an application without polluting the global namespace
        - **Asynchronous JavaScript:** Callbacks and Promises rely on closure to persist state in an asynchronous environment
