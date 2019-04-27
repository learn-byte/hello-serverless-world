# Building a React form that fetches our Github username

### Let's refactor our home page to use our new Github user endoint on our Lambda.

We will use all the concepts we have previously covered in the previous React lessons.  We will use local state and arrow functions to manage the user interaction via typing and clicking the form fields.

Here's how it will end up looking:

```
import React, { Component } from 'react';
import axios from 'axios';


class Home extends Component {
    constructor(props) {
        super(props);
        this.state = {
            user: {},
            username: 'octocat',
        };
    }
    handleClick = (event) => {
        const userUrl = 'https://e9pa7v3btg.execute-api.us-west-2.amazonaws.com/dev/user'
        axios.get(`${userUrl}?name=${this.state.username}`)
            .then(res => {
                this.setState({ user: res.data.message });
            })
        event.preventDefault();
    }
    handleChange = (event) => {
        this.setState({username: event.target.value});
    }
    renderForm() {
        return (
            <div>
                <form onSubmit={this.handleClick}>
                    <label>
                        <h3>Enter Github Username:</h3>
                        <input type="text" value={this.state.username} onChange={this.handleChange} />
                    </label>
                    <input type="submit" value="Get Github User" />
                </form>
            </div>
        )
    }
    render() {
        console.log('this.state.user', this.state.user)
        return (
            <div>
                <h2>Home Page</h2>
                {this.renderForm()}
            </div>
        );
    }
}

export default Home;
```

Don't forget to add `event.preventDefault();` to `the handleClick()` function.  If we don't add this the default behaviour for web forms refreshes the page and we will lose all of our local state.

We'll set a default `username` to `'octocat'` so that user's will have some default content they can load if they don't know any Github usernames.

This page doesn't render any content yet but it is all set for us to start rendering from `this.state.user`.

![enter-github-username](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/enter-github-username.png)

The response from our lambda, is successfully set to `this.state.user`.

Next up, let's render our profile! 👤