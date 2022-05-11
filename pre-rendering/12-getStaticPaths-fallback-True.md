### getStaticPaths fallback True

1. The paths returned from getStaticPaths will be rendered to HTML at build time by getStaticProps.

2. The paths that have not been generated at build time will not result ina404 page. Instead, Next.js will servea"fallback" version of the page on the first request to such a path.

3. In the background, Next.js will statically generate the requested path HTML and JSON. This includes running getStaticProps.

4. When that's done, the browser receives the JSON for the generated path. This will be used to automatically render the page with the required props. From the user's perspective, the page will be swapped from the fallback page to the full page.

5. At the same time, Next.js keeps track of the new list of pre-rendered pages. Subsequent requests to the same path will serve the generated page, just like other pages pre-rendered at
build time.

getStaticPaths fallback: true

### When?

* The true value is most suitable if your app hasavery large number of static pages that depend on data.

* A large e-commerce site.

* You want all the product pages to be pre-rendered but if you have a few thousand products, builds can take a really long time.

* You may statically generateasmall subset of products that are popular and use fallback: true for the rest.

* When someone requestsapage that's not generated yet, the user will see the page withaloading indicator.

Shortly after, getStaticProps finishes and the page will be rendered with the requested data. From then onwards, everyone who requests the same page will get the statically pre-rendered page

This ensures that users always haveafast experience while preserving fast builds and the benefits of Static
Generation


[postId].js
```javascript
import { useRouter } from "next/router";

function Post({ post }) {
  const router = useRouter();

  if (router.isFallback) {
    return <div>Loading...</div>;
  }

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
      { params: { postId: "1" } },
      { params: { postId: "2" } },
      { params: { postId: "3" } },
    ],

    fallback: true,
  };
}

export async function getStaticProps(context) {
  const { params } = context;
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.postId}`
  );
  const data = await response.json();

  if (!data.id) {
    return {
      notFound: true,
    };
  }

  console.log(`Generating page for /posts/${params.postId}`);

  return {
    props: {
      post: data,
    },
  };
}
```

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
