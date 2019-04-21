# Creating Our First Express Route

### Now that we have installed all of our project's basic requirements we can create our first Express route.

At this point the dependencies in your package.json shoud look something like this:

```
  "devDependencies": {
    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-plugin-transform-runtime": "^6.23.0",
    "babel-preset-es2015": "^6.24.1",
    "babel-preset-stage-3": "^6.24.1",
    "serverless-offline": "^3.33.0",
    "serverless-webpack": "^4.4.0",
    "webpack": "^3.12.0",
    "webpack-node-externals": "^1.6.0"
  },
  "dependencies": {
    "babel-runtime": "^6.26.0",
    "express": "^4.16.2",
    "serverless": "^1.38.0",
    "serverless-http": "^1.5.2"
  }
```

Your package versions may be different, but this will generally be the packages you'll want to have installed before creating your first Lambda Express route. 

---

### Create a new entry point for our Express app

We no longer need the handler.js file in our Lambda.  Instead we will create a `src` directory where we can store all of our app's code to keep thins a bit more organized.

Delete `handler.js` and create a new `src` directory in your app's root directory.

Next, create a `index.js` file inside `src`. This will be our app's new entry point. 

Your app's directory structure should look something like this now:

```
├── .serverless
├── node_modules
├── src
│   ├── index.js
├── .babelrc
├── .gitignore
├── package.json
├── README.md
├── serverless.yml
├── webpack.config.js
```

---

### Update your serverless.yml to reflect the new app structure

We need to point our lambda to our new `src/index.js` entrypoint instead of handler.js.  We will also setup our first function in `serverless.yml` to do so make your functions look like so:

```
functions:
  app:
    warmup: false
    handler: src/index.handler
    events:
      - http: ANY /
      - http: 'ANY {proxy+}'
  hello:
    handler: src/index.handler
    events:
      - http: 'GET /hello/'
```

This points our app to use `src/index.handler` as our handler for the app. We have also defined a function we have yet to create, `hello`.

---

### Create the `hello` function and Express route

It won't take much code to get our `hello` function up and running.  We will add to our `index.js` file the following code:

```
import serverless from 'serverless-http';
import express from 'express';

const app = express();

app.use(function (req, res, next) {
    res.header('Access-Control-Allow-Origin', '*');
    res.header('Access-Control-Allow-Methods', 'GET, PUT, POST, DELETE, OPTIONS');
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept, Access-Control-Allow-Origin");
    next();
});

app.get('/hello', function (req, res) {
    async function hello() {
        try {
            res.send("hello world!");
        } catch (e) {
            console.error(e);
        }
    }
    hello();
});

module.exports.handler = serverless(app);
```

This code imports `express` and `serverless-http` and uses them to set up an express app running in our handler function.  After we start the app and configure the `express` app headers we can start defining routes on `app`. 

We declare our first `get` route, `/hello`.

---

### See if it works...

Next we can see if it works locally by running:

`serverless offline` in the projects directory.

Your app should start up at `http://localhost:3000/`

If you direct a browser to `http://localhost:3000/hello` you should see "hello world!"

Success 👋 🌎

