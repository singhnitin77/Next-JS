### Catch All Routes

[...params].js

params - refers to the parameters passed In.

pages/docs/[...params].js

```javascript
import { useRouter } from "next/router";

function Doc() {
  const router = useRouter();
  const { params } = router.query;
  console.log(params);
  return <h1>Docs Home Page</h1>;
}

export default Doc;
```

Unliike dynamic routes, params is an array.

Initially param is undefined because of the pre-rendering feature in next.js.

pages/docs/[[...params]].js

```javascript
import { useRouter } from "next/router";
function Doc() {
  const router = useRouter();
  const { params = [] } = router.query;
  console.log(params);
  if (params.length === 2) {
    return (
      <h1>
        Viewing docs for feature {params[0]} and concept {params[1]}
      </h1>
    );
  } else if (params.length === 1) {
    return <h1>Viewing docs for feature {params[0]}</h1>;
  }
  return <h1>Docs Home Page</h1>;
}

export default Doc;
```
