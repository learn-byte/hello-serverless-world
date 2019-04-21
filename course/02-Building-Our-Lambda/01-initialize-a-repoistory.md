# Initialize a Repository

## Where should we store all this lovely code we will write?

#### There are many different version control and code repository services but we will be using Github.

![github-logo](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/github-logo.png)

You probably already know about Github and already have an account but if you don't then spend some time [learning about Github here](https://lab.github.com/githubtraining/introduction-to-github) and [get signed up for your account](https://github.com/join)!

---

### Once you're logged into your account [create a new Github Repository](https://github.com/new).

![new-github-repository](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/new-github-repository.png)

For this lambda service we we went with the name, `hello-world-serverless-lambda`. When we initialize our client repo we will call it `hello-world-serverless-client`. 

Add a description if you like, make it either public or private, and check "Initialize this repository with a README". 

Finally, from the dropdown add a .gitignore for Node, since we will be writing our Lambda using Express.js and Node.js.

Click `Create Repository`!

---

### Finally, let's get our repository cloned down to our local computer. 

Press the green "Clone or download" button and copy the "Clone with HTTPS" url from the popup. 

![clone-github-repository](https://raw.githubusercontent.com/learn-byte/hello-serverless-world/master/assets/images/clone-repo.png)

Then in a terminal window navigate to a directory where you'd like to store the code, and clone it down!

`git clone https://github.com/your-username/your-repo-name.git`

`cd your-repo-name`

Initialize your package.json with this command:

`npm init`

Finish up by stepping through each question of npm init by providing details for your app.

Let's move on to the next step where we'll install Serverless! 🐑
