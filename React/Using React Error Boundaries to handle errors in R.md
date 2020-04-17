# Using React Error Boundaries to handle errors in React Components

Created: Apr 14, 2020 7:33 PM
Created By: Daniel Hong
Last Edited Time: Apr 14, 2020 7:33 PM

## Using React Error Boundaries to handle errors in React Components

- Chances are, you will eventually run into problems with your code and will behave differently than you expect it to. In React, if a render is thrown and unhandled, your application will be removed from the page and will be a blank screen.
- A open source library called "react-error-boundary" provides a component called _Error Boundary_ to handle our errors.

```js
const ErrorBoundary = ReactErrorBoundary.ErrorBoundary;

function ErrorFallback({ error }) {
  return (
    <div>
      <p>Something went wrong:</p>
    </div>
  );
}

function Bomb() {
  throw new Error("CABOOM!");
}

function App() {
  const [explode, setExplode] = useState(false);
  return (
    <div>
      <div>
        <button onClick={() => setExplode(true)}>Bomb</button>
      </div>
      <div>
        <ErrorBoundary FallbackComponent={ErrorFallback}>
          {explode ? <Bomb /> : "Push the button!"}
        </ErrorBoundary>
      </div>
    </div>
  );
}
```

- To handle React errors, you can create your own error boundary or use the React Error Boundary package from npm.
- To implement, we assign it as a component where we can use it wrap pieces of our code
- Any descendants of that error boundary, or any code that is wrapped by the ErrorBoundary component, will have its error handled accordingly
- The ErrorBoundary library accepts a fallback component and will be rendered in the event of an error allowing you to recover from the error or display an error message without your entire application breaking!
