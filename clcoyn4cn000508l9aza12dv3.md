# React: Concept of useReducer.

useReducer is used to manage the state of your components. Just like useState, useReducer is designed to manage states with data like objects or arrays of objects.

useState is appropriate for managing single data, like string, number or Boolean values, while useReducer is appropriate for managing complex data, like objects and arrays of objects.

I will give you a simple scenario as to when to use each of them before we dive into actually showing you how to use them.

useReducer helps us with grouping all the functions used to update the state of our component into one single function which is the reducer function and I will show you all that very soon.

Now, let's get into how to use useReducer.

useReducer returns an array with two values, the first one is the variable representing the data you will be managing with useReducer and the second one is a dispatch function we use for directing updates to your state based on an event being triggered. And the required values you will be sending to useReducer are the reducer function and the data you will be updated to manage the state of your component.

I will show you an example now and I hope that will make everything clear to you.

```javascript
const [count, distaptch] = useReduder(reducer, {count: 0})
```

### **dispatch**

Here I will explain dispatch briefly with a code example. Let's say we have a counter app and two buttons to add and reduce the number displayed on our UI. dispatch will be used to identify the block of code that should be carried out inside our reducer function. Because all the updates we intend to carry out on our state will be inside one function which is the reducer function and all events will have a dispatch that will be a reference to it. I will give an example.

```javascript
function increment(){
    dispatch({type: "increment"})
}
function decrement(){
    dispatch({type: "decrement"})
}
return(
    <div>
        <button onClick={increment}> + </button>
        <div> {count} </div>
        <button onClick={decrement}> - </button>
    </div>
)
```

Now as you can see, what I was trying to explain is what you've seen above, now

```javascript
{type: "increment"}
```

and

```javascript
{type: "decrement"}
```

that was passed as a parameter to the dispatch function is what we are going to use to Identity these events. Now I will explain the reducer function and then you will understand very well the information I'm trying to pass to you.

### **reducer**

the reducer function is where all our updates are going to take place. and it is best practice to have your reducer function as a global function of your component. let me show you an example now.

```javascript
import { useReducer } from 'react'

function reducer(state, action){
    switch(action.type){
    case "increment": {
    return {
        count: state.count + 1
            }
    }
    break;
    case "decrement": {
    return {
        count: state.count - 1
            }
    }
    break;
    default:
    console.log(state.count)
    break;
    }
}
```

From the code above, you can see what I've explained about the dispatch function. but now I know you might be confused about where the **state** and **action** parameters came from, but I will explain that to you guys shortly.

**state** and **action** are predefined from the useReducer hook, the state represents our initial data and the action represents the object we have sent to dispatch which is referring to our **onClick** event in our previous code example. Now you can see that the reducer function is a means of having a single source of truth, instead of having different functions for each event, the reducer function serves as a single place where all your conditions and rules are stated. Now when the "+" button is clicked, the block of codes within the case for "increment" will be carried out and our state will be updated and the same for the "-" button. Now you can re-read all I have written you will grab every point which was confusing to you from start.

With this, I hope I have been able to make the useReducer hook familiar to you and help you to be able to implement its usefulness in your projects. Thank you.