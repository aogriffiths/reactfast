#React Fast

You are interested in React?!

You might have played with it a bit, or a lot, or maybe never. You heard React development can be really, really awesome but there is lot's of advice and choices and you don't want to wade though it all slowly, you want to get going fast.

You have come to the right place!!

Here you will find an opinionated (but good ;-) way to develop great React apps. We think React, Redux, Storybook, React CDK and React Native work well together. Under the bonnet this will introduce yoman, watchman, babel, eslint, mocha, webpack and more.

You can run every command in this document in the order they appear. It's been tested and it usually works fine ;-). It will reduce your changes if you skip around but things you can miss out are marked as **OPTIONAL**.

Finally, you may find the steps are in a strange order. The approach this guide takes is to do stuff, then explain why afterwards.

So, buckle up and let's go...

# Prerequisites

Install these:

- node (> v4.x.x)
- npm (> v3.x.x
- git (> v2.x.x)

They all take the `--version` option so you can check they are installed.

# Create React App

A CLI tool to create React apps (
[github](https://github.com/facebookincubator/create-react-app)
[npm](https://www.npmjs.com/package/create-react-app))

Install it:
```bash
$ npm install -g create-react-app
```

# React

The *javascript library for building user interfaces* which you're here for! (
[github](https://github.com/facebook/react) [npm](https://www.npmjs.com/package/react) [website](https://facebook.github.io/react/)).

Create a starter React app and run it like this:

```bash
$ create-react-app my-app
$ cd my-app
$ npm start
```

Your app should now be running on http://localhost:3000/, take a look. It's suggesting you edit `src/App.js` so let's do it.

1. Get a second shell up in the `my-app` directory.

2. Set up git to manage your code. (In case you were wondering `create-react-app` gave you a suitable `.gitignore`.)
```bash
$ git init; git add .; git commit -m"init"
```

3. Open `src/App.js` in an editor of your choice.

2. Set your screen up so you can see your editor, the shell you ran `npm start` from and a web browser pointing to `http://localhost:3000/`. See screenshot below.
3.


At this stage you could start building React components the basic way see [here](https://facebook.github.io/react/tutorial/tutorial.html) **OPTIONAL**. But read on for the Storyboard way.



# What are Components and Storyboard anyway?

In React, components are independent, reusable pieces of UI. They manage their own state and can be rendered in the browser, on a server using Node or in mobile apps using React Native.

Storybook helps you develop and design components outside your app in an isolated environment. *It will change how you develop UI components*.

# Get Storybook

Get Storybook is a CLI tool for adding Storybook to React apps. See [github](https://github.com/kadirahq/getstorybook) [npm](https://www.npmjs.com/package/getstorybook).

Install it:
```bash
$ npm install -g getstorybook
```

# Use Storybook
[github](https://github.com/kadirahq/react-storybook) [website](https://getstorybook.io/)

You can now add Storybook to your project and run it.
```bash
$ getstorybook
$ npm run storybook
```

# Write a Story




###React Component Development Kit
The Tool: github [kadirahq/react-cdk](https://github.com/kadirahq/react-cdk). npm [generator-react-cdk](https://www.npmjs.com/package/generator-react-cdk)
npm install -g yo generator-react-cdk

#Addendum

In writing these documents we tested out all commands using a empty ubuntu docker container. It's an easy way to get a clean environment. We have also tested it on our own mac books but would welcome your help. Feel free to buy us an brand new mac or alternativly run these instructions on yours.

1. Get a nice blank machine to work on
  - Ubuntu: maybe follow these instructions https://docs.docker.com/engine/examples/running_ssh_service/
  - Mac: Uh... buy a new machine?
2. Install node and npm [see here](https://nodejs.org/en/download/package-manager)
  - Ubuntu: apt-get install nodejs npm nodejs-legacy
  - Mac: brew install node
3. Git
