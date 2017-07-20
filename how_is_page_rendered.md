# Vuejs 渲染页面的过程和原理

## 渲染过程

1. 最初的最初，我们要知道  `./build/webpack.base.conf.js` 这个文件，是webpack打包的主要配置文件

其中

```
module.exports = {
  entry : {
    app: './src/main.js'   // 这里就定义了vue的入口文件
  }
}
```

知道了这个打包文件，我们就可以知道接下来的事儿了。

2. 找到index.html ，可以看到它的内容如下；


```
<body>
  <div id="app"></div>
</body>
```
这里的  `id='app'`, 就是将来会动态变化的内容。特别类似于 rails的 layout.
只不过这个layout是第一层layout(最大的layout)

3. 回到 `src/main.js` ， 可以看到它的内容如下；

```
import Vue from 'vue'
import App from './App'
import router from './router'


new Vue({
  el: '#app',   // 这里, #app 对应着 <div id=app></div>
  router,
  template: '<App/>',
  components: { App }  // 这里, App就是 ./src/App.vue
})

```

熟悉 jquery, css selector的同学可以看到， `el: '#app'` 就是 `index.html` 中的 `<div id= app>`

4. 注意上面的 `App.vue`,  它会被 `main.js`  加载， App.vue的内容如下：


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

注意上面的 template,  这个就是第二层 layout， 可以看到， 里面还有个 `div id = 'app'`, 这个元素跟
`index.html`中的是同一个元素（暂且这么理解）

所有的 `<router-view>`中的内容，都会被自动替换。

`<script>` 中的代码则是脚本代码。 至此，整个过程就出来了。


## 原理

Vuejs 就是最典型的Ajax 工作方式:  只渲染部分页面.

页面从来不会刷新. 所有的页面变化,都限定在 index.html中的下列代码中:

```
<div id="app"></div>
```

所有的动作,可以靠 url来触发, 例如:

- `/#/books_list` 对应 某个列表页
- `/#/books/3` 对应某个详情页

(qq邮箱是属于那种, url无法跟某个页面一一对应的项目. 所有页面的跳转,都无法根据url 来判断)
