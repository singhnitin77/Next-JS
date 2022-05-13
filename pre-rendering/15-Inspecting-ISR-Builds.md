### Inspecting ISR Builds

Incremental Static Regeneration

* There was a need to update only those pages which neededachange without having to rebuild the entire app.

Incremental Static Regeneration (ISR)

* With ISR, Next.js allows you to update static pages after you've built your application

* You can statically generate individual pages without needing to rebuild the entire site, effectively solving the issue of dealing with stale data

How?

* In the getStaticProps function, apart from the props key, we can specifyarevalidate key.

* The value for revalidate is the number of seconds after whichapage re-generation can occur.

---

* By setting revalidate key to 10s we are asking nextjs to revalidate this product list page every 10s. this will ensure updated data is served almost immediately 
without having to rebuild the entire app.

* Every 10s if we refresh the page the log message will appear in terminal. "Generating / Regenerating ProductList"

* Within that 10s timeframe is we reload even 100 times always the cached page will be served and no regeneration will happen. that's the purpose of revalidate key.

pages/products/index.js
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
          </div>
        );
      })}
    </>
  );
}

export default PostList;

export async function getStaticProps() {
  console.log("Generating / Regenerating ProductList");
  const response = await fetch("https://jsonplaceholder.typicode.com/posts");
  const data = await response.json();

  return {
    props: {
      posts: data,
    },
    revalidate: 30,
  };
}
```

pages/products/[postId].js

```javascript
import { useRouter } from "next/router";

function Product({ product }) {
  const router = useRouter();

  if (router.isFallback) {
    return <div>Loading...</div>;
  }
  return (
    <div>
      <h2>
        {product.id} {product.title} {product.price}
      </h2>
      <p>{product.description}</p>
      <hr />
    </div>
  );
}

export default Product;

export async function getStaticProps(context) {
  const { params } = context;
  console.log("Regenerating product ${params.product.id}");
  const response = await fetch(
    `http://localhost:4000/products/${params.productId}`
  );
  const data = await response.json();
  console.log(`Generating page for /products/${params.productId}`);

  return {
    props: {
      product: data,
    },
    revalidate: 10,
  };
}

export async function getStaticPaths() {
  return {
    paths: [{ params: { productId: "1" } }],
    fallback: true,
  };
}
```

---

1. Using getStaticpaths we can ensure only the popular product pages are generated at build time thereby reducing the build time rest of the pages are generated 
when the user makes the initial req.

2. By setting the revalidate key we have also solved the problem of serving stale data to the user as the individual page will be regenerated based on the revalidate 
key value.

### Re-generation

* A re-generation is initiated only ifauser makesarequest after the revalidate time.

* If a user visits our product details page but there is no other user hitting that page the entire day, the re-generation does not happen.

* Revalidate does not mean the page automatically re-generates every 10 seconds.

* It simply denotes the time after which, ifauser makesarequest,are-generation has to be initiated.

* The re-generation can also fail and the previously cached HTML could be served till the subsequent re-generations succeed.
