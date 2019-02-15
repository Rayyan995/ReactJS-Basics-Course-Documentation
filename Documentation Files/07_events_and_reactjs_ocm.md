# Events and ReactJS-OCM
* Now let's discuss how to use *Events* in **ReactJS**. Generally there is no new things here.
    1. Let's create a simple ` Component ` named ` Counter ` that will contain a counter as a text and a button to increment this counter.
    ```
    import React from 'react';
    export class Counter extends React.Component {
        render() {
            let count = this.props.count;
            return (
                <div>
                  <h1>Counter</h1>
                  <p>{ count }</p>
                  <button>Increment Me</button>
                </div>
            );
        }
    }
    ```
    2. Let's render this ` Counter ` ` Component ` from ` AppComponent `. We're gonna modify ` render ` method in ` AppComponent `.
    ```
    render() {
        return (
            <div>
              <Counter count={ 0 }/>
            </div>  
        );
    }
    ```
    Of-course we need to ` import ` the ` Counter ` ` Component `.
    ```
    import { Counter } from './components/Counter';
    ```
    3. Now the ` Component ` is displayed correctly and we need to add an event that responds to clicking the button ` Increment Me `. First It would be better if we store the ` count ` property as a property in the ` Counter ` class itself to be accessed easily. So let's make a ` constructor ` for this class and assign to the class a ` count ` property.
    ```
    constructor( props ) {
        super();
        this.count = props.count;
    }
    ```
    Also let's define a ` function ` to be called when that event fires.
    ```
    increment() {
        this.count++;
    }
    ```
    Then we define the event by Assigning ` increment ` to the attribute ` onClick ` of the ` button `. Here we modify only ` render ` method.
    ```
    render() {
        return (
            <div>
              <h1>Counter</h1>
              <p>{ this.count }</p>
              <button onClick={ this.increment }>Increment Me</button>
            </div>
        );
    }
    ```
    Until now we expect that the counter should be incremented. However, we get this error: ` TypeError: this is undefined ` on hitting the button. What's going wrong? In the ` increment ` function we access ` this.count ` but when assigning this ` function ` to ` onClick ` attribute ` this ` here does not refer to the ` Counter ` object. It actually refers to ` undefined `[Till now I do not know what it exactly refers to whether the window or the button]. To solve this issue we have two ways:
         * ` bind ` the ` Counter ` object with ` increment ` function.
         ` onClick={ this.increment.bind( this ) } `.
         * Use *arrow* function.
         ` onClick={ () => this.increment() } `  
    By now we solved this problem of *scoping* and the ` count ` property is incremented successfully. However, nothing is changed on screen since we simply did nothing with the DOM. We need to tell **React** that the ` state ` has been changed and thus you should update the DOM.
