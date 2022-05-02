### Static Generation with getStaticProps

Generating the HTML after fetching some external Data.

index.js
```javascript
function Home() {
  return <h1>Next JS pre-rendering</h1>;
}

export default Home;
```

users.js
```javascript
function UserList() {
  return <h1>List of users</h1>;
}

export default UserList;

export async function getStaticProps() {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  const data = await response.json();
  console.log(data);
}

```

users.js

```javascript
function UserList({ users }) {
  return (
    <>
      <h1>List of users</h1>
      {users.map((user) => {
        return (
          <div key={user.id}>
            <p>{user.name}</p>
            <p>{user.email}</p>
          </div>
        );
      })}
    </>
  );
}

export default UserList;

export async function getStaticProps() {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  const data = await response.json();
  console.log(data);

  return {
    props: {
      users: data,
    },
  };
}
```

Displaying a list of articles, list of products on ecommerce page, list of topics on documentation page.
