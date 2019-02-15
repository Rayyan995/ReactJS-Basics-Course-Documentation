# Component Life-cycle
* A ` Component ` has a *life-cycle* that it goes through starting from *initiating*, and *rendering*, handling *rerendering* of the DOM to finally *finishing* and *removing* the ` Component ` from the DOM.
* The ` Component ` *life-cycle* consists of 7 methods which we can divide on 3 stages for simplicity.
    1. **Initial Rendering**  
    As the name suggests, this stage is all about the first time the ` Component ` is being *rendered*. In this stage we have 2 methods:
        1. ` componentWillMount `    
        This method gets executed **right before the initial rendering**. It:
            * **accepts** nothing.
            * **returns** nothing.
        2. ` componentDidMount `   
        This method get executed **right after the initial rendering**. It:
            * **accepts** nothing.
            * **returns** nothing.  
    2. **Handling State Change and Rerendering**  
    As the name suggests, this stage covers what happens after the initial rendering from state change to rerendering when necessary. In this stage we have 4 methods:
        3. ` componentWillReceiveProps `  
        This method gets executed whenever the ` Component ` is about to receive new values for the ` props `. That may occur when you assign to the ` props ` of a ` Component ` a value from the ` state ` object of another ` Component ` and this other ` Component ` ` state ` changes. This method does not get executed in the initial rendering. It:
            * **accepts** ` nexProps `: which is the new ` props ` object.
            * **returns** nothing.
        4. ` shouldComponentUpdate `  
        This method seems like a question and it is. It gets executed whenever the ` state ` of the ` Component ` changes. It asks whether it should rerender due to this ` state ` change. It:
            * **accepts** ` nextProps `: which is the new props after the change, ` nextState `: which is the new state.
            * **returns** a ` boolean ` indicating whether it should rerender(` true `) or it should not(` false `).
        5. ` componentWillUpdate `  
        This method gets executed **right before rerendering is performed** only if ` shouldComponentUpdate ` method returns ` true `. It:
            * **accepts** ` nextProps `, and ` nextState `.
            * **returns** nothing.
        6. ` componentDidUpdate `  
        This method gets executed **right after rerendering is performed** only if ` shouldComponentUpdate ` method returns ` true `. It:
            * **accepts** ` prevProps `: which is the ` props ` object right before this rerendering occurred, and ` prevState `: which is the ` state ` object right before this rerendering occurred.
            * **returns** nothing.  
            [Hint: Invoking methods ` componentWillUpdate ` and ` componentDidUpdate ` does not mean that the DOM has been changed. It only means that the ` shouldComponentUpdate ` returns ` true ` and then **React** checked whether the DOM has to be updated or not].   
    3. **Finishing**  
    As the name suggests, this stage is all about finishing and removing the ` Component ` from the DOM. In this stage we have 1 method:
        7. ` componentWillUnmount `  
        This method gets executed **right after the ` Component ` is removed from the DOM**. It:
            * **accepts** nothing.
            * **returns** nothing.
