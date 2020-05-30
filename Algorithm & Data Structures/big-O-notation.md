# Big O Notation

### Intro to Big O

**Objectives:**

1. The need for Big O
2. What it is
3. Simplify Big O Expressions
4. Define Time Complexity and Space Complexity
5. Evaluate the time complexity and space complexity of different algorithms using Big O Notation
6. Describe what a logarithm is

**Big O Notation:** a system of generalizing code so that we can compare its performance and gauge its efficiency to other code.

**Why does it matter if our code is efficient as long as it works? Who cares?**

- Important to have precise vocab to talk about how our code performs
- Useful for discussing trade-offs between different approaches
- When code slows down or crashes, identifying parts of the code that are inefficient can help us find pain points in our applications

---

### Timing Our Code

What does better mean?

- Faster?
- Less memory-intensive?
- More readable?
- Brevity?

Depends on the situation but usually balance between all three/four 

**The Problem with Time**

- Different machine will record different times
- The same machine will record different times
- For fast algorithms, speed measurements may not be precise enough?

---

### Counting Operations

- If not time, then what?
    - Rather than counting seconds, which are so variable, we can count the number of simple operations the computer has to perform

Ex. 1

    function addUpTo(n){
    	return n * (n + 1) / 2;
    }
    
    //let's count the operations, 1 multiplication, 1 addition, and 1 division
    // note: regardless of the size of n, there will always be 3 simple operations

Ex. 2

    function addUpTo(n){
    	let total = 0;
    	for (let i = 1; i <= n; i++){
    		total += i; 
    	}
    	return total
    }
    
    // as you can see, there are many operations in this solution (n amount of additions
    // assignments, comparisons etc) and the larger the n parameter is,
    // the more operations that will occur.
    
    // notes: regardless of the exact number, the number of operations 
    // grows roughly proportionally with n

- Counting operations can be tricky
- It doesnt matter, what we care about is the general trend. Focus is on the big picture and in the case of example 2, as *n* grows, the number of operations grow in proportion with *n*.

---

### Official Intro to Big O

Cole: "Big O Notation is a way to formalize fuzzy counting. It allows us to talk formally about how the runtime of an algorithm grows as the inputs grow"

- It's a way of describing the relationship between the input to a function as it grows and how that changes the runtime of that function.
- We won't care about the details, only the trends

Example two in prev lesson is constant

- O(1)
- Always three operation

Example one in prev lesson is linear

- O(n)
- Number of operations is (eventually) bounded by a multiple of n (say, 10n)

If you have code that has two O(n) operation (i.e. two for loops, O(2n)), you would simplify it as O(n)

However, if you have a nested for loop, it would technically be O(n * n) or O(n^2). Quadratic runtime.

---

### Simplifying Big O Expressions

- When determining the time complexity of an algorithm, there are some helpful rules of thumb for big O expressions.
- These rules of thumb are consequence of the definition of big O notation.

### Rules:

---

- Analyzing complexity with big O can get complicated
- There are several rules of thumb that can help
- These rule won't always work but are a helpful starting point

---

1. Constants don't matter, we simplify
    - O(2n) → O(n)
    - O(500) → O(1)
    - O(13n^2) → O(n^2)
2. Smaller terms don't matter
    - O(n + 10) → O(n)
    - O(1000n + 50) → O(n)
    - O(n^2 + 5n + 8) → O(n^2)
3. Big O Shorthands
    - Arithmetic operations are constant
    - Variable assignment are constant
    - Accessing elements in an array (by index) or object (by key) is constant
    - In a loop, the complexity is the length of the loop **TIMES** the complexity of whatever happens inside of the loop.

    ---

    ### Space Complexity

    - We've been focusing on time complexity:
        - how can we analyze the runtime of an algorithm as the size of the inputs increase.
    - We can also use big O notation to analyze **space complexity:**
        - How much additional memory do we need to allocate in order to run our code

    What about the inputs?

    - **Auxiliary space complexity:**
        - refers to the space required by the algorithm, not including the space taken up by the inputs
        - we focus about the space within the algorithm and not the space taken up by the size of the input
    - Unless otherwise noted, when we talk about space complexity, we are usually referring to the auxiliary space complexity

    **Rules of Thumbs for Space Complexity in JS**

    - Most primitives (booleans, numbers, undefined, null) are constant space
    - String requires O(n) space (where n is the string length)
    - Reference types are genearlly O(n), where n is the length (for arrays) or the number of keys (for objects)

    ex.1

        function sum(arr){
        	let total = 0;
        	for (let i = 0; i < arr.length; i++){
        		total += arr[i];
        	}
        	return total;
        }
        
        // one number (total = 0)
        // second number (i = 0)
        // regardless of size on the input/arr, the amount of space allocated
        // to the algorithm will always be for those numbers so it has 
        // O(1) space
        // note: no new variables are being added

    ex.2

        function double(arr){
        	let newArr = [];
        	for (let i = 0; i < arr.length; i++){
        		newArr.push(2 * arr[i]);
        	}
        	return newArr;
        }
        
        /* 
        newArr = [] is not that significant when you take into account
        what is going on in the for loop.
        
        As you can see, the size of newArr grows in proportion to the length of the input
        So we drop the constant of (newArr) and recognize that the space complexity
        is ultimately O(n).
        
        */

    ---

    ### Logarithms and Big O Recap

    - Common Complexities we've seen:
        - O(1), O(n), O(n^2)
    - Sometimes big O expressions involve more complex mathematical expressions
    - One that appears more often than you might like is the logarithm

    **Logarithm Review**

    - The inverse of exponentiation
    - log base (value) = exponent
    - log === log2 so we'll shorthand it as log
    - Rule of Thumb
        - The logarithm of a number roughly measures the number of times you can divide tthat number by 2 before you get a value that's less than or equal to one.
        - i.e: log(8) = 3, log(25) ~= 4.64

    Logarithm Complexity

    - Logarithmic time complexity is great! O(log n)
    - O(n log n) not as fast but faster than quadratic.

    Why do we care about logs?

    - Certain serach alorithms have logarithmic time complexity
    - Efficient sorting algorithms involve logarithms
    - Recursion sometimes involves logarithmic space complexity

    Recap:

    - To analyze the performance of an algorithm, we use Big O Notation
    - Big O Notation can give us a high level understanding of the time or space complexity of an algorithm
    - BIg O Notation doesn't care about precision, only general trends (linear, quadratic, constant)
    - The time or space complexity (as measured by Big O) depends only the algorithm, not the hardware used to run the algorithm
    - Big O Notation is everywhere so gets lots of practice

    These Big O Expressions are the most common. Again here they are:

    - O(1)
    - O(n)
    - O(n^2)
    - O(log n)
    - O(n log n)