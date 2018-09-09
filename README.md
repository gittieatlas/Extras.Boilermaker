# Boilermaker

#### Intro

1. Create your project filder `mkdir project`
1. Scaffold out your project and generate a `package.json` file with `npm init`
1. `git init`, and make a `.gitignore` file
   ```json
   node_modules
   bundle.js
   bundle.js.map
   ```

#### React

1. <details><summary>Construct an `index.html`</summary>

   ```html
   <!DOCTYPE html>
   <html>

   <head>
     <meta name="viewport" content="width=device-width, initial-scale=1">
     <meta charset="UTF-8">

     <title>App name</title>
     <script src="/bundle.js" defer></script>
   </head>

   <body>
     <div id="app"></div>
   </body>

   </html>
   ```

   </details>

2. Basic Server: Decide how your index.html will be served up to the browser. Will you use an express server, or a quicker solution like webpack-dev-server, http-server, or some other static file server?
   Tools like webpack-dev-server and http-server are very useful - they will serve up static files (including your index.html) from the folder you start them from. This is great if you want to start writing a client-side application but don't want to write a full express server yet (or if you don't need one - for example, if you write an application that uses a cloud database like Firebase, or a simple client app that just needs to make AJAX requests to some external APIs).

   You could install them on a project-by-project basis, or install them globally using the -g flag.

   if you're using express server...

3. install your DEV dependencies `npm install --save-dev webpack webpack-cli babel-core babel-loader babel-preset-react`

   If you want to be proactive in making sure your code is safe for older browsers, you may also install `babel-preset-env`. If you want to avail yourself of some newer language features (like class properties), you should also install `babel-preset-stage-2`

4. install your regular dependencies `npm install --save react react-dom react-router-dom`

5. <details><summary>Index JS: </summary>
   Decide on an 'entry' file and an 'output' file for your webpack pipeline.

   Your entry file might be something simple like an index.js, app/main.js, client/app.js or browser/index.js.

   Your output file will be created by webpack. You don't need to actually create it yet - just decide where you want it to live. This could be in the root of your app, or a public folder - it's up to you.</details>

6. <details><summary>Write your webpack.config.js</summary>
   ```json
   module.exports = {
     "entry": "./index.js", // assumes your entry point is the index.js in the root of your project folder
     "mode": "development",
     "output": {
       "path": __dirname, // assumes your bundle.js will also be in the root of your project folder
       "filename": "bundle.js"
     },
     "devtool": "source-maps",
     "module": {
       "rules": [
         {
           "test": /\.js$/,
           "exclude": /node_modules/,
           "use": {
             "loader": "babel-loader"
           }
         }
       ]
     }
   }
   ```
   </details>
7. <details><summary>.babelrc</summary>
   By setting babel-loader in your webpack config, you're teaching webpack to use babel. However, we also need to tell babel how to parse our code. We do this with another dot-file called .babelrc! In your root project directory, make a file called .babelrc and configure it with the babel-presets you installed.

   For example, if you were using babel-preset-react, babel-preset-env, and babel-preset-stage-2, your .babelrc might look like this:

   ```json
   {
     "presets": ["react", "env", "stage-2"]
   }
   ```

   </details>

8. <details><summary>Write a basic ReactDOM.render in your entry file</summary>
   ```jsx
   import React from 'react';
   import ReactDOM from 'react-dom';

   ReactDOM.render(

     <div>Hello, world!</div>,
     document.getElementById('app') // make sure this is the same as the id of the div in your index.html
   );
   ```
   </details>

9. <details><summary>Start script</summary>
   In your package.json, set up an npm start command (or some combination of other commands) to build your client javascript and run your server.

   You may choose to have a separate scripts for building your client application and for starting your server, or do both with the same command - it's up to you. (webpack-dev-server does both, out of the box!)

   Here's an example where we run webpack in --watch mode in the background, and simultaneously start a server with nodemon (in server.js).

   ```js
   "start": "node server",
   "start-dev": "webpack -w & nodemon server.js"
   ```

   </details>

10. <details><summary>Liftoff!</summary>
    Run `npm start` or `npm run start-dev`, depending on your naming convention! If everything worked, you should see your React app rendered into the DOM when you navigate to `localhost` on the port your app is running from.

    If something went wrong...here are some suggestions to get back on your feet:

    1. Check all of the previous steps - did you forget anything?
    1. Check both the server console (your terminal) where your webpack and server processes are running, and your client console (Chrome dev tools), and check for error messages. Read the errors
       </details>
