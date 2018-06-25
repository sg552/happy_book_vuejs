# Vuex

Vuex 是 状态管理工具. 跟React中的Redux相似，但是更加简洁直观。 

简单的说, Vuex 帮我们管理 "全局变量", 供任何页面在任何时刻使用.

跟其他语言中的“全局变量”相比， 使用Vuex 的优点是：

1. Vuex中的变量的状态是响应式的。 当某个组件读取这个变量时，只要Vuex中的变量发生变化，那么对应的组件就会发生变化（类似于双向绑定）
2. 用户或者程序无法直接改变Vuex中的变量。必须通过Vuex提供的接口来操作. 这个接口就是通过 "commit mutation"来实现的。

Vuex 非常重要. 不管是大项目还是小项目,都有用到它的时候.  我们必须会用.

完整官方文档:  https://vuex.vuejs.org/zh-cn/getting-started.html   

Vuex 的内容很庞大，用到了比较烧脑的设计模式（这是由于javascript语言本身不够严谨和成熟决定的），所以我不打算带同学们把源代码和实现机理
详细的学一遍。 大家只要可以娴熟的使用就行了。

下面，我们以一个例子来说明如何使用。

## 正常使用的顺序

假设,我们有两个页面:  "页面1" 和"页面2" , 共同使用一个变量: counter.  页面1对 "counter" + 1 后, 页面2的值也会发生变化.

### 1.修改`package.json`

增加 `vuex` 的依赖声明，如下：

```
  "dependencies": {
    "vuex": "^2.3.1"
  },
```

如果不确定你的 vuex 用什么版本,就先手动安装一下:

```
$ npm install vuex --verbose
```

然后看安装过来的版本号就可以了.

### 2.新建store文件

文件名： `src/vuex/store.js`

这个文件的作用,是在整个Vuejs项目中声明: 我们要使用Vuex进行状态管理了.

它的内容如下： 

```
import Vue from 'vue'
import Vuex from 'vuex'

// 这个就是我们后续会用到的counter 状态．
import counter from '@/vuex/modules/counter'

Vue.use(Vuex)

const debug = process.env.NODE_ENV !== 'production'
export default new Vuex.Store({
    modules: {
			counter    			// 所有要管理的module, 都要列在这里.
    },
    strict: debug,
    middlewares: []
})
```

在上面代码中,大部分是鸡肋代码. 有用的代码只有:

```
import counter from '@/vuex/modules/counter'
...
	modules: {
		counter
	}
...
```
这里定义了所有的 vuex module.

### 3.新建vuex/module文件

文件名： `src/vuex/modules/counter.js`

内容如下：

```
import { INCREASE } from '@/vuex/mutation_types'

const state = {
  points: 10
}

const getters = {
  get_points: state => {
    return state.points
  }
}

const mutations = {
  [INCREASE](state, data){
    state.points = data
  }

}

export default {
  state,
  mutations,
  getters
}
```

上面是一个最典型的  vuex module, 它的作用就是计数.

- state: 表示状态. 可以认为state是一个数据库，保存了各种数据。我们无法直接访问里面的数据。
- mutations: 变化。  可以认为所有的state都是由mutation来驱动变化的。 也可以认为它是个setter.
- getter:  取值的方法。  就是getter( 跟setter相对）

我们如果希望"拿到"某个数据，就需要调用 vuex module的`getter` 方法。
我们如果希望"更改"某个数据，就需要调用 vuex module的`mutation` 方法。


### 4.新增文件: `src/vuex/mutation_types.js`

```
export const INCREASE = 'INCREASE'
```

大家做项目的时候, 要统一把 mutation type定义在这里. 它类似于方法列表.

这个步骤不能省略。 Vuejs官方也建议这样写。 好处是维护的同学可以看到 某个mutation有多少种状态。

### 5.新增路由: `src/routers/index.js`

```
import ShowCounter1 from '@/components/ShowCounter1'
import ShowCounter2 from '@/components/ShowCounter2'

export default new Router({
  routes: [
    {
      path: '/show_counter_1',
      name: 'ShowCounter1',
      component: ShowCounter1
    },
    {
      path: '/show_counter_2',
      name: 'ShowCounter2',
      component: ShowCounter2
    }
	]
})
```

6.新增两个页面: `src/components/ShowCounter1.vue`
和 `src/components/ShowCounter2.vue`

这两个页面基本一样.

```
<template>
  <div>
    <h1> 这个页面是 1号页面 </h1>
    {{points}} <br/>
    <input type='button' @click='increase' value='点击增加1'/><br/>
    <router-link :to="{name: 'ShowCounter2'}">
          计数页面2
    </router-link>
  </div>
</template>

<script>
import store from '@/vuex/store'
import { INCREASE } from '@/vuex/mutation_types'
export default {
  computed: {
    points() {
      return store.getters.get_points
    }
  },
  store,
  methods: {
    increase() {
      store.commit(INCREASE, store.getters.get_points + 1)
    }
  }
}
</script>
```

可以看出， 我们可以在 `<script>`中调用 vuex的module的方法。 例如：

```
increase() {
	store.commit(INCREASE, store.getters.get_points + 1)
}
```

这里， `store.getters.get_points` 就是通过`getter`获取到 状态“points"的方法。

`store.commit(INCREASE, .. )` 则是 通过 `INCREASE` 这个`action` 来改变 "points"的值。

## Computed属性

Computed 代表的是某个组件(component)的属性, 这个属性是算出来的。 每当计算因子发生变化时，
这个结果也要及时的重新计算。

上面的代码中：

```
<script>
export default {
  computed: {
    points() {
      return store.getters.get_points
    }
  },
</script>
```

就是定义了一个叫做 'points' 的 'computed'属性。 然后，我们在页面中显示这个”计算属性":

```
<template>
  <div>
    {{points}}
	</div>
</template>
```

就可以把 state中的数据显示出来， 并且会自动的更新了。

重启服务器( `$ npm run dev` ) , 之后运行, 可以看到如下图所示:

![vuex演示 计数器](./images/vuejs_vuex演示.gif)

## Vuex 原理图

为了学会本章内容，大家务必亲手敲一敲代码。

下面是Vuex的原理图. 

![Vuex](./images/vuex.png)

可以看到： 

1.总体分成 ： Action, Mutation, State 三个概念. State由Mutation来变化
2.Vuex 通过 Action 与后端API进行交互
3.Vuex 通过 State 来渲染前端页面。 
4.前端页面通过触发 Vuex的Action，来提交mutation, 达到改变 "state"的目的。

