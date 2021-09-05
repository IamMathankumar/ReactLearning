# 1. Learning
This project is simple project to displaying string and applying styles

## Text

In react we can display text using String, arraylist, and json object in JSX

`const arrayList = ["First text", "second", "Third one"]`

### We can display arraylist just like the below line

`<label>{arrayList}</label>`

### We can call function inside jsx
`function labelText(){
return "First lesson from function"
}`

`<div>{labelText()}</div>`

## Style

In react we can do Inline style, we can call css and we can create js object\
While using style we can't use styling just like css format instead we should call like the below\
`backgroundColor: "Red"`

### Inline style
`<div style = {{backgroundColor:""#00ff", color:"red"}}>Hello</div>`

We should use two braces to styling JSX component. reason is we should use JS object to style a component to get a value from variable or function we need to use JS object braces that's why we need two open and close braces

### Calling JS object to style
we can create separate js object to call it in style props\
`const color = {backgroundColor:""#00ff", color:"red"}`\
`<div style = {color}>Hello</div>`\
Here single brace is enough because we are calling an object


# 2. List components 


### props 

To share value to another component we should use props in react

`<MediaCard image={faker.image.avatar()} title={faker.name.title()} description={faker.lorem.paragraph()}/>`

### Child component and props
In Action card component we appended child component using props.children.

     <Card className={classes.root}>
            <CardActionArea>
            {props.children}
            </CardActionArea>
           ...
        </Card>


While calling Action card from index.js we append MediaCard as nested child,\
to display nested child we should follow the above option

     <ActionCard>
    <MediaCard image={faker.image.avatar()} title={faker.name.title()} description={faker.lorem.paragraph()}/>
    </ActionCard>

Here we can add many components as well there is no limit to pass only single component. it's based on our need i.e

       <ActionCard>
           <div>Hello</div>
           <div>Hello</div>
       </ActionCard>


# GeoLocation,  class components

### Geo location 

Open [Mozilla Geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API/Using_the_Geolocation_API) and follow the instructions to get current location of user

This is the code to get geolocation to use current location user needs to allow our app to use  

    window.navigator.geolocation.getCurrentPosition(
        success => {
            console.log(success)
        },
        positionError => {
            console.log(positionError)
        }
    )

here success and positionError is variable name we can use anything, get current position needs two listener to get success and failure


## Browser Sensors
We can use sensors to change current location to some other place > just like VPN


## Class component
 Here class is a prototype inheritance it's not like actual class like Java but it will work like a class 
 
    class App extends React.Component

we should extend `React.Component` to create class level component
Also we should use render function in class component to make it work

    render() {
    return (<div>Hello</div>)
    }


## state object in class components 
We can create state object inside constructor also we can create without constructor read initialize state without constructor topic to learn how

    constructor(props) {
    super(props);
    /*In class level component we should call state like */
    this.state = {lat: null, lng:null}
    }

we can call the value just like the below 

     <div>
      Hello world my latitude: {this.state.lat} and longitude : {this.state.lng}
      </div>

To update value 

    this.setState({
    lat :  position.coords.latitude,
    lng :  position.coords.longitude
    })


we can return component conditionally like below 

        if (this.state.lat === null && this.state.errorMessage === null) {
                return <div>Loading</div>
            } else if (this.state.lat === null && this.state.errorMessage !== null) {
                return <div>{this.state.errorMessage}</div>
            } else {
                return (<div>
                        Hello world my latitude: {this.state.lat} and longitude : {this.state.lng}
                    </div>)
            }

## Life cycle methods

`componentDidMount()`

this function will be called when content visible on screen

`componentDidUpdate`

this function will be called whenever there is a change occur. (sit and wait for updates)

`componentDidUnmount`
sit and wait until this component no longer shown

We can move geolocation code inside  `componentDidMount()` as it will call only once

## initialize state without constructor 

