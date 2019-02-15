# State of Components
* **State** is an object in the ` React.Component ` class. It is what allows us to dynamically change the *UI* of a component in the running time.
* If we use any property from the ` state ` object in the *UI*(**JSX** returned from ` render ` method of that ` Component `), **ReactJS** keeps listening for this ` state ` object and whenever any property inside ` state ` object changes, **ReactJS** automatically updates the element of *UI* that is affected by this change.
* Now let's solve the problem of updating *UI* that we encountered in the last video. We had a button that updates ` count ` property in running time. So what we will do is to put the ` count ` property in the ` state ` object so whenever the button updates it, this update is reflected on the *UI*. Whenever we need to update the ` state ` we call a method named ` setState ` and pass as an argument an object wrapping what properties we wanna update in the ` state ` object. [Hint: You do no have to worry about other properties in the ` state ` object that you do not wanna update. Just pass as an argument an object wrapping your changes and any properties not mentioned in that argument will stay intact]. Let's modify our ` Counter ` class.
```
import React from 'react';
export class Counter extends React.Component {
    constructor( props ) {
        super();
        this.state = {
            count: props.count
        }
    }
    increment() {
        this.setState( {
            count: this.state.count + 1
        } );
    }
    render() {
        return (
            <div>
              <h1>Counter</h1>
              <p>{ this.state.count }</p>
              <button onClick={ this.increment.bind( this ) }>Increment Me</button>
            </div>
        );
    }
}
```
* As a side note the instructor advised to not assign props to ` state `, as we did, except for the case when it is an initial value(*good practice*).
