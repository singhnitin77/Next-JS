### Link Pre-fetching contd.

Whenapage with getStaticProps is pre-rendered at build time,in addition to the page HTML file, Next.js generatesaJSON file holding the result of running getStaticProps.

The JSON file will be used in client-side routing through next/link,or next/router.

When you navigate to a page that's pre-rendered using getStaticProps,Next.js fetches the JSON file(pre-computed at build time)and uses it as the props to create the 
page component client side.

Client-side page transitions will not call getStaticProps as only the exported JSON is used.

#### Static Generation Summary so far

* Static Generation is a method of pre-rendering where the HTML pages are generated at build time.

* With and without external data.

* Export getStaticProps function for external data.

* HTML,JavaScript and JSON file are generated.

* If you navigate directly to the page route,the HTML file is served.

* If you navigate to the page route fromadifferent route,the page is created client side using the JavaScript and JSON prefetched from the server. There is no additional request to the server.
