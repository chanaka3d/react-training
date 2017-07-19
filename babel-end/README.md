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



