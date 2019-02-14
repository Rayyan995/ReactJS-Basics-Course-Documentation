# Passing Data between Parent and Child Component
* Now let's see an example that **proves** clearly that we can pass data *from child* component *to parent* component.
* We're gonna make a header in the ` AppComponnet ` that displays *App Name*. Initially our app name is "general app" and from the *child component* ` Person ` we wanna update that app name to be "People App".
    * In ` AppComponent `.
    ```
    class AppComponent extends React.Component {
        constructor() {
            super();
            this.state = {
                appName: "General App"
            };
        }

        changeAppName( newName ) {
            this.setState( {
                appName: newName
            } );
        }

        render() {
            let p = {
                name: "Hossam",
                age: 22,
                friends: ["Ismail", "Ayman"]
            };
            return (
                <div>
                  <div>
                    <h1>{ this.state.appName }</h1>
                  </div>
                  <div>
                    <Person personObj={ p } changeAppNameFun={ this.changeAppName.bind( this ) }/>
                  </div>
                </div>
            );
        }
    }
    ```
        * Here we added a ` state ` object to the ` AppComponent ` and defined a property in that ` state ` named ` appName ` and assigned it in the ` constructor ` initial value "General App".
        * We defined a ` function ` named ` changeAppName ` that change that property by calling ` setState ` method. This ` function ` accepts the new app name which will be passed from the *child component* ` Person `.
        * We added an ` <h1> ` tag and set its value to ` appName ` property in the ` state ` object so once this property is changed by invoking the ` changeAppName ` ` function ` this `<h1> ` tag is rerendered.
        * We pass this ` changeAppName ` ` function ` to the *child component* to be called from there with the new app name. Notice that we *binded* ` this ` with ` changeAppName ` ` function `.
    * In ` Person `.
    ```
    import React from 'react';
    export const Person = ( props ) => {
        let name = props.personObj.name;
        let age = props.personObj.age;
        let friends = props.personObj.friends;
        let appName = "People App";
        let changeAppNameFun = props.changeAppNameFun;

        return(
            <div>
              <h2>Person</h2>
              <p>{ name }</p>
              <p>age: { age }</p>
              <h4>Friends</h4>
              <ul>
                { friends.map( (friend, i) => <li key={ i }>{ friend }</li> ) }
              </ul>
              <button onClick={ () => changeAppNameFun( appName ) }>Change App Name</button>
            </div>
        );
    }
    ```
    Here we just accepted the ` changeAppName ` ` function ` from ` props ` and assigned it to the event handler of a button.
