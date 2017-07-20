# 语法入门

本节参考: https://segmentfault.com/a/1190000009276670

我们在使用的过程中,会发现vuejs中充满了一些不常见 的语法. 下面是一些说明.


## import

import 用来引入 第三方程序.

```
import Vue from 'vue'
import Router from 'vue-router'
```

上面两个,是引入 package.json 中的第三方包,所以可以直接 `import ... from <包名>`.

```
import SayHi from '@/components/SayHi'
```

上面这个,在from后面,有 `@`符号, 表示是在本地文件系统中,引入文件. `@`代表 源代码目录,一般是 src.

在 `@`出现之前,我们在编码的时候也会这样写:

```
import Swiper from '../components/swiper'
import SwiperItem from '../components/swiper-item'
import XHeader from '../components/header/x-header'
import store from '../vuex/store'
```

大量使用了 `../..` 这样的代码,会引起代码的混乱. 所以推荐使用 `@` 方法.


## export default {..}

我们会看到,在每个 vue文件中的 `<script>`代码端中,都会存在这个代码.它的作用是方便其他代码对这个代码
的引用.

对于vue程序员,我们就记住这个写法就好了.  没它不行, 有它也没太大意义. 鸡肋代码.

## 一些简写

我们会发现,这样的代码:

```
<script>
export default {
  data () {
    return { }
  }
}
</script>
```

实际上,上面的代码是一种简写形式,它等同于下面的代码:

```
<script>
export default {
  data: function() {
    return { }
  }
}
</script>
```

## let, var, 常量 与全局变量

声明本地变量,使用 let 或者 var .两者的区别是:

- var: 有可能引起 变量提升,或者 块级作用域的问题.
- let: 就是为了解决这两个问题存在的.

最佳实践: 多用let, 少用var. 遇到诡异变量问题的时候,就查查是不是var的问题.

下面是三个对比:

```
var title = '标题';   // 没问题
let title = '标题';   // 没问题
title = '标题';       // 这样做会报错.
```

记得,在 webpack下的 vuejs中, 使用任何变量,都要使用 var 或者let来声明.

常量:

```
const TITLE='标题';
```

对于全局变量, 直接在 index.html 中声明即可. 例如:

```
window.title = '我的博客列表'
```

## 箭头函数 =>

跟coffeescript一样, es script也可以通过箭头来表示函数.

```
  .then(response => ... );
```

等同于:

```
  .then(function (response) {
    // ...
  })
```

## hash中同名的 key, value的简写

```
let title = '...';

return {
  title: title;
}
```

等同于:

```
let title = '...';

return {
  title
}
```

## 解构赋值

我们先定义好一个hash:
```
let person = {
  firstname : "steve",
  lastname : "curry",
  age : 29,
  sex : "man"
};

```
let {firstname, lastname} = person;
```

等价于:
```
let firstname = person.firstname;
let lastname = person.lastname;
```

我们可以这样定义函数:

```
function greet({firstname, lastname}) {
  console.log(`hello,${firstname}.${lastname}!`);
};

greet({
  firstname: 'steve',
  lastname: 'curry'
});
```

但是不建议大家这样使用. 有一些奇淫技巧的感觉. 另外,浏览器和一些第三方支持的不是太好,
我们在实际项目中,曾经遇到过与之相关的很奇葩的问题.

