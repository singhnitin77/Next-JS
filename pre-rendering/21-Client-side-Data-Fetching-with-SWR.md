### Client-side Data Fetching - with SWR

useSWR is a hook. 1st argument is the unique key for the req, 2nd argument is the function where we fetch the data.

useSWR returns many things. from it we can destructure data and error.

data - API data
error - Any err

pages/dashboard-swr.js

```javascript
import useSWR from 'swr'

const fetcher = async () => {
  const response = await fetch('http://localhost:4000/dashboard')
  const data = await response.json()
  return data
}

function DashboardSWR() {
  const { data, error } = useSWR('dashboard', fetcher)

  if (error) return 'An error has occurred.'
  if (!data) return 'Loading...'

  return (
    <div>
      <h2>SWR Dashboard</h2>
      <h2>Posts - {data.posts}</h2>
      <h2>Likes - {data.likes}</h2>
      <h2>Followers - {data.followers}</h2>
      <h2>Following - {data.following}</h2>
    </div>
  )
}

export default DashboardSWR
```
