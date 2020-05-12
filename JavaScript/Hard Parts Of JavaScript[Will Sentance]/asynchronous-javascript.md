# Asynchronous JavaScript

## Key Takeaways

- Web Browser API are separated from JavaScript but work alongside together
    - Web Browser features like HTML DOM, DevTools, Network Requests, and Browser Timer are respectively referred to in JS as:
        - document.(code)
        - console.(code) [i.e: console.log, console.dir]
        - xhr / .fetch()
        - setTimeout/setInterval
- ES5 Solution of Asynchronous Code was with callback functions and web browser APIs
    - In the execution context when an asynchronous function is used like setTimeout, code is sent to the WebAPI context and then to the callback queue
    - The **event loop** is continuously checking for code to execute in the call stack and will only push code from callback queue to the call stack when all the function or frames (in the global execution context) has finished executing.
- Problems with ES5 Async Callbacks:
    - our response data is only available in the callback function - **callback hell**
    - error handling is implicit
- Benefits:
    - Super explicit once you understand how it works under-the-hood

---

## Notes

- Single Threaded Execution Review
    - Promises, Async & the Event Loop
        - Promises - the most significant ES6 feature
        - Asynchronicity - the feature that makes dynamic web application possible
        - The event loop - JavaScript's triage
        - Microtask queue, Callback queue and Web Browser features (APIs)
    - A reminder of how JS executes code

    ```jsx
    const num = 3;
    function multiplyBy2 (inputNumber){
    	const result = inputNumber * 2;
    	return result
    }

    const output = multiplyBy2(num);
    const newOutput = multiplyBy2(10);

    /* Execution Context 

    Global Memory:
    num : 3
    multiplyBy2 : function
    output : 6
    newOutput : 20
    thread of execution 

    **output = multiplyBy2(3) Execution Context**
    	Local Memory 
    	inputNumber : 3
    	[return] result : 6

    	thread of execution 
    	inputNumber * 2 = result
    **end execution context**

    **newOutput = multiplyBy2(10) Execution Context**
    	Local Memory 
    	inputNumber : 10
    	[return] result : 20

    	thread of execution 
    	inputNumber * 2 = result
    **end execution context**
    */
    ```
---
- Asynchroncity In JavaScript

    Asynchronicity is the backbone of modern web development in JS yet...

    - JS is single threaded (one command runs at a time)
    - Synchronously executed (each line is run in order the code appears)
    - Assuming we have a task:
        - Accessing Twitter's server to get new tweets that take a long time
        - Code we want to run using those tweets
        - Challenge: We want to wait for the tweets to be stored in tweets so that they're there to run displayTweets on - but no code can run in the meantime

    ```jsx
    //Slow function blocks further code running

    const tweets = getTweets('URL')

    // there's a wait while a request is setn to a twitter
    displayTweets(tweets)

    // more code to run
    console.log('let me run!')

    ```

    ```jsx
    // What if we delay a function directly using setTimeout?

    function printHello(){
    	console.log('hello')
    }

    setTimeout(printHello, 1000);
    console.log("Me first");

    ////
    setTimeout(printHello, 0);
    console.log("Me first");

    ```

    - JavaScript is not enough - we need new pieces (some of which aren't javascript at all)
        - Core JavaScript engine: Thread of execution, memory/variable environment, callstack
        - Our new components:
            - Web Browser APIs/Node background APIs
            - Promises
            - Event loop, Callback/Task queue and microtask queue
---
- Asynchronous Browser Features

    Browser Features: 

    - DevTools (console), Network Requests (XHR/Fetch), HTML DOM (document), Timer (setTimer),
    - We use JavaScript to work with these Web Browser APIs
    - These browser features are not native to JavaScript.

---
- Web API Examples

    ```jsx
    // ES5 Solution: Introducing 'callback function', and Web Browser APIs

    function printHello(){
    	console.log('Hello')
    }

    setTimeout(printHello, 1000);

    console.log("Me first")

    /* Execution Context 

    Global Memory:
    	printHello : function

    thread of execution:
    	setTimeout(printHello, 1000)
    		web browser : 1000ms
    	
    	console.log("Me first")

    web browser features:
    	in 1000ms => printHello() 

    **console**
    1. Me first
    2. (after 1000ms): Hello
    */
    ```

    - In the thread of execution, after setTimeout sends the function and the time parameter to the web browser features "thread of execution"(timer), it is technically finished on the execution context of javascript so the console.log of "me first" shall run first and after 1000ms, the printHello function will execution.
---
- Web API Rules & Callback Queue & Event Loop

    ```jsx
    // ES5 Web Browser APIs w/ callback functions
    // We're interaction with a world outside of JS now - so we need rules

    function printHello(){
    	console.log('Hello')
    }
    function blackFor1Sec(){
    	// blocks in the javascript thread for 1 sec
    }

    setTimeout(printHello, 0);

    blockFor1Sec();
    console.log('Me first')

    /* Execution Context 

    Global Memory:
    	printHello : function
    	blockFor1Sec: function

    thread of execution:
    	setTimeout(printHello, 0)
    		web browser : 0ms
    	
    	blockFor1Sec()

    	console.log("Me first")

    web browser features:
    	timer feature
    		in 0ms => printHello() 

    **console**
    1. after 1000ms Me first
    2. Hello
    */
    // Notes: printHello is thrown into the callback queue and 
    // jump into the call stack until the global execution context is 
    // done finished execution.
    ```
    - Callback Queue
        - where the asynchronous code gets pushed to, waits for the execution
    - Event Loop
        - job is to continuously check if call stack(main stack) has any functions or frames to run. If not, it checks the callback queue and if there is anything in the callback queue, it will be pushed into the call stack.
    - For clarification on chart below:
        - Stack = call stack where code/functions gets pushed and executed, gets popped once the execution is done
        - Heap = where all the memory allocation happens for variables
    - Problems:
        - our response data is only available in the callback function - callback hell
        - maybe feels odd to think of passing a function into another function only for it to run much later
        - error handling is implicit
    - Benefits:
        - Super explicit once you understand how it works under-the-hood