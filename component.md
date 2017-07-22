# 组件

组件是 Vuejs中最最重要的部分.

每一个页面文件( .vue) 都可以认为是一个组件.

当然,这里说的内容, 跟 官方文档的"[原始组件](https://cn.vuejs.org/v2/guide/single-file-components.html)" 不是一个东西.
本章的内容,仅使用于" webpack 项目"中的组件. 对应的文档是: [单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)

在Vuejs 1.x中, 组件跟 视图 是分别放到不同的文件夹下面的.

在Vuejs 2.8以后, 所有的视图文件,都保存到 'components' 目录下.

可见 "组件" 这个概念已经越来越重要和普及了.

## 如何查看文档

1. 先"粗糙的"看 "原始组件": https://cn.vuejs.org/v2/guide/single-file-components.html
对所有的概念有所了解. (因为这个原始组件的开发环境跟 webpack下项目的开发环境不太一样,
所以很多以 webpack 作为入门的同学(例如本书读者) 会蒙圈)

2. 再看 "单文件组件" : https://cn.vuejs.org/v2/guide/single-file-components.html
就可以对 webpack项目下的组件有清晰的认识.

3. 遇到问题之后,再看 "原始组件", 这里包括很多API级别的概念和解释.


## 作用: 可以重用

我们可以想象一个场景: 有两个页面, 每个页面的头部都要有个LOGO图片.

那么我们每次都写成原始HTML的话, 代码会比较重复:


页面1的代码:
```
  <div class='logo'>
    <img src='http://siweitech.b0.upaiyun.com//image/569/upsz-fyfkzhs9232258.jpg'>
  </div>
  页面1的其他代码
```


页面2的代码:
```
  <div class='logo'>
    <img src='http://siweitech.b0.upaiyun.com//image/569/upsz-fyfkzhs9232258.jpg'>
  </div>
  页面2的其他代码
```

所以,我们可以把这段代码抽取出来,成为一个新的组件(component).

## 组件的创建

新建一个文件: `src/components/Logo.vue`

```
<template>
  <div class='logo'>
    <img src='http://siweitech.b0.upaiyun.com//image/570/siwei.me_header.png'/>
  </div>
</template>
```

这个文件定义了一个最最简单的component.

然后,修改对应的页面:

```
<template>
  <div >
    <my-logo>
    </my-logo>
		...
</template>

<script>
import MyLogo from '@/components/Logo'

export default {
	...
  components: {
    MyLogo
  }
}
```

注意,上面的  `components: { MyLogo } ` , 必须是这个写法,它等同于:

```
components: {
  MyLogo: MyLogo   // 前面的MyLogo 是template中的名字
                  // 后面的MyLogo 是import进来的代码.
}
```

就可以了. 两个页面都发生了变化, 如下图:

![两个页面都具备了logo](./images/vuejs_增加了logo_components.gif)


## 向组件中传递参数

如果我希望两个页面, 每个页面都有个title, 但是内容不同,该怎么办? 就需要传递参数了.

声明的时候, 这样:

文件: `src/components/Logo.vue`

```
<template>
  <div class='logo'>
    <h1>{{title}}</h1>
		...
  </div>
</template>

<script>
export default {
  props: ['title']    // 加上了这个声明.
}
</script>
```

### 参数是字符串

在调用的时候, 传递字符串:

```
<my-logo title="博客列表页">
</my-logo>
```

就可以了.

### 接收变量.

如果要传递的参数是一个变量, 就要这么写:

```
<template>
    <my-logo :title="title">
    </my-logo>
    <input type='button' @click='change_title' value='点击修改标题'/><br/>
</template>

<script>
export default {
  data: function() {
    return {
      title: '博客列表页',
    }
  },
  methods: {
    change_title: function(){
      this.title = '好多文章啊(标题被代码修改过了)'
    }
  },
</script>
```

如下图:

![传递变量给组件](./images/vuejs_传递参数给组件.gif)
