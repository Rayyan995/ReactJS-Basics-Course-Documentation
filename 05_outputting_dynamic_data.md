# Outputting Dynamic Data
* Since **JSX** is simply *JavaScript code* even if it seems *XML-like*, we can output dynamic data in the **JSX** simply by wrapping this data in *curly braces* **{}**.
* This dynamic data can be any *logic* such as mathematical calculation or a variable and more. However we are *restricted* to embed a single line of code not more inside those curly braces.
* So what we can do if our logic is multi-line? Simply we can do that logic within the ` render ` method before we return a **JSX** and prepare a variable to be outputted in the **JSX**.
* Based on that let's see some examples that work and some that do not: [Since all of our work will exist in ` AppComponent ` class inside the ` render ` method, we will write this portion only]
    * **Literals or values**
    ```
    render() {
        return {
            <h1>{ "Hello" }</h1>
        };
    }
    ```
    Works.
    * **Mathematical calculation**
    ```
    render() {
        return {
            <h1>Square root of 25 = { Math.sqrt(25) }</h1>
        };
    }
    ```
    Works.
    * **Logic**
    ```
    render() {
        let x = 5;
        return (
            <h1>{ if( x > 0 ) { "x is positive" } }</h1>
        );
    }
    ```
    Does not work(multi-line). Solutions:
        * Put the logic outside the returning object and prepare the content.
        ```
        render() {
            let x = 5;
            let content = "";
            if( x > 0 ) {
                content = "x is positive";
            } else {
                content = "x is negative";
            }
            return (
                <h1>{ content }</h1>
            );
        }
        ```
        * Use ternary operator.
        ```
        render() {
            let x = 5;
            return (
                <h1>{ (x > 0)? "x is positive": "x is negative" } }</h1>
            );
        }
        ```
