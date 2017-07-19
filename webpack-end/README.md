Webpack is use to get all the dependencies and our scripts and output it to a single javascript file. In the following example we are using babel to convert the ES6 syntax to ES5 syntax and JSX to React javascript. 

Create a new directory and cd in to it ( say webpack-start )
```
npm init
```
It will ask some questions. Press enter/return and accept the default options.

New file is created ( package.json )

Install the following devolopment dependencies
```
npm install --save-dev webpack
npm install --save-dev babel-core
npm install --save-dev babel-loader
npm install --save-dev babel-preset-es2015
npm install --save-dev babel-preset-react
```
Install dependencies
```
npm install --save react
npm install --save react-dom
```
Now create the following folder and file structure
```
├── dist
│   └── index.html
├── package.json
├── src
│   └── index.jsx
└── webpack.config.js
```
Add the babel configuration json file ( .babelrc ) with the following command. This is to let babel know that we need to use the previously install es2015 preset and react preset.
```
echo '{ "presets": ["es2015","react"] }' > .babelrc
```
## Copy and paste the following content to dist/index.html

```
<html>
  <head>
    <meta charset="utf-8">
    <title>React.js using NPM, Babel6 and Webpack</title>
  </head>
  <body>
    <div id="app" />
    <script src="bundle.js" type="text/javascript"></script>
  </body>
</html>
```

## Copy and paste the following content to webpack.config.js
```
var webpack = require('webpack');
var path = require('path');

var BUILD_DIR = path.resolve(__dirname, 'dist');
var APP_DIR = path.resolve(__dirname, 'src');

var config = {
  entry: APP_DIR + '/index.jsx',
  output: {
    path: BUILD_DIR,
    filename: 'bundle.js'
  },
  devtool: 'source-map',
  devServer: {
  	inline: true,
  	contentBase: BUILD_DIR,
  	port: 3333
  },
  module : {
    loaders : [
      {
        test : /\.jsx?/,
        include : APP_DIR,
        loader : 'babel-loader'
      }
    ]
  }
};

module.exports = config;
```

## Copy and paste the following content to  src/index.jsx

```
import React from 'react';
import {render} from 'react-dom';

class App extends React.Component {
  render () {
    return <p> Hello React hello</p>;
  }
}

render(<App/>, document.getElementById('app'));
```

## Now add the new build task to the package.json
```
"dev": "webpack-dev-server"
```
Run the newly created task ( dev )
```
npm run dev
```

Now you can browse to http://localhost:3333 to see the reults.




















