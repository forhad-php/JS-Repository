# apollographql
## Source 1 → https://mrinalbd.com/setup-for-react-front-end/

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
Also we need more cuple of think,
+ https://milligram.io/ for quick style
+ https://www.styled-components.com/
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

#### :point_right: Open src/index.js, because it application start. Remove index.css in App importer. At last, use AppRouter in ReactDom. So the fiinal code at src/inde.js like,
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
