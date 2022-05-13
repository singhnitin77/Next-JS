### getStaticPaths fallback: 'blocking'

fallback 'blocking' is very similar to fallback true, only difference is that instead of showing a fallback page we'll not see any new content in the ui while the 
page is being generated on the server.

#### How fallback set to blocking affects pre-rendering.

1. The paths returned from getStaticPaths will be rendered to HTML at build time by getStaticProps.

2. The paths that have not been generated at build time will not result ina404 page. Instead, on the first request, Next.js will render the page on the server and return the generated HTML.

3. When that's done, the browser receives the HTML for the generated path. From the user's perspective, it will transition from "the browser is requesting the page" to "the full page is loaded". There is no flash of loading/fallback state.

4. At the same time, Next.js keeps track of the new list of pre-rendered pages. Subsequent requests to the same path will serve the generated page, just like other pages pre-rendered at
build time.

[postId].js
```javascript.js
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
      { params: { postId: "1" } },
      { params: { postId: "2" } },
      { params: { postId: "3" } },
    ],
    fallback: "blocking",
  };
}

export async function getStaticProps(context) {
  const { params } = context;
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/posts/${params.postId}`
  );
  const data = await response.json();

  console.log(`Generating page for /posts/${params.postId}`);

  return {
    props: {
      post: data,
    },
  };
}
```

Pages for the postId: 1,2,3 are statically generated as they are returned from getstaticPaths.

When we make initial req to /4 Nextjs will start to render the page on the server for postId = 4, during this time tab shows loading spinner indicating that a req is being made after the page has completed rendering on the server, the browser recieves it.

Because of the blocking behaviour the first request has the content returned there is no flash or loading state between the req and the page load.

Instead of rendering the fallback page, the ui is blocked till the new page is received in the browser.

When?

* On a UX level, sometimes, people prefer the page to be loaded without a loading indicator if the wait time isafew milli seconds. This helps avoid the layout shift.

* Some crawlers did not support JavaScript. The loading page would be rendered and then the full page would be loaded which was causingaproblem.
