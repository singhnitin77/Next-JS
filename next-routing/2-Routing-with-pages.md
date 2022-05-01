### Routing with Pages

Scenario - 1

Let's add a route that needs to be rendered when a user visits our website.

index.js
```javascript
function Home() {
return <h1>Home Page</h1>
}
export default Home
```

The index.js file within the pages folder will map to the root of our domoain.

Scenario - 2

for this scenario we need two more routes one route to render when the user visits the about page and another to render when the user visits the profile page 
so in the url slash about and slash profile 

about.js
```javascript
function About() {
  return <h1>About Page</h1>;
}
export default About;
```
```javascript
profile.js
function Profile() {
  return <h1>Profile Page</h1>;
}
export default Profile;
```

The second point to keep in mind is that pages are associated with a route based on their file name.

 
