# Adding The tools we will need to our Lambda

### Express.js is a web application framework which we can take advantage of to add routing for multiple Lambda functions with one entrypoint. 

If you are new to Express.js [check out it's documentation here](https://expressjs.com/en/guide/routing.html) to see how it handles routing. 

---

### Let's get Express.js added to our project

`npm install --save express`

Great, now we can take advantage of the routing Express has to offer.  Before we start writing our Express code, let's get some more tooling set up to give our development experience a better flow.

---

### Add local development capabilities and serverless-http

We will want to be able to test and run our serverless project locally so that we don't have to deploy our application just to test our code.  To get this started install `serverless-offline`:

`npm install --save-dev serverless-offline serverless-http`

And add the plugin to our serverless.yml template as a top level key:

```
plugins:
  - serverless-offline
```

We will also include `serverless-http` to enable our lambda to act as an http server.

`npm install --save serverless-http`

---

### Include Webpack

To bundle up our code automatically for use in the Lambda we will take advantage of Webpack. Install Webpack for local use with this command:

`npm install --save-dev serverless-webpack`

We will want to exclude our `node_modules` directory from being bundled so we will also include a package for helping us exclude that directory:

`npm install --save-dev webpack-node-externals`

Awesome! Now we can create a `webpack.config.js` file in our main directory to get webpack setup.

Add this to our `webpack.config.js` file:

```
const slsw = require("serverless-webpack");
const nodeExternals = require("webpack-node-externals");

module.exports = {
  entry: slsw.lib.entries,
  target: "node",
  externals: [nodeExternals()],
  // skip node_modules
  module: {
    rules: [
      {
        test: /\.js$/,
        loader: "babel-loader",
        include: __dirname,
        exclude: /node_modules/
      }
    ]
  }
};
```

This imports our recently installed modules into the config file.  Then we use these modules to setup the transpiling using `babel-loader` and excluding our `node_modules` directory. 

Finally include the `serverless-webpack` as a plugin in `serverless.yml`.

```
plugins:
  - serverless-offline
  - serverless-webpack
```

---

### Setup Babel

We have specified in our webpack file that we will be using Babel for compiling our code to more advanced versions of javascript.  You can [read more about Babel](https://babeljs.io/docs/en/) to better understand the compiling process. 

We need to add Babel to our project next. Install all the Babel modules necessary:

`npm install --save-dev babel-core babel-loader babel-plugin-transform-runtime babel-preset-es2015 babel-preset-stage-3`

Then create a `.babelrc` file in your home directory of the project with this content:

```
{
    "plugins": ["transform-runtime"],
    "presets": ["es2015", "stage-3"]
}
```

## All set! 🚀

We did a lot of setup getting webpack, babel, and other modules we will need installed. Now we are ready to write some Express code!




