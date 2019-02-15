# Communication between Parent and Child component
* We know how to let a *parent component* communicate with a *child component*. We do that by passing ` props ` from *parent component* to *child component*. But the question is: Can we pass data in the reverse direction from *child component* to a *parent component*. The answer is that there is no a **direct** way to do that. However, we have an **indirect** way to do that.
* Since in **JavaScript** a ` function ` is treated as a *first-class citizen* which means we can pass it as an argument, we can pass a ` function ` from the *parent component* using ` props ` and execute this method on the *child component* using data of the *child component*. Now we execute a ` function ` defined in the *parent component* with data from the *child component* and by that we successfully pass arguments from the *child component* to the *parent component* **indirectly**.
* Let's do that in our ` Person ` *component*. We're gonna define a ` function ` in the *parent component* which is ` AppComponent ` to welcome the person with a welcoming message from the *child component* which is ` Person `. We're gonna also set a button in ` Person ` *component* to trigger this ` function `.
    * In ` AppComponent `.
    ```
    class AppComponent extends React.Component {
        welcomePerson( welcomeMessage, personName ) {
            alert( welcomeMessage + personName );
        }
        render() {
            let p = {
                name: "Hossam",
                age: 22,
                friends: ["Ismail", "Ayman"]
            };
            return (
                <div>
                  <Person personObj={ p } welcomeFun={ this.welcomePerson }/>
                </div>
            );
        }
    }
    ```
    * In ` Person ` *component*.
    ```
    import React from 'react';
    export const Person = ( props ) => {
        let name = props.personObj.name;
        let age = props.personObj.age;
        let friends = props.personObj.friends;
        let welcomeMessage = "Welcome on Board ";
        let welcomeFun = props.welcomeFun;

        return(
            <div>
              <h2>Person</h2>
              <p>{ name }</p>
              <p>age: { age }</p>
              <h4>Friends</h4>
              <ul>
                { friends.map( (friend, i) => <li key={ i }>{ friend }</li> ) }
              </ul>
              <button onClick={ () => welcomeFun( welcomeMessage, name ) }>Welcome me</button>
            </div>
        );
    }
    ```     
