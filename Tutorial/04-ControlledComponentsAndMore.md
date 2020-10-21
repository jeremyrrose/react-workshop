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

>Learn more about forms in React: https://reactjs.org/docs/forms.html

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

### API Data

Because React is compiled in Node, it's possible to import *functions* from external files just as easily as importing components. One typical pattern is to store functions that communicate with an API in a `/services` directory in `/src`.

For instance, you might place this in `/services/index.js`:
```javascript
export const getMessages = async (token) => {
    const resp = await fetch(apiUrl + 'api/messages/',
        {
            method: 'GET',
            headers: {
                "Content-Type": 'Application/JSON',
                "Authorization": `JWT ${token}`               
            }  
        }
    ).then(response => response.json())
    return resp
}
```
>Notice the `export const`. We'll use that in a moment!

Your component, then, might look something like this:
```javascript
import React from 'react'

import {getMessages} from '../services'

class DataDisplayer extends React.Component {

    constructor(props) {
        super(props)
        this.state = {
            data: []
        }
    }

    componentDidMount = async () => {
        await this.getMessagesMethod()
    }

    // assumes a JWT is passed as props from parent component that holds login state
    getMessagesMethod = async () => {
        const resp = await getMessages(this.props.token)
        console.log(resp)
        this.setState({
            data: resp.data
        })
    }

    render () {
        return (<></>)
    }
}
```

>Take a look at this repository to see an example of a login system that imports `fetch`-based functions from `/services` into a component: https://github.com/jeremyrrose/logger-inner

## Router

If your project would benefit from URL routing, you can install React Router by running `npm i react-router-dom` in your project directory. [React Router has very nice docs.](https://reactrouter.com/)

The easiest setup is to use a `<Switch>` component with nested `<Route>` components:

```javascript
// with other imports
import { BrowserRouter, Switch, Route } from 'react-router-dom';

// in render
        <BrowserRouter>
          <Switch>
            <Route exact path="/">
              <LandingPage propOne={propOne} etc={etc} />
            </Route>
            <Route path="/login">              
              <Login propOne={propOne} etc={etc} />
            </Route>
            <Route path="/register">              
              <Register propOne={propOne} etc={etc} />
            </Route>
            {/* The following will show the userId route param in props.match.params in the Profile component */}
            <Route path="/profile/:userId">
              <Profile propOne={propOne} etc={etc} />
            </Route>
          </Switch>
        </BrowserRouter>
```

>You will need to use a `<Link>` component to navigate between pages. Look it up in the docs!
