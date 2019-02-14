# First Component
* As we know **ReactJS** works by **rendering** and **managing** *components*.
* Let's render our first component. In our **index.js** file we will replace the script we put for testing with a script that renders a component.
    1. First, we need to import the dependencies we need which are the 2 React libraries: the core library(` 'react' `) and the one responsible for dealing with the DOM(` react-dom `).
    ```
    import React from 'react';
    import { render } from 'react-dom';
    ```
    Note: I expect that this syntax ` { render } ` is **destructuring** syntax in JavaScript which allows us to extract certain pieces from large data structures. Here we extract only ` render ` function from ` react-dom ` library.
    2. To define a **component** to be rendered, we define a class for that component which ` extends ` ` React.Component ` class which contains a long list of methods(that we will see later) to manage components. For now we will **override** ` render ` method which is used to **render** that component. ` render ` should return a **JSX**(JavaScript XML) node. **JSX** is an XML-like syntax used to draw React components. ` render ` must return a single root node(This node can wrap any number of nodes nested together. The restriction to return one parent node with no siblings).
    ```
    class AppComponent extends React.Component {
        render() {
            return (
                <div>
                  <h1>Hello, This is the first component</h1>
                </div>  
            );
        }
    }
    ```
    After we have defined our own component we can render it by calling ` render ` method(which we imported from ` react-dom `) in the root of our script. ` render ` method accepts as arguments:
        * The name of the class that defines the component we wanna render wrapped in a tag like this ` < /> `.
        * A reference to wherever this component should be rendered. So we should create a tag in ` index.html ` file and reference it using class or id with the appropriate method.
    3. In ` index.html ` file under ` <body> `:
    ```
    <div id="app"></div>
    ```
    4. In ` index.js ` file:
    ```
    render( <AppComponent/>, window.document.getElementById("app") );
    ```    
        * Hint: to use any method on ` document ` we should precede it with ` window ` since this code is not lying in the ` window `.
