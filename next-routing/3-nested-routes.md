### Nested Routes

http://localhost:3000/blog

blog.js
```javascript
function Blog() {
  return <h1>Blog Page</h1>;
}
export default Blog;
```

http://localhost:3000/blog/first

first.js
```javascript
function FirstBlog() {
  return <h1>First blog Page</h1>;
}
export default FirstBlog;
```

http://localhost:3000/blog/second

second.js
```javascript
function SecondBlog() {
return <h1>Second blog Page</h1>
}
export default SecondBlog
```
