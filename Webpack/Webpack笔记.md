# 构建工具

## 简介

- 当我们习惯了在node中编写代码的方式后，在回到前端编写html、css、js这些东西会感觉到各种的不便。比如：不能放心的使用<u>模块化</u>规范（浏览器兼容性问题）、即使可以使用模块化规范也会面临模块过多时的加载问题。
- 我们就迫切的希望有一款工具可以对代码进行打包，将多个模块打包成一个文件。这样一来即解决了兼容性问题，又解决了模块过多的问题。
- 构建工具就起到这样一个作用，通过构建工具可以将使用ESM规范编写的代码转换为旧的JS语法，这样可以使得所有的浏览器都可以支持代码。

## Webpack

### 概念

本质上，**webpack** 是一个用于现代 JavaScript 应用程序的 *静态模块打包工具*。当 webpack 处理应用程序时，它会在内部从一个或多个入口点构建一个[依赖图(dependency graph)](https://www.webpackjs.com/concepts/dependency-graph/)，然后将你项目中所需的每一个模块组合成一个或多个 *bundles*，它们均为静态资源，用于展示你的内容。【按需打包】

> webpack在node中运行

### 使用步骤

1. 初始化项目`yarn init -y`
2. 安装依赖`webpack`、`webpack-cli`

```
npm add -D webpack webpack-cli
```

1. 在项目中创建`src`目录，然后编写代码（默认主文件index.js）
2. 执行`yarn webpack`来对代码进行打包（打包后观察dist目录）

> `cli`: command line interface 命令行工具
>
> 安装依赖`yarn add -D webpack webpack-cli`, -d表示设置为开发依赖
>
> src 目录下的是遵循前端开发规范的，src 以外的要用node规范CommonJS

### 配置文件（webpack.config.js）

```javascript
const path = require("path")
module.exports = {
    mode: "production", 
    entry: "./src/index.js",
    output: {
    }, 
    module: {
        rules: [
            {
                test: /\.css$/i,
                use: ["style-loader", "css-loader"]
            }
        ]
    }
}
```

> 书写对象的时候，可以在最后一个属性值后面加上`,`并且属性名可以不为字符串
>
> 但在写JSON的时候，属性名也需要加上`“”`并且最后不能加上`,`

#### [mode](https://www.webpackjs.com/configuration/mode/)

告知 webpack 使用相应模式的内置优化

- none：不使用任何默认优化选项
- production：生产模式
- development：开发模式

#### [entry](https://www.webpackjs.com/concepts/entry-points/)

默认值是 `./src/index.js`（一般不改，约定优于配置）

- 单个入口语法【最常见】 `entry: string | [string]`
- 多个传数组 `entry: ['./src/file_1.js', './src/file_2.js']`
- 对象写法分别命名打包 `entry: {app: './src/app.js',adminApp: './src/adminApp.js',},`

#### [output](https://www.webpackjs.com/concepts/output/)

默认值是 `./dist/main.js`，其他生成文件默认放置在 `./dist` 文件夹中

- `filename: "bundle.js"` 设置打包后的文件名

  > 多个入口 entry 的情况 `filename: [name]-[id]-[hash].js`
  >
  > 使用 [占位符(substitutions)](https://www.webpackjs.com/configuration/output/#template-strings) 来确保每个文件具有唯一的名称（很少用）

- `clean: true` 自动清理<u>打包目录</u>（path指定的目录），只保留当前这次打包的文件

- `path:  ""` 指定打包目录，必须要绝对路径

  > 一般会使用Node.js中的path模块来操作文件路径
  >
  > ```js
  > const path = require('path');	//引入path模块
  > path.resolve(__dirname, "dist")	//表示当前目录下的dist文件夹
  > ```

#### [loader](https://www.webpackjs.com/concepts/loaders/)

**loader** 让 webpack 能够去处理<u>其他类型</u>的文件（默认只能处理js文件），并将它们转换为有效 [模块](https://www.webpackjs.com/concepts/modules)，以供应用程序使用，以及被添加到依赖图中。

使用步骤：

1. 安装对应的 loader：`yarn add css-loader style-loader ts-loader -D`

2. 配置方式（推荐）：

   - test 属性：识别出哪些文件需要被转换（使用正则表达式`/\.css$/i`）
   - use 属性：定义出在进行转换时，使用哪个 loader（字符串、数组、对象）
   - type 属性：[加载图像资源](https://www.webpackjs.com/guides/asset-management/#loading-images)，设置为`"asset/resource"`
   - exclude 属性：不需要转换的文件夹（正则表达式）

   ```js
   module.exports = {
     module: {	// 易漏点
       rules: [ 
         { test: /\.css$/, use: ['style-loader','css-loader'] },
         { test: /\.ts$/, use: 'ts-loader' },
         { test:/\.(jpg|png|gif)$/i,type:"asset/resource" },
       ],
     },
   };
   ```

   > css-loader 只负责打包，style-loader 负责渲染生效【单一职责原则】  
   >
   > loader 执行顺序为**从后向前**执行，因此 use 的数组顺序不能调换

3. *内联方式：在每个 `import` 语句中显式指定 loader。

   使用 `!` 将资源中的 loader 分开。每个部分都会相对于当前目录解析。

   ```js
   import Styles from 'style-loader!css-loader?modules!./styles.css';
   ```

   - 使用`!`前缀，将禁用所有已配置的 normal loader(普通 loader)
   - 使用`!!`前缀，将禁用所有已配置的 loader（preLoader, loader, postLoader）
   - 使用`-!`前缀，将禁用所有已配置的 preLoader 和 loader，但是不禁用 postLoaders

   选项可以传递查询参数，例如 `?key=value&foo=bar`，或者一个 JSON 对象，例如 `?{"key":"value","foo":"bar"}`。

   > 尽可能使用 `module.rules`，因为这样可以减少源码中样板文件的代码量，并且可以在出错时，更快地调试和定位 loader 中的问题。

##### [babel](https://www.webpackjs.com/loaders/babel-loader)

###### 概念

- 在编写js代码时，经常需要使用一些js中的新特性，而新特性在旧的浏览器中兼容性并不好。此时就导致我们无法使用一些新的特性。

- 但是我们现在希望能够使用新的特性，我们可以采用折中的方案。依然使用新特性编写代码，但是代码编写完成时我们可以通过一些工具将新代码转换为旧代码。

- babel就是这样一个工具，可以将新的js语法转换为旧的js，以提高代码的兼容性。

- 如果希望在webpack支持babel，则需要向webpack中引入babel的loader

  > 是 loader 中的一种

###### 使用步骤

1. 安装 `npm install -D babel-loader @babel/core @babel/preset-env`

   - babel-loader：连接webpack和babel的中间件
   - @babel/core：babel的转换核心
   - @babel/preset-env：预设环境

2. 配置：

   ```javascript
   module: {
     rules: [
       {
         test: /\.m?js$/,
         exclude: /(node_modules|bower_components)/,
         use: {
           loader: 'babel-loader',
           options: {
             presets: ['@babel/preset-env']
           }
         }
       }
     ]
   }
   ```

3. 在package.json中设置兼容列表

   ```json
   "browserslist": [
           "defaults"
    ]
   ```

   配置参考：https://github.com/browserslist/browserslist

#### [plugin](https://www.webpackjs.com/concepts/plugins/)

##### 概念

- 插件用来为webpack来扩展功能
- 插件目的在于解决 [loader](https://www.webpackjs.com/concepts/loaders) 无法实现的其他事。
- Webpack 提供很多开箱即用的 [插件](https://www.webpackjs.com/plugins/)。

##### 常用插件

html-webpack-plugin

- 这个插件可以在打包代码后，自动在打包目录生成html页面

使用步骤：

1. 安装依赖`yarn add -D html-webpack-plugin`
2. 引入依赖`const HTMLPlugin = require("html-webpack-plugin")`
3. 配置插件

```javascript
plugins: [
        new HTMLPlugin({
            // title: "Hello Webpack",	//设置title
            template: "./src/index.html"	//模板，自动引入script脚本
        })
    ]
```

#### [devtool](https://www.webpackjs.com/configuration/devtool/#root)

`devtool:"inline-source-map"`配置源码的映射，方便调试打包后的代码。

### 开发服务器（webpack-dev-server）

- 安装：`yarn add -D webpack-dev-server`
- 启动：`yarn webpack serve --open`（`--open`表示启动服务器后自动打开）

> 配置 `webpack –watch` 执行，（在本地文件夹中访问）代码发生变化时自动更新打包。
>
> ![image-20230222152155721](img\image-20230222152155721-1677050518425-1.png)

### grunt/glup的对比

## [Vite](https://cn.vitejs.dev/)

### 概念

- Vite也是前端的构建工具

- 相较于webpack，Vite采用了不同的运行方式：

  - 开发时，并不对代码打包，而是直接采用**ESM（ES模块）**的方式来运行项目
  - 在项目部署时，再对项目进行打包

- 除了[速度外](https://cn.vitejs.dev/guide/why.html#slow-server-start)，Vite使用起来也更加方便（开箱即用，都配置好了）

- 本质上 Vite 和 Webpack 是打包工具，只是 Webpack 比较底层，需要自己手动去配置。

  > ESM 必须通过 url 加载页面（即需要通过服务器运行）

### 基本使用

1. 安装开发依赖 Vite `yarn add -D vite`

2. Vite 的源码目录默认就是项目**[根目录](https://cn.vitejs.dev/guide/#index-html-and-project-root)**

   - 在页面中引入 js 文件的时候要指定 `type=“module”`
   - 修改路径直接在 script 标签中修改 src 属性正确即可（webpack需要配置）

3. 开发命令：

   - `vite` 启动**开发**服务器

   - `vite build` 打包代码

   - `vite preview` **预览**打包后代码

4. [使用命令构建项目](https://cn.vitejs.dev/guide/#scaffolding-your-first-vite-project)：

  ```bash
  npm create vite@latest	#使用 NPM
  yarn create vite	#使用 Yarn
  pnpm create vite	#使用 PNPM
  #Vanilla 表示原生JS开发项目
  ```

5. [使用插件](https://cn.vitejs.dev/guide/using-plugins.html)

   1. 安装插件：`npm add -D @vitejs/plugin-legacy`

      > `@vitejs/plugin-legacy`：兼容传统浏览器的语法转换插件

   2. 配置文件：`vite.config.js`

      ```javascript
      // vite.config.js
      import legacy from '@vitejs/plugin-legacy'	//引入插件
      import { defineConfig } from 'vite'	//语法提示（可选）
      export default defineConfig({	//写上defineConfig配置时会有提示
        plugins: [	//配置插件
          legacy({
            targets: ['defaults', 'IE 11'],	//配置兼容版本
          }),
        ],
      })
      
      ```

      > 需要使用ES6的模块化（`export default`）去暴露文件（区别于 webpack 使用`require`）