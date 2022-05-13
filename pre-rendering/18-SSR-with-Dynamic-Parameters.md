### SSR with Dynamic Parameters

Context parameter is an object which contains a key called params.

params object will contain category route parameter which again can be destructured.

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
  const { params } = context;
  const { category } = params;
  const response = await fetch(
    `http://localhost:4000/news?category=${category}`
  );
  const data = await response.json();

  return {
    props: {
      articles: data,
      category,
    },
  };
}
```
