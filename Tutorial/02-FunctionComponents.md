## Function components

Function components like the one you built in the last section are the simplest way to render elements to the DOM in React. Often, they require no logic aside from retrieving information from `props` and plugging it into a JSX template.

We built the last component in `App.js`, but it is common (and smart!) to build each component in its own file. This is the basic structure:

```javascript
import React from 'react';

const NewComponent = (props) => {
    // any JS logic can go here -- additional functions or variables as needed!
    return (
        // JSX to render goes here
    )
}

// export the component to enable use in other files
export default NewComponent;
```
>In the last line, `export default NewComponent` ensures that we can use this component in *other* files by including `import NewComponent from '<<PATH TO FILE>>'` in any other file.

### Props pass information

Suppose a component called `Record` is called from within a parent component. We might see the following in the parent component's `render` -- `id`, `title`, `artist`, and `releaseYear` are all `props`:

```javascript
    <Record id={2} title="Disintegration" artist="The Cure" releaseYear={1989} />
```

In the component's `return` statement, we might see this:

```javascript
    return (
        <div className="record">
            <h2>{props.title}</h2>
            <h3>{props.artist}</h3>
            <p>This album was released in {props.releaseYear}, {2020 - props.releaseYear} years ago.</p>
        </div>
    )
```

>Look at how the information from `props` is used. What datatype is `props.releaseYear`?

### Mapping a list

If we want to return more than one record component based on array of data, we can use JavaScript's `.map()` method:

```javascript
const recordData = [
    {id: 1, title: "Synchronicity", artist: "The Police", releaseYear: 1984},
    {id: 2, title: "Disintegration", artist: "The Cure", releaseYear: 1989},
    {id: 3, title: "Graceland", artist: "Paul Simon", releaseYear: 1986}
]

const records = recordData.map(record => {
    return (
        <Record id={record.id} title={record.title} artist={record.artist} releaseYear={record.releaseYear} />
    )
})
```

Now if we plug `records` into a `render` statement, it will produce a `Record` component for each element in the `recordData` array.

>**RENDER YOUR MAPPED COMPONENTS:** Create a new file called `Record.jsx`. In this file, define and export your `Record` component using the pattern above.
>
>Next, import your component into `App.js` by including `import Record from './Record'` among the other `import` statements. Now, inside `function App()` but *before* the `return` statement, paste the code to create `recordData` and `records` above.
>
>Now you can insert `records` into the page! Just below `<NewComponent />`, add `{ records }`. Save and check your browser!

**Now move on to [Part 3 - Class Components](03-ClassComponents.md)!**
