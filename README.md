# React

## Key Concepts

* Node dev server
* JSX
* Virtual DOM

* Component types:

    * Functional
    * Class-based

* Render:

    * Triggered by change in props or state
    * `return` in functional component; `render()` method in class

* Props:

    * Passed in as object
    * Access: `props` in functional components; `this.props` in class components
    * Declaration: `<ComponentName id=1 data={[]} myFunc={() => return false} />` creates:
    ```javascript
    props = {
        id: 1,
        data: [],
        myFunc: () => return false
    }
    ```

* Mapping:

    * Use a `.map()` method to render a list of components

```javascript
const things = this.state.thingsArray.map(thing => <Thing prop1={thing.prop1} prop2={thing.prop2}>)

// in return()
{ things }
```

* Class components and `state`:

    * Access: `this.state`
    * To set: `this.setState({key: value})` DO NOT SET DIRECTLY!

* Lifecycle methods:

    * Full description: https://reactjs.org/docs/react-component.html
    * Most used: `constructor`, `componentDidMount`, `componentDidUpdate`

* Other useful ideas:

    * Conditional rendering: `&&` and `?` for `if` and `if...else` behavior
    * Controlled components: Link `onChange` to state via a handler function; value equal to value in state


* Planning concepts:

    * Component structure and file paths
    * Where will state be held?
    * Router vs. pure single-page app



