:black_large_square: এই পর্বে আমরা `src/AppRouter.js` এর উপর কাজ করব।

- `react-router-dom` থেকে  `{ BrowserRouter, Route, Switch }` import করব
- **React** কে **Apollo** এর সাথে কানেক্ট করার জন্য `apollo-boost` প্যাকেজ থেকে `ApolloClient` এবং `{gql}` ইম্পোর্ট করব
- `milligram CSS` ইম্পোর্ট করব
- আমাদের সকল ইম্পোর্ট করা দেখতে হবে এরকম →

```JS
import React from "react";
import { BrowserRouter, Route, Switch } from "react-router-dom";
import ApolloClient, { gql } from "apollo-boost";
import "milligram";
import App from './components/App';
import Post from './components/Post';
import NotFound from './components/NotFound';
```

:black_large_square: এই state এর মধ্যে আমরা ডাটা স্টোর করে রাখতে পারব এবং অন্য কোন কম্পনেন্টে ইউজ করতে পারব।

```JS
state = {
  posts: []
},
```

:black_large_square: এরপর `client` ডিফাইন্ড করার পর আমরা query করব data fetch করার জন্য। Query মেথড ইউজ করব `gql` যা একদম শুরুতে ইম্পোর্ট করেছিলাম। wpgraphql কুয়েরি কিভাবে লিখতে হয় তার জন্য তাদের অফিসিয়াল ডকুমেন্ট [docs.wpgraphql.com](https://docs.wpgraphql.com/getting-started/posts)

query যদি সম্পন্ন হয় তাহলে একটা array ফাংশান রান করবে এটাকেই বলা হয় promise এবং **result** হচ্ছে একটা parameter
স্টেট আপডেট করার জন্য setState মেথড ব্যাবহার করতে হয়। এই মেথডটা পোস্টের ডাটা থেকে posts আপডেট করবে। এবং ডাটা আনবে আমরা যে কুয়েরি লিখেছি সেখান থেকে।

```JS
client
    .query({
      query: gql`
        {
          generalSettings {
              title
            }
          posts {
            edges {
              node {
                id
                title
                date
                link
                content
                excerpt
              }
            }
          }
        }
      `
    })
    .then(result => {
      this.setState({ posts: result.data.posts.edges });
    });
```

:black_large_square: এরপর `BrowserRouter, Route, Switch` কম্পোনেন্টগুলো লিখব এইভাবে,

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
> `Switch` কম্পোনেন্টটা যেভাবে কাজ করে,
- যখন URL `path="/"` বা root পর্যায়ে থাকে,
- যদি URL `path="/post/:postID"` বা **single post** হয় তাহলে <Post> কম্পোনেন্ট render হবে parent **props** এবং **state**
- আর যদি কোন ইউজার ভুল URL এ চলে যায় তাহলে `BrowserRouter` render করবে `NotFound` কম্পোনেন্ট

তাহলে আমাদের `src/AppRouter.js` এর সম্পুর্ন কোড দেখতে এমন →

```JS
import React from "react";
import { BrowserRouter, Route, Switch } from "react-router-dom";
import ApolloClient, { gql } from "apollo-boost";
import App from "../App";
import Post from "./Post";
import NotFound from "./NotFound";
class AppRouter extends React.Component {
  state = {
    posts: []
  };
  componentDidMount() {
    const client = new ApolloClient({
      uri: "http://localhost/wordpress/?graphql"
    });
    client
      .query({
        query: gql`
          {
            posts {
              edges {
                node {
                  id
                  title
                  date
                  link
                  content
                  excerpt
                }
              }
            }
          }
        `
      })
      .then(result => {
        this.setState({ posts: result.data.posts.edges });
      });
  }
  render() {
    return (
      <BrowserRouter>
        <Switch>
          <Route exact path="/" render={props => <App {...props} state={this.state.posts} />} />
          <Route
            path="/post/:postID"
            render={props => <Post {...props} state={this.state.posts} />}
          />
          <Route component={NotFound} />
        </Switch>
      </BrowserRouter>
    );
  }
}
export default AppRouter;
```
