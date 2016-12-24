# React Fast

So, you're interested in React?!

You might have played with it a bit, or a lot, or maybe never. You heard React development is awesome but there's lots to read up on and you don't want to wade though it all slowly. You want to get going with React, fast.

You have come to the right place!

Here you will find an opinionated (but good ;-) way to develop great React apps. We think React, Redux, Storybook, React CDK and React Native work well together. Under the bonnet this will introduce yoman, watchman, babel, eslint, mocha, webpack and more. It's written for macOS but we would welcome translations for other OS's.

You can run every command in this document; it's been tested and should work fine if you run them in the order they appear. It's unlikely to work if you skip around but you can miss out the stuff marked **OPTIONAL**.

Finally, you might find the steps are in a strange order. The approach is to do stuff, then explain what is going on. Hope you enjoy it, buckle up and let's go...

## Prerequisites

Bare minimum:
- `node` (> v4.x.x). Node.js. ([website](https://nodejs.org/))
- `npm` (> v3.x.x). A JavaScript package manager. ([website](https://docs.npmjs.com/cli/npm))

If you want to build React native apps consider:
- `Xcode`. Apple's IDE. ([website](https://developer.apple.com/xcode/))
- `Android Studio`. Google's IDE for Android. ([website](https://developer.android.com/studio/index.html))

Optionally:
- `git` (> v2.x.x). The version control system. ([website](https://git-scm.com/))
- `atom`. Or some other text editor. ([website](https://atom.io/))
- `brew`. *The missing package manager for macOS*. ([website](http://brew.sh/))

`brew` can speed you up, and is way nicer than installing things manually, for example:
```bash
$ brew install node
$ brew install npm
$ brew install git
```

# PART 1 - Getting Started

## Create React App
([github](https://github.com/facebookincubator/create-react-app),
[npm](https://www.npmjs.com/package/create-react-app))

`create-react-app` is an officially supported CLI tool for creating React apps. It offers a modern build setup with no configuration. Install it using `npm`.
```bash
$ npm install -g create-react-app
```
## React

([github](https://github.com/facebook/react), [npm](https://www.npmjs.com/package/react), [website](https://facebook.github.io/react/))

The *JavaScript library for building user interfaces*. The thing you're here for right? Create a React app as follows.

```bash
$ create-react-app my-app
$ cd my-app
$ npm start
```

Your app should now be running on http://localhost:3000/, take a look.

## Your First Line of Code

The homepage of your app is suggesting you edit `src/App.js`, so let's do it:

1. **OPTIONAL** Your first terminal shell is tied up running you app so get a second in the `my-app` directory. In the first terminal this macOS keystroke will get you a second:

  Press `⌘ T`


2.  **OPTIONAL** Set up git to manage your code.
  ```bash
  $ git init; git add .; git commit --m "First commit!"
  ```

3. If you did the optional steps git lists the files being committed nicely. These make up a skeleton, aka<sup>[1](#myfootnoteaka)</sup> template, aka scaffolding, aka starter React app. They are:

  ```bash
  .gitignore           # Only version control the files needed
  README.md            # Read or replace it
  package.json         # Take a look and edit the boilerplate stuff if you want
  public/favicon.ico   # Replace this one day
  public/index.html    # First page sent to the browser
  src/App.css          # Styles for App.js
  src/App.js           # The only React component so far
  src/App.test.js      # Unit tests for App.js
  src/index.css        # Styles for index.js
  src/index.js         # Bootstraps the React app
  src/logo.svg         # React's logo
  ```

4. Open `src/App.js` in an editor of your choice. If you're using atom you could open the `my-app` directory as a project folder from the command line with:
```bash
$ atom .
```

5. Change the line which begins with "To get started..." to something like this:
```html
<p className="App-intro">
  I just edited <code>src/App.js</code> and saved it.
</p>
```

5. Save `App.js` and...


#### What happened?

Hopefully your browser updated live. But how? In short, the webpack dev server triggered a rebuild of the React app and refreshed the client side code in the browser, using Hot Module Replacement (HMR). If you want to know the details [check this out](Webpack-dev-server.md). <a name="back-from-webpack-dev-server"></a>


## So Where's the React bit?

Take a look at the code in `/src`.

`App.js` introduces a React Component. It's written in ES6 (notice the import, export and class statements?) and using JSX (notice the inline XML? Think JavaScript + XML = JSX).

`import ... Component ... from 'react'` and  ` class App extends Component` tells you `App` is a React Component. React Component's have a `render()` function which typically returns some JSX.

`index.js` shows where the `App` component is rendered into the DOM.

Take a look at `App.js`. The JSX returned from the `render()` function is very similar to the html you want to render into the browser's DOM, but with some differences:

 - Lower case JSX elements elements refer to their html equivalent, e.g.
 ```js
 <div></div>
 ```
 - Upper case JSX elements refer to React components. e.g.
 ```js
 <App/>
 ```
 - JSX is closer to JavaScript than html, so attributes follow the camelCase naming conversion used for [JavaScript element properties](https://developer.mozilla.org/en-US/docs/Web/API/Element). So this in JSX:
 ```js
 <div className="myclass" tabIndex="1"></div>
 ```
 becomes this in html:
 ```js
 <div class="myclass" tabindex="1"></div>
 ```
 - Inside JSX, anything wrapped in curly braces will be evaluated as a JavaScript expression. e.g. all these are valid:

 ```js
 <pre>{1 + 2}</pre>
 <h2>{story.title}</h2>
 <div>{story.getBody()}</div >
 ```
 - `if`, `for`, `while`, `switch` are not JavaScript expressions, they are control flow and loop statements, so this isn't valid (plus it's really ugly!):

 ```js
 <h2>{if(err){}
    "Something is wrong";
 {}else{}
    "All is good";
 {}}</h2>
 ```
 - But you can use JSX like a regular JavaScript object so this is valid:

 ```js
 if(err){
    return <h2>Something is wrong</h2>;
 }else{
    return <h2>All is good</h2>;
 }
 ```
 - Arrays of JSX objects get flattend as follows:
 ```js
 var listItems = [<li>One</li>,<li>Two</li>,<li>Three</li>];
 return <ul>{listItems}</ul>
 ```
 - Bringing all these techniques together, you can do things like this:
 ```js
// a conditional statement
var message = err ? <h2>Something is wrong</h2> : <h2>All is good</h2>;
// an array and a loop
var list = ["One","Two","Three"];
var listItems = list.map(function(item){return <li>{item}</li> });
// combining a JSX object and JSX array into another JSX object
return <div>
  <div>{message}</div>;
  <ul>{listItems}</ul>
</div>;
 ```

**OPTIONAL** At this stage you could start learning more about React components and JSX with the official tutorial [here](https://facebook.github.io/react/tutorial/tutorial.html). Come back here when your done, or keep going! (You can always learn the finer details of  components and JSX later.)


## Part 1 Wrap Up

React is a JavaScript library for building user interfaces. `create-react-app` is a command line tool for creating a bare bones React app; it includes scripts to compile the ES6 and JSX code you write into a standard JavaScript bundle (take a look at `package.json` and you'll see they are called react-scripts). In development mode this is done live by the webpack dev server, which triggers the compilation and a hot module reload (MHR) of code in the browser when you save your changes (just run `npm start`). For production the compilation outputs a compressed build optimised for performance (just run `npm run build`).

A core concept of a React app is components which are independent, reusable pieces of UI. They manage their own state and can be rendered in the browser, on a server using Node or in mobile apps using React Native.

# PART 2 - Picking Up Speed

Storybook helps you develop and design components outside your app in an isolated environment; *"It will change how you develop [React] UI components"*.

# Get Storybook

`getstorybook` is a CLI tool for adding Storybook to React apps. See [github](https://github.com/kadirahq/getstorybook) [npm](https://www.npmjs.com/package/getstorybook).

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

You'll get a URL, something like `http://localhost:9009/`, so open it up and have a look. This is a Storybook, containing a single Welcome story and two stories about Button. Runnning your React app like we did in Part 1 (with `npm start`) is good for seeing your components as you intend them to be, all together in one app. Running storybook (with `npm run storybook`) allows you to see your components in isolation and in different scenarios. Both approaches use the webpack dev server so any edits you make to the source code are updated in the browser using HMR.

# Write a Story

Edit `/src/stories/index.js` and add a new story at the bottom, like:

```js
storiesOf('Mini Profile', module)
  .add('with no data', () => (
    <MiniProfile/>
  ))
```
This is specifying stories about something called a "Mini Profile". The first story is "Mini Profile with no data". Save the file and the storybook at http://localhost:9009/ will refresh. Click on "Mini Profile" on the left hand side and you get an error "MiniProfile is not defined", which makes sense, because you haven't defined it yet...

# Defining a Component

Create `/src/MiniProfile.js` and start with a basic React Component:

```js
import React, { Component } from 'react';

export default class MiniProfile extends Component {
  render() {
    return (
      <div>This is a Mini Profile</div>
    );
  }
}
```

In `/src/stories/index.js` import your new component with:

```js
import MiniProfile from '.../MiniProfile';
```

Congratulations, you just fixed a bug! Now Let's make the mini profile look a little nicer. Change the JSX of the Mini Profile component to be:

```js
<div className="miniprofile">
	<div className="avatar" style={{backgroundImage: "url(" + (user.profileImg || "https://github.com/aogriffiths/reactfast/raw/master/userprofile.png") + ")"}}></div>
	<h1 className="name">{user.name || "Name"}</h1>
	<h2 className="tagline">{user.tagline || "Tagline"}</h2>
</div>
```

But it lacks style. Create `/src/MiniProfile.css` as follows (adapted from original css by (Pat.ch)[http://cssdeck.com/labs/profilesbypatch/]):

```css
.miniprofile {
	width: 400px;
	height:100px;
	background: #f1f1f1;
	overflow: hidden;
	border: 1px solid #f3f3f3;
	border-radius: 4px;
	box-shadow: 0 1px 2px;
}

.avatar {
	background-size: cover;
	background-position: center;
	width: 100px;
	height: 100px;
	margin: 0px auto 0px 0px;
	border-radius: 50%;
	float: left;
  box-shadow: inset 0 0 0 2px #3f3f3f;
}

.name{
	margin: 0 0 0 110px;
	font-size: 28px;
	color: #030303;

}

.tagline{
	margin: 0px 0px 25px 110px;
	font-size:13px;
	color: #B9B9B9;
}
```

Now here's the really neat part you can import css into your React component by adding the following to `/src/MiniProfile.js`:

```js
import './MiniProfile.css';
```

And the styles have been applied. The cleverness here isn't a React thing, it's webpack, which has detected the `import` statement and packed the `MiniProfile.css` css into the JavaScript bundle. In the browser this is unpacked into `<style>` tags. Webpack's HMR works with this too; add this to `/src/MiniProfile.css` and the fonts will update live in the browser:

```css
.avatar, .tagline, .name {
	font-family: sans-serif;
	font-weight: normal;
	pointer-events: none;
}
```

 If you want to find out more about how webpack works see [here]([http://webpack.github.io/), and for HMR specifically see [here](http://webpack.github.io/docs/hot-module-replacement-with-webpack.html).


## Redux

So you've seen how state needs to be kept immutable using `setState()` but as your app scales there's going to be more challenges. How do components share state - the "readers" of state? Which components can change state - the "writers" of state? How do the writers consistently notify the the readers?

Enter Redux, *a predictable state container for JavaScript apps*. The Key concepts are:
    * **Store State**: The state of your whole application is stored in an object tree within a single store.
    * **Write State with Actions and Reducers**: The only way to change the state tree is to emit an action, an object describing what happened. To specify how the actions transform the state tree, you write a reducer function.
    * **Reading State with Subscribers**: Any part of your app which is dependant on the data in the state tree subscribes to the store to get notified when it changes.

Redux can be used in any app, react-redux provides the official React bindings for Redux:

```bash
$ npm install --save react-redux
```

First let's consider the shape of our store. Something like this:

```json
{
  "users":[
    {
      "id":"1234567789",
      "name":"Full Name"
    }, ...
  ],
  "display": "ALL"
}
```

Now let's define the types of Actions which can happen to the store as constants:
```js
//file: /src/actionTypes.js
const SET_USERS = "SET_USERS";     //fills the store with an initial set of users
const ADD_USER = "ADD_USER";       //Add one new user to the store
const REMOVE_USER = "REMOVE_USER"; //Remove one user from the store
const UPDATE_USER = "UPDATE_USER"; //Change the data for one user in the store
const SHOW_USER = "SHOW_USER";     //Change the display status to a single user
const SHOW_ALL_USERS = "SHOW_ALL_USERS"; //Change the display status to all users
```

And some helper functions to create actions, these might seem a bit basic to state with, but by keeping them together in one place you can be sure actions are always created consistently:



```js
//file: /src/actionCreators.js

let nextUserId = 0;

export const setUsers = (userlist) => {
  return {
    type: 'SET_USERS',
    users: userlist,
  }
}

export const addUser = (user) => {
  return {
    type: 'ADD_USER',
    user: {
      ...user,             // take the user data given as a base
      "id":nextUserId++};  // add a unique id to it. (this is not a production ready approach!)
  }
}

export const removeUser = (userid) => {
  return {
    type: 'REMOVE_USER',
    userid: userid,
  }
}

export const updateUser = (user) => {
  return {
    type: 'UPDATE_USER',
    user: user,
  }
}

export const showUser = (user) => {
  return {
    type: 'SHOW_USER',
    user: user,
  }
}

export const showAllUsers = () => {
  return {
    type: 'SHOW_ALL_USERS'
  }
}
```

Now let's write a reducer function, it should have the signature `(previousState, action) => newState` and be a *pure* function, which means given the same arguments it MUST return the same results. The kinds of things it MUST NOT do are:
   * Mutate its arguments;
   * API calls and routing transitions;
   * Call non-pure functions like Date.now() or Math.random().

Also, there's a really neat pattern to writing reducers, but in order to understand, its best to work up to it.

First off here's a basic reducer. If there's no state it returns an initial state, otherwise it  returns the current state unchanged. It ignores any action.

```js
const initialState = {
  "users":[],
  "display": "ALL"
}

function mainReducer(previousState, action) {  
  if (typeof previousState === 'undefined') {
    return initialState;
  }else{
    return previousState;
  }
}
```

Using the [ES6 default arguments syntax](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/default_parameters) the reducer can be simplified to:

```js
function mainReducer(previousState = initialState, action) {  
  return previousState;
}
```

Now let's handle out first action:

```js
import * as actionType from './actionTypes';
// .. define initialState here
function mainReducer(previousState = initialState, action) {  
  switch (action.type) {
    case actionType.SET_USERS:
      var newState = {};
      newState.display = previousState.display;
      newState.users = action.users;
      return newState;
    default:
      return previousState;
  }
}
```

Notice how newState is a new object and previousState is not mutated? There's a more succinct way of returning a new state based on previousState:

```js
    case actionType.SET_USERS:
      return { ...previousState,
         users: action.users
      };
}
```

Now lets handle the add, remove, update, show user and show all users actions:


```js
case actionType.ADD_USER:
  return { ...previousState,
    users: [
      ...users,
      action.user
    ]
  };
case actionType.REMOVE_USER:
  return { ...previousState,
    users: previousState.users.filter(user => user.id != action.userid)
  };
case actionType.UPDATE_USER:
  return { ...previousState,
    users: previousState.users.map(user => user.id == action.user.id ? action.user : user)
  };
case actionType.SHOW_USER:
  return { ...previousState,
    display: action.user.id
  };   
case actionType.SHOW_ALL_USERS:
  return { ...previousState,
    display: "ALL"
  };
```

Notice how `mainReducer` is getting large and also how four of the cases (set, add, remove and update) effect just the users part of the tree while two of the cases (show and show all) effect just the display part. We can break things down using reducer composition which is a de-facto pattern in Redux.

```js
function mainReducer(previousState = initialState, action) {  
  switch (action.type) {
    case actionType.SET_USERS:
    case actionType.ADD_USER:
    case actionType.REMOVE_USER:
    case actionType.UPDATE_USER:
      return { ...previousState,
        users: usersReducer(previousState.users, action)
      };
    case actionType.SHOW_USER:
    case actionType.SHOW_ALL_USERS:
      return { ...previousState,
        display: displayReducer(previousState.display, action)
      };
    default:
      return previousState;
  }
}
```
`usersReducer` and `displayReducer` can now focus on just a subset of the actions and a subtree of the state. As so:

```js
function usersReducer(previousState, action) {  
  switch (action.type) {
    case actionType.SET_USERS:
      return action.users;
    case actionType.ADD_USER:
      return  [...previousState, action.user];
    case actionType.REMOVE_USER:
      return previousState.filter(user => user.id != action.userid);
    case actionType.UPDATE_USER:
      return previousState.map(user => user.id == action.user.id ? action.user : user)
    default:
      return previousState;
  }
}

function displayReducer(previousState, action) {  
  case actionType.SHOW_USER:
    return action.user.id;
  case actionType.SHOW_ALL_USERS:
    return "ALL";
  default:
    return previousState;
}
```

That's cut some code out but we can go further, the main reducer doesn't need the switch statements at all, it can just defer to the other reducers as so:

```js
function mainReducer(previousState = initialState, action) {  
  return {
    users: usersReducer(previousState.users, action),
    display: displayReducer(previousState.display, action)
  }
}
```

This is such a common pattern redux produces a helper function to combine reducers as so:

```js
import { combineReducers } from 'redux'

const mainReducer = combineReducers({
  users: usersReducer,
  display: displayReducer
})
```

And if you want to be really efficient rename your reducers to match the part of the state tree they work on as so:

```js
import { combineReducers } from 'redux'

const initialState = {
  "users":[],
  "display": "ALL"
}

const mainReducer = combineReducers({
  users,
  display
});

function users(state = initialState.users, action) {  
  switch (action.type) {
    case actionType.SET_USERS:
      return action.users;
    case actionType.ADD_USER:
      return  [...state, action.user];
    case actionType.REMOVE_USER:
      return state.filter(user => user.id != action.userid);
    case actionType.UPDATE_USER:
      return state.map(user => user.id == action.user.id ? action.user : user)
    default:
      return state;
  }
}

function display(state = initialState.display, action) {  
  case actionType.SHOW_USER:
    return action.user.id;
  case actionType.SHOW_ALL_USERS:
    return "ALL";
  default:
    return state;
}
```

Now you have actionTypes, actionCreators and reducers you can add the redux store to your app. in index.js create the  store with `createStore()` and provide it to your app with the `<Provider>`  component:

```js
import { createStore } from 'redux';
import { Provider } from 'react-redux'
import mainReducer from './reducers';
let store = createStore(mainReducer);

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

You could now pass store to child components and use it directly but the React Redux way is to use the connect function


## React Router

```bash
$ npm install --save react-router
```



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

## Footnotes
<a name="myfootnoteaka">1</a> "aka" abbreviates "also know as"