we can initialize like below without constructor because babel will create constructor for us.\
when we are initializing globally **we don't need to use `this`** \ but we should use `this` in constructor  
`state = {lat: null, lng:null}`


## To display style, icon and text dynamically 

A getSeason function returns "summer" and "winter" based on latitude and current month for north and south side

### To display text

    const displayText = {
    summer : {
    text : "It's too hot",
    iconName : "sun" //here iconName is semantic UI icon name just like material icon in material UI
    },
    winter : {
    text : "It's too cool",
    iconName : "snowflake" //here iconName is semantic UI icon name just like material icon in material UI
    }
    }

after creating this function we are calling the following function to get only a selected object

    const displayObject = seasonConfig[season] // here we are getting only the selected type object by passing season value

Now we can get only the selected object and can display the content like below

    <i className={`icon-left massive ${displayObject.iconName} icon`}/>
    <h1 className={`text-center `}>{displayObject.text}</h1>
    <i className={`icon-right massive ${displayObject.iconName} icon`}/>

## Style dynamic placement 
Same way we can create .summer, .winter style and we can display style based on current value
`  <div className={`root ${season}`}>`


## default props
If we want to set some default value for props we can do like this

    Spinner.defaultProps = {
    message : "Loading..."
    }

Here Spinner is function name or component name

 we can also  set default value like below

`<div style={colorForText}>{props.message || "Error"}</div>`

## To put common element in render function

we are using conditional return in index.js if we want to use common style for all the conditions like applying border we should write in all condition

    if (this.state.lat === null && this.state.errorMessage === null) {
    return <Spinner message={"Accept location"}/>
    } else if (this.state.lat === null && this.state.errorMessage !== null) {
    return <Error message={this.state.errorMessage}/>
    } else {
    return <SeasonDisplay lat={this.state.lat} lng={this.state.lng}/>
            }


to avoid this we can create new function to hold these conditional statement and we can call it in render function

    render() {
        return (
            <div className={`border red`}>
                {this.renderComponent()}
            </div>
        )

    }
    
    
    #4 Handling inputs, form and  state object in input plus this operator  

## Form on submit

When we are using forms for input objects we should handle onsubmit, reason is when user clicks enter button page will start to reload by default behaviour whenever we don;t need default behaviour we should call this below function in event

    event.preventDefault() //This is must needed to disable default on submit behaviour in form

## Handling `this` operator

When we are using state object in class component we should use this operator to call the global variable
But when we are calling this operator inside handler like `onChange` and `onSubmit` `this` operator won't work in normal function 

In javascript `this` operator is handled in many way. In simple words `this` operator is referring the class or object that called from
Just like in Java we can't use this operator directly in event handler function the same way in Javascript

To solve this issue we can use arrow function or arrow function call or we can bind this in constructor of class for the function

### solution 1 arrow function

    onFormSubmit = (event) => {
    console.log(this.state.text)
    console.log(event)
    event.preventDefault() //This is must needed to disable default on submit behaviour in form
    }

In arrow function this operator is handled by default

### solution 2 call a  normal function using arrow
Calling normal function in this way
    `onSubmit={ e => this.onFormSubmit(e)}`
Normal function

    onFormSubmit(event){
    console.log(this.state.text)
    console.log(event)
    event.preventDefault() //This is must needed to disable default on submit behaviour in form
    }

### Solution 3 create binding for a normal  function in class constructor

    constructor(props) {
        super(props);
        this.onFormSubmit = this.onFormSubmit.bind(this) //we can bind this like this  to avoid this undefined error for this function
    }


## no need parenthesis while calling a function from event handler
Because we can use the reference of a function if we avoid to use open close parenthesis


## Passing value from child to parent
Using props we can send a value from child to parent 

In onsubmit we used `this.props.onSubmit(this.state.text)` to send a value to parent

    onFormSubmit = event => {
        event.preventDefault() //This is must needed to disable default on submit behaviour in form
        this.props.onSubmit(this.state.text)
    }

