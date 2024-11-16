# 整理 `webpack` 相关的面试题

### 🔴 说一下 `webpack` 性能优化？

来自：`字节`

<details>

<summary>以下是一些 Webpack 性能优化的策略：</summary>

#### 一、优化构建速度

**1. 缩小文件搜索范围**

**优化 `resolve.modules` 配置**：`resolve.modules` 用于配置 `Webpack` 去哪些目录下寻找第三方模块。默认情况下，它会在 `node_modules` 目录中查找。可以将其设置为一个特定的目录路径数组，优先从项目本地的 `node_modules` 目录查找，避免去全局的 `node_modules` 目录搜索，减少搜索范围。例如：

```js
resolve: {
  modules: [path.resolve(__dirname, "node_modules")];
}
```

**优化 `resolve.extensions` 配置**：`resolve.extensions` 用于配置在导入模块时，`Webpack` 自动添加的文件扩展名。默认包含了 `.js`、`.json` 等多种扩展名。可以将其设置为项目中常用的扩展名，减少不必要的文件查找。例如，如果项目主要使用 `.js` 和 `.jsx` 文件，可以这样设置：

```js
resolve: {
  extensions: [".js", ".jsx"];
}
```

**2. 使用 `DllPlugin` 和 `DllReferencePlugin`**

**`DllPlugin` 原理和使用场景**：动态链接库（`DLL`）是一种可以在多个应用程序之间共享代码的机制。在 `Webpack` 中，`DllPlugin` 可以将一些不经常变化的第三方库（如 `React`、`Vue` 等）预先打包成一个独立的动态链接库文件。这样在后续的项目构建过程中，这些库就不需要重新打包，从而大大加快构建速度。

**具体操作步骤：**

首先，创建一个 `webpack.dll.config.js` 文件用于配置 `DLL` 打包。例如，对于打包 `React` 相关的库：

```js
const path = require("path");
const webpack = require("webpack");

module.exports = {
  entry: {
    react_dll: ["react", "react-dom"],
  },
  output: {
    path: path.resolve(__dirname, "dist/dll"),
    filename: "[name].dll.js",
    library: "[name]_library",
  },
  plugins: [
    new webpack.DllPlugin({
      path: path.resolve(__dirname, "dist/dll/[name]-manifest.json"),
      name: "[name]_library",
    }),
  ],
};
```

运行 `webpack --config webpack.dll.config.js` 命令来生成 `DLL` 文件和对应的清单文件。然后，在主 `webpack.config.js` 文件中使用 `DllReferencePlugin` 来引用 `DLL` 文件。例如：

```js
const path = require("path");
const webpack = require("webpack");

module.exports = {
  //...其他配置
  plugins: [
    new webpack.DllReferencePlugin({
      context: __dirname,
      manifest: require("./dist/dll/react_dll-manifest.json"),
    }),
  ],
};
```

**3. 开启多进程构建**

**`HappyPack` 原理和使用场景**：在 `Webpack` 构建过程中，有很多加载器（`Loader`）是单线程执行的，如 `babel-loader` 等。`HappyPack` 可以将这些加载器的任务分配到多个进程中并行处理，从而提高构建速度。

**具体操作步骤：**

首先安装 `happypack` 包：`npm install --save -dev happypack`。然后在 `webpack.config.js` 文件中使用。例如，对于 `babel-loader` 的优化：

```js
const HappyPack = require("happypack");
const os = require("os");
const happyThreadPool = HappyPack.ThreadPool({ size: os.cpus().length });

module.exports = {
  //...其他配置
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: "HappyPack/loader?id=babel",
      },
    ],
  },
  plugins: [
    new HappyPack({
      id: "babel",
      loaders: ["babel-loader"],
      threadPool: happyThreadPool,
    }),
  ],
};
```

#### 二、优化输出结果

**1. 代码压缩**

**`UglifyJSPlugin`（`JavaScript`）**：在生产环境下，使用 `UglifyJSPlugin` 来压缩 `JavaScript` 代码。它会删除代码中的注释、空格，以及对变量名进行缩短等操作，从而减小代码体积。例如：

```js
const webpack = require("webpack");

module.exports = {
  //...其他配置
  plugins: [
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false,
      },
    }),
  ],
};
```

**`CSSnano`（`CSS`）**：对于 `CSS` 文件，使用 `CSSnano` 来进行压缩。它可以通过 `postcss-loader` 来集成到 `Webpack` 中。首先安装 `cssnano` 和 `postcss-loader`：`npm install --save -dev cssnano postcss-loader`。然后在 `webpack.config.js` 文件的 `module.rules` 中配置：

```js
module.exports = {
  //...其他配置
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          "style-loader",
          "css-loader",
          {
            loader: "postcss-loader",
            options: {
              plugins: [require("cssnano")()],
            },
          },
        ],
      },
    ],
  },
};
```

**2. 提取公共代码（`CommonsChunkPlugin` 和 `SplitChunksPlugin`）**

**`CommonsChunkPlugin`（旧版本）**：在 `Webpack 4` 之前，使用 `CommonsChunkPlugin` 来提取多个入口文件之间的公共代码。例如，如果有 `app.js` 和 `vendor.js` 两个入口文件，想要提取它们之间的公共部分（如 `React` 等库）

```js
const webpack = require("webpack");

module.exports = {
  entry: {
    app: "./src/app.js",
    vendor: "./src/vendor.js",
  },
  //...其他配置
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: "common",
      chunks: ["app", "vendor"],
    }),
  ],
};
```

**`SplitChunksPlugin`（`Webpack 4+`）**：`Webpack 4` 引入了 `SplitChunksPlugin` 来自动提取公共代码，它的配置更加智能和灵活。默认情况下，它会自动提取所有入口点（`entry-point`）和异步模块（`async-module`）之间的公共代码。例如：

```js
module.exports = {
  //...其他配置
  optimization: {
    splitChunks: {
      chunks: "all",
    },
  },
};
```

**3. `Tree Shaking`**

**原理和使用场景**：`Tree Shaking` 是一种通过静态分析代码来消除未使用的代码的技术。在 `Webpack` 中，它主要用于 `JavaScript` 模块。如果一个模块中导入了某些函数或变量，但在代码中没有实际使用，`Tree Shaking` 就会将这些未使用的部分从最终的打包文件中删除。

**配置和注意事项**：要使用 `Tree Shaking`，首先需要确保在 `package.json` 文件中的 `scripts` 配置里，`build` 命令（或者其他构建命令）的 `mode` 设置为 `production`，因为 `Tree Shaking` 在开发模式下是默认不启用的。例如：

```json
{
  "scripts": {
    "build": "webpack --mode=production"
  }
}
```

同时，在代码中需要使用 `ES6` 模块语法（`import` 和 `export`）来导入和导出模块，因为 `Webpack` 的 `Tree Shaking` 机制主要是基于 `ES6` 模块的静态结构进行分析的。

</details>
