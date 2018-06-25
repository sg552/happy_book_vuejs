# Slot

作为对Component的补充，Vuejs 增加了 Slot 这个功能. 

我们从具体的例子来说明。

```
<html>
<head>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
	<div id='app'>
		<study-process>
			我学习到了Slot 这个章节。
		</study-process>
	</div>
	<script>
		Vue.component('study-process', {
		  data: function () {
		    return {
		      count: 0
		    }
		  },
		  template: '<div><slot></slot></div>'
		})
		var app = new Vue({
			el: '#app', 
			data: {
			}
		})
	</script>
</body>
</html>
```

从上面的代码从，我们可以看到，我们先是定义了一个 component: 

```
Vue.component('study-process', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<div><slot></slot></div>'
})
```

在这个component的template中，是这样的：  

```
template: '<div><slot></slot></div>'
```

这里就使我们定义的 slot. 

然后，我们在调用这个 component的时候，这样： 

```
<study-process>
	我学习到了Slot 这个章节。
</study-process>
```		

所以，“我学习到了Slot 这个章节。”就好像一个参数那样传入到了 component中， component 发现自身已经定义了 slot, 就会把这个字符串放到slot的位置，然后显示出来。 