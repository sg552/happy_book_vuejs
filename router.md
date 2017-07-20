# 路由

## 基本用法

每个vue页面,都要对应一个路由.  例如, 我们要做一个"博客列表页", 那么,我们需要两个东西:

1. vue文件,例如: `src/components/books.vue`   负责展示页面
2. 路由代码, 让  `/#/books` 与 上面的vue文件对应.

下面的代码就是一个完整的路由文件:

```
import Vue from 'vue'
import Router from 'vue-router'

// 增加这一行, 作用是引入 SayHi 这个component
import SayHi from '@/components/SayHi'

Vue.use(Router)
export default new Router({
  routes: [

    // 增加下面几行, 表示定义了  /#/say_hi 这个url
    {
      path: '/say_hi',
      name: 'SayHi',
      component: SayHi
    },
  ]
})
```

写法是固定的. 其中的:

- path: 定义了 链接地址, 例如:   `/#/say_hi`
- name: 为这个路由加个名字, 方便以后引用,例如:   this.$router.push({name: 'SayHi'})
- component: 该路由由哪个 component来处理.

## 跳转到某个路由时,带上参数

### 对于 普通型的参数

例如:

```
routes: [
  {
    path: '/blog',
    name: 'Blog'
  },
]
```

在视图中, 我们这样做:

```
<router-link :to="{name: 'Blog', query:{id: 3} }">User</router-link>
```

在script中,也可以这样做:

```
this.$router.push({name: 'Blog', query: {id: 3}})
```

都会跳转到:  `/#/blog?id=3` 这个url.

### 对于在路由中声明的参数

例如:

```
routes: [
  {
    path: '/blog/:id',
    name: 'Blog'
  },
]
```

在视图中, 我们这样做:

```
<router-link :to="{name: 'Blog', params: {id: 3} }">User</router-link>
```

在script中,也可以这样做:

```
this.$router.push({name: 'Blog', params: {id: 3}})
```

都会跳转到:  `/#/blog/3` 这个url.

## 根据路由获取参数

Vue的路由中,参数获取有两种方式:  query 和 params


### 获取普通参数

对于 `/#/blogs?id=3` 中的参数,这样获取:

```
this.$route.query.id  // 返回结果3
```

### 获取路由中定义好的参数

对于 `/#/blogs/3` 这样的参数, 对应的路由应该是:


```
  routes: [
    {
      path: '/blogs/:id',  // 注意这里的 :id
      ...
    },
  ]
```

这个 named path, 就可以通过下面代码来获取id:

```
this.$route.params.id  // 返回结果3
```



