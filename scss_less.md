# 与CSS预处理器结合使用

20年前的《程序员修炼之道》这本书，就提到了程序员的一个职业习惯： DIY。 (Don't Repeat Yourself), 不要做重复的事儿。

目前的编程语言，几乎都具备了消灭重复代码的能力。

除了CSS

CSS 是唯一不具备 支持变量的 编程语言。 因为CSS 本身只是一个DSL（Domain Specific Language领域特定的语言）, 它不是一个“编程语言”。

这样就决定了它的特点 ： 上手极快， 可以很好的表现HTML中某个元素的外观。 缺点就是： 无法通过常见的重构手法（Extract Method, Extract Variable.. ) 来精简代码。

所以， SCSS, SASS, LESS 等一系列的 "CSS 预处理器" (precompiler) 应运而生。 

## SCSS 

全名叫 Sassy CSS, （时髦的CSS）  是 SASS 3 引入新的语法，其语法完全兼容 CSS3，并且继承了 SASS 的强大功能。 

也就是说，任何标准的 CSS3 样式表都是具有相同语义的有效的 SCSS 文件。

官方网站同 SASS。 

由于 SCSS 是 CSS 的扩展，因此，所有在 CSS 中正常工作的代码也能在 SCSS 中正常工作。 也就是说，对于一个 SASS 用户，只需要理解 SASS 扩展部分如何工作的，就能完全理解 SCSS。 

大部分的用法都跟SASS相同。 唯一不同的是，SCSS 需要使用分号和花括号而不是换行和缩进。 

SCSS可以说是全面取代了 SASS。

我们看下面的例子： 

```
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```
在上面的代码中， 定义了两个变量： `$font-stack` 和 `$primary-color` . 编译后的CSS如下：

```
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

更多内容，可以到官方网站来学习： https://sass-lang.com/guide 非常简单，有一点儿CSS功底的人，往往可以瞬间上手。

## LESS 

LESS 也是一种 CSS 预处理器，它的自我介绍是： 只是多了"一丢丢"内容的CSS. ( It's CSS, with just a little more). 

官方网址： http://lesscss.org/ , Github: https://github.com/less/less.js  ， 截止到 2018-6-25 , github关注数是 15591 

它的作用跟SCSS一样，也是为了让代码更加精简，去掉无意义的重复。 我们看下面的例子：

```
// Variables
@link-color:        #428bca; // sea blue
@link-color-hover:  darken(@link-color, 10%);

// Usage
a,
.link {
  color: @link-color;
}
a:hover {
  color: @link-color-hover;
}
.widget {
  color: #fff;
  background: @link-color;
}
```

可以看到，上面的例子定义了 两个变量：  `@link-color` 和 `@link-color-hover`. 并且在下方进行了引用。 同时， 还有使用了换算功能 `darken(@link-color, 10%)`。 

上面的代码会被编译成下面的CSS： 

```
a,
.link {
  color: #428bca;
}
a:hover {
  color: #3071a9;   
}
.widget {
  color: #fff;
  background: #428bca;
}
```

可以看到， less的功能非常强大。 

## SASS

提到了SCSS, LESS， 就不得不提及SASS

官方网站： https://sass-lang.com/   , github: https://github.com/sass/sass , 截止到 2016-6-25, github关注数是 11376

特点是去掉了 花括号，分号，看起来特别简单。 使用空格来标记不同的段落层次。 跟HAML基本是一样的。 

我们看下面的例子： 

```
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

在上面的代码中， 定义了两个变量： `$font-stack` 和 `$primary-color` .  并且在下面对它们进行了引用。 

我们看编译后的结果：

```
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

不过在实际应用当中，却很少使用这个语言。 因为实际应用中，程序员最喜欢的事情，就是把“UI” 或者“美工” ， 或者“前端工程师”给过来的CSS文件直接使用。 如果使用SASS的话就很尴尬，
还要再动作做一遍转换。 浪费时间。 而且“美工”同学可以看得懂CSS，却无法看懂SASS。 

所以这个技术比较落没。 慢慢的被SCSS (SASS 3.0) 所取代。

所以，同学在这个技术的故事上要学习到一个道理： 程序员认为好的技术，在团队配合的过程和实践中是不一定适用的。 SASS 团队也做的非常不做，立刻就在SASS 3.0的时候推出了SCSS。


## 在 Vuejs 中使用CSS预编译器

使用的前提，是我们以 Webpack的形式使用Vuejs. 

使用方法非常简单。 我们以SASS为例： 

1.安装依赖: "sass-loader" 和 "node-sass", 运行下面命令：

```
$ npm i sass-loader node-sass -D
```

2.在"webpack.base.conf.js"中添加相关配置：

```
{
    test: /\.s[a|c]ss$/,
    loader: 'style!css!sass'
}
```

3.在对应的 ".vue" 文件中，我们就可以这样的定义某个样式： 

```
<style lang='sass'>
td {
  border-bottom: 1px solid grey;
}
</style>
```

上面的代码，会在运行的时候，被webpack编译成对应的CSS文件。 

