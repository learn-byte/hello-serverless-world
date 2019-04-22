# Adding Routes To Our React App

### Let's extend our React app with new routes. We will create a "greeting" route which will eventually fetch our "hello world!" greeting from our lambda. 

Open up the React project in a text editor of your choice, I am a big fan of (VS Code)[https://code.visualstudio.com/] and its free price tag.

First off let's open up `App.css` and get rid of the default styles that `create-react-app` comes pre-baked with.

Delete everything except for the `.App` declaration and add a new declaration which will give padding around our navigation links.

```
.App {
  text-align: center;
}

.nav a {
  padding: 20px;
  display: inline-block;
  text-align: center;
}

```

This is what our new `App.css` should look like.

---

### Add react-router-dom

Next up we need to install `react-router-dom` in our project.  `create-react-app` comes with a very limited set of initial modules and allows the user to add whatever they need, including routing.  Install `react-router-dom` like so:

`npm install --save react-router-dom`

With `react-router-dom` in place we are all set to refactor our `App.js` to include routes.

Here's what we will want to end up with for our `App.js` file:

```
import React, { Component } from 'react';
import { BrowserRouter as Router, Route, Link } from "react-router-dom";
import Home from './Home';
import Hello from './Hello';

import './App.css';

class App extends Component {
  renderNav() {
    return (
      <div className="nav">
        <Link to="/">Home Page</Link>
        <Link to="/hello/">Greeting Page</Link>
        <hr />
      </div>
    )
  }
  render() {
    return (
      <div className="App">
        <Router>
          <div>
            {this.renderNav()}
            <Route path="/" exact component={Home} />
            <Route path="/hello/" component={Hello} />
          </div>
        </Router>
      </div>
    );
  }
}

export default App;
```

This will set us up with a very simple navigation component that links to our two planned pages, a `Home` page and a `Hello` page, which will show our greeting from our Lambda.

At this point the application will not render.  We need to define our Home page and our Hello page first.

---

### Creating new pages

To make our new pages we will need two new files.  Create `Hello.js` and `Home.js` in the `src` directory. 

These files will be very simple at first, we would just like to get our app rendering again before adding new content.  Here is what we should create for these pages:

```
import React, { Component } from 'react';


class Home extends Component {
    render(){
        return(
            <div>Home Page</div>
        );
    }
}

export default Home;
```

The `Home` page and the `Hello` page can be almost exactly the same for now.  We should create the `Hello` page to be the same as the `Home` page except replace the word `Home` for `Hello`.  
---

### App renders navigation

With these changes to our `App.js` page and the addition of our new `Home.js` and `Hello.js` we should be able to click between two pages. 

![simple-web-page](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/simple-web-page.png)

---

Next up we can add a little interactivity to our application! 🔥
