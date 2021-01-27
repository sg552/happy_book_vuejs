# 实体书的勘误表

非常抱歉，由于我的个人失误，草稿以markdown格式书写，在复制粘贴的时候，代码中的 `{{ }}` 没有复制到 word中。

不过在code_example文件夹中的中都很完整。读者可以直接运行那边的代码。

## 2.1 极速入门(实体书第10页)

`{{show_my_text}}`在例子中缺失

错误的内容:

```
<div id='app'>

</div>
```

正确的内容应该是:
```
<div id='app'>
  {{show_my_text}}
</div>
```

## 2.2.2 HTML代码的<head>部分(实体第19页)

章节号标记错误

错误的原文:

```
// 下面的window.onload函数暂时省略。 会在 2.2.3 js代码部分讲解到。
...
  <!-- 这里的代码暂时省略。会在 2.2.2 HTML代码的body部分中讲解到 -->
```

正确的内容应该是:

```
// 下面的window.onload函数暂时省略。 会在 2.2.4 js代码部分讲解到。
...
  <!-- 这里的代码暂时省略。会在 2.2.3 HTML代码的body部分中讲解到 -->

```


## 4.1.4 定义并显示变量 (实体书第54页 )

代码缺失

错误的原文:

```
<template>
  <div>
  <!--  步骤2: 在这里显示 message -->

  </div>
</template>
```

正确的内容应该是:

```
<template>
  <div>
  <!--  步骤2: 在这里显示 message -->
  {{message}}
  </div>
</template>
```


## 4.4.1 渲染某个变量(实体书64)

代码缺失

错误的原文:

```
可以这样来显示它:
<div></div>

完整代码如下:
<template>
  <div>

  </div>
</template>

```


正确的内容应该是:

```
可以这样来显示它:
<div>{{my_value}}</div>

完整代码如下:
<template>
  <div>
    {{message}}
  </div>
</template>
```

## 4.5.6 v-on (实体书73页)

代码缺失.

错误的原文:

```
<body>
  <div id='app'>

    <br/>
```

正确的内容应该是:


```
<body>
  <div id='app'>
    {{message}}
    <br/>
```

## 4.7.2 显示博客详情页 (实体书87页)

代码缺失

错误的原文:

```
<div>
  <p> 标题: </p>
  <p> 发布于: </p>
  <div>

  </div>
</div>
```

正确的内容应该是:

```
<div>
  <p> 标题: {{blog.title}} </p>
  <p> 发布于: {{blog.created_at}} </p>
  <div>
    {{blog.body}}
  </div>
</div>

```

## 4.7.5 修改博客列表页的跳转方式2: 使用v-link (实体书91页)

代码缺失

错误的原文:

```
<td>
  <router-link :to="{name: 'Blog', query: {id: blog.id}}">

  </router-link>
</td>
```

正确的内容应该是:

```
<td>
  <router-link :to="{name: 'Blog', query: {id: blog.id}}">
    {{blog.id}}
  </router-link>
</td>
```

## 4.10 双向绑定(实体书96页)


代码缺失

错误的原文:

```
    <!-- 显示　this.my_value 这个变量 -->
    <p>页面上的值:   </p>
```


正确的内容应该是:


```
    <!-- 显示　this.my_value 这个变量 -->
    <p>页面上的值: {{my_value}}  </p>
```


## 4.11 表单项目的绑定(实体书99-100页)



代码缺失

错误的原文:
```
<template>
  <div>
    input： <input type='text' v-model="input_value"/>,
    输入的值：
    <hr/>
    text area： <textarea v-model="textarea_value"></textarea>,
    输入的值：
    <hr/>
    radio:
    <input type='radio' v-model='radio_value' value='A'/> A,
    <input type='radio' v-model='radio_value' value='B'/> B,
    <input type='radio' v-model='radio_value' value='C'/> C,
    输入的值：

    <hr/>
    checkbox:
    <input type='checkbox' v-model='checkbox_value'
      v-bind:true-value='true'
      v-bind:false-value='false'
      /> ,
    输入的值：

    <hr/>
    select:
    <select v-model='select_value'>
      <option v-for="e in options" v-bind:value="e.value">
        {{e.text}}
      </option>
    </select>
    输入的值：
  </div>
</template>
```


正确的内容应该是:

```
<template>
  <div>
    input： <input type='text' v-model="input_value"/>,
    输入的值：{{input_value}}
    <hr/>
    text area： <textarea v-model="textarea_value"></textarea>,
    输入的值：{{textarea_value}}
    <hr/>
    radio:
    <input type='radio' v-model='radio_value' value='A'/> A,
    <input type='radio' v-model='radio_value' value='B'/> B,
    <input type='radio' v-model='radio_value' value='C'/> C,
    输入的值：
    {{radio_value}}
    <hr/>
    checkbox:
    <input type='checkbox' v-model='checkbox_value'
      v-bind:true-value='true'
      v-bind:false-value='false'
      /> ,
    输入的值：
    {{checkbox_value}}
    <hr/>
    select:
    <select v-model='select_value'>
      <option v-for="e in options" v-bind:value="e.value">
        {{e.text}}
      </option>
    </select>
    输入的值：{{select_value}}
  </div>
</template>
```

