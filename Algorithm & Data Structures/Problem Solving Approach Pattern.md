# Problem Solving Approach & Pattern

## Introduction:

Why is it important to learn algorithms?
- Almost everything that you do in programming involves some kind of algorithm
- It's the foundation for being a successful problem solving and developer
- Also applies to interviews

How do you improve?
1. Devise a plan for solving problems
2. Master common problem solving patterns
    - A lot of these interview questions can be broken down and classified under a category and if you can identify them, there are some steps you can follow to solve the problem

**Problem Solving**
1. **Understand the Problem**
2. **Explore Concrete Examples**
3. **Break it Down**
4. **Solve/Simplify** 
5. **Look Back and Refactor**

Approach won't solve the problem for you but it helps you sit and think about a problem and how to break it down. 

Many of these strategies are adapted from George Polya, whose book "How To Solve It" is a great resource for anyone who wants to become a better problem solver.

---

## Understand the Problem

1. Can I restate the problem in your own words? (not word for word)
    - To make sure you really understand the question
2. What are the inputs that go into the problem?
3. What are the outputs that should come from the solution to the problem?
4. Can the outputs be determined from the inputs?
    - In other words, do I have enough information to solve the problem?
        - (You may not be able to answer this question until you set about solving the problem. That's okay; it's still worth considering the question at this early stage.)
5. How should I label the important pieces of data that are a part of the problem?

```js
    // Write a function which takes two numbers and returns their sum
    
    /* 
    1. Can I restate the problem in my own words?
    - "implement addition
    
    2. What are the inputs that go into the problem?
    - ints? floats? strings for large numbers?
    
    3. what are the outputs that should come from the solution 
    to the problem?
    - int? floats string?
    
    4. Can the outputs be determined from the inputs?
    - Most of the time yes
    - But if you think about it, what happens if someone passes 
    only one number? We don't have enough information to do addition
    at that point. Do we add zero or return undefined or null? 
    What do we do? It dpends. It's good to ask interviewers at that 
    point  
    
    5. How should I label the important pieces of 
    data that are a part of the problem?
    - function called Add
    - num 1 & num 2
    - sum (to be returned)
    */
```
---

## Explore Concrete Examples

- Coming up with examples can help you understand the problem better
- Examples also provide sanity checks that your eventual solution works how it should
- Applies to User Stories & Unit Test

Explore Examples:

- Start with Simple Examples
    - Two or three simple examples, easiest use cases
- Progress to more Complex Examples
- Explore Examples with Empty Inputs
- Explore Examples with Invalid Inputs (more for real world)

```js
    // Write a function which takes in a string and returns 
    counts of each character in the string.
    
    charCount("aaaa") // {a: 4}
    
    // with these examples, the question that come up are as follows
    charCount("hello") /* do we want to account for all letters in
    the alphabet or only print the letters in the string?
    */
    charCount("my phone number is 182763") // do we include numbers and spaces
    charCount("Hello hi") // how about uppercase and lowercases? how do we handle?
    
    // These are questions we need to clarify
    
    charCount("") //
    charCount(null, 123) // invalid inputs
```

---

## Break It Down

- Explicitly write out the steps you need to take.
    - This forces you to think about the code you'll write before you write it, and helps you catch any lingering conceptual issues or misunderstandings before you dive in and have to worry about details (i.e language syntax/built-in methods) as well
- take the actual steps of the problem, and write it down. Use comments as a guide for steps that you need to take
- interviewers are looking for you to communicate what you're doing

```js
    //examples
    charCount("aaaa") // {a: 4}
    charCount("hello") // { h: 1, e: 1, l: 2, o: 1 } 
    charCount("my phone number is 182763")
    
    // 1. 
    function charCount(str){
    	//do something
    	// return an object (only lowecase alphanumeric characters)
    }
    
    // 2. 
    function charCount(str){
    	// make object to return at end
    	// loop over string, for each character...
    		// if the char is a number/letter AND is a key in object, add one to count
    		// if the is a number/letter AND char is not in object, add it to the object and set value to 1
    		// if character is something else (space, period, etc), don't do anything
    	// return object at end
    }
```
---

## Solve and Simplify

- "Solve the problem. If you can't, solve a simpler problem!"
- In an interview, you want to have something to show for yourself so instead of getting stuck on one difficult part of a problem and making zero progress at all because.
- Putting all of your effort into solving the problem before even writing code when you're stuck often looks very bad
- It's much better to just start writing code to the stuff you know how to do all the while keeping in mind that you do need to come back the problem you have yet to solve.
- Secondly, It's common that in simplifying a problem, you'll gain insight into the actual solution, into the harder part of the problem and something will into place.

Simplify:

1. Find the core difficulty in what you're trying to do
2. Temporarily ignore that difficulty
3. Write a simplified solution
4. Then incorporate that difficulty back in

    //examples
    charCount("aaaa") // {a: 4}
    charCount("hello") // { h: 1, e: 1, l: 2, o: 1 } 
    charCount("my phone number is 182763")
    
    function charCount(str){
    	// make object to return at end
    	// loop over string, for each character...
    		// if the char is a number/letter AND is a key in object, add one to count
    		// if the is a number/letter AND char is not in object, add it to the object and set value to 1
    		// if character is something else (space, period, etc), don't do anything
    	// return object at end
    }
    
    function charCount(str){
    	// make object to return at end
    	var result = {};
    	// loop over string, for each character...
    	for(var i = 0; i < str.length; i++){
    		var char = str[i].toLowerCase();
    			// if the char is a number/letter AND is a key in object, add one to count
    		if (result[char] > 0){
    			result[char]++
    		// if the is a number/letter AND char is not in object, add it to the object and set value to 1
    		} else {
    			result[char] = 1;
    		}
    	}
    		// if character is something else (space, period, etc), don't do anything
    	// return object at end
    	return result;
    }
    
    //this solution does not account for alphanumeric check, 
    //example is assuming that we coded what we can 
    //and coming back to the problem we don't know

---

## Look Back and Refactor

- This step is the most important in terms of improving as a better developer
- Solved? Awesome! But you're not done!

Ask these questions out loud when done!

- Refactoring questions:
    - can you check the result?
        - obviously, to check if code works
    - can you derive the result differently?
        - can you think of different approaches now that you've solved it one way?
    - can you understand it at a glance?
        - how intuitive is your solution? does it make sense on paper or on a whiteboard?
    - can you use the result or method for some other problem?
        - note: benefits of solving a problem helps you develop a "spider" sense or an intuition for solving other solution
    - can you improve the performance of your solution?
        - how we can make it perform better, time complexity and space complexity.
    - can you think of other ways to refactor?
        - minor things:
            - does your code follow the company guidelines style guide
            - conventions of language
            - spacing
    - how have other people solved this problem?
        - in an interview, may be beneficial to pick interviewers brain
            - ask, what other approaches are there, what did i miss?
            - you can learn a lot about how people solve

---