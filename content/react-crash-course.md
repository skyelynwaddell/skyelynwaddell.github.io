+++
title = 'React Crash Course'
date = 2024-10-05T12:17:06-06:00
draft = false
description = "A big manual of useful React knowledge and basics referencing the BroCode youtube video."
image = "/images/react.webp"
categories = ["react", "javascript", "webdev"]
authors = ["Skye Waddell", "BroCode"]
avatar = "/images/avatar.webp"
+++
# Skye's React Manual 👽

Here is all my documentation on React and what I find to be most useful for use, and reference.

I recommend checking out this Youtube tutorial by **BroCode**.\
[**React Full Course for free ⚛️ (2024)**](https://www.youtube.com/watch?v=CgkZ7MvWUAA&t=7751s)\
it is very in depth and goes over all topics mentioned below.

<span style="font-size: 21px">Table of Contents</span>

- [**<u>Getting Started</u>**](#getting-started)
- [**<u>Basic Rules for React</u>**](#basic-rules-for-react)
- [**<u>React Bootstrap</u>**](#react-bootstrap)
- [**<u>Create a Functional Component .JSX</u>**](#create-a-functional-component-jsx)
- [**<u>Importing a Component within another Component</u>**](#importing-a-component-within-another-component)
- [**<u>Including Javascript / Variables in your Component</u>**](#including-javascript-in-your-component)
- [**<u>Mapping Items from an Array / Multi-Line Javascript</u>**](#mapping-items-from-an-array)
  - [**<u>Sorting Examples</u>**](#sorting-examples)
- [**<u>Conditional Rendering</u>**](#conditional-rendering)
- [**<u>useState</u>**](#usestate)
  - [**<u>useState Variable Updater Example</u>**](#usestate-variable-updater-example)
  - [**<u>useState Counter Increaser Example</u>**](#usestate-counter-increaser-example)
  - [**<u>useState Boolean Toggler Example</u>**](#usestate-boolean-toggler-example)
  - [**<u>useState Update Objects</u>**](#usestate-update-objects)
  - [**<u>useState Update Arrays</u>**](#usestate-update-arrays)
  - [**<u>useState Update Array of Objects</u>**](#usestate-update-array-of-objects)
- [**<u>Props</u>**](#props)
  - [**<u>PropTypes</u>**](#prop-types)
  - [**<u>Default Props</u>**](#default-props)
- [**<u>onClick Event</u>**](#onclick-event)
  - [**<u>onClick Event Properties</u>**](#onclick-event-properties)
  - [**<u>Change Button Text onClick</u>**](#change-button-text-onclick)
  - [**<u>Hide Image onClick</u>**](#hide-image-onclick)
- [**<u>onChange Event</u>**](#onchange-event)
  - [**<u>onChange Input Box</u>**](#onchange-input-box)
  - [**<u>onChange Textarea</u>**](#onchange-textarea)
  - [**<u>onChange Option Box</u>**](#onchange-option-box)
  - [**<u>onChange Radio Buttons</u>**](#onchange-radio-buttons)
- [**<u>Updater Functions</u>**](#updater-functions)
- [**<u>useEffect</u>**](#useeffect)
  - [**<u>useEffect after re-render of a Component</u>**](#useeffect-after-re-render-of-a-component)
  - [**<u>useEffect when a Component mounts</u>**](#useeffect-when-a-component-mounts)
  - [**<u>useEffect when value changes</u>**](#useeffect-when-value-changes)
- [**<u>useContext</u>**](#usecontext)
- [**<u>useRef</u>**](#useref)
  - [**<u>useRef on an Element</u>**](#useref-on-an-element)
- [**<u>NodeJS & React</u>**](#nodejs-&-react)
- [**<u>Axios</u>**](#axios)
  - [**<u>GET Request</u>**](#get-request)
  - [**<u>POST Request</u>**](#post-request)

# Getting Started

Start by installing NodeJS and creating a new folder

Run commands

```
npm create vite@latest
```

Select **React**\
Select **Javascript**

To run the app, enter

```javascript
npm run dev
```

# Basic Rules for React

- File names for your html like components are .jsx
- Class is a reserved keyword in React, because there are classes, use instead the className keyword!

```javascript
//HOW IT WAS DONE IN HTML
<button class="btn btn-primary">Click Me!</button>

//HOW YOU DO IT IN REACT JSX
<button className="btn btn-primary">Click Me!</button>
```

- A component may only return 1 element! The following example is invalid syntax in React

```javascript
//THIS WILL THROW AN ERROR!!!
return(
    <div>
        <h1>Hello World!</h1>
    </div>
    
    <div>
        <h2>Hello Universe!</h2>
    </div>
)
```

Instead you should contain everything in 1 outer div, or within an empty element!

```javascript
//THIS WILL WORK :) (use empty element <> or a <div>)
return(
    <>
    <div>
        <h1>Hello World!</h1>
    </div>
    
    <div>
        <h2>Hello Universe!</h2>
    </div>
    </>
)
```

# React Bootstrap

<https://react-bootstrap.netlify.app/docs/getting-started/introduction>

Install React Bootstrap in your React app with the following line

```javascript
npm install react-bootstrap bootstrap
```

To include React Bootstrap within your React App, include the following import statement in your main.jsx file, or whichever component you would like Bootstrap on

```javascript
import 'bootstrap/dist/css/bootstrap.min.css'
```

# Create a Functional Component .JSX

You may also get ES7 React extension in VSCODE and type ***rafc*** for a snippet of this code. You may use default Javascript function syntax, or arrow function syntax.

**Default Functional Component Syntax**

```javascript
import React from 'react'

function App(){
  return (
    <div>
      <h1>Hello World!</h1>
    </div>
  )
}

export default App
```

**Arrow Functional Component Syntax**

```javascript
import React from 'react'

const App = () => {
  return (
    <div>
      <h1>Hello World!</h1>
    </div>
  )
}

export default App
```

# Importing a Component within another Component

Since you are exporting each component, you may include them within other components by using the **<u>import</u>** statement, and then calling it within your component as an element.

```javascript
import React from 'react'
import ComponentName from './Component.jsx'

const App = () => {
  return (
    <>
      //both of the following are valid ways to
      //include the component after importing it
      <ComponentName></ComponentName>
      <ComponentName />
    </>
  )
}

export default App
```

# Including Javascript in your Component

You can include Javascipt within your component's return statement, by wrapping the variable name, or direct Javascript within curly brackets, like the following.

```javascript
import React from 'react'

const name = "Skye";

const App = () => {
  return (
    <div>
      <h1>{name}</h1>
      <h1>{true}</h1>
      <h1>{1000 - 100}</h1>
    </div>
  )
}

export default App
```

# Mapping Items from an Array

Below is an example of two topics. Dynamically displaying an array of variables, as well as how to implement many lines of Javascript in React.

In this case we include the whole statement within curly brackets, and any curly brackets that would normally be in the code, must be replaced with rounded brackets ( )\
Within the { } you may still include more HTML, or variables surrounded with { }

When mapping through items, you must pass the element a unique value as their key property, a common practice is to pass an index argument, and set it to that.

```javascript
import React from 'react'

const App = () => {

  const names = [
    'Brad',
    'Mary',
    'Joe',
    'Sally'
  ]

  return (
      <ul>

      {names.map((name, index) => (
        <li key={index}>{name}</li>
      ))}

      </ul>
    </div>
  )
}

export default App
```

Now lets use the map function to render a list a little more efficiently, as well as while using objects inside the array, as well as many sorting examples you can use in your projects.

```javascript
function List(){
    const fruits = [
        { id: 1, name: "apple", calories: 95 },
        { id: 2, name: "orange", calories: 45 },
        { id: 3, name: "banana", calories: 105 }
    ]

    const listItems = fruit.map(fruit => {
        <li key={fruit.id}>
        {fruit.name} {fruit.calories}
        </li>
    })

    const list = <ol>{listItems}</ol>

    return(list)
    
}

export default List;
```

# Sorting Examples

```javascript
const fruits = [
        { id: 1, name: "apple", calories: 95 },
        { id: 2, name: "orange", calories: 45 },
        { id: 3, name: "banana", calories: 105 }
    ]

//sort fruits by name alphabetically
fruits.sort((a, b) => a.name.localeCompare(b.name));

//sort fruits by name reverse alphabetical
fruits.sort((a, b) => b.name.localeCompare(a.name));

//sort by calories asc
fruits.sort((a, b) => a.calories - b.calories);

//sort by calories desc
fruits.sort((a, b) => b.calories - a.calories);

//find low calories fruits (less than 100)
const lowCalFruit = fruits.filter(fruit => fruit.calories < 100);

//find high calorie fruits (greater/equal to 100)
const highCalFruit = fruits.filter(fruit => fruit.calories >= 100);
```

# Conditional Rendering

React doesn't support IF statements within the return statement of the component, however you may use a turnery operator.

```javascript
import React from 'react'

const App = () => {

  const loggedIn = true;

  return (
    <div>
      { loggedIn ? "hello member" : "hello guest" }
    </div>
  )
}

export default App
```

 Or, you may do it outside the return statement.

```javascript
import React from 'react'

const App = () => {

  const loggedIn = true;
   
  if (loggedIn)
  {
      return (
        <div>
          Hello Member
        </div>
      )
  } 
  else 
  {
      return (
        <div>
          Hello Guest
        </div>
      )
   }
}

export default App
```

However these ways, both seem messy right? Let's do it like this instead.

```javascript
const loggedIn = false;

function App () {
    const welcomeMsg = <h1> Hello World </h1>
    const loginPrompt = <h1> Please Login! </h1>

    return(
        loggedIn ? welcomeMsg : loginPrompt;
    );
}
```

Conditionally render a component based on values/lengths of arrays.\
This is called **Short Circuiting.**

```javascript
import List from './ListComponent.jsx';

const fruits = [
    {id: 1, name: "orange", calories: "100"},
    {id: 1, name: "apple", calories: "95"},
    {id: 1, name: "banana", calories: "104"},
]

function App() {
    return (
        <>
            { fruits.length > 0 && <List items={fruits}/> }
        </>
    );
}
```

# useState

In order to have variables modifiable and interactive, you must setup something called state!\
You can not update declared variables, unless you use state in React.

**<span style="font-size: 15px">Declare a variable with useState</span>**

- **First variable in the array is the Variable Name (GETTER).**
- **Second variable in the array is the Function you use to update the first variable (SETTER).**
- **Parameter of useState is the default value of the variable.**

```javascript
//must import useState first
import React, { useState } from "react";

const [newItem, setNewItem] = useState("");
```

**<span style="font-size: 15px">Update a variable with useState</span>**

To update a useState variable, you call the second variable from the useState array as a function.

```javascript
setNewItem("Hello World");
```

# useState Variable Updater Example 

```javascript
//must import useState first
import React, { useState } from "react";

//name getter/setter
const [name, setName] = useState("Guest");

//update name function
const updateName = () => {
    setName("Lorem Ipsum");
}

function App(){

    return(
        <>
            //update name button
            <h1> Name: {name} </h1>
            <button onClick={updateName}>
                Update Name
            </button>
        </>
    );
}

export default App;
```

# useState Counter Increaser Example

```javascript
//must import useState first
import React, { useState } from "react";

//count getter/setter
const [count, setCount] = useState(0);

//increase count function
const increaseCount = () => {
    setCount(count + 1);
}

function App(){

    return(
        <>
            //update count button
            <button onClick={ increaseCount }>
                Count: { count }
            </button>
        </>
    );
}

export default App;
```

# useState Boolean Toggler Example

```javascript
//must import useState first
import React, { useState } from "react";

//clicked getter/setter
const [clicked, setClicked] = useState(false);

//toggle boolean function
const toggleBoolean = () => {
    setCount(!clicked);
}

function App(){

    return(
        <>
            //update count button
            <button onClick={ toggleBoolean }>
                <h1>
                { clicked ? "Clicked" : "Not Clicked" }
                </h1>
            </button>
        </>
    );
}

export default App;
```

# useState Update Objects

If you are updating an object with useState, if you just update one value it will replace all the rest of the object's key value pairs. So what you must do is include all the key value pairs that would be required, for example car needs a year, make and model every time it is updated. 

If you would like to keep the other values the same without having to explicitly try and calculate every field, whenever any field has to be updated you can use a spread operator. 

This looks like 3 periods, following the objects name you are trying to update. Below is an example of how you can update an object whilst using useState.

```javascript
import React, { useState } from "react";

function MyComponent(){
    const [car, setCar] = useState({
        year: 2024,
        make: "Ford",
        Model: "Mustang"
    })

    function handleYearChange(event){    
        setCar(_car => ({ ..._car, year: event.target.value }) );
    }
    
    function handleMakeChange(event){
        setCar(_car => ({ ..._car, make: event.target.value }) );
    }
    
    function handleModelChange(event){
        setCar(_car => ({ ..._car, model: event.target.value }) );
    }
    
    return(
        <>
            <h1> Your favorite car: {car.year} {car.make} {car.model} </h1>
            <input type="number" value={car.year} onChange={handleYearChange}>
            <input type="text" value={car.make} onChange={handleMakeChange}>
            <input type="text" value={car.model} onChange={handleModelChange}>
        </>
    );                       
}

export default MyComponent;
```

# useState Update Arrays

You can use the following methods in order to update an array, or delete from a position in the array.\
Common naming practice for variables that never get used in the code, is name them as an underscore.

```javascript
import React, { useState } from "react";

function MyComponent(){
    
    const [foods, setFoods] = useState(["Apple", "Orange", "Banana"]);
    
    function handleAddFood(){
        const newFood = document.getElementById("foodInput").value;
        document.getElementById("foodInput").value = "";

        setFoods(_foods => [..._foods, newFood]);
    }
    
    function handleRemoveFood(index){
        setFoods(_foods => _foods.filter((_, i) => i !== index));
    }

    return(
        <>
            <h1> List of Foods </h1>
            <ul>
                {foods.map((food, index) => 
                <li onClick={ () => handleRemoveFood(index) } 
                key={index}> {food} 
                </li> )}
            </ul>
            
            <input type="text" id="foodInput" placeholder="Enter food name...">
            <button onClick={handleAddFood}> Add Food </button>
        </>
    );
}

export default MyComponent;
```

# useState Update Array of Objects

```javascript
import React, { useState } from "react";

function MyComponent(){
    
    const [cars, setCars] = useState([]);
    const [carYear, setCarYear] = useState(new Date().getFullYear());
    const [carMake, setCarMake] = useState("");
    const [carModel, setCarModel] = useState("");

    function handleAddCar(){
        const newCar = {
            year: carYear,
            make: carMake,
            model: carModel,
        }
        setCars(_cars => [..._cars, newCar]);

        setCarYear(new Date().getFullYear());
        setCarMake("");
        setCarModel("");
    }

    function handleRemoveCar(index){
        setCars(_cars => _cars.filter((_, i) => i !== index ));
    }

    function handleYearChange(){
        setCarYear(_carYear => event.target.value);
    }

    function handleMakeChange(){
        setCarMake(_carMake => event.target.value);
    }

    function handleModelChange(){
        setCarModel(_carModel => event.target.value);
    }

    return(
        <>
            <h1> List of Car Objects </h1>

            <ul>
                {cars.map((car,index) => 
                    <li key={index} onClick={() => handleRemoveCar(index)}> {car.year} {car.make} {car.model} </li>
                )}
            </ul>
            
            <input type="number" value={carYear} onChange={handleYearChange}>
            <input type="text" value={carMake} onChange={handleMakeChange} placeholder="Enter Car Make...">
            <input type="text" value={carModel} onChange={handleModelChange} placeholder="Enter Car Model">
        
            <button id="insertCarButton"> Add New Car </button>
        </>
    );
}

export default MyComponent;
```

# Props

**Read-Only** properties that are shared between components. A parent component can send data to a child component, with the following method

```
<Component key=value />
```

Your child object must accept the key passed, as an argument

- **<span style="font-size: 15px">Child Component</span>**

```javascript
const Student = (props) => {
  return (
    <div>
      <h1>Name: { props.name }</h1>
      <h1>Age: { props.age }</h1>
      <h1>Student: { props.isStudent ? "Yes" : "No" }</h1>
    </div>
  )
}
```

- **<span style="font-size: 15px">Parent Component</span>**

```javascript
import Student from './Student.jsx';

const App = () => {
    return(
    <>
        <Student 
            name="Spongebob" 
            age={30} 
            isStudent={true}
        />
    </>
    )
}

export default App;
```

# Prop Types

PropTypes allow you to enforce strict typing on variables passed through props and is included in the Node Modules folder after installing React.

Here is how to create, and include PropTypes to enforce & verify variables passed down by Props are of the correct typing you want them to be.

```javascript
//must import PropTypes first
import PropTypes from 'prop-types';

//for reference, itemsArray contains the following
const itemsArray = [
    {id: 1, name: "item1"},
    {id: 2, name: "item2"},
    {id: 3, name: "item3"},
]

//your component
const Student = (props) => {
  return (
    <div>
      <h1>Name: { props.name }</h1>
      <h1>Age: { props.age }</h1>
      <h1>Student: { props.isStudent ? "Yes" : "No" }</h1>
      <ol>
      { props.itemsArray }
      </ol>
    </div>
  )
}

//setting up proptypes for your component
Student.PropTypes = {
    name: PropTypes.string,
    age:  PropTypes.number,
    isStudent: PropTypes.bool,

    itemsArray: PropTypes.arrayOf(PropTypes.shape({
        id: PropTypes.number,
        name: PropTypes.string
    }))
}

export default Student;
```

# Default Props

You may also setup Default Props for any Component that receives props, this is handy when a variable fails to get passed to the child Component, or if you want to have default values for a Component instance that doesn't receive props.

```javascript
const Student = (props) => {
  return (
    <div>
      <h1>Name: { props.name }</h1>
      <h1>Age: { props.age }</h1>
      <h1>Student: { props.isStudent ? "Yes" : "No" }</h1>
      <ol>
      { props.itemsArray }
      </ol>
    </div>
  )
}

Student.defaultProps = {
    name: "Guest",
    age:  13,
    isStudent: "false",
    itemsArray: [],
}

export default Student;
```

# onClick Event

When a user clicks on an element, we can respond to clicks by passing a callback to the **onClick** event handler, you can also use **onDoubleClick** instead!

- **<span style="font-size: 15px">Basic onClick Function</span>**

```javascript
function Button(){

    //onClick function
    const handleClick = () => {
        console.log("WOW!");
    }

    return(

        //onClick function
        <button onClick={ handleClick }>
            Click Me!
        </button>
    );
}

export default Button;
```

- **<span style="font-size: 15px">onClick Function with Arguments</span>**

  **MUST** be called with an arrow function, or else it will be AUTOMATICALLY called on run!

```javascript
function Button(){

    //onClick function with arguments
    const handleClick2 = (name) => {
        console.log(`${name} stop it!`)
    }

    return(

        //onClick function with arguments
        <button onClick={ () => handleClick2("Skye") }>
            Don't Click Me!
        </button>
    );
}

export default Button;
```

# onClick Event Properties

When you click on a button, there is an event that can be retrieved, and modified which contains much information about the click, to view these properties, use the following.

```javascript
function Button(){

    const handleClick = (e) => {
        console.log(e)
    }

    return(

        //onClick function with arguments
        <button onClick={ (e) => handleClick(e) }>
            Event Properties
        </button>
    );
}

export default Button;
```

# Change Button Text onClick

```javascript
function Button(){

    const handleClick = (e) => {
        e.target.textContent = "Updated Button";
    }

    return(
        <button onClick={ (e) => handleClick(e) }>
            Non-Updated Button
        </button>
    );
}

export default Button;
```

# Hide Image onClick

```javascript
function Button(){

    const handleClick = (e) => {
        e.target.style.display = "none";
    }

    return(
        <img src="./your-image.png"
            onClick={ (e) => handleClick(e) }>
        </img>
    );
}

export default Button;
```

# onChange Event

Event handler used primarily with form & input elements. It triggers a function every time the value of the input changes.

# onChange Input Box

```javascript
import React, { useState } from "react";

function MyComponent(){
    
    //input text
    const [name, setName] = useState("No Name"); //string
    const [age, setAge] = useState(13); //number

    //change name onChange of name input field
    function handleNameChange(event){
        setName(event.target.value);
    }

    //change age onChange of age input field
    function handleAgeChange(event){
        setAge(event.target.value);
    }

    return(
        <>
            <h1> Name: { name } </h1>
            <input value={ name } onChange={ handleNameChange }/>

            {/* INPUT : age field */}
            <h1> Age: { age } </h1>
            <input value={ age } onChange={ handleAgeChange }/>
        </>
    );
}

export default MyComponent;
```

# onChange Textarea

```javascript
import React, { useState } from "react";

function MyComponent(){
    
    //textarea
    const [comment, setComment] = useState("");

    //change comment
    function handleCommentChange(event){
        setComment(event.target.value);
    }

    return(
        <>
            <h1> Comment: { comment } </h1> 
            <textarea value={ comment } onChange={ handleCommentChange }
            placeholder="Enter comment..." />
        </>
    );
}

export default MyComponent;
```

# onChange Option Box

```javascript
import React, { useState } from "react";

function MyComponent(){

    //options
    const [payment, setPayment] = useState("label");

    return(
        <>
            <select value={ payment } onChange={ handlePaymentChange }>
                <option value="label"> Select an Option </option>
                <option value="Visa"> Visa </option>
                <option value="Mastercard"> Mastercard </option>
                <option value="Giftcard"> Giftcard </option>
            </select>
            <h1>Payment Type: { payment }</h1>
        </>
    );
}

export default MyComponent;
```

# onChange Radio Buttons

```javascript
import React, { useState } from "react";

function MyComponent(){
    
    const [shipping, setShipping] = useState("Delivery");
    
    function handleShipping(event){
        setShipping(event.target.value);
    }
    
    return(
        <>
            <label>
                <input type="radio" value="Pick Up"
                checked={shipping === "Pick Up"}
                onChange={handleShippingChange}/>
                Pick Up
            </label>

            <label>
                <input type="radio" value="Delivery"
                checked={shipping === "Delivery"}
                onChange={handleShippingChange}/>
                Delivery
            </label>

            <h1> Shipping: { shipping } </h1>
        </>
    );
}

export default MyComponent;
```

# Updater Functions

A function passed as an argument to setState usually.\
ex. setYear( arrow function );

Allow for safe updates based on the previous state. Used with multiple state updates and async functions. Good practice to use updater functions but is not required.

The below example, calls setCount to increase +1 three times!\
However, useState, uses the current state of the variable to do calculations so this would still only make count = 1, even though it was called three times.

```javascript
//WRONG
function MyComponent() {
    const [count, setCount] = useState(0);

    function increment(){
        setCount(count + 1);
        setCount(count + 1);
        setCount(count + 1);
    }    
}

export default MyComponent;
```

Instead what you should do is pass the current count into a temporary variable, with an arrow function. This will create a new "temporary" count, do the calculations and set count to the proper amount.\
All three setCount lines have different common naming conventions for the useState temp variable.

```javascript
//CORRECT
function MyComponent(){
    const [count, setCount] = useState(0);

    function increment(){
        setCount(prevCount => prevCount + 1);
        setCount(_count => _count + 1);
        setCount(c => c + 1);
    }
}

export default MyComponent
```

# useEffect

A React hook that tells React to **DO SOME CODE WHEN....**

- ...This component re-renders.
- ...This component mounts (when you create & append it to the DOM).
- ...The state of a value changes.

**useEffect** is usually not really obvious as to what this hook does, a more explicit name would be\
**useSideCode.**

```
useEffect(function, [dependencies]);
```

```
useEffect(() => {});            //Runs after every re-render
useEffect(() => {}, []);        //Runs only on mount
useEffect(() => {}, [value]);   //The state of a value changes
```

You will often see **useEffect** associated with the following

- Event Listeners
- DOM manipulation
- Subscriptions (real-time-updates)
- Fetching data from an API
- Clean up when a component unmounts

Here are some example of all 3 types of useEffect you may use when different events happen.

# useEffect after re-render of a Component

```javascript
import React, { useState, useEffect } from "react";

function MyComponent(){

    const [count, setCount] = useState(0);
    const [color, setColor] = useState("#FF00FF");

    {/*useEffect after every re-render*/}
    useEffect(() => {
        document.title = `Count: ${count}`;
    });
    
    function addCount(){
        setCount(_count => _count + 1);
    }

    return(
        <>
            <h1> Count: {count} </h1>
            <button onClick={addCount}> Add </button>
        </>
    );
}   

export default MyComponent;
```

# useEffect when a Component mounts

```javascript
import React, { useState, useEffect } from "react";

function MyComponent(){

    const [count, setCount] = useState(0);
    const [color, setColor] = useState("#FF00FF");

    {/*useEffect only when component mounts*/}
    useEffect(() => {
        document.title = `Count: ${count}`;
    }, []);

    function addCount(){
        setCount(_count => _count + 1);
    }

    return(
        <>
            <h1> Count: {count} </h1>
            <button onClick={addCount}> Add </button>
        </>
    );
}   

export default MyComponent;
```

# useEffect when value changes

```javascript
import React, { useState, useEffect } from "react";

function MyComponent(){

    const [count, setCount] = useState(0);
    const [color, setColor] = useState("#FF00FF");

    {/*useEffect only when state of a value changes
       When this component mounts + this value changes, then do this
    */}
    useEffect(() => {
        document.title = `Count: ${count}`;

    //you may check for multiple values that change, by seperating the values with commas
    }, [count, color]); 
    
    function addCount(){
        setCount(_count => _count + 1);
    }

    return(
        <>
            <h1> Count: {count} </h1>
            <button onClick={addCount}> Add </button>
        </>
    );
}   

export default MyComponent;
```

# useEffect Cleanup

When using Event Listeners, or Timers with Javascript inside a useEffect hook, it is best idea to clean up those event listeners, and timers or else there will be multiple instantiated every time the component re-renders.

```javascript
import React, { useState, useEffect } from "react";

function MyComponent(){

    const [width, setWidth] = useState(window.innerWidth);
    const [height, setHeight] = useState(window.innerHeight);

    useEffect(() => {
        window.addEventListener("resize", handleResize);

        //perform cleanup on Event Listener
        return () => {
           window.removeEventListener("resize", handleResize);
        }
    }, []); 
    
    function handleResize(){
        setWidth(window.innerWidth);
        setHeight(window.innerHeight);
    }

    return(
        <>
            <h1> Width: {width} </h1>
            <h1> Height: {height} </h1>
        </>
    );
}   

export default MyComponent;
```

# useContext

A React hook that allows you to share values between multiple levels of components without passing props through each level.

There must be a "Provider" Component which passes the data it's child Components. 

First create a state variable, then export the const with **createContext()**. After that you must wrap you child component that receives this data, within the context.Provider element, as shown below.

- **Component A \[Provider Component\]**

```javascript
import React, { useState, useContext } from "react";
import ComponentB from "./ComponentB.jsx";

export const UserContext = createContext();

function ComponentA(){
    
    const [user, setUser] = useState("Guest");
    
    return(
        <>
            <h1> Component A </h1>
            
            <UserContent.Provider value={user}>
            <ComponentB/>
            <UserContext.Provider/>
        </>
    );
}

export default ComponentA;
```

- **ComponentB \[Consumer Component\]**

```javascript
import React, { useState, useContext } from "react";

import { UserContext } from "./ComponentA.jsx";

function ComponentB(){

    const user = useContext(UserContext);

    return(
        <h1> Component B </h1>
        <h1> { `Bye ${user}` } </h1>
    );
}

export default ComponentB;
```

# useRef

useRef and useState are very similar, however...\
When you call your setter method with useState, it re-renders the component when the state value changes but useRef does not re-renders upon value changes.

useRef is useful for when you want a Component to "remember" some data, but you don't want that data to trigger new renders.

When we click the button below, the ref count increases, however the component and button do not re-render.

**useRef()** function return an object with 1 property of "current"

Example use cases:

- Accessing/Interacting with DOM elements
- Handling focus, animations, and transitions
- Managing Timers and Intervals

```javascript
import React, { useState, useRef } from "react";

function MyComponent(){

    const ref = useRef(0);

    function handleClick(){
        ref.current++;
    }    

    return(
        <>
            <button onClick={handleClick}>
                Click Me!
            </button>
        </>
    );
}

export default MyComponent;
```

# useRef on an Element

You can use useRef for an element such an an input element, and give its reference to be changed. This is very similar in native Javascript to using a query selector, or getElementById selector and modifying the element's properties.

```javascript
import React, { useState, useRef } from "react";

function MyComponent(){

    const inputRef = useRef(null);

    function handleClick(){
        inputRef.current.focus();
    }    

    return(
        <>
            <button onClick={handleClick}>
                Click Me!
            </button>

            <input ref={inputRef}>
        </>
    );
}

export default MyComponent;
```

# NodeJS & React

You will need to install **cors** on your **NodeJS** server if your **React** app is running on a different port / host. Create a new **/server** folder outside of your **React** app and create a **server.js** file in there.

Run the following commands in the root of your /server directory.

```javascript
npm init //select server.js as your entrypoint during setup
```

```
npm install express cors
```

Setup a route in your **NodeJS** server that will handle the requests.

```javascript
const express = require('express');
const cors = require('cors');
const app = express();
const port = 8081;

// Enable CORS for all routes
app.use(cors());

// Middleware to parse JSON bodies
app.use(express.json());

// Sample endpoint to handle GET requests
app.get('/api/data', (req, res) => {
    const receivedData = req.body;
    console.log(receivedData); // This should log the received data
    res.json({ message: 'Data received successfully', data: receivedData });
});

// Sample endpoint to handle POST requests
app.post('/api/data', (req, res) => {
    const receivedData = req.body;
    console.log(receivedData); // This should log the received data
    res.json({ message: 'Data received successfully', data: receivedData });
});

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});
```

# Axios

You can use **Axios** in you **React** app to do GET/POST requests to your server. **Axios** handles some thing's so that your server and **react** app can communicate even though they are different apps.

First, in your **React** app, install the NPM package **Axios**.

```
npm install axios
```

# GET Request

Use **Axios** for a GET request in a **React Component**

```javascript
import React, { useState, useEffect } from 'react';
import axios from "axios";

const App = () => {

    const [data, setData] = useState("");

    {/* When component loads, do a GET request */}
    useEffect(() => {
      axios.get("http://localhost:8081/api/data")
      .then(res => {
        setData(res.data.message);
      })
      .catch(e => console.error(e))
    }, [])

    return (
        <>
           <h1> {data ? data : "Loading..."} </h1>
        </>
    );
};

export default App;
```

# POST Request

Here is how to do a POST Request using the **Axios** NPM Pacakage.

```javascript
import React, { useState } from 'react';
import axios from "axios";

const App = () => {

    const [data, setData] = useState("");
    
    function postRequest(){
      axios.post("http://localhost:8081/api/data")
      .then(res => {
        setData(res.data.message);
      })
      .catch(e => console.error(e));
    }

    return (
        <>
           <h1> {data ? data : "Loading..."} </h1>
           <button onClick={postRequest}> Post Request </button>
        </>
    );
};

export default App;
```