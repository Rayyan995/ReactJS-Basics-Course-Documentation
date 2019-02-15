# Tow-Way Binding
* Now let's allow the user to dynamically update the *app name* which is a text in the *parent component* ` AppComponent ` from inside the *child component* ` Person `.
    * In ` Person ` *component* we will add a text input field to let the user enters the app name at any given time. The initial value of that text input field we will accept from ` AppComponent ` in ` props ` as ` initialAppName `. Then we need any time the user changes the text we store this value and on hitting the button we trigger a ` function ` that takes this value and pass it to another ` function ` that changes the *UI*. So we need to make the ` appName ` a property in the ` state ` of the ` AppComponent ` so once we need to update the *UI* we invoke the ` function ` ` setState ` for the ` AppComponent `. We also need to store the value of the text input field in the ` state ` of ` Person ` *component* so that we can update it when the user updates the text input field and access it when the user hits the button.  
    ```
    import React from 'react';
    export class Person extends React.Component {
          constructor( props ) {
              super();
              this.state = {
                  appName: props.initialAppName
              }
          }
          onAppNameChange( newName ) {
              this.setState( {
                  appName: newName
              } );
          }
          render() {
            let name = this.props.personObj.name;
            let age = this.props.personObj.age;
            let friends = this.props.personObj.friends;
            let changeAppNameFun = this.props.changeAppNameFun;
            return(
                <div>
                  <h2>Person</h2>
                  <p>{ name }</p>
                  <p>age: { age }</p>
                  <h4>Friends</h4>
                  <ul>
                    { friends.map( (friend, i) => <li key={ i }>{ friend }</li> ) }
                  </ul>
                  <input type="text" value={ this.state.appName } onChange={ (event) => this.onAppNameChange( event.target.value ) } />
                  <button onClick={ () => changeAppNameFun( this.state.appName ) }>Change App Name</button>
                </div>
            );
        }
    }
    ```
    * In ` AppComponent ` we define a ` constructor ` to store the value of app name in the ` state `. We store an initial value in the ` constructor ` and then we define a ` function ` which will be invoked from the ` Person ` *component* that takes as arguments the new app name. In this ` function ` we take the new app name and change the ` state ` using ` setstate ` ` function `. Do not forget to ` bind ` ` this ` with the ` function ` since it will be invoked from ` Person ` *component*. We also assign the app name in the ` state ` to the ` props ` of the ` Person ` *component*.
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
                    <Person personObj={ p } initialAppName={ this.state.appName } changeAppNameFun={ this.changeAppName.bind( this ) }/>
                  </div>
                </div>
            );
        }
    }
    ```
    * The reason why we need to store the app name in ` Person ` *component* as a ` state ` not a normal property ` this.appName ` is that we need to display the initial app name we accepted from ` AppComponent ` on the text input field. If we tried to assign the ` value ` attribute of the text input field ` this.appName ` instead of ` this.state.appName `, on hovering over the text input field and type the new text will not appear since it is assigned a static value. However, in the case of ` state ` on typing we change the ` state ` and it is updated automatically on the DOM. If we do not want to displlay an initial value in the text input field we could use the app name as a normal property in ` Person ` *component*.
