# 路由

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

