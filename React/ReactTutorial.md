# ReactJS


## What is React?
* `React is a JavaScript library` – one of the most popular ones, with over 100,000 stars on GitHub.
* `React is not a framework` (unlike Angular, which is more opinionated).
* React is an `open-source project` created by Facebook.
* React is used to `build user interfaces (UI) on the front end`.
* React is the `view layer of an MVC application` (Model View Controller)

## What can you do with it?
* Create `components`, which are like custom, reusable _HTML_ elements
* `Streamline` how `data` is stored and handled, using `state` and `props`

## Getting Started

### Online Playgrounds
If you’re interested in playing around with __React__. Try a __Hello World__ template on [CodePen](https://reactjs.org/redirect-to-codepen/hello-world) or [CodeSandbox](https://codesandbox.io/s/new).

### Your own text editor
You can also download [this HTML file](https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html)

### Add React to a Website
You can add React to an HTML page in one minute. You can then either gradually expand its presence, or keep it contained to a few dynamic widgets.


### Installing the application
1. `Add a DOM Container to the HTML.`
We gave this `<div>` a unique id HTML attribute. This will allow us to find it from the JavaScript code later and display a React component inside of it. `You can place a “container” <div> like this anywhere inside the <body> tag. You may have as many independent DOM containers on one page as you need. They are usually empty`

        <!-- ... existing HTML ... -->

        <div id="like_button_container"></div>

        <!-- ... existing HTML ... -->

1. `Add the Script Tags`:

        <!-- Load React. -->
        <!-- Note: when deploying, replace "development.js" with "production.min.js". -->
        <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
        <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>

        <!-- Load our React component. -->
        <script src="like_button.js"></script>
        
1. `Create a React Component`:

        const e = React.createElement;

        class LikeButton extends React.Component {
            constructor(props) {
                super(props);
                this.state = { liked: false };
            }

            render() {
                if (this.state.liked) {
                    return 'You liked this.';
                }

                return e(
                    'button',
                    { onClick: () => this.setState({ liked: true }) },
                    'Like'
                    );
                }
        }
        const domContainer = document.querySelector('#like_button_container');
        ReactDOM.render(e(LikeButton), domContainer);

1. `Try React with JSX`

        // Display a "Like" <button>
        return (
            <button onClick={() => this.setState({ liked: true })}>
                Like
            </button>
        );
                
The quickest way to try JSX in your project is to add this `<script>` tag to your page:

        <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

Now you can use JSX in any `<script>` tag by adding type="text/babel" attribute to it. Here is an example HTML file with JSX that you can download and play with.

This approach is `fine for learning and creating simple demos`. However, it makes your website slow and `isn’t suitable for production`.


### Add JSX to a Project
        npm init -y

if it fails [here’s a fix](https://gist.github.com/gaearon/246f6380610e262f8a648e3e51cad40d)

        npm install babel-cli@6 babel-preset-react-app@3


We’re using npm here only to install the JSX preprocessor; you won’t need it for anything else. Both React and the application code can stay as `<script>` tags with no changes.


### Run JSX Preprocessor
Create a folder called src and run this terminal command:

        npx babel --watch src --out-dir . --presets react-app/prod 

`npx — it’s a package runner tool that comes with npm 5.2+.`


If you now create a file called _src/like_button.js_ with this __JSX__ starter code, the watcher will create a preprocessed _like_button.js_ with the plain JavaScript code suitable for the browser. When you edit the source file with JSX, the transform will re-run automatically.

### Minimum setup

1. Create a new project folder

        mkdir new-react-app && cd new-react-app

1. Initialise a new node project (this will add a package.json)

        yarn init

1. Install react dependencies

        yarn add react react-dom react-hot-loader

1. Install dev dependencies like Babel to use ES2015 syntax and JSX, webpack etc

        yarn add -D webpack webpack-cli babel-loader @babel/preset-react @babel/core @babel/preset-env webpack-dev-server css-loader style-loader

1. Create a Babel configuration file .babelrc in the root project

        {
            "presets": [
                [
                    "@babel/preset-env",
                    {
                        "modules": false
                    }
                ],
                "@babel/preset-react"
            ],
            "plugins": [
                "react-hot-loader/babel"
            ]
        }

1. Create dist and src directories like this:
        
        src
            - components
                Hello.js
            - style
                main.css
            app.js
        dist
            index.html

1. Create a webpack.config.js and add this (for simple presets use [this](https://webpack.jakoblind.no/)):

        const webpack = require('webpack');
        const path = require('path');

        const config = {
            entry: './src/app.js',
            output: {
                path: path.resolve(__dirname, 'dist'),
                filename: 'bundle.js'
            },
            module: {
                rules: [
                    {
                        test: /\.(js|jsx)$/,
                        exclude: /node_modules/,
                        use: 'babel-loader'
                    },
                    {
                        test: /\.css$/,
                        use: [
                            'style-loader',
                            'css-loader'
                        ]
                    }
                ]
            },
            resolve: {
                extensions: [
                    '.js',
                    '.jsx'
                ]
            },
            devServer: {
                contentBase: './dist'
            }
        }

        module.exports = config;


1. Create a simple HelloWorld component in your components folder and add this to your HelloWorld.js file:

        import React from 'react';

        const HelloWorld = () => {
            return (
                <div className='hello-world'>
                <h1>Hello World</h1>
                <p>Welcome to my world</p>
                </div>
            )
        }

        export default HelloWorld;

1. Add this to your index.html

        <!DOCTYPE html>
        <html>
        <head>
            <title>Simplest React App Setup</title>
        </head>
        <body>
            <div id='app'></div>
            <script src='/bundle.js'></script>
        </body>
        </html>

1. Add this to your app.js (This should be in your root directory)

        import React from 'react';
        import ReactDOM from 'react-dom';
        import HelloWorld from './components/HelloWorld';
        import './style/main.css';

        ReactDOM.render(<HelloWorld />, document.getElementById('app'));

1. Add this "start": "webpack-dev-server --hot --mode development" to the script section of your package.json file. It should look like below:

        {
            "name": "step-1",
            "version": "1.0.0",
            "main": "index.js",
            "license": "MIT",
            "private": false,
            "scripts": {
                "build-dev": "webpack -d --mode development",
                "build-prod": "webpack -p --mode production",
                "start": "webpack-dev-server --hot --mode development"
            },
            "dependencies": {
                "react": "^16.5.2",
                "react-dom": "^16.5.2",
                "react-hot-loader": "^4.3.8"
            },
            "devDependencies": {
                "webpack": "^4.19.1",
                "webpack-cli": "^3.1.0",
                "babel-loader": "^8.0.2",
                "@babel/preset-react": "^7.0.0",
                "@babel/core": "^7.1.0",
                "@babel/preset-env": "^7.1.0",
                "webpack-dev-server": "^3.1.8",
                "css-loader": "^1.0.0",
                "style-loader": "^0.23.0"
            }
        }


1. Start the app

        yarn start

By now you should have your app running at http://localhost:8080/

### Create REACT app

Facebook has created Create React App, an environment that comes pre-configured with everything you need to build a React app. It will create a live development server, use Webpack to automatically compile React, JSX, and ES6, auto-prefix CSS files, and use ESLint to test and warn about mistakes in the code.

To set up create-react-app, run the following code in your terminal, one directory up from where you want the project to live. Make sure you have 5.2 or higher in Node.js.

    npx create-react-app react-tutorial

Once that finishes installing, move to the newly created directory and start the project.

    cd react-tutorial
    npm start

## Thinking in React

### 1. `Break The UI Into A Component Hierarchy`
* Draw boxes around every component (and subcomponent) in the mock and give them all names

### 2. `Build A Static Version in React`
* The easiest way is to build a version that takes your data model and renders the UI but has no interactivity.
* Build components that reuse other components and pass data using __props__. 
* __props__ are a way of passing data from parent to child.
* __don’t use state at all to build this static version__. State is reserved only for interactivity, that is, data that changes over time. Since this is a static version of the app, you don’t need it.

### 3. `Identify The Minimal (but complete) Representation Of UI State`
* Trigger changes to your underlying data model. React makes this easy with __state__.
* Which one is state. Simply ask three questions about each piece of data:

        Is it passed in from a parent via props? If so, it probably isn’t state.
        Does it remain unchanged over time? If so, it probably isn’t state.
        Can you compute it based on any other state or props in your component? If so, it isn’t state.

### 4. `Identify Where Your State Should Live`
* Identify which component mutates, or owns, this state.
* `React is all about one-way data flow down the component hierarchy`

        * Identify every component that renders something based on that state.
        * Find a common owner component (a single component above all the components that need the state in the hierarchy).
        * Either the common owner or another component higher up in the hierarchy should own the state.
        * If you can’t find a component where it makes sense to own the state, create a new component simply for holding the state and add it somewhere in the hierarchy above the common owner component.

### 5. `Add Inverse Data Flow`
* Pass callbacks to SearchBar that will fire whenever the state should be updated.
* Call setState(), and the app will be updated.

=================================================

## Build something
### What Are We Building?
In this tutorial, we’ll show how to build an interactive tic-tac-toe game with React.

You can see what we’ll be building here: [Final Result](https://codepen.io/gaearon/pen/gWWZgR?editors=0010).

Start with the simple React app setup.

1. We have the following components and structure:

        Game
            - Board
                - Square

1. In __components__ forder create file App1.js and paste:

        import React from 'react';

        class Square extends React.Component {
            render() {
                return (
                    <button className="square">
                        {/* TODO */}
                    </button>
                );
            }
        }

        class Board extends React.Component {
            renderSquare(i) {
                return <Square />;
            }

            render() {
                const status = 'Next player: X';

                return (
                    <div>
                        <div className="status">{status}</div>
                        <div className="board-row">
                            {this.renderSquare(0)}
                            {this.renderSquare(1)}
                            {this.renderSquare(2)}
                        </div>
                        <div className="board-row">
                            {this.renderSquare(3)}
                            {this.renderSquare(4)}
                            {this.renderSquare(5)}
                        </div>
                        <div className="board-row">
                            {this.renderSquare(6)}
                            {this.renderSquare(7)}
                            {this.renderSquare(8)}
                        </div>
                    </div>
                );
            }
        }

        class Game extends React.Component {
            render() {
                return (
                    <div className="game">
                        <div className="game-board">
                            <Board />
                        </div>
                        <div className="game-info">
                            <div>{/* status */}</div>
                            <ol>{/* TODO */}</ol>
                        </div>
                    </div>
                );
            }
        }

        export default Game;


1. Paste this in main.css:

        body {
            font: 14px "Century Gothic", Futura, sans-serif;
            margin: 20px;
        }
        ol, ul {
            padding-left: 30px;
        }
        .board-row:after {
            clear: both;
            content: "";
            display: table;
        }
        .status {
            margin-bottom: 10px;
        }
        .square {
            background: #fff;
            border: 1px solid #999;
            float: left;
            font-size: 24px;
            font-weight: bold;
            line-height: 34px;
            height: 34px;
            margin-right: -1px;
            margin-top: -1px;
            padding: 0;
            text-align: center;
            width: 34px;
        }
        .square:focus {
            outline: none;
        }
        .kbd-navigation .square:focus {
            background: #ddd;
        }
        .game {
            display: flex;
            flex-direction: row;
        }
        .game-info {
            margin-left: 20px;
        }

1. Import App2.js in app.js like this:

        import Game from './components/App2';
        import './style/main.css';

1. Passing Data Through __Props__

Pass data Board -> Square.

    class Board extends React.Component {
        renderSquare(i) {
            return <Square value={i} />;
        }

Change Square’s render method to show that value by replacing {/* TODO */} with {this.props.value}:

    class Square extends React.Component {
        render() {
            return (
                <button className="square">
                    {this.props.value}
                </button>
            );
        }
    }

6. Interact, show X on click - enter __State__

* `use __state__ to __“remember”__ things.`
* `set it in __constructor__`
* `it is __private__ to each component`
* `change value only by __this.setState()__`
* `changing any value from state -> __re-render__ (it and all it's children)`

We want Square to remember that is was clicked:

    class Square extends React.Component {
        constructor(props) {
            super(props);
            this.state = {
                value: null,
            };
        }

        render() {
            return (
                <button className="square" onClick={() => this.setState({value: 'X'})}>
                    {this.state.value}
                </button>
            );
        }
    }

### Completing the Game

We need to be able to put __"O__" and __"X"__ to determine a winner. The parent must know the value of each box.

7. Lifting State Up

`keep state in parent` - vs - `ask for it from children`
easy to implement and maintain - possible, but hard to maintain



    * collect data from multiple children
    * children communicate with each other
    ________________________________________
    => declare shared state in their parent
        -  parent component can pass the state back down to the children by using props
        -  keeps the child components in sync with each other and with the parent component.

Move state in Board:

    class Board extends React.Component {
        constructor(props) {
            super(props);
                this.state = {
                squares: Array(9).fill(null),
            };
        }

        renderSquare(i) {
            return <Square value={i} />;
        }

        render() {
            const status = 'Next player: X';

            return (
            <div>
                <div className="status">{status}</div>
                <div className="board-row">
                    {this.renderSquare(0)}
                    {this.renderSquare(1)}
                    {this.renderSquare(2)}
                </div>
                <div className="board-row">
                    {this.renderSquare(3)}
                    {this.renderSquare(4)}
                    {this.renderSquare(5)}
                </div>
                <div className="board-row">
                    {this.renderSquare(6)}
                    {this.renderSquare(7)}
                    {this.renderSquare(8)}
                </div>
            </div>
            );
        }
    }

When we fill the board in later, the board will look something like this:

        [
            'O', null, 'X',
            'X', 'X', 'O',
            'O', null, null,
        ]

__Square__ need to tell __Board__ what the new state is, but since state is private, it can't change it from Square => pass handler to __Square__

    renderSquare(i) {
        return (
            <Square
                value={this.state.squares[i]}
                onClick={() => this.handleClick(i)}
            />
        );
    }


* The __onClick__ prop on the built-in DOM `<button>` component tells React to set up a click event listener.
* When the button is clicked, React will call the __onClick__ event handler that is defined in Square’s __render()__ method.
* This event handler calls __this.props.onClick()__. The Square’s __onClick__ prop was specified by the Board.
* Since the Board passed __onClick={() => this.handleClick(i)}__ to Square, the Square calls __this.handleClick(i)__ when clicked.

Define __handleClick()__:

        class Board extends React.Component {
            constructor(props) {
                super(props);
                this.state = {
                    squares: Array(9).fill(null),
                };
            }

            handleClick(i) {
                const squares = this.state.squares.slice();
                squares[i] = 'X';
                this.setState({squares: squares});
            }

            renderSquare(i) {
                return (
                <Square
                    value={this.state.squares[i]}
                    onClick={() => this.handleClick(i)}
                />
                );
            }

            render() {
                const status = 'Next player: X';

                return (
                <div>
                    <div className="status">{status}</div>
                    <div className="board-row">
                        {this.renderSquare(0)}
                        {this.renderSquare(1)}
                        {this.renderSquare(2)}
                    </div>
                    <div className="board-row">
                        {this.renderSquare(3)}
                        {this.renderSquare(4)}
                        {this.renderSquare(5)}
                    </div>
                    <div className="board-row">
                        {this.renderSquare(6)}
                        {this.renderSquare(7)}
                        {this.renderSquare(8)}
                    </div>
                </div>
                );
            }
        }

`Note how in handleClick, we call .slice() to create a copy of the squares array to modify instead of modifying the existing array.`

### Why Immutability?

Data Change with Mutation

    var player = {score: 1, name: 'Jeff'};
    player.score = 2;
    // Now player is {score: 2, name: 'Jeff'}

Data Change without Mutation

    var player = {score: 1, name: 'Jeff'};

    var newPlayer = Object.assign({}, player, {score: 2});
    // Now player is unchanged, but newPlayer is {score: 2, name: 'Jeff'}

    // Or if you are using object spread syntax proposal, you can write:
    // var newPlayer = {...player, score: 2};

Benefits:

* Complex Features Become Simple 
    - ex. __undo__ and __redo__

* Detecting Changes
    - mutable: dufficult because it is the same object sa it has to be parsed
    - imutable: easy because it is a new object

* Determining When to Re-render in React
    - based on change determining it cand be easy to know when to re-render

You can learn more about shouldComponentUpdate() and how you can build pure components by reading [Optimizing Performance](https://reactjs.org/docs/optimizing-performance.html#examples).

### Functional Components

* __Simpler__ way to write components
* Only contain a __render__ method
* Don’t have their __own state__.
* will be __remade on each render__.

Replace the Square class with this function:

        function Square(props) {
            return (
                <button className="square" onClick={props.onClick}>
                    {props.value}
                </button>
            );
        }

We have changed `this.props` to `props` both times it appears.
In a class, we used an arrow function to access the correct `this` value, but in a functional component we don’t need to worry about `this`.

### Taking Turns

8. Add the __"O"__

        class Board extends React.Component {
            constructor(props) {
                super(props);
                this.state = {
                    squares: Array(9).fill(null),
                    xIsNext: true,
                };
            }

Each time the player moves, __xIsNext__ is toggled

        handleClick(i) {
            const squares = this.state.squares.slice();
            squares[i] = this.state.xIsNext ? 'X' : 'O';
            this.setState({
                squares: squares,
                xIsNext: !this.state.xIsNext,
            });
        }

Set 'X' or 'O'

        render() {
            const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

Finally __Board__ should look like this:

        class Board extends React.Component {
            constructor(props) {
                super(props);
                this.state = {
                    squares: Array(9).fill(null),
                    xIsNext: true,
                };
            }

            handleClick(i) {
                const squares = this.state.squares.slice();
                squares[i] = this.state.xIsNext ? 'X' : 'O';
                this.setState({
                    squares: squares,
                    xIsNext: !this.state.xIsNext,
                });
            }

            renderSquare(i) {
                return (
                <Square
                    value={this.state.squares[i]}
                    onClick={() => this.handleClick(i)}
                />
                );
            }

            render() {
                const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

                return (
                    <div>
                        <div className="status">{status}</div>
                        <div className="board-row">
                            {this.renderSquare(0)}
                            {this.renderSquare(1)}
                            {this.renderSquare(2)}
                        </div>
                        <div className="board-row">
                            {this.renderSquare(3)}
                            {this.renderSquare(4)}
                            {this.renderSquare(5)}
                        </div>
                        <div className="board-row">
                            {this.renderSquare(6)}
                            {this.renderSquare(7)}
                            {this.renderSquare(8)}
                        </div>
                    </div>
                );
            }
        }

### Declaring a Winner

9. Add this helper function and calculate in Boards render if player has won

        function calculateWinner(squares) {
            const lines = [
                [0, 1, 2],
                [3, 4, 5],
                [6, 7, 8],
                [0, 3, 6],
                [1, 4, 7],
                [2, 5, 8],
                [0, 4, 8],
                [2, 4, 6],
            ];
            for (let i = 0; i < lines.length; i++) {
                const [a, b, c] = lines[i];
                if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
                    return squares[a];
                }
            }
            return null;
        }

We’ll replace the status declaration in Board’s render function with this code:

    render() {
        const winner = calculateWinner(this.state.squares);
        let status;
        if (winner) {
            status = 'Winner: ' + winner;
        } else {
            status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
        }

        return (
        // the rest has not changed
        ......


10. Change the Board’s handleClick function to return early by ignoring a click if someone has won the game or if a Square is already filled:

    handleClick(i) {
        const squares = this.state.squares.slice();
        if (calculateWinner(squares) || squares[i]) {
            return;
        }
        squares[i] = this.state.xIsNext ? 'X' : 'O';
        this.setState({
            squares: squares,
            xIsNext: !this.state.xIsNext,
        });
    }

### Adding Time Travel

11. Storing a History of Moves

We’ll store the past squares arrays in another array called history.

    history = [
        // Before first move
        {
            squares: [
            null, null, null,
            null, null, null,
            null, null, null,
            ]
        },
        // After first move
        {
            squares: [
            null, null, null,
            null, 'X', null,
            null, null, null,
            ]
        },
        // After second move
        {
            squares: [
            null, null, null,
            null, 'X', null,
            null, null, 'O',
            ]
        },
        // ...
    ]

12. Lifting State Up, Again

__Board__ keeps all values of __Boxes__, but now we need to keep all values of the __Board__.
So we place the `history` in __Game__.

    class Game extends React.Component {
        constructor(props) {
            super(props);
            this.state = {
            history: [{
                squares: Array(9).fill(null),
            }],
            xIsNext: true,
            };
        }

        render() {
            return (
            <div className="game">
                <div className="game-board">
                <Board />
                </div>
                <div className="game-info">
                <div>{/* status */}</div>
                <ol>{/* TODO */}</ol>
                </div>
            </div>
            );
        }
    }

* Delete the constructor in Board.
* Replace this.state.squares[i] with this.props.squares[i] in Board’s renderSquare.
* Replace this.handleClick(i) with this.props.onClick(i) in Board’s renderSquare.

        class Board extends React.Component {
            handleClick(i) {
                const squares = this.state.squares.slice();
                if (calculateWinner(squares) || squares[i]) {
                    return;
                }
                squares[i] = this.state.xIsNext ? 'X' : 'O';
                this.setState({
                    squares: squares,
                    xIsNext: !this.state.xIsNext,
                });
            }

            renderSquare(i) {
                return (
                <Square
                    value={this.props.squares[i]}
                    onClick={() => this.props.onClick(i)}
                />
                );
            }

            render() {
                const winner = calculateWinner(this.state.squares);
                let status;
                
                if (winner) {
                    status = 'Winner: ' + winner;
                } else {
                    status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
                }

                return (
                    <div>
                        <div className="status">{status}</div>
                        <div className="board-row">
                            {this.renderSquare(0)}
                            {this.renderSquare(1)}
                            {this.renderSquare(2)}
                        </div>
                        <div className="board-row">
                            {this.renderSquare(3)}
                            {this.renderSquare(4)}
                            {this.renderSquare(5)}
                        </div>
                        <div className="board-row">
                            {this.renderSquare(6)}
                            {this.renderSquare(7)}
                            {this.renderSquare(8)}
                        </div>
                    </div>
                );
            }
        }

We’ll update the __Game__ component’s __render__ function to use the most recent history entry to determine and display the game’s status:

    render() {
        const history = this.state.history;
        const current = history[history.length - 1];
        const winner = calculateWinner(current.squares);

        let status;
        if (winner) {
            status = 'Winner: ' + winner;
        } else {
            status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
        }

        return (
            <div className="game">
                <div className="game-board">
                
                <Board
                    squares={current.squares}
                    onClick={(i) => this.handleClick(i)}
                />

                </div>
                <div className="game-info">
                
            <div>{status}</div>
                <ol>{/* TODO */}</ol>
                </div>
            </div>
        );
    }

Since the Game component is now rendering the game’s status, we can remove the corresponding code from the __Board’s__ __render__ method. After refactoring, the Board’s render function looks like this:

    render() {
        return (
            <div>
                <div className="board-row">
                    {this.renderSquare(0)}
                    {this.renderSquare(1)}
                    {this.renderSquare(2)}
                </div>
                <div className="board-row">
                    {this.renderSquare(3)}
                    {this.renderSquare(4)}
                    {this.renderSquare(5)}
                </div>
                <div className="board-row">
                    {this.renderSquare(6)}
                    {this.renderSquare(7)}
                    {this.renderSquare(8)}
                </div>
            </div>
        );
    }

Finally, we need to move the handleClick method from the Board component to the Game component. We also need to modify handleClick because the Game component’s state is structured differently. Within the Game’s handleClick method, we concatenate new history entries onto history.

    handleClick(i) {
        const history = this.state.history;
        const current = history[history.length - 1];
        const squares = current.squares.slice();
        if (calculateWinner(squares) || squares[i]) {
            return;
        }
        squares[i] = this.state.xIsNext ? 'X' : 'O';
        this.setState({
            history: history.concat([{
                squares: squares,
            }]),
            xIsNext: !this.state.xIsNext,
        });
    }

`Unlike the array push() method you might be more familiar with, the concat() method doesn’t mutate the original array, so we prefer it.`

We learned earlier that React elements are first-class JavaScript objects; we can pass them around in our applications. To render multiple items in React, we can use an array of React elements.

In JavaScript, arrays have a `map()` method that is commonly used for mapping data to other data, for example:

    const numbers = [1, 2, 3];
    const doubled = numbers.map(x => x * 2); // [2, 4, 6]

Using the map method, we can `map` our `history` of moves to React elements representing buttons on the screen, and display a list of buttons to `“jump”` to past moves.

Let’s `map` over the `history` in the Game’s render method:

    render() {
        const history = this.state.history;
        const current = history[history.length - 1];
        const winner = calculateWinner(current.squares);

        const moves = history.map((step, move) => {
            const desc = move ?
                'Go to move #' + move :
                'Go to game start';
            return (
                <li>
                    <button onClick={() => this.jumpTo(move)}>{desc}</button>
                </li>
            );
        });

        let status;
        if (winner) {
            status = 'Winner: ' + winner;
        } else {
            status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
        }

        return (
            <div className="game">
                <div className="game-board">
                <Board
                    squares={current.squares}
                    onClick={(i) => this.handleClick(i)}
                />
                </div>
                <div className="game-info">
                <div>{status}</div>
                
                <ol>{moves}</ol>
                </div>
            </div>
        );
    }

For each move in the tic-tac-toes’s game’s history, we create a list item `<li>` which contains a button `<button>`. The button has a onClick handler which calls a method called `this.jumpTo()`. We haven’t implemented the `jumpTo()` method yet. For now, we should see a list of the moves that have occurred in the game and a warning in the developer tools console that says:

`Warning: Each child in an array or iterator should have a unique “key” prop. Check the render method of “Game”.`

Picking a Key
When we render a list, React stores some information about each rendered list item. When we update a list, React needs to determine what has changed. We could have added, removed, re-arranged, or updated the list’s items.

Imagine transitioning from

    <li>Alexa: 7 tasks left</li>
    <li>Ben: 5 tasks left</li>

to

    <li>Ben: 9 tasks left</li>
    <li>Claudia: 8 tasks left</li>
    <li>Alexa: 5 tasks left</li>

From our perspective, our transition swapped Alexa and Ben’s ordering and inserted Claudia between Alexa and Ben. However, React is a computer program and does not know what we intended. Because React cannot know our intentions, we need to specify a key property for each list item to differentiate each list item from its siblings. The strings alexa, ben, claudia may be used as keys. If we had access to a database, Alexa, Ben, and Claudia’s database IDs could be used as keys.

    <li key={user.id}>{user.name}: {user.taskCount} tasks left</li>

key is a special and reserved property in React (along with ref, a more advanced feature). When an element is created, React extracts the key property and stores the key directly on the returned element. Even though key may look like it belongs in props, key cannot be referenced using this.props.key. React automatically uses key to decide which components to update. A component cannot inquire about its key.

When a list is re-rendered, React takes each list item’s key and searches the previous list’s items for a matching key. If the current list has a key that does not exist in the previous list, React creates a component. If the current list is missing a key that exists in the previous list, React destroys a component. Keys tell React about the identity of each component which allows React to maintain state between re-renders. If a component’s key changes, the component will be destroyed and re-created with a new state.

It’s strongly recommended that you assign proper keys whenever you build dynamic lists. If you don’t have an appropriate key, you may want to consider restructuring your data so that you do.

If no key is specified, React will present a warning and use the array index as a key by default. Using the array index as a key is problematic when trying to re-order a list’s items or inserting/removing list items. Explicitly passing key={i} silences the warning but has the same problems as array indices and is not recommended in most cases.

Keys do not need to be globally unique. Keys only needs to be unique between components and their siblings.

Implementing Time Travel
In the tic-tac-toe game’s history, each past move has a unique ID associated with it: it’s the sequential number of the move. The moves are never re-ordered, deleted, or inserted in the middle, so it’s safe to use the move index as a key.

In the Game component’s render method, we can add the key as `<li key={move}>` and React’s warning about keys should disappear:

    const moves = history.map((step, move) => {
        const desc = move ?
            'Go to move #' + move :
            'Go to game start';
        return (
            <li key={move}>
                
            <button onClick={() => this.jumpTo(move)}>{desc}</button>
                </li>
            );
    });

Clicking any of the list item’s buttons throws an error because the jumpTo method is undefined. Before we implement jumpTo, we’ll add stepNumber to the Game component’s state to indicate which step we’re currently viewing.

First, add stepNumber: 0 to the initial state in Game’s constructor:

    class Game extends React.Component {
        constructor(props) {
            super(props);
            this.state = {
                history: [{
                    squares: Array(9).fill(null),
                }],
                stepNumber: 0,
                xIsNext: true,
            };
        }

Next, we’ll define the jumpTo method in Game to update that stepNumber. We also set xIsNext to true if the number that we’re changing stepNumber to is even:

    handleClick(i) {
        // this method has not changed
    }

    jumpTo(step) {
        this.setState({
        stepNumber: step,
        xIsNext: (step % 2) === 0,
        });
    }

    render() {
        // this method has not changed
    }

We will now make a few changes to the Game’s handleClick method which fires when you click on a square.

The stepNumber state we’ve added reflects the move displayed to the user now. After we make a new move, we need to update stepNumber by adding stepNumber: history.length as part of the this.setState argument. This ensures we don’t get stuck showing the same move after a new one has been made.

We will also replace reading this.state.history with this.state.history.slice(0, this.state.stepNumber + 1). This ensures that if we “go back in time” and then make a new move from that point, we throw away all the “future” history that would now become incorrect.

    handleClick(i) {
        const history = this.state.history.slice(0, this.state.stepNumber + 1);
        const current = history[history.length - 1];
        const squares = current.squares.slice();
        if (calculateWinner(squares) || squares[i]) {
            return;
        }
        squares[i] = this.state.xIsNext ? 'X' : 'O';
        this.setState({
            history: history.concat([{
                squares: squares
            }]),
            stepNumber: history.length,
            xIsNext: !this.state.xIsNext,
        });
    }

Finally, we will modify the Game component’s render method from always rendering the last move to rendering the currently selected move according to stepNumber:

  render() {
    const history = this.state.history;
    const current = history[this.state.stepNumber];
    const winner = calculateWinner(current.squares);

    // the rest has not changed