# React Intro Checkpoint

## React

### Question #1

Edit the snippet below so that two properties – `title` and `author` – are passed down into the `App` component as props. The values that are passed down can be of your choosing.

```js
import React from "react"
import ReactDOM from "react-dom"

ReactDOM.render(
  <App
  title= {'React App'}
  author={'Cleen'}
  />,
  document.getElementById('root')
);
```

### Question #2

Edit the snippet below so that the passed-in properties from the previous question –  `title` and `author` – are rendered in the `App` component's UI.

```js
import React, { Component } from "react"

class App extends Component {
  render () {
    return (
      <div>
        <h1>Welcome to {this.props.title}</h1>
        <footer>This site is designed by {this.props.author}</footer>
      </div>
    )
  }
}

export default App
```

### Question #3

Assume we have defined a component named `Post` that is located in `/js/components/Post.js`. Edit the below code snippet to import the `Post` component and render it as a child within the `Main` UI. `Main` is located in `/js/components/Main.js`.

```js
import React, { Component } from "react"
import Comments from "../Comments"
import Post from "./Post"

class Main extends Component {
  render () {
    return (
      <div>
        <Comments />
        <Post />
      </div>
    )
  }
}

export default Main
```

### Question #4

`Products` receives a prop called `listings`, which contains an array of objects. Each object in `listings` contains a key for `name` (string) and `price` (number). Edit the below code snippet to render a list of `Comment` components that take `name` and `price` as props.
<!-- def know Im not reading this right, first though just listing items, the Comment portion confused me that it has the jsx to render the items in that component. soo here we are -->

```js
import React, { Component } from "react"
import Products from "../Products"
import Comment from "../Comment"

class Products extends Component {
  render () {
    let comments = this.props.comments.map( (name, price, index) => {
      return <Comment name = {name} price={price} key = {index}/>
      // return (
      //   <div key = {index}>
      //     <p>{comment.name}</p>
      //     <p>{comment.price}</p>
      //   </div>
      // )
    })  
    return (
      <div>
        {comments}
      </div>
    )
  }
}

export default Products
```

### Question #5

In the code snippet below we want text entered into the input field to be displayed inside the `<p>`. Do the following things...
- Define a property `message` in the `state` of the `App` component
- Make it so that whenever the form's input is modified, `message` in `state` is updated accordingly

> Hint: `onChange`


```js
import React, { Component } from "react"

class App extends Component {
  constructor (props) {
    super()
    this.state = {
      message: props.message
    }
    this.handleTextInput = this.handleSearchInput.bind(this)
  }
    handleTextInput(e) {
    this.setState({
      message: e.target.value
    })
  }
  render() {
    return (
      <div>
        <form>
          <label>Input: </label>
          <input type="text" onChange={this.props.handleTextInput}/>
        </form>
        <p>Message: { this.state.message }</p>
      </div>
    );
  }
}

export default App
```

## React-Router

### Question #6

You are in your terminal, inside of an existing React application. Enter the command(s) needed to add `React Router` to the current app.

```bash
# your command(s) here
npm install --save react-router-dom
```

### Question #7

Edit the following code snippet. Add the `<Router>` provider component, and rewrite the rest of this snippet to incorporate `<Link/>`s and matching `<Route/>`s. Each `<Route/>` will render a component at a `path` matching its `<Link/>`'s `to` prop (without spaces).

```js
// Assume all necessary components are imported above

class App extends Component {
  render () {
    return (
      <Router>
        <div>
          <h1>Welcome to My shopping site</h1>
          <nav>
            <Link to="/">Home</Link>
            <Link to="/products">Products</Link>
            <Link to="/cart">Shopping Cart</Link>
          </nav>
          <main>
            <Route exact path ="/"
                component={Home}
              />
            <Route path ="/products"
                component={Products}
              />
            <Route path ="/cart"
                component={ShoppingCart}
              />  
          </main>
          <footer>This site is designed by us</footer>
        </div>
      </Router>
    )
  }
}

export default App
```

### Question #8

Edit the code snippet below so that once the `App` component has loaded, a GET request is made to 'http://api.example.com/info'. Display the results of that request in the provided `<div>`.

> You can use the API tool of your choice to answer this question.

```js
// Assume all necessary components are imported above

class App extends Component {
  // Assume the constructor is complete
  componentDidMount () {
    axios.get('http://api.example.com/info')
    .then((response) => {
      console.log(response)
      this.setState({
        results: response.data
      })
    })
    .catch((err) => {
       console.log(err)
     })
}


  render () {
    return (
      <div>
        <h1>Results</h1>
        <div>{ this.state.results }</div>
      </div>
    )
  }
}

export default App
```
