### More on getStaticProps

getStaticProps

* getStaticProps runs only on the server side.

* The function will never run client-side.

* The code you write inside getStaticProps won't even be included in the JS bundle that is sent to the browser.

---

* You can write server-side code directly in getStaticProps.

* Accessing the file system using the fs module or querying a database can be done inside getStaticProps.

* You also don't have to worry about including API keys in getStaticProps as that won't make it to the browser.
---

* getStaticProps is allowed only in a page and cannot be run from a regular component file

* It is used only for pre-rendering and not client-side data fetching.

---
* getStaticProps should return an object and object should contain a props key which is an object*

* In our example, we returned an object & the object contained a props key which was an object as well.
---

* getStaticProps will run at build time.

* During development, getStaticProps runs on every request.
