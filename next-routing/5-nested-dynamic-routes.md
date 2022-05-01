8 - Nested Dynamic Routes

[reviewId].js

pages/product/[productid]/review/reviewId.js

```javascript
import { useRouter } from "next/router";
function Review() {
  const router = useRouter();
  const { productId, reviewId } = router.query;
  return (
    <h1>
      Review {reviewId} for product {productId}
    </h1>
  );
}

export default Review;
```
