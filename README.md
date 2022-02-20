# face-detect
Face Detection for authentication

## Step 1: Initialize NPM (Node Package Manager)
cd face-detect
npm init --y

## Step 2: Install React, Webpack, and Babel
npm install react react-dom 
npm install --save-dev webpack webpack-cli webpack-dev-server html-webpack-plugin @babel/core babel-loader @babel/preset-env @babel/preset-react

## Step 3: Create the files
Let's create the files now.

touch webpack.config.js
mkdir src
cd src
touch index.js
touch index.html


### webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  // the output bundle won't be optimized for production but suitable for development
  mode: 'development',
  // the app entry point is /src/index.js
  entry: path.resolve(__dirname, 'src', 'index.js'),
  output: {
  	// the output of the webpack build will be in /dist directory
    path: path.resolve(__dirname, 'dist'),
    // the filename of the JS bundle will be bundle.js
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
      	// for any file with a suffix of js or jsx
        test: /\.jsx?$/,
        // ignore transpiling JavaScript from node_modules as it should be that state
        exclude: /node_modules/,
        // use the babel-loader for transpiling JavaScript to a suitable format
        loader: 'babel-loader',
        options: {
          // attach the presets to the loader (most projects use .babelrc file instead)
          presets: ["@babel/preset-env", "@babel/preset-react"]
        }
      }
    ]
  },
  // add a custom index.html as the template
  plugins: [new HtmlWebpackPlugin({ template: path.resolve(__dirname, 'src', 'index.html') })]
};



### src/index.js
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<h1>Helloworld React!</h1>, document.getElementById('root'));

### src/index.html
<html>
  <head>
    <title>Hello world App</title>
  </head>
  <body>
  <div id="root"></div>
  <script src="bundle.js"></script>
  </body>
</html>


## Step 4: Create NPM run scripts
Modify package.json scripts property to include the following npm scripts:

  // package.json
    ...
  "scripts": {
    "start": "webpack-dev-server --open",
    "build": "webpack"
  },
  ...
