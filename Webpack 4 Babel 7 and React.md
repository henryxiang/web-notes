# Webpack 4 + Babel 7 for React App Dev

## Dependencies
```bash
npm install -s \
    react \
    react-dom

npm install -D \
     @babel/core   \
     @babel/plugin-proposal-class-properties   \
     @babel/plugin-proposal-export-namespace-from   \
     @babel/plugin-proposal-throw-expressions   \
     @babel/plugin-syntax-dynamic-import   \
     @babel/polyfill   \
     @babel/preset-env   \
     @babel/preset-react   \
     babel-loader   \
     copy-webpack-plugin   \
     css-loader   \
     html-webpack-plugin   \
     mini-css-extract-plugin   \
     node-sass   \
     optimize-css-assets-webpack-plugin   \
     sass-loader   \
     style-loader   \
     uglifyjs-webpack-plugin   \
     webpack   \
     webpack-cli   \
     webpack-dev-server   \
     webpack-merge   \
     webpack-visualizer-plugin  
```

## Babel Configuration
```json
// .babelrc
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ],
  "plugins": [
    "@babel/plugin-syntax-dynamic-import",
    "@babel/plugin-proposal-class-properties",
    "@babel/plugin-proposal-export-namespace-from",
    "@babel/plugin-proposal-throw-expressions"
  ]
}
```

## Webpack Configuration
```javascript
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader'
        }
      },
      {
        test: /\.scss$/,
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
      },
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({ 
      template: './src/index.html', 
      filename: './index.html',
    }),
    new CopyWebpackPlugin({ from: 'src/static' }),
  ]
}
```
```bash
webpack-dev-server \
  --mode development \
  --config config/webpack.base.config.js \
  --open --hot --history-api-fallback
```

## References
1. [Webpack 4 and Babel 7 to create a fantastic React app](https://medium.freecodecamp.org/how-to-combine-webpack-4-and-babel-7-to-create-a-fantastic-react-app-845797e036ff)
1. [Set up React, webpack 4, and Babel](https://www.valentinog.com/blog/react-webpack-babel)
