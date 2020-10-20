## More React Quirks

### Forms and State

Creating forms in React is a bit counterintuitive, especially for developers accustomed to Vue's `v-model` property. In React, the `value` of an `input` element is tied to a value in state, then the input is linked to a "handler" function via the `onChange` property. To the user, it just looks like they are typing in a form; for the developer, it's slightly awkward to set up.

Consider this pattern:
```javascript
// in constructor
this.state = {
     username: ''
}
// as a method of the component
    handleChange = e => {
        this.setState({ [e.target.name]: e.target.value })
    }
// attach the method to the input's onChange attribute
<input type='text' name='username' value={this.state.username} onChange={(e) => this.handleChange(e)}/>
```

In this example, `e.target.name` refers to the `name` property of the `input` -- the `handleChange` method ties this named input to the key in state of the same name.

### Logical Operators

Logical operators (`&&`, `||`, and `?`) are often used as a shorthand to create conditional rendering in JSX. The key to this is knowing what is *returned* by these operators:
* `&&` returns `false` if any condition is not met and returns *the last element* if all evaluate true
* `||` returns the first condition that evaluates `true` or `false` if none
* `?` returns the first element after the question mark if the condition is met, the second if not

Some typical patterns:
```javascript
// before render
const records = this.state.records[0] && this.state.records.map(record => <Record info={record.info} />)

// in render
{ this.state.clicked ? (<h3>It's clicked!</h3>) : (<button onClick={() => this.setState({clicked: true})}>Click here!</button>) }
```

Keep an eye out for opportunities to use these operators for `if` and `if...else`-type logic.

