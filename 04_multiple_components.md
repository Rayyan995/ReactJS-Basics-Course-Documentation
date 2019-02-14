# Multiple Components
* Let's take a step further and render **multiple** components.
* To do that let's create a folder to hold all of our components. We make this folder under ` src/app/ ` and we name it ` components ` for convention.
* Under this folder we can make a **.JS** file for each component we wanna **define**. Remember that in these files we will just **define** the component. However, we will render it in **index.js** file.
* Let's make component and name it ` Home `.
    1. Create a file and name it ` Home.js `
    2. Import only ` react `. No need here to import ` react-dom ` since we will not use any thing from it even ` render ` method.
    ```
    import React from 'react';
    ```
    3. define your class that ` extends ` ` React.Component `. But here we will make a new thing. We will ` export ` this class since we need to use it in **index.js** file.
    ```
    export class Home extends React.Component {
        render() {
            return (
                <div>
                  <p> Home </p>
                <div>
            );
        }
    }
    ```
* Follow these steps to make the second Component with just changing names and the **JSX**.
* Now let's combine these two components into the App component in **index.js** file and render it.
    1. First, import both ` react ` and ` react-dom `.
    2. Import your own Components.
    ```
    import { Home } from './components/Home';
    import { Header } from './components/Header';
    ```
    3. Let's redefine our **AppComponent** class.
    ```
    class AppComponent extends React.Component {
        render() {
            return(
                <div>
                  <div>
                    <Home/>
                  </div>
                  <div>
                    <Header/>
                  </div>
                </div>
            );
        }
    }
    ```
    4. Invoke ` render ` method in the root of ` index.js ` script with changing nothing.  
