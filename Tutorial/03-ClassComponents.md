## Class components

Class components in React must `extend` (inherit from) the `React.Component` class. These components are more complex than function-based components, and they are the basis for a very important React concept: **state**. 

### State

State is meant to hold information that might be dynamically changed -- by user interactions, API calls, or any other change in the data your app draws from. When information changes in state, the component re-renders by default, meaning that relevant changes are immediately reflected on the page.

State is initialized in the class `constructor()` method:

```javascript
    class RecordList extends React.Component {
        constructor(props) {
            super(props)  // super() must be called in the constructor to use React capabilities
            this.state = {
                itemOne: 'some value',
                itemTwo: 'another value'
            }
        }
    }
```

After this initialization, any methods within the class can access these values by calling the appropriate key in `this.state`.

### Rendering

Class components have a `render` method, the contents of which look a lot like the return of a function component:
```javascript
    render() {
        return (
            <div>
                <h2>{this.state.itemOne}</h2>
                <h3>{this.props.firstProp}</h3>
            </div>
        )
    }
```

>Props can be passed to class components just like with function components -- except that in class components, they are accessed as `this.props`.

### Setting State

React state is designed to automatically re-render any components that depend on the information in state -- in other words, if you change state, what you see on the screen will automatically change accordingly. To take advantage of this capability, though, state **must** be set using the `setState()` method.

```javascript
    this.setState({
        itemTwo: 'yet another value'
    })
    // in the above component, this would change the "itemTwo" attribute in state and automatically re-render dependent components
```

### Custom Methods

In addition to `constructor()` and `render()`, class-based components may include any number of instance methods -- these are a typical way to bring about changes in state depending on user interaction.

```javascript
class Methodizer extends React.Component {
  constructor(props) {
      super(props)
      this.state = {
          clicked: false
      }
  }

  // this method changes a property in state
  clickHandler = () => {
      this.setState({ clicked: true })
  }

  render () {
      // this.clickHandler is attached to the <button> below
      return (
        <div>
          { this.state.clicked ? (<h1>CLICKED</h1>) : (<button onClick={this.clickHandler}>Click here!</button>) }
        </div>
      )
  }
}
```

>**NOTE:** It's best practice to declare methods using ES6 arrow notation -- i.e. `methodName = (params) => {}` -- for reasons that are outside the scope of this workshop. Basically, this notation binds the function to the instance of the class. Look this up sometime! But for now, just make it a habit to use this notation.

### State and Methods as Props

Often, a React app will hold state in one or just a few components, while most component will simply accept props. State information will often be passed from a parent component to a child as props, like so:
```javascript
        <ChildComponent name={this.state.name} color={this.state.color} />
```

That's pretty straightforward. What's much wilder is that *methods* may be passed as props from parent to child as well:
```javascript
        <ChildComponent name={this.state.name} clickFunction={this.clickHandler} />
```
In this case, the child component can invoke `props.clickFunction()` and the function will run **on the parent component**. This means that information can be passed **upward** through such a method into the parent component. There's no other native way to move information **up** the component tree in React.

### Lifecycle methods

You may also define **lifecycle methods** that are invoked at a certain point in a component's lifecycle. `constructor()` is one of these, for instance -- it is invoked as soon as the instance is created. You can read more about these here: https://reactjs.org/docs/react-component.html

The most commonly used lifecycle methods are `componentDidMount` and `componentDidUpdate`. Importantly, `componentDidMount` is fired as soon as the component is inserted into the React tree, which means it is **the most common** place to make API calls to retrieve info that your component will need to render correctly.

>**BUILD A REACTIVE COMPONENT WITH STATE:** Create a new class-based component called `RecordList` and include the record data from the last section in state:

```javascript
class RecordList extends React.Component {
    constructor(props) {
    super(props)
    this.state = {
        recordData: [
            {id: 1, title: "Synchronicity", artist: "The Police", releaseYear: 1984},
            {id: 2, title: "Disintegration", artist: "The Cure", releaseYear: 1989},
            {id: 3, title: "Graceland", artist: "Paul Simon", releaseYear: 1986}
        ]
    }
}
```

>Import your `Record` component. Now, in the `render` method of the `RecordList` component, use state data and the `.map()` method to render a `Record` for each item in the array.
>
>Create a method called `recordAdder` that will use `setState` to add a record of your choice to this array. Now attach this method to the `onClick` attribute of a new button element to make the list of records update when you click.

**Now move on to [Part 4 - Controlled Components and More](04-ControlledComponentsAndMore.md)!**