# Setup Workspace with Webpack
* Let's setup our workspace step by step: [Note: If anything is not mentioned how it can be done so you can find that in either **chapter 2** of the course **Up and running with ECMAScript 6** or **chapter 11** of the course **JavaScript Essential training** or **chapter 1** of the course **Learning functional programming with JavaScript**]
    1. Navigate to where you want to setup a **React** workspace and start a **React** project. Use ` mkdir ` make directory command to create a new directory and ` cd ` change directory command to navigate to a child directory.
    2. Make sure that **Node.js** and **NPM** are installed.
    3. Initiate **npm** and provide some info about your project to create your ` package.json ` file.
    4. We need 2 libraries: the **React core** library and the one responsible for **rendering the DOM**. Since these libraries are needed for our application to run in production they are called **production dependencies**. To install them hit ` npm install react react-dom --save `. ` --save ` means that they are production dependencies.
    5. Of-course We won't write all of our code in a single file instead we will write **modular code** distributed over multiple files. For that reason we need a tool to **load** all of these files and **bundle** them together for the browser. Once I said **load**, certainly **Webpack** tool came to your head. We used this tool in the course **Up and Running with ECMAScript 6** chapter 2(Transpiling ES6) to automate the process of transpiling ES6 code. If you can remember **Webpack** is a tool used to load all your assets, bundle them together and possibly make some transformations on your assets(such as transpiling) by loading the plugins you need in **Webpack** to do these transformations. Since **Webpack** is needed only in development to bundle and prepare files for deployments it is a **development dependency**. To install it hit ` npm install webpack --save-dev `. ` --save-dev ` means that it is a development dependency.
    6. However we are working in front-end development, we need a server to run our application because we are not working with normal HTML files(the reason is not yet clear for me). To install it hit ` npm install webpack-dev-server --save-dev `  
    It seems that we have two ways of rendering **React components**:
        * **Client-side rendering**    
        Here the browser downloads a minimal HTML page and it renders the **React** components to fill the content.
        * **Server-side rendering**  
        Here the server renders the entire HTML file from **React** components and the browser downloads this ready file.
        * Reference: https://medium.freecodecamp.org/server-side-rendering-your-react-app-in-three-simple-steps-7a82b95db82e.
    7. We need to install **Babel** for transpiling. To install it hit ` npm install babel-loader @babel/core @babel/preset-react @babel/preset-env --save-dev `.
    8. Create a folder in the project where you will put your code which will be accessed by Webpack and bundled. You can name it **src** for example.
    9. In the **src** folder create a file named **index.html** which will be the entry point of your application and populate it with an HTML5 file skeleton.
    10. In the **src** folder create another folder named **app** for example to hold your **react** app.
    11. In the root folder of your application create a file named **webpack.config.js** which we created before in chapter 2 of the course **Up and running with ECMAScript 6**. This file will tells **Webpack** what it should do in our project. Populate the file with these configurations:
    ```
    var webpack = require( "webpack" );
    var path = require( "path" );  // A node.js library to resolve the path of my application

    var DIST_DIR = path.resolve( __dirname, "dist" );  // distribution directory where to distribute weback output
    var SRC_DIR = path.resolve( __dirname, "src" );  // Source directory where to get webpack input

    var config = {  // config object holds configurations of webpack in our project
        mode: "development",  // Current mode: development or production or none
        entry: SRC_DIR + "/app/index.js",  // webpack entry point(where webpack starts its job)
        output: {  // where webpack should output everything
            path: DIST_DIR + "/app",
            filename: "bundle.js",
            publicPath: "/app/" // for webpack development server
        },
        module: {  // modules used like transpiling
            rules: [
                {
                    test: /\.js?/,  // which kind of files this loader work with
                    include: SRC_DIR,  // where to find these files
                    loader: "babel-loader",  // what kind of loader
                    query: {
                        presets: ["@babel/react", "@babel/env"]
                    }
                }
            ]
        }  
    };

    module.exports = config; // export the config object
    ```
    12. Create a file called **index.js** in the **/src/app/** folder and populate it with any script for testing.
    13. Reference the output of Webpack in **index.html** body.
    ```
    <script src="/app/bundle.js"></script>
    ```
    This HTML file will be copied into the ` DIST_DIR ` soon and ` bundle.js ` will be in the ` DIST_DIR ` also but under a nested directory ` dist/app `.
    14. Store a script in **package.json** file in **scripts** object which you will use to run you app.
    ```
    "scripts": {
      "start": "npm run build",
      "build": "webpack -d && cp src/index.html dist/index.html && webpack-dev-server --content-base src/ --inline --hot",  // -d means development mode
      "build:prod": "webpack -p && cp src/index.html dist/index.html"  // -p means production mode
    }
    ```
    Here we copied the HTML file in  the ` DIST_DIR `.
    15. Now in the command window run ` npm start ` and everything should work.
* Note: I had a big and silly bug which is solved in this [issue](https://github.com/babel/babel-loader/issues/540). The problems were:
    * to replace preset **es2015** with peset **env**.
    * to remove preset **stage-2**.
    * to install presets and babel core using ` npm install @babel/core `, ` npm install @babel/preset-react `, ` npm install @babel/preset-env ` not using ` npm install babel-core `, etc.
    *  to add to config object: ` mode: development `.


# Setup Git
* As we know we initiate a git repository using ` git init `.
* We also create a file named **.gitignore** which contains files that we do not want Git to keep track of. To include a folder in **.gitignore** file precede its name with ` / `.
```
/dist
/node_modules
/npm-debug.log
```
* To add to staging area all the files in the project except those that are in **.gitignore** file hit ` git add . `
