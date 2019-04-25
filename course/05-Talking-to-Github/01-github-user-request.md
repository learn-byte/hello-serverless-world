# Making an API request in a Lambda to Github

### We should add some more interesting functionality to our application.

###Let's get any user's Github inofrmation from our Lambda so we can return it to our web app.

Hop back over to your Lambda code and start off by adding a new file. Call it `getUser.js` since we be getting our user information back from it.  You can be more specific like `getGithubUser.js` if you want.

We are going to make our API call using axios.  Axios is a promise based HTTP client so we will set up our `getUser()` function to return a Promise.  If you're new to promises you can [read about them here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).  The name describes fairly well what they are.  A promise to return a value at some later time. 

Here's what the file ends up looking like:

```
import axios from 'axios';

export default function getUser(username) {
    return new Promise(resolve => {
        axios.get(`https://api.github.com/users/${username}`)
        .then(function (response) {
          resolve({ message: response.data });
        })
        .catch(function (error) {
          console.log(error);
        })
    })
};
```

We make a `GET` request to Github's users endpoint and send along a `username` string which we will pass into this function.  Then we'll return the data from the response if all goes well, else for now we will just log the error.

---

### Great! Now we need to import this new function into our index.js file and invoke it

Start off by importing the function at the top of the file:

`import getUser from './getUser';`

Next, we'll create a new `GET` endpont.  Let's call it `/user`.  It is similar to the `/hello` we already made.  The biggest difference is that we will be invoking an async function in this endpoint and make a request to our `getUser()` function using the `await` keyword. 

[Async/await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) is a fairly new feature which came out in 2017, it makes writing asynchronous functions legible and easy to reason about. 

Here's what our endpoint looks like:

```
app.get('/user', function (req, res) {
    async function user() {
        try {
            const username = req.query.name;
            const user = await getUser(username);
            res.send(user);
        } catch (e) {
            console.error(e);
        }
    }
    user();
});
```

---

### Finish up and get it deployed!

There's only one more step before we deploy this Lambda.  We need to add this new function to our `serverless.yml` file so that it is deployed as an endpoint in API Gateway.

Add this declaration to your `serverless.yml` file under the `functions` key just like the `hello` declaration.

```
  user:
    handler: src/index.handler
    events:
      - http: 'GET /user/'
```

#### All set! We are ready to deploy

Run: 

`sls deploy`

To get this launched in AWS.  Your Lambda function you previously deployed will be replaced with this new Lambda we wrote.

Hit the new endpoint!
https://e9pa7v3btg.execute-api.us-west-2.amazonaws.com/dev/user?name=octocat

![user-request](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/user-request.png)

Success 👏
