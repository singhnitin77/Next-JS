### API Route

- Next JS is a full stack framework.

- You can write the FE code in React and also write APIS that can be called by the front end code.

- API routes allow you to create RESTful endpoints as part of your Next.js application folder structure.

- Within the pages folder, you need to createafolder called 'api'.

- Within that 'api' folder, you can define all the API for your application.

- You can add business logic without needing to write any additional custom server code and without having to configure any API routes.

- Next JS gives you everything you need to write full-stack React+Node applications.

- Next JS not only simplifies the front-end but also the backend as well.

.status is a function to set the status code.
.json - function that sends a json response.

http://localhost:3000/api

```javascript
pages/api/index.js
export default function handler(req, res) {
  res.status(200).json({ name: "Home API route" });
}
```

http://localhost:3000/api/dashboard

```javascript
pages/api/dashboard.js
export default function handler(req, res) {
  res.status(200).json({ name: "Dashboard API route" });
}
```

http://localhost:3000/api/blog

```javascript
pages/api/blog/index.js
export default function handler(req, res) {
  res.status(200).json({ name: "Blog API route" });
}
```

http://localhost:3000/api/blog/recent

```javascript
pages/api/blog/recent.js
export default function handler(req, res) {
  res.status(200).json({ name: "Recent blog API route" });
}
```

http://localhost:3000/api

http://localhost:3000/api/dashboard


We can also create nested folders.

The code we write in the api folder is never bundled with the frontend code.
