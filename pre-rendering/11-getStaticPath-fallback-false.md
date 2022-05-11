### getStaticPaths fallback false

It is mandatory

falseback key accepts 3 psbl values

getStaticPaths and fallback

* fallback: false
* fallback: true
* fallback: 'blocking'

getStaticPaths fallback: false

1. The paths returned from getStaticPaths will be rendered to HTML at build time by getStaticProps.

2. If fallback is set to false, then any paths not returned by getStaticPaths will result ina404
page


index.js
```javascript
function PostList({ posts }) {
  return (
    <>
      <h1>List of Posts</h1>
      {posts.map((post) => {
        return (
          <div key={post.id}>
            <h2>
              {post.id} {post.title}
            </h2>
            <hr />
          </div>
        );
      })}
    </>
  );
}

export default PostList;

export async function getStaticProps() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  const data = await response.json();

  return {
    props: {
      posts: data.slice(0,3),
    },
  };
}
```

[postId].js

```javascript
function Post({ post }) {
  return (
    <>
      <h2>
        {post.id} {post.title}
      </h2>
      <p>{post.body}</p>
    </>
  );
}

export default Post;

export async function getStaticPaths() {
  // const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  // const data = await response.json();
  // const paths = data.map((post) => {
  //   return {
  //     params: { postId: `${post.id}` },
  //   };
  // });

  return {
    paths: [
      { params: { postId: '1' } },
      { params: { postId: '2' } },
      { params: { postId: '3' } }
    ],
  
    fallback: false,
  };
}

export async function getStaticProps(context) {
  const { params } = context;
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.postId}`
  );
  const data = await response.json();

  return {
    props: {
      post: data,
    },
  };
}
```

getStaticPaths fallback: false
When?

* The false value is most suitable if you have an application with a small number of paths to pre-render.

* When new pages are not added often.

* A blog site withafew articles isagood example for fallback set to false 
