# 使用Computed properties(计算得到的属性)和watchers(监听器) 

很多时候，我们在页面上想要显示某个变量的值时，都需要经过一些计算， 例如： 

```
<div id="example">
  {% raw %}{{{% endraw %} some_string.split(',').reverse().join('-') }}
</div>
```

越是复杂，到后期越容易出错。 

这个时候，我们就需要一种机制，可以方便的创建这样的通过计算得来的数据。  

所以， Computed Properties 就是我们的解决方案。

## 典型例子

```
<html>
<head>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
	<div id='app'>
		<p> 原始字符串： {{my_text}} </p>
		<p> 通过运算后得到的字符串： {{my_computed_text}} </p>
	</div>
	<script>
		var app = new Vue({
			el: '#app',
			data: {
				my_text: 'good good study, day day up'
			},
			computed: {
				my_computed_text: function(){
					// 先去掉逗号，然后按照空格分割成数组，然后翻转，并用'-'来连接
					return this.my_text.replace(',', '').split(' ').reverse().join('-')
				}
			}

		})
	</script>
</body>
</html>
```

可以看到，上面的关键代码是，在 Vue的构造函数中， 传入一个 `computed`的段落。 

使用浏览器运行后，可以看到结果如下图所示：

![computed properties例子](./images/computed_properties.png)

我们也打开 console 来查看。 

输入
```
> app.my_text    
```
会得到：  "good good study, day day up"

输入

```
> app.my_computed_text
```
会得到转换后的： "up-day-day-study-good-good"

## Computed Properties 与 普通方法的区别。

根据上面的例子，我们可以使用 普通方法来实现： 

```
<html>
<head>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
	<div id='app'>
		<p> 原始字符串： {{my_text}} </p>
		<p> 通过运算后得到的字符串： {{my_computed_text() }} </p>
	</div>
	<script>
		var app = new Vue({
			el: '#app',
			data: {
				my_text: 'good good study, day day up'
			},
			methods: {
				my_computed_text: function(){
					return this.my_text.replace(',', '').split(' ').reverse().join('-') + '，我来自于 function, 不是computed '
				}
			}
		})
	</script>
</body>
</html>
```

上面的代码，运行后如下图所示： 

![使用function代替computed properties](./images/computed_properties_use_function.png)

可以发现，他们达到的效果是一样的。 

他们的区别在于：  使用computed properties的方式，会把结果“缓存”起来。  每次调用对应的computed properties时，只要对应的依赖数据没有改动， 
那么就不会变化。 

而使用 "function" 实现的版本，则不存在缓存问题。 每次都会重新计算对应的数值。 

所以， 我们需要按照实际情况，来选择是使用 "computed properties" ， 还是使用普通function的形式。

