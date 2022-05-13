### Client-side Data Fetching

Two forms of pre-rendering

Static Generation & Server-side Rendering

How to fetch data

getStaticProps & getServerSideProps

You might not always need to pre-render the data

Ex: User dashboard page

It is private, that is behindalogin screen

Highly user-specific and SEO is not relevant

No need to pre-render the data

You can rely on client side data fetching

pages/dashboard.js
```javascript
import { useState, useEffect } from "react";

function Dashboard() {
  const [isLoading, setIsLoading] = useState(true);
  const [dashboardData, setDashboardData] = useState(null);
  useEffect(() => {
    async function fetchDashboardData() {
      const response = await fetch("http://localhost:4000/dashboard");
      const data = await response.json();
      setDashboardData(data);
      setIsLoading(false);
    }
    fetchDashboardData();
  }, []);

  if (isLoading) {
    return <h2>Loading...</h2>;
  }

  return (
    <div>
      <h2>Dashboard</h2>
      <h2>Posts - {dashboardData.posts}</h2>
      <h2>Likes - {dashboardData.likes}</h2>
      <h2>Followers - {dashboardData.followers}</h2>
      <h2>Following - {dashboardData.following}</h2>
    </div>
  );
}

export default Dashboard;
```

* If we are creating a page that is private does not need seo and user-specific then client-side data fetching is the way to go.

* This is handy when our page is split into components and you want to fetch data from the individual components and render them as when the data is fetched rather 
than wait for the entire page data to be loaded.

* Componetns unlike pages cannot execute getstaticProps or getserversideprops and hence client-side data fetching is the only possibility.
