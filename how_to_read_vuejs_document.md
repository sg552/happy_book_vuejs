# 如何阅读官方文档

我们在查看vue-js的文档的时候，会发现它跟我们真正使用的项目的代码完全不一样。 例如，vuejs的官方文档的讲解，都是这样：

（完全是把所有代码都写在了js中）

```
var Child = {
  template: '
A custom component!
'
}
new Vue({
  // ...
  components: {
    //  将只在父模板可用
    'my-component': Child
  }
})
```

而我们的实际代码是这样：

```
<template>
....
</template>
<script>
.....
</script>
<style>
</style>
```

原因就在于我们在实际项目中使用了 `vue-loader`, 它可以非常好的帮我们自动加载所有的内容，按照webpacke + vue的约定。

## webpack

webpack就是一种工具，可以把各种js/css/html代码最后打包编译到一起。

Vuejs中已经集成了这个工具， 我们在使用vue-cli的时候，就会根据命令来生成 `webpack`所要求的
文件结构，然后在打包的时候(`npm run build`) ，vuejs的源代码就会
被webpack打包成正常的html代码和文件目录。

这个内容我们以后会讲到。大家知道我们以后所用的知识，都是"基于
webpack的vuejs" 就好。 光看vuejs的官方文档，是看不懂的。

## 官方文档地址

https://cn.vuejs.org/  (点击右上角的 translation就可以看到入口）


