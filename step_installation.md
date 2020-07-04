## step 1
mkdir new-react-app
cd new-react-app
npm init --y
## step 2
npm install --save-dev @babel/core babel-loader @babel/preset-env @babel/preset-react html-webpack-plugin
npm i --save-dev webpack webpack-dev-server webpack-cli
npm i --save-dev react react-dom
## step 3
touch webpack.config.js
mkdir src
cd src
touch index.js
touch index.html

===========================================/webpack.config.js/============================================
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
============================================================================================================
========================================/src/index.html/====================================================
<html>
  <head>
    <title>Hello world App</title>
  </head>
  <body>
  <div id="root"></div>
  <script src="bundle.js"></script>
  </body>
</html>
============================================================================================================
========================================/src/index.js/======================================================
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<h1>Helloworld React!</h1>, document.getElementById('root'));
============================================================================================================


## step 4
add this to package.json
"scripts": {
    "start": "webpack-dev-server --open",
    "build": "webpack"
  },

## step 5
to start project 
npm build
npm start