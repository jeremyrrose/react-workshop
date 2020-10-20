# React - Key Concepts

## Node development environment

A dev server running on your machine dynamically builds your React app for display in the browser, based on the files you create or edit in your project directory.

>**GET STARTED!** Choose or make a directory on your computer to host your React work. Inside that directory, type `npx create-react-app workshop` --  this will create a new React project in a directory called `workshop`. `cd` into that directory and type `npm start` to fire up the React boilerplate.

## JSX

React components can use JSX, a hybrid HTML/JavaScript syntax extension, to make it simpler to define dynamic user interface components.

## Components

Components may be defined as either function or as a class. Some characteristics are shared by all React components.

### Rendering

* Components dynamically re-render; this is triggered by change in props or state.
* Code to be rendered is in the `return` statement in a functional component or the `render()` method in a class component.

### Props

* Props pass information from a parent component to a child -- this information can be of *any* datatype, and often you'll send entire functions as props!
* Props can included when a component is declared in another component's `render`: 

```javascript
    <ComponentName id=1 data={[]} myFunc={() => return false} />

    // the above creates the below "props" object in the child component

    props = {
        id: 1,
        data: [],
        myFunc: () => return false
    }
```

* Within the child component, props are accessed one of two ways: as `props` in functional components, and as `this.props` in class components.

>**BUILD A COMPONENT:** In your new `/workshop` directory, find `App.js` -- this is the root component that React will render to the page by default. In this file, between the line that says `import './App.css';` and the line that says `function App() {`, let's define a new component:
```javascript
    const NewComponent = () => {
        return (
            <h3>This is a new component!</h3>
        )
    }
```
>Now let's render by referencing it in the `return` statement, between the `</header>` and `</div>` tags, like so:
```javascript
            </header>
            <NewComponent />
        </div>
```

>Save your file and take a look in your browser!

**Now move on to [Part 2 - Function Components](02-FunctionComponents.md)!**
