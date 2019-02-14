# Passing Data with Props
* Since **ReactJS** is all about creating *components* and *reusing* them, it will be good if we have a way to define *general components* and specify them when we wanna render by passing data to specify them.
* In other words we wanna pass data from *components* to other *components* to be displayed by the latter.
* In **ReacyJS** we have a property in the ` React.Component ` class called ` props ` which is short for *properties*. We can use this property to pass data and display them.
* So we have two parts:
    * **Passing data**
    We pass data by specifying them in **JSX** as if they were attributes and we assign these attributes values by surrounding these values by *curly braces*. So let's say we will create a ` Component `  called ` Person ` and this component will accept these properties: ` name `, ` age `. In ` AppCmponent ` we modify ` render ` method.
    ```
    render() {
        return (
            <div>
              <Person name={ "Hossam" } age={ 22 } />
              <Person name={ "Ismail" } age={ 24 } />
            </div>
        );
    }
    ```
    Also we have to impot the ` Person ` component.
    ```
    import { Person } from './components/Person';
    ```
    * **Displaying data**
    Now let's define this ` Person ` ` Component ` , receive these data and display them. We create this ` Component ` under ` src/app/component ` directory.
    ```
    import React from 'react';
    export class Person extends React.Component {
        render() {
            let name = this.props.name;
            let age = this.props.age;
            return(
                <div>
                  <h2>Person</h2>
                  <p>Name: { name }</p>
                  <p>age: { age }</p>
                </div>
            );
        }
    }
    ```
* We can send data of any types including **objects**. So let's wrap this ` Person ` related data in an object.
    * In ` AppComponent ` let's modify ` render ` method.
    ```
    render() {
        var p1 = {
            name: "Hossam",
            age: 22
        };
        var p2 = {
            name: "Ismail",
            age: 24
        };
        return(
            <div>
              <Person personObj={ p1 }/>
              <Person personObj={ p2 }/>
            </div>
        );
    }
    ```
    * In ` Person ` let's modify ` render ` method.
    ```
    render() {
        let name = this.props.personObj.name;
        let age = this.props.personObj.age;
        return(
            <div>
              <h2>Person</h2>
              <p>Name: { name }</p>
              <p>age: { age }</p>
            </div>
        );
    }
    ```
* Now let's try to send an *array* ` friends ` and display it in an *unordered list* dynamically.
    * In ` AppComponent ` let's modify ` render ` method.
    ```
    render() {
        var p1 = {
            name: "Hossam",
            age: 22,
            friends: ["Ismail", "Ayman"]
        };
        var p2 = {
            name: "Ismail",
            age: 24,
            friend: ["Hossam", "Ayman"]
        };
        return(
            <div>
              <Person personObj={ p1 }/>
              <Person personObj={ p2 }/>
            </div>
        );
    }
    ```
    * In ` Person ` let's modify ` render ` method.
    ```
    render() {
        let name = this.props.personObj.name;
        let age = this.props.personObj.age;
        let friends = this.props.personObj.friends;
        return(
            <div>
              <h2>Person</h2>
              <p>Name: { name }</p>
              <p>age: { age }</p>
              <h4>Friends</h4>
              <ul>
                { friends.map( (friend, i) => <li key={ i }>{ friend }</li> ) }
              </ul>
            </div>
        );
    }
    ```
    Here we used the ` map ` method introduced in *ES6* to output a ` <li> ` for each friend in the ` friends ` array. We also configured the *callback* of ` map ` function to send not only the item but also its index and used this index to give each ` <li> ` a **unique id**(This is required for **ReactJS** to have a way to reference these items in the future.
* We know that **JavaScript** is a *weekly-typed* language. However, we have a way in **ReactJS** to define the *types* of ` props ` and it is a good practice to do so. Let's modify the ` Person ` ` Component ` to do so.
```
import React from 'react';
export class Person extends React.Component {
    render() {
        let name = this.props.personObj.name;
        let age = this.props.personObj.age;
        let friends = this.props.personObj.friends;
        return(
            <div>
              <h2>Person</h2>
              <p>Name: { name }</p>
              <p>age: { age }</p>
              <h4>Friends</h4>
              <ul>
                { friends.map( (friend, i) => <li key={ i }>{ friend }</li> ) }
              </ul>
            </div>
        );
    }
}
Person.propTypes = {
    personObj: React.PropTypes.object
};
```
Here after defining the class for our component, we assign a property named ` propTypes ` an object that contains key-value pairs: key for any property and its value the required type. However, it seems there is a problem with *Webpack* with this. H get an error saying: ` TypeError: react__WEBPACK_IMPORTED_MODULE_0___default.a.PropTypes is undefined `.
* We have another similar way to send and display data in a ` Component `. It is sending data as ` Component ` *children*.
    * In ` AppCompnent ` let's modify ` render ` method.
    ```
    render() {
        var p = {
            name: "Hossam",
            age: 22,
            friends: ["Ismail", "Ayman"]
        };
        return(
            <div>
              <Person personObj={ p }>
              Hello
              </Person>
            </div>
        );
    }
    ```
    * In ` Person ` let's modify ` render ` method.
    ```
    render() {
        let name = this.props.personObj.name;
        let age = this.props.personObj.age;
        let friends = this.props.personObj.friends;
        let welcome = this.props.children
        return(
            <div>
              <h2>Person</h2>
              <p>{ welcome } { name }</p>
              <p>age: { age }</p>
              <h4>Friends</h4>
              <ul>
                { friends.map( (friend, i) => <li key={ i }>{ friend }</li> ) }
              </ul>
            </div>
        );
    }
    ```  
    Here we send an argument as a child to the ` Component ` and accessed using ` this.props.children `. 
