
10 - Link Component Navigation

import Link from 'next/link'

Link component is used for client side routing which means routing within our application.

pages/index.js

```javascript
import Link from "next/link";
function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      <Link href="/blog">
        <a>Blog</a>
      </Link>
      <Link href="/product">
        <a>Products</a>
      </Link>
    </div>
  );
}

export default Home;
```

pages/product/index.js

```javascript
import Link from "next/link";

function ProductList({ productId = 100 }) {
  return (
    <>
      <Link href="/">
        <a>Home</a>
      </Link>
      <h2>
        <Link href="product/1">
          <a>Product 1</a>
        </Link>
      </h2>
      <h2>
        <Link href="product/2">
          <a>Product 2</a>
        </Link>
      </h2>
      <h2>
        <Link href="product/3" replace>
          <a>Product 3</a>
        </Link>
      </h2>
      <h2>
        <Link href={`product/${productId}`}>
          <a>Product {productId}</a>
        </Link>
      </h2>
    </>
  );
}

export default ProductList;
````
