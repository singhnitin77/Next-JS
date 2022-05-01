7 - Dynamic Routes

pages/product/index.js

```javascript
function ProductList() {
  return (
    <>
      <h2>Product 1</h2>
      <h2>Product 2</h2>
      <h2>Product 3</h2>
    </>
  );
}

export default ProductList;
```

[productid].js - file name

pages/product/[productid].js

```javascript
function ProductDetail() {
  return <h1>Details about product</h1>;
}

export default ProductDetail;
```

Nextjs treats square brackets in a filename as a dynamic segment to create a dynamic route.

useRouter()
The hook returns a router object. From this router object we accesss the query parameters object.
 
```javascript
import { useRouter } from "next/router";

function ProductDetail() {
  const router = useRouter();
  const productId = router.query.productId;
  return <h1>Details about product {productId}</h1>;
}

export default ProductDetail;
```

Productid can be any string not just a number. 

Dynamic route is useful in implementing the list detail pattern in any UI application.

pages-folder/product-folder/sweater.js

```javascript
function Sweater() {
  return <h1>Landing page for Sweaters</h1>;
}
export default Sweater;
````

http://localhost:3000/product/sweater - Landing page for Sweaters

Nextjs will always try to match the route path with a file name in the pages folder nested or not before trying to match a dynamic route.
