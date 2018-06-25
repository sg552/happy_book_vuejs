# Vuejs 渲染页面的过程和原理

只有知道了一个页面是如何被渲染出来的，我们才可以更好的理解框架和调试代码。 下面我们就来仔细看一下这个过程。

## 渲染过程1. js入口文件

最初的最初，我们要知道  `./build/webpack.base.conf.js` 这个文件，是webpack打包的主要配置文件. 一个典型的代码如下：

```
var path = require('path')
var utils = require('./utils')
var config = require('../config')
var vueLoaderConfig = require('./vue-loader.conf')

function resolve (dir) {
  return path.join(__dirname, '..', dir)
}

module.exports = {
  entry: {
    app: './src/main.js'
  },
  output: {
    path: config.build.assetsRoot,
    filename: '[name].js',
    publicPath: process.env.NODE_ENV === 'production'
      ? config.build.assetsPublicPath
      : config.dev.assetsPublicPath
  },
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src')
    }
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: vueLoaderConfig
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        include: [resolve('src'), resolve('test')]
      },
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('img/[name].[hash:7].[ext]')
        }
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
        }
      }
    ]
  }
}

```

在上面的代码中，

```
module.exports = {
  entry : {
    app: './src/main.js'   // 这里就定义了Vuejs的入口文件
  }
}
```

很重要， 其中的 `app: './src/main.js'` 就定义了Vuejs的入口文件

知道了这个打包文件，我们就可以知道接下来的事儿了。

## 渲染过程2. 静态的HTML页面： index.html

因为我们每次打开的都是 'http://localhost/#/', 实际上打开的文件是 'http://localhost/#/index.html'

所以找到`index.html` ，可以看到它的内容如下；

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>演示Vue的demo</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

这里的  `<div id="app"></div>`, 就是将来会动态变化的内容。特别类似于 Rails的 layout（模板文件）. 

这个index.html 文件是最外层的 模板。 

## 渲染过程3. main.js 中的 Vue定义

我们回头看 `src/main.js`， 它的内容如下；

```
import Vue from 'vue'
import App from './App'
import router from './router'
import VueResource from 'vue-resource';
Vue.use(VueResource);

Vue.config.productionTip = false
Vue.http.options.emulateJSON = true;

new Vue({
  el: '#app',   // 这里, #app 对应着 <div id=app></div>
  router,
  template: '<App/>',
  components: { App }  // 这里, App就是 ./src/App.vue
})
```

熟悉 jquery, css selector的同学可以看到， `el: '#app'` 就是 `index.html` 中的 `<div id= app>`

注意上面的 `App.vue`,  它会被 `main.js`  加载， App.vue的内容如下：

```
<template>
  <div id="app">
		<router-view class="view"></router-view>
  </div>
</template>
<script>
</script>
<style>
</style>
```

上面代码中的 `<template/>`,  这个就是第二层的模板。 可以认为该页面的内容，就是在这个位置被渲染出来的。

上面的代码中，还有个 `<div id = 'app'>...</div>`, 这个元素跟`index.html`中的是同一个元素（暂且这么理解）

所有的 `<router-view>`中的内容，都会被自动替换。

`<script>` 中的代码则是脚本代码。 至此，整个过程就出来了。

## 原理

Vuejs 就是最典型的Ajax 工作方式:  只渲染部分页面.

浏览器的页面从来不会整体刷新. 所有的页面变化都限定在 `index.html` 中的`<div id="app"></div>`代码中，如下图所示:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>演示Vue的demo</title>
  </head>
  <body>
    <div id="app"></div>   <!-- 都在这一行 -->
  </body>
</html>
```

所有的动作,可以靠 url来触发, 例如:

- `/#/books_list` 对应 某个列表页

- `/#/books/3` 对应某个详情页

这个技术，就是靠 vuejs 的核心组件 `vue-router` 来实现的。  

## 不使用router的技术：QQ邮箱

QQ邮箱是属于: url无法跟某个页面一一对应的项目.

所有页面的跳转,都无法根据url 来判断

最大的特点： 无法保存页面的状态， 难以调试， 无法根据url直接进入某个页面。

