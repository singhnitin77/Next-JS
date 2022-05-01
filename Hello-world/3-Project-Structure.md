### Project Structure

Build script needs to run prior to running the start script.

next.config.js File - Next js configuration file.
React strict mode is a development mode only feature for highlighting potential problems in an application.

It helps to identify unsafe life cycles, legacy API usage.

.eslintrc - Configuration file for eslint.

.next file - This folder is generated when we run either the dev or the build scripts, it is from this folder that our nextjs application is served from.

node_modules

styles folder - Contains some styles for our application. GLobal styles and component specific styles.

public folder holds all the public resources for our application. icons, images etc.

There's a feature called pre-rendering which determines how and when the html files are generated.

pages folder - Responsible for the entire routing feature in our application, index.js is the file that gets served in the browser when we visit  local host.

* When we run the command yarndev or npm run dev the execution is transferred to _app.js which contains my app component, my app component automatically receives a component and page props which are then returned as part of the jsx. 

* When we navigate to localhost port 3000 in the browser the component prop will refer to the component defined in index.js which is the home component and that is how we see hello world in the browser

* This is the control flow from package.json to _app.js to index.js in the pages folder.
