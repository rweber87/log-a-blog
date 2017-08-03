---
layout: post
title:  "React-ing with tic-tac-toe"
date:   2017-05-24 15:30:04 -0400
categories: React-ing with tic-tac-toe
---

The game tic-tac-toe can be traced back to ancient egyptian civilizations. It's only fitting that we take such an ancient tradition and rebuild it utilizing some of the most modern front end web frameworks known to developers, or React. Let's start off by creating our own directory and building a fresh new application.

Build a fresh new application by running these commands:

```javascript
npm install -g create-react-app
create-react-app my-app

cd my-app
npm start
```

I was having difficulty running the intial `npm install...` because it was requiring an admin to do so. The work around is to run it as `sudo npm install -g create-react-app`. At this point you should be able to use your shortcut to open up the directory in your preferred text editor. I'll be using sublime 3 but any should suffice. Now run `npm start` to start your server and open your browser to the URL `http://localhost:3000`.

Next, replace all of the existing code in your already populated index.css file with the code below.

```javascript
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
```

Replace all of the code in your index.js file with the code below with the exception of the the first 5 lines you're importing from other directories/libraries.

```javascript
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

// ========================================

ReactDOM.render(
  <Game />,
  document.getElementById('root')
);
```
You should now be able to view in the browser a board that looks something like this.

![tictactoeFirst](https://rweber87.github.io/log-a-blog/assets/post4/tictactoeFirst.png)

It's a bit plain and there's not much to interact with. Let's change that up and bring some of our components to life. Each of our components can take in props or 'properties' as a way to pass data from one part of our application to the next. We'll start by passing some informatin from our Board class down to our Square component. 

Change the Board render method by passing along a `value` prop to the Square component. After that we're going to chang our Square's render method to reflect the new property it's receiving. Each method should look as such

Board 
```javascript
class Board extends React.Component {
  renderSquare(i) {
     return <Square value={i} />;
  } ...
```

Square Render method
```javascript
	render() {
	    return (
	      <button className="square">
	        {this.props.value}
	      </button>
	    );
	  }
```

Our board should now look something like this:

![tictactoeSecond](https://rweber87.github.io/log-a-blog/assets/post4/tictactoeSecond.png)

The reason why each Square is numbered is because of our render method inside of our Board class. Here we created three nested `<div>`s inside of one larger `<div>` with three squares per `<div>`. Each square is numbered via the `renderSquare` method defined in our Board class that creates a new Square component with a new property of a number passed in by the board.

```javascript
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
```
Again, there's nothing too exciting about our application just yet so let's add more to spice things up! We'll add some functionality now and change the square to render an 'X' once it's been selected by the user. Update our Square component to maintain it's own state via the constructor method return a `<button>` that has a property onClick that's set to a function. This function will be what changes the state of an individual square to be 'X' when it's been clicked.

```javascript
class Square extends React.Component {
  constructor() {
    super();
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
```
The limitations we face by having a square control it's own state is the inability to alternate between players and determining who wins the game. Let's refactor this a bit to have the Board class handle this functionality now. Add a constructor method that controls the state of the Board by setting an array of length 9 to an array of null values.

```javascript
 constructor() {
    super();
    this.state = {
      squares: Array(9).fill(null),
    };
  }
```

Modify a the `renderSquare` method so a square receives a prop value and an `onClick` method that we'll define in just a second.

```javascript
  renderSquare(i) {
    return <Square value={this.state.squares[i]} onClick={() => this.handleClick(i)} />;
  }
```

With our board handling the state and passing some logic down to a square we can modify our square code to look something like this.

```javascript
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={() => this.props.onClick()}>
        {this.props.value}
      </button>
    );
  }
}
```

Our square is accepting properties being pass from our Board. Because these are properties passed from a parent class via the props we can call `this.props` then whatever we're gaining access to i.e. the value from the renderSquare method on the board or the onClick method from the prop onClick in the render square method (see code above for a point of reference).

Now let's go ahead and define that handleClick method in our Board class that changes the square based on who's turn it is as well as maintaining that person's turn in the state of our Board.

```javascript
  constructor() {
    super();
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
```

Now we're getting somewhere! You're grid should now be able to alternate between 'X' and 'O' with ease! 

![tictactoeThird](https://rweber87.github.io/log-a-blog/assets/post4/tictactoeThird.png)

Let's tell the user who's turn it is by rendering out that detail in the `render()` function of our Board class.

```javascript
render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    ...
```

The last thing we'll do is determine who the winner is. Here let's build a function that gets called whenever the board is rendered.

```javascript
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
```

Here we have an array of all combinations possible to obtain a win. Because our `handleClick()` method updates the state of the Board by changing the Square that's been selected with who's turn it was (i.e. 'X' or 'O') we're able to iterate over that each time to see if three spaces equal each other. All that's left is to check if someone has won when the Board is rendered. Replace the status in the Board's render method with the below conditional.

```javascript
render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }
```

Let's also prevent the user from clicking if a winner has been determined. Add this code to our `handClick()` function as a conditional to stop the game.

```javascript
if (calculateWinner(squares) || squares[i]) {
      return;
    }
```

Voila! A working tic tac toe game using React!

![tictactoeFourth](https://rweber87.github.io/log-a-blog/assets/post4/tictactoeFourth.png)

Finished code with some additional functionality can be found on my github account here [React Tic Tac Toe](https://github.com/rweber87/reactTicTacToe)

All credit to the React team for creating such an easy to follow instructional for this tutorial.

[React](https://facebook.github.io/react/tutorial/tutorial.html)

Questions or comments? Feel free to shoot me an email (click the link below).

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->