# apollographql
# Source 1 → https://mrinalbd.com/setup-for-react-front-end/

### :point_right: First clone the graphql in your plugin folder 
https://github.com/wp-graphql/wp-graphql

### After activate the plugin, visit http://localhost/wordpress/?graphql

### If it show a page of error, then confirmed wp-graphql plugin works.

### Let's create a brand new react app by the command
`npx create-react-app apollographql`
> Note: npx is a npm package runner. The typical use is to download and run a package temporarily or for trials.

- [ ] go to project folder and start this app
`cd apollographql && npm start`

- [ ] We need to install three packages to use graphQL in React. Apollo makes possible to write a query in graphQL.
1. https://www.npmjs.com/package/apollo-boost
2. https://www.npmjs.com/package/react-apollo
3. https://www.npmjs.com/package/graphql
Also we need more cuple of think,
+ https://milligram.io/ for quick style
+ https://www.styled-components.com/
+ https://reacttraining.com/react-router/web/guides/quick-start for pagination system
+ https://github.com/cure53/DOMPurify for safe DOM rander in React app

Install these packages with the command -
`npm i apollo-boost react-apollo graphql react-router-dom milligram styled-components dompurify`
Note: By default, these packages install for development only. Here, `i` is the shorthand for `install` command. 

- [ ] We will create some components. These are:
AppRouter
App
Posts
PostWidget
Post
NotFound

Open src/index.js, because it application start. Remove index.css in App importer. At last, use AppRouter in ReactDom. So the fiinal code at src/inde.js like,
