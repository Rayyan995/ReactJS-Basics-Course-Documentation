# React-Router Navigation and Parameters
* Until now hitting the items in the ` Header ` does not navigate. Let's add this navigation. To do that we modify the ` Header ` ` Component `.
```
import React from 'react';
const Header = (props) => {
    return(
        <nav>
          <ul>
            <li><Link to="/home">Home</Link></li>
            <li><Link to="/person">Person</Link></li>
          </ul>
        </nav>
    );  
};
```
We just changed the ` <a> ` tag to ` <Link> ` tag and the ` href ` attribute to ` to ` attribute. These are required by ` react-router ` which will eventually be converted into ` <a> ` tag in the browser.
* To add another way to navigate from a ` Route ` to another one(let's say from ` Person ` to ` Home `) we use the ` browserHistory.push( "/home" ) ` which we can wrap in a ` function ` and assign it to ` onClick ` event handler of a button or whatever.
* Now let's see how we can pass parameters from a ` Component ` to another. Let's accept the ` ID ` of the ` Person `. We do that by using ` props.params ` and then use whatever param names we want to accept.
```
import React from 'react';
class Person extends React.Component {
    render() {
        return (
            <div>
              <h2>Person Page</h2>
              <p>Person ID: { this.props.params.id }</p>
            </div>
        );
    }
}
```
We also need to specify that the ` path ` to the ` Person ` ` Route ` accepts params named ` id ` as we named it in ` props.params.id `. This is done in the entry point where we specified the ` Route ` of ` Person `. So the ` Route ` of ` Person ` becomes:
```
<Route path="person/:id" component={ Person }/>
```
Now the ` path ` of ` Person ` accepts an ` id ` param.  
By that from any ` Component ` we can navigate to the ` Person ` ` Component ` and pass the ` id ` parameter by adding the ` id ` parameter to the link ` /person/7 ` for example.
