# 声明组件

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

就可以了. 两个页面都发生了变化, 如下图:

![两个页面都具备了logo](./images/vuejs_增加了logo_components.gif)