## 6.3.1 典型例子 (实体书135页)



代码缺失

错误的原文:

```
<div id='app'>
    <p> 原始字符串： </p>
    <p> 通过运算后得到的字符串： </p>
</div>
```


正确的内容应该是:

```
<div id='app'>
    <p> 原始字符串： {{my_text}} </p>
    <p> 通过运算后得到的字符串：{{my_computed_text}} </p>
</div>

```

## 6.3.2 Computed Properties 与普通方法的区别(实体书137页)



代码缺失

错误的原文:

```
    <div id='app'>
        <p> 原始字符串：  </p>
        <p> 通过运算后得到的字符串： {{my_computed_text() }} </p>
    </div>
```


正确的内容应该是:

```
    <div id='app'>
        <p> 原始字符串：{{my_text}} </p>
        <p> 通过运算后得到的字符串： {{my_computed_text() }} </p>
    </div>
```

## 6.3.3 watched properties (实体书138,139页)



代码缺失

错误的原文:

```
(138页)
<p> 我所在的详细一些的地址：  （每次其他两个发生变化，这里就会跟着变化) </p>
(139页)
<p> 我所在的详细一些的地址：  （这是使用computed 实现的版本) </p>
```


正确的内容应该是:

```
(138页)
<p> 我所在的详细一些的地址：{{full_address}}  （每次其他两个发生变化，这里就会跟着变化) </p>
(139页)
<p> 我所在的详细一些的地址：{{full_address}}  （这是使用computed 实现的版本) </p>

```

## 8.5 用户的注册和微信授权(实体书196页)


错误的原文:

```
if(this。user_info。open_id)
```


正确的内容应该是:

```
if(this.user_info.open_id)
```
## 8.9 商品列表页 (实体书218页)


代码缺失

错误的原文:

```
<div class="title">

</div>
```


正确的内容应该是:

```
<div class="title">
  {{name}}
</div>
```
## 8.10 商品详情页 (实体书220页)


代码缺失

错误的原文:

```
    <p class="p_name"></p>
    <div class="product_pric">
      <span>￥</span>
      <span class="rel_price"></span>
      <span></span>

      <span style='color: grey;
      text-decoration: line-through;
      font-size: 18px;
      margin-left: 14px;'>
        原价: ￥
      </span>
    </div>
```


正确的内容应该是:

```
    <p class="p_name">{{good.name}}</p>
    <div class="product_pric">
      <span>￥</span>
      <span class="rel_price">{{good.price}}</span>
      <span></span>

      <span style='color: grey;
      text-decoration: line-through;
      font-size: 18px;
      margin-left: 14px;'>
        原价: ￥{{good.original_price}}
      </span>
    </div>

```


## 8.11 购物车(实体书228页)


代码缺失

错误的原文:

```
<div class="item_names">
    <a>
        <span></span>
    </a>
</div>
<div class="cart_weight">
    <span class="my_color" style="color: #979292;"></span>
</div>
<div class="cart_product_sell">
    <span class="product_money">￥<strong class="real_money"></strong></span>
```


正确的内容应该是:

```
<div class="item_names">
    <a>
        <span>{{item.title}}</span>
    </a>
</div>
<div class="cart_weight">
    <span class="my_color" style="color: #979292;">{{item.title}}</span>
</div>
<div class="cart_product_sell">
    <span class="product_money">￥<strong class="real_money">{{item.price}}</strong></span>

```

## 8.13 微信支付（实体书235页)

代码缺失

错误的原文:

```
<div class="title">

</div>
<div class="logo_and_shop_name">
  <div class="product_pric">
    <span>￥</span>
    <span class="rel_price"> </span>
    <span> &nbsp x  </span>
  </div>
</div>

```


正确的内容应该是:

```
<div class="title">
  {{good.name}}
</div>
<div class="logo_and_shop_name">
  <div class="product_pric">
    <span>￥</span>
    <span class="rel_price">{{good.price}}</span>
    <span> &nbsp x {{buy_count}}</span>
  </div>
</div>

```

## 8.13 微信支付（实体书236页)

代码缺失

错误的原文:

```
<div class="title">

</div>
<div class="logo_and_shop_name">
  <div class="product_pric">
    <span>￥</span>
    <span class="rel_price"> </span>
    <span> &nbsp x  </span>
  </div>
</div>
```


正确的内容应该是:

```
<div class="title">
  {{product.title}}
</div>
<div class="logo_and_shop_name">
  <div class="product_pric">
    <span>￥</span>
    <span class="rel_price">{{product.price}}</span>
    <span> &nbsp x {{product.quantity}}</span>
  </div>
</div>
```
