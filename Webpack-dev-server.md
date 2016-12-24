
## Webpack Dev Server - The Details

**40,000 ft view**
 - When you ran `npm start` it started a [webpack dev server](https://webpack.github.io/docs/webpack-dev-server.html) to serve your app on http://localhost:3000
 - All your code in `/public` and `/src` is processed, compiled, linked, bundled up and delivered to the browser and just works!
 - If you change any source files the browser will refresh to use the latest version.

Enough detail? [go back](#back-from-webpack-dev-server)

**10,000 ft view**

To take a closer look fire up your browser's developer tools. Press `⌥ ⌘ I` in Chrome and go to the Network tab. Refresh the page and you should see a few requests.
 - [/](http://localhost:3000/) - routes to the files in `/public`.
 - [/static](http://localhost:3000/static) - routes, indirectly, to the code in `/src`.
 - [/sockjs-node/](http://localhost:3000/sockjs-node) - routes to a live socket connection which allows the webpack dev server to communicate with the browser and trigger a browser refresh when any source files change.

Enough detail? [go back](#back-from-webpack-dev-server)

**1,000 ft view**
- Content served by the webpack dev server is processed by webpack plguins.
- [/](http://localhost:3000/) - returns `/public/index.html`, processed by plugins including:
  - [InterpolateHtmlPlugin](https://www.npmjs.com/package/react-dev-utils) replaces ``%PUBLIC_URL%`` with `/`
  -  [HtmlWebpackPlugin](https://www.npmjs.com/package/html-webpack-plugin) injectcs `<script type="text/javascript" src="/static/js/bundle.js">` just before the `</body> tag`.
- [/static/js/bundle.js](http://localhost:3000/static/js/bundle.js) returns code in `/src` processed by [babel](https://babeljs.io/) which:
  - Converts any React JSX and ECMAScript 2015 in `.js` or `.jsx` files to ECMAScript 5 (i.e from JavaScript which web browsers don't support to JavaScript they do).
  - Includes any dependancies (i.e. the import statements in index.js and App.js).
  - Injects some client side socksjs code.
  - And bundles it all together into `bundle.js`.
- [/sockjs-node/](http://localhost:3000/sockjs-node) is base path used by the client socksjs code to connects to the server. When the server detects a change in one of your source files (using [watchman](https://facebook.github.io/watchman/) to monitor the filesystem) it uses this socket connection to alert the browser and trigger a refresh.

Enough detail? [go back](#back-from-webpack-dev-server)

**1 ft view**
- The webpack dev server is an express app, you can read the source code. If you're thinking you need to, consider finding out about the `npm run eject` which comes with `create-react-app` and will make the code and configuration easier to follow.

Enough detail? [go back](#back-from-webpack-dev-server)
