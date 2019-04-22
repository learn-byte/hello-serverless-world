# Interactive Button

#### Now that we have a `Hello` page setup, let's add some interactivity. 

Our end goal will be to add a button that allows the user to retrieve the greeting our Lambda returns at the `/hello` route. But to start out let's just get it rendering and showing basic interactivity in the console.

Let's jump right in!

---

### Create the Button

Let's start small by just getting a button to render in our React app.  We will do this work in our new `Hello.js` page. 

Let's create a couple new functions, one that will render the button, and one that will handle the `onClick` event from the rendered button.

Here is an idea for how we can create the `renderButton()` method. 

```
    renderButton() {
        return (
           <button onClick={this.handleClick}>
                Click to fetch greeting!
            </button>
        )
    }
```

As you can see we will be calling the handleClick method whenever the button is clicked on. Let's create that method now. 

```
    handleClick() {
        console.log('clicked!')
    }
```

To get started let's just log the word "clicked!" to the console.  We can add in the API call once we have the button calling our `handleClick` method correctly. 

Once we call the `renderButton()` method in our `render()` method we should see the button and be able to interact with it.  Here's our `Hello` page now:

```
import React, { Component } from 'react';


class Hello extends Component {
    handleClick() {
        console.log('clicked!')
    }
    renderButton() {
        return (
            <button onClick={this.handleClick}>
                Click to fetch greeting!
            </button>
        )
    }
    render() {
        return (
            <div>
                <h2>Hello Page</h2>
                {this.renderButton()}
            </div>
        );
    }
}

export default Hello;
```

---

#### Sure enough, the button "clicks!"

![button-clicking](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/button-clicks.png)

Move onto the next lesson to learn how to make an API call 📞
