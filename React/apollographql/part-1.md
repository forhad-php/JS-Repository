:black_large_square: প্রথমেই `https://github.com/wp-graphql/wp-graphql` রিপোজিটোরি টি আমাদের ওয়ার্ডপ্রেস সাইটে ক্লোন করে নেই। wp-graphql হচ্ছে, যেকোন ওয়ার্ডপ্রেস থেকে GraphQL schema এবং API প্রদানকারী একটা প্লাগিন।
প্লাগিনটি একটিভ করার পর আমি যদি আমার ওয়ার্ডপ্রেস সাইটে ভিজিট করি এইভাবে `http://localhost/wordpress/?graphql` এবং যদি দেখি এরকম
```{"errors":[{"message":"GraphQL Request must include at least one of those two parameters: \"query\" or \"queryId\"","category":"request"}]}```

একটা ইরর মেসেজ, তাহলে বুঝব প্লাগিনটি কাজ করেছে।

:black_large_square: এবার আমারা ওয়ার্ডপ্রেস থেকে বেরিয়ে আসব।

এখন আমরা `apollographql` নামে একটা রিয়েক্ট আপ্লিকেশন তৈরি করব। এর জন্য আমাদের যে কমান্ডটি লিখতে হবে,

```npx create-react-app apollographql```

`npx` হচ্ছে `npm package runner`, যা নগদে যে কোন প্যাকেজ টেম্পরারি ডউনলোড করে রান করে দিবে। এর জন্য আপনাকে জেসন ফাইলে গিয়ে প্যাকেজের নাম লিখে তারপর ইন্সটল হাবিজাবি কিচ্ছু করা লাগবেনা।

:black_large_square: এখন আমারা প্রজেক্ট ফোল্ডারে ঢুকব এবং npm স্টার্ট দিব। এর জন্য আমাদের যে কমান্ডটি লিখতে হয়,

```cd apollographql && npm start```

রিয়েক্টে গ্রাফ কিউ এল ব্যাবহার করতে হলে যে তিনটা প্যাকেজ লাগবে তা হল,

- apollo-boost
- react-apollo এবং
- graphql

apollo যেটা করে যে, graphQL এর মধ্যে query লিখে।

আমাদের আরো যে ৪টা জিনিস লাগবে তা হলঃ

- milligram (কুইক CSS লিখার জন্য)
- styled-components (components স্টাইল করার জন্য)
- quick-start (pagination system তৈরি করার জন্য)
- DOMPurify (সেইফলি DOM রেন্ডারিং এর জন্য)

এবার এই সবগুলা প্যাকেজ এবং টুলস একসাথে ইন্সটল করার জন্য আমারা যেই কমান্ডটি লিখতে পারিঃ

```npm i apollo-boost react-apollo graphql react-router-dom milligram styled-components dompurify```

> এখানে `i` মানে install
> বাই ডিফল্ট প্যাকেজগুলা ইন্সটল হবে শুধু ডেভেলপমেন্ট এর জন্য।

:black_large_square: এখন আমারা কিছু কম্পনেন্ট তৈরি করব। এগুলো হচ্ছেঃ

- AppRouter
- App
- Posts
- PostWidget
- Post
- NotFound

তাহলে আর দেরি না করে `src/components` নামের একটা ফোল্ডার তৈরি করে ফেলি। এবং এর ভিতরে,

- App.js
- Post.js
- PostWidget.js
- Posts.js
- NotFound.js
এই পাঁচটা ফাইল তৈরি করে ফেলি।

:black_large_square: এখন আমারা `/src` ফোল্ডারের ভিতর `AppRouter.js` ফাইলটি তৈরি করব। Naming convention টা ঠিক রাখতে হবে। React হচ্ছে Camel case টা ফলো করে। আমরা জানি প্রতিটা কম্পনেন্টের ভিতর React ইম্পোর্ট করতেই হয়। তো `src/AppRouter.js` ফাইলটার ভিতরে আমরা আপাতত কিছু একটা লিখব,

```JS
import React from "react";
class AppRouter extends React.Component {
  render() {
    return <div>Router</div>;
  }
}
export default AppRouter;
```

- এখন `src/index.js` ফাইলটা খুলি। এটাই মূলত অ্যাপ্লিকেশানটা ওপেন করে।
- সেখানে ইম্পোর্টার থেকে `index.css` এবং `App.js` রিমুভ করে দিব। অর্থাৎ import করা লাইন দুইটা কেটে দিব। 
- এবং এই নামের ফাইল দুইটা, `src/index.css` এবং `src/App.js` ডিলিট করে দিব। 
- অবশেষে `ReactDom` থেকে `AppRouter` টা ইউজ করব।
- তাহলে আমাদের `src/index.js` ফাইলের ফাইনাল কোড হবে এমনঃ

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

:black_large_square: এখন তাহলে কম্পনেন্টগুলো রেডি করে ফেলি,
`src/components/App.js` ফাইলের ভিতর লিখি,

```JS
import React from "react";
class App extends React.Component {
  render() {
    return <div>App</div>;
  }
}
export default App;
```

`src/components/Posts.js` ফাইলের ভিতর লিখি,
```JS
import React from "react";
class Posts extends React.Component {
  render() {
    return <div>Post Archive</div>;
  }
}
export default Posts;
```

`src/components/Post.js` ফাইলের ভিতর লিখি,
```JS
import React from "react";
class Post extends React.Component {
  render() {
    return <div>Single Post</div>;
  }
}
export default Post;
```

`src/components/PostWidget.js` ফাইলের ভিতর লিখি,
```JS
import React from "react";
class PostWidget extends React.Component {
  render() {
    return <div>Post Widget</div>;
  }
}
export default PostWidget;
```

`src/components/NotFound.js` ফাইলের ভিতর লিখি,
```JS
import React from "react";
class NotFound extends React.Component {
  render() {
    return <div>Not Found!!!</div>;
  }
}
export default NotFound;
```

:black_large_square: তাহলে `src/AppRouter.js ` এর ভিতরে থাকল `App`, `Post`, এবং `NotFound.`
```JS
import App from './components/App';
import Post from './components/Post';
import NotFound from './components/NotFound';
```

এবং `src/components/App.js` এর ভিতরে থাকল `Posts` এবং `PostWidget`
```JS
import Posts from "./components/Posts";
import PostWidget from "./components/PostWidget";
```

> `Post` কম্পনেন্টটা কাজ করবে সিঙ্গেল পোস্টের জন্য এবং `NotFound` কম্পনেন্ট কাজ করবে wrong URL ধরার জন্য।

