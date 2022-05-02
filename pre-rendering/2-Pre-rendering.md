### Pre-rendering 

React vs Next JS

By default, Next JS pre-renders every page in the application

What does pre-render mean?

* Next JS generates HTML for each page in advance instead of having it all done by client-side JavaScript.

* In a react app the javascript is loaded which then executes to mount the html elements onto the dom, so when the page is served we just have a div tag with id equal 
to root. Once the javascript for the page is loaded it will execute in the browser create the different dom nodes and mount them onto the root div element this process is also called hydration 

* In the next Js app the pages are pre-rendered or in simpler words the html is already generated with the necessary data and then sent to the browser, the javascript 
would then load and make the page interactive but the html is there to begin with.

So prerender just means render in advance of sending it to the browser and pre-rendering is done by default in the next Js app which is why you see all the html 
elements in the page source code.

Why pre-render?

Pre-rendering improves performance

* In a React app, you need to wait for the JavaScript to be executed.
• Perhaps fetch data from an external API and then render the UI
• There is a wait time for the user 
* With a pre-rendered page, the HTML is already generated and loads faster.

Pre-rendering helps with SEO

* If you're building a blog or an e-commerce site, SEO is a concern

* With a React app, if the search engine hits your page, it only sees a div tag with id equal to root

* If search engine hits a pre-rendered page though, all the content is present in the source code which
will help index that page

* If SEO is of concern for your app, pre-rendering is what you want


Pre-rendering Summary

1. Pre-rendering refers to the process of generating HTML in advance with the necessary data for a page in our
application.

2. Pre-rendering can result in better performance and SEO.

