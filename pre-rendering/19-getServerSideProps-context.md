### Context parameter

One of the limitation of the basic static generation is that we dont get access to the incoming req, which prevents us from fetching data that is user specific.

Whereas getServerSideProps gives us access to the incoming request.

from the context, we can destructure req, res.

To set a cookie 

pages/news/[category].js
```javascript
function ArticleListByCategory({ articles, category }) {
  return (
    <>
      <h1>Showing news for category "{category}"</h1>
      {articles.map((article) => {
        return (
          <div key={article.id}>
            <h2>
              {article.id} {article.title}
            </h2>
            <p>{article.description}</p>
            <hr />
          </div>
        );
      })}
    </>
  );
}

export default ArticleListByCategory;

export async function getServerSideProps(context) {
  const { params, req, res, query } = context;
  const { category } = params;
  const response = await fetch(
    `http://localhost:4000/news?category=${category}`
  );
  const data = await response.json();
  res.setHeader("Set-Cookie", ["name=Nitin"]);
  console.log(req.headers.cookie);
  console.log(query);
  return {
    props: {
      articles: data,
      category,
    },
  };
}
```

Query strings are quite common when we have to filter a client side and ensure the url can be share with others.
