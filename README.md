# babel-end sample
We are using babel to convert our ES6 javascript syntax to ES5 syntax. This is done because ES6 features are not supported by all the browsers.

Create a new directory and cd in to it ( say babel-start )
```
npm init
```
It will ask some questions. Press enter/return and accept the default options.

New file is created ( package.json )

Install babel-cli
```
npm install --save-dev babel-cli
```
Note that --save-dev is to specify babel is only needed at the development time.

Install babel-preset-es2015
```
npm install --save-dev babel-preset-es2015
```
Add the babel configuration json file ( .babelrc ) with the following command. This is to let babel know that we need to use the previously install es2015 preset.
```
echo '{"presets":["es2015"]}' > .babelrc
```

Create a new folder to ouput the generated file with babel.
```
mkdir dist
```

Create a new file to write our ES6 js code.
```
touch script.js
```

Add the following content to script.js
```
if(true){
  let foo=4;
}
console.info(foo);
```
Add a new task to the package.json file so it will run the babel command and conver the script.js file javascript syntax in to es5 syntax and put it in the dist directory.
```
{
......
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "babel script.js -d dist"
  }
  .......
}
```
Run the newly created task ( build )
```
npm run build
```
View the content in the dist/script.js file.
It contians ES5 syntax


# webpack-end sample
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

├── dist
│   └── index.html
├── package.json
├── src
│   └── index.jsx
└── webpack.config.js

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

## Copy and paste the following content to  src/index.jsx ( final version )

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




















