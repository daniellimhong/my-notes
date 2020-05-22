# Introduction: Object-Oriented JavaScript

## OOP: a popular paradigm for structuring our complex code

- easy to add features, functionality
- easy for us and other developers to reason about (a clear structure)
- Performant (efficient in terms of memory)
- need to organize our code as it gets more complex so it's not just an endless series of commands

### side note: Paradigm === an approach to organize code

# Object Creation

## Encapsulation

- the idea of bundling data and methods that work on that data within one unit

## Creating methods:

- Object Literal

```JavaScript
const user1 = {
	name: "Phil"
	score: 4,
	increment: function(){
		user1.score++
	}
};

user1.increment();
```

- Object dot notation

```JavaScript
const user2 = {}; // create empty object

user2.name = "Julia"; // assign properties to that object
user2.score = 5;
user2.increment = function(){
	user2.score++;
}
```
- Object.create

```JavaScript
const user3 = Object.create(null);

user3.name = "Eva"
user3.score = 9
user3.increment = function(){
	user3.score++;
}
```

## Creating Objects with Functions
```JavaScript
function userCreator(name, score){
	const newUser = {};
	newUser.name = name;
	newUser.score = score;
	newUser.increment = () {
		newUser.score++;
	}
	return newUser;
}

const user1 = userCreator("Phil", 4);
const user2 = userCreator("Julia", 5);
user1.increment
```
- This solution is fundamentally correct but inefficient bc it wastes memory and space for each increment method created for each user
