### Catch ALL API Routes

For any no. of segments we add, the same API route handler is executed with all the segments being available on the request.query object.

Cath all routes are not meant to handle routes without any parameters at all.

pages/api/[...params].js

```javascript
export default function handler(req, res) {
  const params = req.query.params;
  console.log(params); //params refers to the file name
  res.status(200).json(params);
}
```

double square brackets - [[...params]].js
