# ======Webpack 基础搭建

## 安装依赖

**安装 webpack 以及 webpack-cli（使用 webpack 必须的依赖）安装 webpack-dev-server（用于调试，热更新等）**

```js
yarn add webpack webpack-cli webpack-dev-server -g
```

## 一、构建项目目录结构

## 二、在 main.js 中

```js
alert("Webpac Test");
```

## 三、在 Webpack.config.js 中

```js
const path = require("path");
module.exports = {
  //输入文件
  entry: "./src/main.js",
  // 输出文件
  output: {
    path: path.resolve(__dirname, "./dist"),
    publicPath: "/dist/",
    filename: "app.js"
  },
  // /本地开发/服务
  devServer: {
    historyApiFallback: true,
    overlay: true
  }
};
```

**entry：要打包的 js 文件
path:最后生成文件的路径
publicPath:使用调试模式时文件的位置
filename:最后生成的文件名**

## 四、在 index.html 加上

```html
<script src="/dist/app.js"></script>
```

## 五、改动 package.json 的 script 脚本

```json
"scripts": {
    "serve": "webpack-dev-server --open --hot",
    "build": "webpack --progress --hide-modules"
  }

```

## 测试

```js
运行 npm run serve
```

# =============Babel

**用来适配新语法的 加入一些语法，如箭头函数，let**

## 安装依赖

```js
npm install babel-loader @babel/core @babel/preset-env babel-polyfill
```

**还有一点要提的是 babel 默认只转换新的 JavaScript 句法（syntax），而不转换新的 API，比如 async/await。若想要转化的话要使用 babel-polyfill 关于 babel-polyfill 的话，它提供一个环境让浏览器可以使用不支持的那些语法，比如旧的浏览器中不支持 await，则 babel-polyfill 会在全局定义一个 await 并实现它，到最后浏览器就可以正常使用。**

## 在根目录创建.babelrc 文件（用于配置），现在我们先放空

```js
{
}
```

## 改动 webpack.config.js

```js
const path = require("path");
// const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装

module.exports = {
  // 入口文件
  entry: ["babel-polyfill", "./src/main.js"], //使用babel-polyfill 转义
  // 输出文件
  output: {
    path: path.resolve(__dirname, "./dist"),
    publicPath: "/dist/",
    filename: "app.js"
  },
  // 本地开发
  devServer: {
    historyApiFallback: true,
    overlay: true
  },
  //
  module: {
    rules: [
      //解析js新语法
      {
        // test说明需要处理的文件类型，exclude是要忽略的文件，use中就是处理的方法
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env"]
          }
        }
      }
    ]
  }
};
```

## 用 es6 中的 async/await 试一下，改动 main.js

```js
function sendMes() {
  return new Promise((resolve, reject) => {
    resolve("这里是数据");
  });
}
async function getData() {
  const data = await sendMes();
  console.log(data);
}
getData();
```

## 测试打开 F12 consle.log()

# ============使用 sass(css 同理)

## 安装依赖

```js
yarn add node-sass css-loader vue-style-loader sass-loader
```

**注意安装 node-sass 时 会有坑，安装失败解决办法另文章分享**

## 在 src 目录下新建 styles 文件夹 再新建 common.sass

```sass
body{
    div{
        color: red;
    }

}
```

## 改动 webpack.config.js

```js
rules: [
  // 解析新语法js
  {
    test: /\.js$/,
    exclude: /node_modules/,
    use: {
      loader: "babel-loader",
      options: {
        presets: ["@babel/preset-env"]
      }
    }
  },
  //   css
  {
    test: /\.css$/,
    use: ["vue-style-loader", "css-loader"]
  },
  //   sass
  {
    test: /\.scss$/,
    use: ["vue-style-loader", "css-loader", "sass-loader"]
  }
];
```

**先用 sass-loader 后 css-loader 加载 css，再用 vue-style-loader 把加载好的样式**

## 引入 mian.js 中

```js
improt './styles/common.sass'
```

**再次运行即可看到效果**
