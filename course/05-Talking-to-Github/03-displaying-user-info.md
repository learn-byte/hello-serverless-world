# Displaying our profile

### We have all the data we need to render information about our Github user. There's nothing to it but to do it!

Let's make a new component which will render our User Profile.  We will pass the data down from the `Home.js` component through props. Props can be any data type that we like.  We are able to pass data down to child components through props.  

Take a look at our new `Home.js` file where we have imported a new `UserProfile.js` dependency and are rendering that dependency and passing a `user` prop with our Github API result in it:

```
import React, { Component } from 'react';
import axios from 'axios';

import UserProfile from './UserProfile';

class Home extends Component {
    constructor(props) {
        ...
    }
    handleClick = (event) => {
        ...
    }
    handleChange = (event) => {
        ...
    }
    renderForm() {
        ...
    }
    render() {
        return (
            <div>
                <h2>Home Page</h2>
                {this.renderForm()}
                <br />
                <UserProfile user={this.state.user}/>
            </div>
        );
    }
}

export default Home;

```

---

### With our Home page requiring a new UserProfile dependency let's go ahead and make it

Create a new file in the `src` directory called `UserProflie.js`.  In this component we will have access to a `user` prop which we have declared in the parent component. 

We are using a ternary function to conditionally render the content of the User Profile.  If we have a profile login we will render the User Profile else we'll just render some empty `<div></div>`.

```
import React, { Component } from 'react';


class UserProfile extends Component {
    renderUserProfile(){
        return (
            <div>
                <h4>User Profile</h4>
                <img width={"120"} src={this.props.user.avatar_url} />
                <h3>{this.props.user.login}</h3>
                <h4>Created at: {this.props.user.created_at}</h4>
                <h4>Github profile: <a href={this.props.user.html_url}>{this.props.user.html_url}</a></h4>
            </div>
        )
    }
    render() {
        const profile = this.props.user.login !== undefined ? this.renderUserProfile() : <div></div>;
        return (
            profile
        );
    }
}

export default UserProfile;
```

---

### Check it out! Our final working product! 

![octocat-profile](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/octocat-profile.png)

We're ready to iterate from here and create something even more interesting.  But before we start planning the next project let's get this all deployed. 😎