from parent component we should get the event by calling the function name just like the below
` <SearchBar onSubmit={ this.handleOnSubmit}/>`

Here OnSubmit is a function that called by a child component and we are getting those values and passing to another function to process it

    handleOnSubmit(e){
        console.log(e)
    }


## Async and Then 

We are using axios to get network api result instead of default fetch\
axios provides an async option while fetching data 

    axios.get('/user?ID=12345')
    .then(function (response) {
    // handle success
    console.log(response);
    })

### we have another way to do `async` task 

In function we should add `async`

    async onSubmit(e){
    cosnt result = await axios.get('/user?ID=12345')
     // handle success
    console.log(result);
    }

 here we used async before function name to make this function as `async` function and waiting to get result from axios we added `await` 

## Access `this` in async function
We cannot access `this` operator in normal function. so we should make it as arrow function. 
while changing async function to arrow function like normal function it won't work it will give error

We should follow this way

    handleOnSubmit = async (e)  => {
    const result = await  axios.get(`https://api.unsplash.com/search/photos?client_id=3_IMYdblxFL_0Vw7ADbJOugzj-29ITKw_7VnjnzVOCI&query=${e}`)
    console.log(result);
    this.setState({images : result.data.results})
    }
### default value for array list

usually we wil assign null as a default value for an object but for arraylist we should use empty array to avoid undefined exception
`state = {images : []}`

## Reference object and event listener for load
In some cases we need to get the size of image view after loading, In that case we need a reference of a component 
In class level component we should create and assign a reference like this

    constructor(props) {
        super(props);
        this.refImage = React.createRef()
    }

To assign a value for a reference 

`return (<img ref={this.refImage} src={item.image} alt={item.description} className={classes.root}/>)`

Here make sure you are calling ref in top level component or direct child component\
because it didn't worked for nested childs please check when you are needed 


# useState, useEffect, useRef, Navigation

## UseState

In class component we used `state ={item : null}` state object here in functional component we should use `useState` instead of `state` object

while using useState, useEffect or useRef we should add it in import statement

`import React, {useState} from "react";`

syntax to create useState object

`const [selectedIndex, setSelectedIndex] = useState(0)`

To set a value in useState object we can do like the below

`setSelectedIndex(e)`

we can use value directly in div component with JS object curly race `{selectedIndex}`

## useEffect `!important`
while using useState, useEffect or useRef we should add it in import statement

`import React, {useState, useEffect} from "react";`

### Useeffect with empty array
    useEffect(()=>{
    }, [])

Use effect with empty array will run only once art initial rendering

### UseEffect without second parameter

    useEffect(()=>{
    })
without second parameter will render everytime whenever view rendered and also in initial render

### UseEffect with value in array

`const [selectedIndop0iex, setSelectedIndex] = useState(0)`

    useEffect(()=>{
    }, [selectedIndex])

It will execute in initial render and whenever the object changes inside we added in array 

We can add many object in that array if we want

    useEffect(()=>{
    }, [selectedIndex])


## useEffect with async
We cannot change useEffect as async function we should create a function inside useEffect and then we should call it
### solution 1 :

    useEffect(()=>{
    const search = async () => {
    const value = await axios.get("")
    }
    search()
    }, [selectedIndex])

### solution 2:
 same way we removed variable and added a function inside paranthesis and called the function 

    useEffect(()=>{
    (async () => {
    const value = await axios.get("")
    })()
    }, [selectedIndex])

### solution 3: 
Using promise

    useEffect(()=>{
    axis.get().then((response)=>{
    });
    },[selectedindex])


## useEffect with return function (**more important**)
Initially useEffect function will be called when new component rendered and when there is changes return function will be called and component will be rendered again useEffect function will be called(based on above three types of useEffect)
    
useEffect(()=>{

    return ()=>{
    }
    });

## Throttling API requests

While user changing text we are calling apis everytime Instead of that we can use timer to wait for 500ms for next change if change is not  occur we can call the api

