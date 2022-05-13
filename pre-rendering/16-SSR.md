### Server Side Rendering

Two forms of pre-rendering
1. Static Generation
2. Server-side Rendering

#### Static Generation

* The HTML is statically generated at build time. The built page is then cached and reused for each request.

* For a dynamic page with getStaticPaths and fallback set to true the page is not generated at build time but is generated on the initial request.

* With incremental static regeneration,apage can be regenerated for a request after the revalidation time has elapsed.

* For the most part, the pages are generated using getStaticProps when you build the project.


---

### Problems with Static Generation

1. We cannot fetch data at request time.

* With not being able to fetch data per request, we run into the problem of stale data.

* Let's say we are building a news website.

* The content is very dynamic in the sense that new articles can be published almost every second.

* getStaticProps will fetch the news at build time which is not suitable at all.

* getStaticPaths will help fetch the data on the initial request but it is then cached for subsequent requests.

* Incremental static regeneration (ISR) can help but if revalidate is 1 second, we still might not always see the most up to date news when the regeneration is 
happening in the background.

* Rather fetch the data on the client side by makingaget request from the component. But no SEO

* The first problem of Static Generation is that we can't fetch data per request and pre-render .

Second problem is that we don't get access to the incoming request, if the page is pre-rendered at build time.

2. We don't get access to the incoming request.

* Problem when the data that needs to be fetched is specific to a user.

* Let's say we are buildingawebsite similar to twitter.

* As a user,Ishould be able to see tweets that are personalized based on my interests.

* The tweets thatIsee also need to be SEO friendly as it is public content that anyone in the world can see.

* To fetch tweets specific to the user, we need the userld. And that can be obtained only if have we access to the incoming request.

* You could do it client side in useEffect for example but that means you again miss out on SEO.

---

### Server-side Rendering

* With SSR, Next.js allows you to pre-renderapage not at build time but at request time.

* The HTML is generated for every incoming request

* SSR is a form of pre-rendering where the HTML is generated at request time.

* SSR is required when you need to fetch data per request and also when you need to fetch personalized data keeping in mind SEo.

How?

* How does Next.js make it possible to fetch data at request time ?

* How does Next.js make it possible to get access to the incoming request which will facilitate fetching data personalized for a user.
