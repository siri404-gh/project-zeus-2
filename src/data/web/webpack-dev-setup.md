# Webpack Dev Setup

## Summary

In the previous chapters, we saw how to setup the development environment, we pushed the initial set of code, we configured editorconfig, eslint, we created the entry point, configured babel to parse the javascript and we saw why we should compile and bundle the source code.

Because browsers dont support the latest features of Javascript, we use babel to compile our JS to ES5 format. We can tell webpack to do that. It compiles the code using babel bundles it to create an output file. You need to specify the configuration in a file called `webpack.config.js`. You can also have multiple config files for different environments. For eg, `webpack.dev.js` for Development and `webpack.prod.js` for Production. You just need to specify which environment to build for via command line. In this case, we have a `webpack.config.js` and a `webpack.dev.js` and we invoke it using:

```shell
webpack --env=dev --config=_webpack/webpack.config.js
```

## Install

```shell
npm i --save-dev webpack webpack-cli
```

## Configure

Create a file called `_webpack/webpack.config.js` and `_webpack/webpack.dev.js` at the root with the following code.

## Code for webpack.config.js

```js
module.exports = env => require(`./webpack.${env}.js`);
```

## Code for webpack.dev.js

```js
const path = require('path');

module.exports = {
  entry: {
    app: './src/client/index.js',
  },
  output: {
    path: path.resolve(__dirname, '../_dist'),
    filename: 'my-first-webpack.bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
    ],
  },
  mode: 'development',
};
```

## Execute

```shell
npx webpack --env=dev --config=webpack/webpack.config.js
```

The output will look like this. Notice the build time, asset name and the asset size. These are important.

![webpack dev code](/posts/web/webpack-dev-code.png "webpack dev code")

&nbsp;

## Concepts

### Entry

This is the entry file to tell webpack where to start the packaging from. In our case, its `src/client/index.js`.

### Output

This tells webpack where to output the end product. Also specified is the name of the file to be output as. So, all the code in our `src/client/index.js` will be output as `_dist/my-first-webpack-bundle.js`. If you look at the source code and the output code, they will look vastly different. The output will look like this given below.

![webpack dev output](/posts/web/webpack-dev-output.png "webpack dev output")

### Module

You need to tell webpack how to compile files. We specify this in the `module` section. In our config, we tell webpack to compile all the `.js` files using `babel-loader`.

Commit and push.
