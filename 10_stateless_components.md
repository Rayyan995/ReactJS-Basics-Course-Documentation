# Stateless Components
* We have two kinds of *Components* in **ReactJS**:
    * **Stateful Components**  
    These are *components* that have ` state ` like the ` Counter ` *Component* in our project.
    * **Stateless Components**  
    These are *Components* that do not need ` state `. It may be a *static component* that does not change. *Components* that can be *stateless* in our project are ` Person `, ` Home `, and ` Header `.
* Having *stateless components* as many as possible is good. ` state ` has significant consequences on **behavior, performance, and testability**. Having **many** *stateful components* in complex applications creates **unpredictable** behavior as well as makes it really **hard** to **test** the application. So on the other hand, having **many** *stateless components* makes your application **more manageable and testable**.
* A *stateless component* actually is not more than a ` function ` that returns a **JSX** to be rendered and optionally accepts ` props `. So with *stateless components* we do not need to extend ` React.Component ` any more. Let's convert the ` Person ` ` Component ` to a *stateless component*.  
First let's render the ` Person ` *component* in ` AppComponent ` instead of ` Counter ` *component*.
```
render() {
    let p = {
        name: "Hossam",
        age: 22,
        friends: ["Ismail", "Ayman"]
    };
    return (
        <div>
          <Person personObj={ p }>
            Hello
          </Person>
        </div>
    );
}
```
And now it's time to move to a *stateless component*
    * From
    ```
    import React from 'react';
    export class Person extends React.Component {
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
    }
    ```
    * To
    ```
    import React from 'react';
    export const Person = ( props ) => {
        let name = props.personObj.name;
        let age = props.personObj.age;
        let friends = props.personObj.friends;
        let welcome = props.children
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
