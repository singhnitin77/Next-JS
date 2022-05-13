
In Next js to use server side rendering for a page, export async function - getServerSideProps. It will be called by the server on every req, inside that function 
we can fetch external data and send it as props to the page. Similar to getstaticprops.

pages/news/index.js
```javascript
function NewsArticleList({ articles }) {
  return (
    <>
      <h1>List of News Articles</h1>
      {articles.map((article) => {
        return (
          <div key={article.id}>
            <h2>
              {article.id} {article.title} | {article.category}
            </h2>
            <hr />
          </div>
        );
      })}
    </>
  );
}

export default NewsArticleList;

export async function getServerSideProps() {
  const response = await fetch("http://localhost:4000/news");
  const data = await response.json();

  return {
    props: {
      articles: data,
    },
  };
}
```

This form of pre-rendering is slower compared to static generation as the server must compute the result on every request.

### getServerSideProps

1.
* getServerSideProps runs only on the server side.

* The function will never run client-side.

* The code you write inside getServerSideProps won't even be included in the JS bundle that is sent to the browser.

2.
* You can write server-side code directly in getServerSideProps.

* Accessing the file system using the fs module or queryingadatabase can be done inside getServerSideProps.

* You also don't have to worry about including API keys in getServerSideProps as that won't make it to the browser.


getServerSideProps contd.

3.
* getServerSideProps is allowed only inapage and cannot be run from a regular component file.

* It is used only for pre-rendering and not client-side data fetching

4.
* getServerSideProps should return an object and object should containaprops key which an object*
