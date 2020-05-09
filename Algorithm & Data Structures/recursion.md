# Recursion

Objective:

- Define what recusion is and how it can be used
- Understand two essential components of a recursive function
- Visualize the call stack to better debug and understand recursive function
- Use helper method recursion and pure recursion to solve more difficult problems

## What is recursion and why use it?

- A process (a function in our case) that calls itself

### Why use it?

- It is widely used!
    - These uses recursion!
        - JSON.parse / JSON.stringify
        - document.getElementById and DOM traversal algorithms
        - Object traversal
- It is sometimes a cleaner alternative to iteration!
- Important in more complex data structures

## The Call Stack:

- call stack is a stack data structure
- any time a function is invoked it is placed (pushed) on the top of the call stack
- when JavaScript sees the return keyword or when the functions ends, the compiler will remove (pop)

**Why is the call stack important?**

- When we write recursive functions, we keep pushing new functions onto the call stack!