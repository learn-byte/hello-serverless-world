# Making a Call to Our Lambda

### With a button that clicks we are ready to do something more exciting.  Let's make an API call to our Lambda to fetch our "hello world!" greeting

To start let's install `axios` which will make it easy to make HTTP requests from our React client. 

`npm install --save axios`

Great!  We are ready to refactor our `handleClick()` function.

Let's refactor the `handleClick()` function be an anonymous ES6 arrow function. This anonymous function will correctly bind the `this` keyword so that we will be able to call it when we `setState()`. Read (more about ES6 arrow functions here)[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions].

We will also add our api call to the `handleClick()` function using the `axios` module we just installed.

It will become:

```
    handleClick = () => {
        axios.get(`https://e9pa7v3btg.execute-api.us-west-2.amazonaws.com/dev/hello`)
            .then(res => {
                this.setState({ greeting: res.data });
            })
    }
```

We are now making a `GET` request to our Lambda at the endpoint that serverless returned to us when we initially launched the lambda with `serverless deploy`.  Your endpoint will obviously be different than the one shown here.

---

### Adding the Constructor

We need to implement a constructor at the top of our React component in order to utilize local state information.  The constructor is the first method called when the comoponent is instantiated.  This is where we will define the initial value of our greeting state.

The constructor is an important part of React, more information can be (found at the official React docs)[https://reactjs.org/docs/react-component.html#constructor]. 

```
    constructor(props) {
        super(props);
        this.state = { greeting: '' };
      }
```

We declare the greeting to be equal to an empty string for now.  When the data is fetched it will become "hello world!"

---

### Rendering the Greeting

Finally, the last part we need to accomplish is rendering the greeting into the (DOM)[https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model] where the user will see it. 

Let's update our `render()` function to include a new greeting displayed with `this.state.greeting`.

```
    render() {
        return (
            <div>
                <h2>Greeting Page</h2>
                {this.renderButton()}
                <h3>The greeting is: {this.state.greeting}</h3>
            </div>
        );
    }
```

---

#### Boom! There is our greeting response from our Lambda deployed into AWS, hello world!

There's a lot we can do with this knowledge.  By adding more Lambda endpoints to Create Read Update and Delete we can have a working application with many features. 

![greeting-works](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/greeting-works.png)

This endpoint is working.  Let's add another endpoint to our Lambda now! 💪