# Create our React App

### With our serverless lambda deployed, let's get our client set up to interact with the data our lambda is returning.

To start we need to initialize a repository for our client.  We can (follow the lesson)[/course/hello-serverless-world/02-Building-Our-Lambda/01-initialize-a-repository] where we created a repository for the lambda. 

Create a repository with a name like `hello-world-serverless-client`

---

### Create React App

From our newly created repository we will create a new React app.  Create React App let's us get up and running fast with a new React application. 

Check out (Facebook's documentation)[https://facebook.github.io/create-react-app/docs/getting-started] for more details on their officially supported Create React App template.

```
npx create-react-app hello-world-serverless-client
cd hello-world-serverless-client
npm start
```

Your app should start up at http://localhost:3000 in your browser. 

![create-react-app](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/create-react-app.png)

`create-react-app` ready to go.



