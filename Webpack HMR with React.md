# Webpack Hot Module Replacement with Express.js and React.js

## Dependencies
```bash
npm install -D \
  webpack \
  webpack-dev-middleware \
  webpack-hot-middleware \
  express \
  react \
  react-dom \
  react-hot-loader
```

## Setup Webpack to use HMR
```javascript
// webpack.config.js
const path = require('path');
const webpack = require("webpack");

module.exports = {
    entry: [
      "webpack-hot-middleware/client?path=/__webpack_hmr&timeout=20000",
      "./src/index.js"
    ],
    output: {
      path: path.resolve(__dirname, "./public"),
      filename: "[name].bundle.js",
      publicPath: "/",
    },
    plugins: [new webpack.HotModuleReplacementPlugin()]
};
```

## Setup Express.js middleware
```javascript
// server/index.js
const express = require(“express”);
const webpack = require('webpack');
const webpackConfig = require('./webpack.config');
const webpackDevMiddleware = require('webpack-dev-middleware');
const webpackHotMiddleware = require('webpack-hot-middleware');

const app = express();
const compiler = webpack(webpackConfig);

//// Webpack HMR ////
app.use(
  webpackDevMiddleware(compiler, {
    hot: true,
    publicPath: webpackConfig.output.publicPath
  })
);
app.use(
  webpackHotMiddleware(compiler, {
    path: "/__webpack_hmr"
  });
)
```

## Setup React application
```json
// .babelrc
{
  "plugins": ["react-hot-loader/babel"]
}
```

```javascript
// App.js - mark the root component as hot-exported
import React from 'react'
import { hot } from 'react-hot-loader'

const App = () => <div>Hello World!</div>

export default hot(module)(App)
```

## References:
1. [Understanding Webpack HMR](https://www.javascriptstuff.com/understanding-hmr)
1. [Webpack HMR Tutorial](https://www.javascriptstuff.com/webpack-hmr-tutorial)
1. [Webpack HMR with Express](https://medium.com/@johnstew/webpack-hmr-with-express-app-76ef42dbac17)
1. [How to use Webpack with React](https://medium.freecodecamp.org/learn-webpack-for-react-a36d4cac5060)
1. [HMR with Webpack Middleware](https://blog.cloudboost.io/live-reload-hot-module-replacement-with-webpack-middleware-d0a10a86fc80)
1. [react-hot-loader](https://gaearon.github.io/react-hot-loader/getstarted/)
