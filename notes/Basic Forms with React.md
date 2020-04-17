# Basic Forms with React

Created: Apr 10, 2020 1:43 PM

## Making Basic Forms with React

- Forms are a basic building block of websites.
- Form elements accept input/data from users.
- With forms, it is better practice to use an onsubmit prop on the form tag because inputs are automatically submitted when enter is pressed in an input within the form. Common and BETTER UX
- the onSubmit handler will be invoked when the button is pressed or if they hit enter
- By default, when a form is submitted in the browser, there will be a full page refresh. What's happening is that when a form is submitted, it automatically makes a post request to the current URL. This can be seen in the network tab of the devtools.
- in our handleSubmit function, we avoid using "document.querySelector()" because it causes problems when trying to scale the component or function if we wanted to render multiples. They could conflict with each other. Querying the entire document breaks the encapsulation of the component because you won't be able to use the UsernameForm component in the context of other components.
- Best practice: properly associating our label to the input with "htmlFor" and "id"/"name". both of id and name can be used interchangeably in this scenario so that our handleSubmit can easily access it
- we could use the useRef way but it might be unnecessary if you don't need to use the ref functionality
- It is important that any button you have inside the form has a type. Implicitly, it will have a type of submit by default without the type but that may not be the case as you could have a cancel or reset button which aren't submit. For those buttons, you would give it a type "button"

```javascript
    function UsernameForm(){
    
    	// function usernameInputRef = useRef();
    	
    	function handleSubmit(event){
    		event.preventDefault(); //prevents full page refresh on submit.
    		const username = event.target.elements.usernameInput.value; //suggested way
    		
    		// ref method:
    		// const username = usernameInputRef.current.value
    	}
    
    	return (
    		<form>
    			<label htmlFor="usernameInput">Username:</label>
    			<input ref={usernameInputRef} name="usernameInput" type="text"/>
    			<button type="submit">Submit</button>
    			<button type="button" onClick={cancelHandler...}>cancel</button>
    		</form>
    	)
    }
```

## Making Dynamic Forms With React

- It is useful to know keep track of the user's input as they're typing it and use that info to change what is rendered.
- Can be good for dynamic searches, filter inputs, triggering changes, users checking a checkbox and more.
- We're using state to keep track of the value of the input. The handleChange function is associated with the input and setting the username state to the current value as it's being typed or updated.
- Our dynamic functionality for this form is to display an error and disable the submit button if the username input contains a uppercase character because let's say we don't want any uppercase characters in our users' username.
- We create two helper variables that are conditional booleans.
    - isLowerCase is a boolean that determines if the username state has all lowercase
    - error uses a ternary that outputs an error message if isLowerCase is false
- It is being rendered only if isLowerCase is false in the return statement.
- Additionally, our submit button has a disabled property that is controlled by a boolean.
```javascript
function UsernameForm(){
	const [username, setUsername] = useState('')

	const isLowerCase = username === username.toLowerCase();	
	const error = isLowerCase ? null : 'Username must be lower case'
	
	function handleSubmit(event){
		event.preventDefault(); //prevents full page refresh on submit.
		alert(`you alerted: ${username}`)
	}

	function handleChange(event){
		setUsername(event.target.value);
	}
	
	return (
		<form onSubmit={handleSubmit}>
			<label htmlFor="usernameInput">Username:</label>
			<input onChange={handleChange} type="text"/>
			<div>
				{error}
			</div>
			<button disabled={Boolean(error)} type="submit">Submit</button>
		</form>
	)
}
```

Resource: 
- [Make Basic Forms with React](https://egghead.io/lessons/react-make-basic-forms-with-react-601487f6)
- [Make Dynamic Forms with React](https://egghead.io/lessons/react-make-dynamic-forms-with-react-897b233b)

Test!

