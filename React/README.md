# apollographql
## Part 1: [Setup](https://mrinalbd.com/setup-for-react-front-end/)

#### :point_right: First clone the graphql in your plugin folder from https://github.com/wp-graphql/wp-graphql

#### :point_right: After activate the plugin, visit http://localhost/wordpress/?graphql

#### :point_right: If it show a page of error, then confirmed wp-graphql plugin works.

#### :point_right: Let's create a brand new react app by the command;
`npx create-react-app apollographql`
> Note: npx is a npm package runner. The typical use is to download and run a package temporarily or for trials.

#### :point_right: Go to project folder and start this app
`cd apollographql && npm start`

#### :point_right: We need to install three packages to use graphQL in React. Apollo makes possible to write a query in graphQL.
1. https://www.npmjs.com/package/apollo-boost
2. https://www.npmjs.com/package/react-apollo
3. https://www.npmjs.com/package/graphql

**Also we need more cuple of think,**
+ https://milligram.io/ for quick style
+ https://www.styled-components.com/ styling components
+ https://reacttraining.com/react-router/web/guides/quick-start for pagination system
+ https://github.com/cure53/DOMPurify for safe DOM rander in React app

#### :point_right: Install these packages with the command -
`npm i apollo-boost react-apollo graphql react-router-dom milligram styled-components dompurify`
> Note: By default, these packages install for development only. Here, `i` is the shorthand for `install` command. 

#### :point_right: We will create some components. These are:
- [ ] AppRouter
- [ ] App
- [ ] Posts
- [ ] PostWidget
- [ ] Post
- [ ] NotFound

#### :point_right: First, create a file in `/src` named `AppRouter.js`. Be sure about the naming convention. React follow camel casing for both filename and class name.
**Open `src/AppRouter.js`. We know, for every react component we have to import React from react package. For the first sight, we will define AppRouter in this file.**

```JS
import React from "react";
class AppRouter extends React.Component {
  render() {
    return <div>Router</div>;
  }
}
export default AppRouter;
```

#### :point_right: Open src/index.js, it application start. 
- Remove **index.css** and **App.js** in App importer.
- Also delete the **src/App.js** file
- At last, use **AppRouter** in **ReactDom**. So the fiinal code at **src/inde.js** like,
```JS
import React from "react";
import ReactDOM from "react-dom";
import AppRouter from "./AppRouter";
import * as serviceWorker from "./serviceWorker";
ReactDOM.render(<AppRouter />, document.getElementById("root"));
// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

- AppRouter component is defined as **App**, **Post**, and **NotFound**.
- The app is mixed up with **Posts** and **PostWidget**.
- **Posts** and a **PostWidget** components will use in the **App** component
- **Post** component for a single post and **NotFound** component for the wrong URL enter our application. 
- For this Application, we will take advantage of **ES6** and **JSX**. 
-  Besides these packages, we will also use five custom components.

#### :point_right: Create a folder component. 
- In this folder, create **App.js**, **Posts.js**, **PostWidget.js**, **Post.js**, **NotFound.js**. 
- Here, just declare a component class for now.

#### :point_right: Open src/components/App.js and write the following code.

```JS
import React from "react";
class App extends React.Component {
  render() {
    return <div>App</div>;
  }
}
export default App;
```
#### :point_right: Open src/Posts.js and write the following code.

```JS
import React from "react";
class Posts extends React.Component {
  render() {
    return <div>Post Archive</div>;
  }
}
export default Posts;
```
#### :point_right: Open src/components/Post.js and write the following code.

```JS
import React from "react";
class Post extends React.Component {
  render() {
    return <div>Single Post</div>;
  }
}
export default Post;
```
#### :point_right: Open src/components/PostWidget.js and write the following code.
```JS
import React from "react";
class PostWidget extends React.Component {
  render() {
    return <div>Post Widget</div>;
  }
}
export default PostWidget;
```
#### :point_right: Open src/components/NotFound.js and write the following code.
```JS
import React from "react";
class App extends React.Component {
  render() {
    return <div>App</div>;
  }
}
export default App;
```

## Part 2 [AppRouter component](https://mrinalbd.com/approuter-setup-with-react-graphql-wordpress-app/)

#### :point_right: In this part, we will build `src/AppRouter.js`.
- We will use **{ BrowserRouter, Route, Switch }** from **react-router-dom**.
- use **ApolloClient** and **{gql}** from **apollo-boost** package to connect **React** with **Apollo**.
- And import **milligram CSS** & **App** component here. 
- Also, **Post** and **NotFound** component import here from respective files.
```JS
import React from "react";
import { BrowserRouter, Route, Switch } from "react-router-dom";
import ApolloClient, { gql } from "apollo-boost";
import "milligram";
import App from './App';
import Post from './components/Post';
import NotFound from './components/NotFound';
```
#### :point_right: Use react-router-dom’s { BrowserRouter, Route, Switch } components here.
```JS
render() {
    return (
      <div className="container">
        <BrowserRouter>
          <Switch>
            <Route
              exact
              path="/"
              render={props => <App {...props} state={this.state.posts} />}
            />
            <Route
              path="/post/:postID"
              render={props => <Post {...props} state={this.state.posts} />}
            />
            <Route component={NotFound} />
          </Switch>
        </BrowserRouter>
      </div>
    );
  }
```
#### :point_right: Here, the mechanism of Switch is like that,
- When URL is root BrowserRouter render App component.
- If URL is going to single post BrowserRouter render Post component. Here `:postID` placeholder will be changed with real post id. Here, we render Post component with parent props and state.
- If any user goes to another URL, BrowserRouter renders NotFound component.

#### :point_right: In AppRouter class, the state is defined here. We can store data in state and use this state in a different component.
```JS
state = {
  posts: []
},
```

#### :point_right: At this point, we will use the componentDidMount life cycle. This life cycle is hooked when component mounted.
- Here, we will use an instance of ApolloClient class. ApolloClient class needs URI which is http://localhost/wordpress/?graphql .

```JS
componentDidMount() {
  const client = new ApolloClient({
    uri: 'https://mrinalbd.com/?graphql'
  });
}
```
