# Vuejs 中的 ECMAScript 

对于稍微有一定编程经验的同学，会发现我们使用的不是"原生的javascript", 而是一种新的语言。  这个语言就是 ECMAScript.  

严格的说， ECMAScript是Javascript的规范，Javascript是ECMA的实现。

ECMAScript出了 javascript, 还有Jscript 和 ActionScript这样的实现（也叫方言）

ECMAScript 也简称叫ES。 版本比较多， 有ES 2015, ES2016, ES2017 等。  很多时候我们用ES6来泛指这三个版本。  从这里： http://kangax.github.io/compat-table/es6/ 
可以看到，ES6 的90%的特性都已经被各大浏览器实现了。 阮一峰先生的《ECMAScript入门》中对ES的历史有着非常精彩的阐述。

具体的细节我们不去深究，我们就暂且认为ECMAScript实现了很多 普通js无法实现的功能。 同时，在Vuejs项目中大量的使用了ES的语法。 

下面是一个极简版的ES6的入门。 大家只要可以看懂这些代码，就可以通读本书。

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

## 导入代码： import

import 用来引入导入外部代码. 如下所示： 

```
import Vue from 'vue'
import Router from 'vue-router'
```

上面的代码, 目的是引入 `vue` 和 `vue-router` (由于他们是在`package.json` 中定义了, 所以可以直接 `import ... from <包名>`. 否则要加上路径）

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

## 方便其他代码来使用自己: export default {..}

我们会看到,在每个 vue文件中的 `<script>`中, 都会存在这个代码.它的作用是方便其他代码对这个代码来引用.

对于Vuejs 程序员,我们就记住这个写法就好了. 

在ES6之前js没有一个统一的模块定义方式，流行的定义方式有AMD, CommonJS等, 这些方式都是使用一种“打补丁”的形式来实现这个功能，总给人一种怪怪的感觉。 而ES6从语言层面对定义模块的方式进行了统一。

假设有: `lib/math.js` 文件内容如下:

```
export function sum(x, y) {
  return x + y
}
export var pi = 3.141593
```

可以看到， `lib/math.js` 文件，可以导出两个东西，一个是 `function sum`, 一个是 `var pi`. 

我们可以定义一个新的文件， `app.js`,  文件内容如下:

```
import * as math from "lib/math"
alert("2π = " + math.sum(math.pi, math.pi))
```

可以看到，在上面的代码中， 可以直接调用 `math.sum` 和 `math.pi`方法。 

我们再看一个例子： 新建一个文件 `other_app.js` , 内容如下:

```
import {sum, pi} from "lib/math"
alert("2π = " + sum(pi, pi))
```

可以看到， 上面的代码中，通过 `import {sum, pi} from "lib/math"`, 可以在后面直接调用 `sum()` 和 `pi` 

而 `export default { ... } ` 则是暴露出一段没有名字的代码, (不像 `export function sum(a,b){ .. }`这样有个名字(叫sum) .  )

在webpack下的Vuejs ，会自动对这些代码进行处理。 都属于框架内的工作。各位同学只需要按照这个规则来写代码，就一定没问题。

## ES中的简写

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

## 箭头函数 =>

跟coffeescript一样, ES 也可以通过箭头来表示函数.

```
  .then(response => ... );
```

等同于:

```
  .then(function (response) {
    // ...
  })
```

这样写法的好处，是强制定义了作用域。 使用了 `=>` 之后，可以避免很多由于作用域产生的问题。 建议大家多使用。

## hash中同名的 key, value的简写

```
let title = 'triple body'

return {
  title: title
}
```

等同于:

```
let title = 'triple body'

return {
  title
}
```

## 分号可以省略

例如： 

```
var a = 1
var b = 2
```

等同于：

```
var a = 1;
var b = 2;
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

然后，我们可以这样做定义：

```
let {firstname, lastname} = person
```

上面一行代码，等价于:

```
let firstname = person.firstname
let lastname = person.lastname
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


## 学习资料

国内比较好的中文教材，是阮一峰编写的 <<ECMAScript 6入门>>. 书中非常详实的阐述了相关的内容，概念和用法。 

我们也可以在网上直接查看这本书的电子版： http://es6.ruanyifeng.com
