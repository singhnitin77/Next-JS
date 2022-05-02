### Static Generation

Pre-rendering in Next JS

Next JS supports two forms of pre-rendering

* Static Generation
* Server-side Rendering

### Static Generation

* It is a  method of pre-rendering where the HTML pages are generated at build time.

* The HTML with all the data that makes up the content of the web page are generated in advance when we build your application

* Recommended method to pre-render pages whenever possible because page can be built once, cached by a CDN and served to the client almost instantly.

Ex: Blog pages, e-commerce Product pages, documentation and marketing pages


### Static Generation - How?

* Next JS, by default will pre-render every page in our app.

* The HTML for every page will automatically be statically generated when we build our application.

* "Throughout this video, you've been mentioning that pages are generated at build time. But there is no build for application yet, is there? Aren't we running the application in development mode?"

* #### Prod Server - An optimized build is created once and you deploy that build. You don't make code changes on the go once it is deployed

* #### Dev Server - We should be able to make changes in our code and we want that code to immediately reflect in the browser.

For production builds, a page will be pre-rendered once when we run the build command.

In development mode, the page is pre-rendered for every request you make.

---

Static Generation contd.

Next JS, by default, without any configuration, statically generates every page in our app when
we build it for production. This allows the page to be cached by a CDN and indexed by a search
engine.

---

Static generation can be done with our without data.
