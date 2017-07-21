# 视图中的渲染

## 渲染某个变量

假定我们定义了一个变量：　

```
<script>
export default {
  data () {
    return {
      my_value: '默认值',
    }
  },
}
</script>

```

我们就可以这样来显示它：　

```
<div>{{my_value}}</div>
```

## 方法的声明和调用


声明一个方法：　show_my_value
```
<script>
export default {
  data () {
    return {
      my_value: '默认值',
    }
  },
  methods: {
    show_my_value: function(){
      // 注意下面的　this.my_value, 要用到this这个关键字．
      alert('my_value: ' + this.my_value);
    },
  }
}
</script>
```

调用上面的方法

```
<template>
  <div>
    <input type='button' @click="show_my_value()" value='...'/>
  </div>
</template>
```

对于有参数的方法，直接传递参数就好了．　例如:

```
<template>
  <div>
    <input type='button' @click="say_hi('Jim')" value='...'/>
  </div>
</template>
<script>
export default {
  data () {
    return {
      my_value: '默认值',
    }
  },
  methods: {
    say_hi: function(name){
      alert('hi, ' + name)
    },
  }
}
</script>
```

上面代码中，

```
<input type='button' @click="say_hi('Jim')" value='...'/>
```

就会调用 say_hi , 传入参数　'Jim'

## 事件处理：　v-on

我们看到，很多时候，　`@click`
```
<input type='button' @click="say_hi('Jim')" value='...'/>
```
等同于：　
```
<input type='button' v-on:click="say_hi('Jim')" value='...'/>
```

以上就是我们实际当中最常见的用法.　

