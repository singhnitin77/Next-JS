### Static Generation & Issues

* Static Generation is a method of pre-rendering where the HTML pages are generated at build time.

* The pre-rendered static pages can be pushed to a CDN, cached and served to clients across the globe almost instantly.

* Static content is fast and better for SEO as they are immediately indexed by search engines

* Static generation with getStaticProps for data fetching and getStaticPaths for dynamic pages seems like a really good approach toawide variety of applications 
in production

Issues

1. The build time is proportional to the number of pages in the application.

2. A page, once generated, can contain stale data till the time you rebuild the application

---

#### Issue with build time

* The build time is proportional to the number of pages in the application.

Example Scenario

* A page takes 100ms to build.

* E-commerce app with 100 products takes 10 seconds to build.

* E-commerce app with 100,000 products takes>2.5 hours to build.

* It's not just the time, there are cost implications as well.

* The problem only gets worse with more products you add to the system as every new page increases the overall build time.

---

#### Issue with stale data

* What if we build the app only once in a while?

* Depending on the nature of your application, you might run into the issue of stale data.

* E-commerce app is not an application which you can build and deploy once inawhile. Product details, especially product prices can vary everyday.

* The entire app has to be re-built and the page with updated data will be statically generated.

---

#### What about getStaticPaths?

* Pre-render only few pages at build time and rest of the pages can be pre-rendered on request.

* Can we not use the that to render say 1000 most popular pages and rest of the 99000 pages can be pre-rendered on request.

* If your application has 90% static pages and 10% dynamic pages, getStaticPaths will not help much.

* An e-commerce site typically will have 90% dynamic pages and 10% static pages. So we can reduce the total build time by using getStaticPaths.

* It still does not fix the issue of stale data.

* If you render 1000 pages at build time, and then the rest are generated based on incoming request, using fallback true or fallback 'blocking', changes in data 
will not update the already pre-rendered pages.


---

#### Json Server - lets you create a fake REST API with 0 coding.

db.json
```javascript
{
  "products": [
    {
      "id": 1,
      "title": "Product 1",
      "price": 700,
      "description": "Description 1"
    },
    {
      "id": 2,
      "title": "Product 2",
      "price": 1050,
      "description": "Description 2"
    },
    {
      "id": 3,
      "title": "Product 3",
      "price": 2600,
      "description": "Description 3"
    }
  ]
}
```

List of 3 items as a product array.

"serve-json": "json-server --watch db.json --port 4000"

In the terminal - npm run serve-json

We are able to create fake Rest API endpoint.

pages/products/index.js

```javascript
function ProductList({ products }) {
  return (
    <>
      <h1>List of products</h1>
      {products.map((product) => {
        return (
          <div key={product.id}>
            <h2>
              {product.id} {product.title} {product.price}
            </h2>
            <hr />
          </div>
        );
      })}
    </>
  );
}

export default ProductList;

export async function getStaticProps() {
  console.log("Generating / Regenerating ProductList");
  const response = await fetch("http://localhost:4000/products");
  const data = await response.json();

  return {
    props: {
      products: data,
    },
  };
}
```

The only difference is the api endpoints inside getstaticprops. we now make a req to our local json server
getStaticProps() makes a get request to /products , an array of 3 prodcuts is fetched, which is returned as products and injected into the component as props.

pages/products/[productId].js

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
  const response = await fetch(
    `http://localhost:4000/products/${params.productId}`
  );
  const data = await response.json();
  console.log(`Generating page for /products/${params.productId}`);

  return {
    props: {
      product: data,
    },
  };
}

export async function getStaticPaths() {
  return {
    paths: [{ params: { productId: "1" } }],
    fallback: true,
  };
}
```

getStaticProps extracts the product id from params, makes an API call to /product/id and returns the individual data as props which is then passed into the component. 
Destructure it from the props and render the product id, title, price and description.

fallback: true,

pages for product id 2 and 3 are not generated at built time, but are generated when a req is made.

---

### Incremental Static Regeneration

* There wasaneed to update only those pages which neededachange without having to rebuild the entire app.

* Incremental Static Regeneration (ISR)

* With ISR, Next.js allows you to update static pages after you've built your application.

* You can statically generate individual pages without needing to rebuild the entire site, effectively solving the issue of dealing with stale data.

### How?

* In the getStaticProps function, apart from the props key, we can specifyarevalidate key.
