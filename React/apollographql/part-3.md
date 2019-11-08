এই পর্বে আমরা `src/components/App.js` এর উপর কাজ করব।

প্রথমেই আমরা `styled-components` ইম্পোর্ট করব। আর প্রথম পর্বে আমরা **Posts** এবং **PostWidget** ইম্পোর্ট করে রেখেছিলাম।

```JS
import styled from "styled-components";
import Posts from "./Posts";
import PostWidget from "./PostWidget";
```

এখন আমরা **render()** মেথড ব্যাবহার করব। এবং **return** এর ভিতর মিলিগ্রামের গ্রিড ব্যাবহার করব।
[milligram.io/#grids](https://milligram.io/#grids)

```JS
render() {
    return(
        <div className="row">
          <div className="column column-80">Post Archive</div>
          <div className="column column-20">Widget</div>
        </div>
    );
  }
```

এখন আমরা রিটার্নের আগে কন্ডিশন লিখব।
- রিটার্ন হবে যদি **state** এ কোন পোস্ট থাকে
- তারপর মেইন কম্পোনেন্ট রিটার্ন করবে

```JS
render() {
   if (this.props.state.length) {
    return(
        <div className="row">
          <div className="column column-80">Post Archive</div>
          <div className="column column-20">Widget</div>
        </div>
    );
  }
  return <p>Loading...</p>;
  }
```

এখন আমরা **post** এরেকে ম্যাপিং করে দেখাব।
এরে ম্যাপ সম্পর্কে পরিষ্কার হওয়ার জন্য এই লিঙ্কটা দেখা যেতে পারে।
[Array Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

```JS
{this.props.state.map(post => (
  <Posts key={post.node.id} post={post} />
))}
```

**Widget** এ আমরা একইভাবে কাজ করব। কিন্তু ম্যাপিং করার আগে আমরা array slice করে প্রথম দুইটা পোস্ট নিব

```JS
{this.props.state.slice(0, 2).map(post => (
  <PostWidget key={post.node.id} post={post} />
))}
```

আমরা **Widget** কে div ট্যাগ হিসেবে define করব।

```JS
const Widget = styled.div`
  border: 1px solid gray;
  padding: 10px;
  p {
    margin-bottom: 0;
    border-top: 1px solid gray;
    }
  }
`;
```

Widget কম্পোনেন্ট এভাবে ব্যাবহার করতে পারি,

```JS
<Widget>
   <h3>Recent posts</h3>
     {this.props.state.slice(0, 2).map(post => (
       <PostWidget key={post.node.id} post={post} />
     ))}
</Widget>
```

তাহলে `src/components/App.js` এর সম্পুর্ন কোড হচ্ছে →

```JS
import React from "react";
import styled from "styled-components";
import Posts from "./Posts";
import PostWidget from "./PostWidget";
const Widget = styled.div`
  border: 1px solid gray;
  padding: 10px;
  p {
    margin-bottom: 0;
    border-top: 1px solid gray;
    }
  }
`;
class App extends React.Component {
  render() {
    if (this.props.state.length) {
      return (
          <div className="row">
            <div className="column column-80">
              {this.props.state.map(post => (
                <Posts key={post.node.id} post={post} />
              ))}
            </div>
            <div className="column column-20">
              <Widget>
                <h3>Recent posts</h3>
                {this.props.state.slice(0, 2).map(post => (
                  <PostWidget key={post.node.id} post={post} />
                ))}
              </Widget>
            </div>
          </div>
      );
    }
    return <div>Loading...</div>;
  }
}
export default App;
```
