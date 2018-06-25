# Mixin

Mixin是一种更好的复用代码的模式.

我们知道 java , Object C 中的 interface , implements,  extends 等关键字的意义,就是为了让代码可以复用、继承.

但是这几种方法, 都理解起来很不直观, 给人一种拐弯抹角的感觉. 特别是像我这样很不习惯 “设计模式”的人。 

在js, ruby等动态语言中, 我们如果要复用代码的话,直接使用 mixin 就好了.

## Mixin 的 概念

Mixin 实际上是利用语言的特性（关键字），以更加简洁易懂的方式，实现了 “设计模式”中的 “组合模式”。 可以定义一个公共的类，这个类就叫做"mixin". 
然后让其他的类，通过“include” 这样的语言特性，来包含mixin, 直接具备了 mixin 所具备的各种方法。

我们下面看一下在 Vuejs 中如何使用mixin 这种强大的工具。

## 建立一个Mixin文件

可以在 `src/mixin` 目录下创建, 例如:

文件:  `src/mixin/common_hi.js`:

```
export default {
  methods: {
    hi: function(name){
      return "你好, " + name;
    }
  }
}
```

## 使用 

Mixin使用起来很简单,在对应的 js文件, 或者 vue文件的`<script>`代码中引用即可.

例如,新建一个vue文件:

`src/components/SayHiFromMixin.vue`, 内容如下:

```
<template>
  <div>
    {% raw %}{{{% endraw %}hi("from view")}}
  </div>
</template>

<script>
import CommonHi from '@/mixins/common_hi.js'
export default {
  mixins: [CommonHi],
  mounted() {
    alert( this.hi('from script code'))
  }
}
</script>
```

注意:

- 使用的时候, `mixins: [CommonHi]` 这里的是中括号,表示是数组.
- 在js代码中调用的话, 需要带有this关键字,例如: `this.hi()`

路由如下:

```
import SayHiFromMixin from '@/components/SayHiFromMixin'

export default new Router({
  routes: [
    {
      path: '/say_hi_from_mixin',
      name: 'SayHiFromMixin',
      component: SayHiFromMixin
    }
  ]
} )

```

运行效果如下:

![mixin的效果](./images/vue_mixin.png)
