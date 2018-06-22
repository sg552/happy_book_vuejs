# 视图中的Directive (指令)

我们在学习java的时候，知道有jsp 页面， 对于.net语言，有 .asp, aspx页面， 对于ruby, 有erb这样的页面。

在Vuejs中，我们也有类似的编程能力。 

但是由于 Vuejs 是一种框架，所以它的稍微特殊一些，只能与标签做结合使用。 叫做Directive. (指令)

我们之前看到的 `v-on`, `v-bind` 等，以`v`开头的，都是Directive. 

原理： 

1. 用户在浏览器中输入网址，回车. 
2. 浏览器加载所有的资源（js, html内容。） 此时尚未解析。
3. 浏览器加载Vuejs  
4. Vuejs程序被执行， 发现 页面中的 `Directive`, 进行相关的解析
5. HTML中的内容被替换。 展现给用户。

所以，我们在开发一个Vuejs项目的时候，会看到大量的Directive。 这里的基础务必打好。

## 循环: v-for


完整的例子如下：

```
<html>
<head>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
	<div id='app'>
		<p>Vuejs周边的技术生态有： <p>
		<br/>
		<ul>
			<li v-for="tech in technologies">
				{% raw %}{{{% endraw %}tech}}
			</li>
		</ul>
	</div>
	<script>
		var app = new Vue({
			el: '#app', 
			data: {	
				technologies: [
					"nvm", "npm", "node", "webpack", "ecma_script"
				]
			}
		})
	</script>
</body>
</html>
```

可以注意到，上面代码中的 `technologies`是在`data` 中被定义的： 

```
data: {	
	technologies: [
		"nvm", "npm", "node", "webpack", "ecma_script"
	]
}
```

然后在下面代码中， 被循环显示: 

```
<li v-for="tech in technologies">
	{{tech}}
</li>
```

用浏览器打开上面代码后，如下图所示： 

![v-for循环](./images/directive-v-for.png)

## 判断: v-if

条件Directive, 是由 `v-if`, `v-else-if`, `v-else` 配合完成的。 下面是个完整的例子： 

```
<html>
<head>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
	<div id='app'>
		<p>我们要使用的技术是： <p>

		<div v-if="name === 'vuejs'">
			Vuejs !
		</div>
		<div v-else-if="name === 'angular'">
			Angular
		</div>
		<div v-else>
			React
		</div>		
	</div>
	<script>
		var app = new Vue({
			el: '#app', 
			data: {	
				name: 'vuejs'
			}
		})
	</script>
</body>
</html>
```

注意，

上面的代码中，  `v-if` 后面的引号中，是 `name === 'vuejs'`, `===` 是 Ecmascript 的语言， 表示严格的判断。 
（由于js的 `==` 有先天的缺陷，所以我们在95%的情况下， 都是用 三个等号的形式) 


用浏览器打开上面代码后，如下图所示： 

![v-if 判断](./images/directive-v-if.png)

## v-if 与 v-for 的优先级

当 `v-if` 与 `v-for` 一起使用时，`v-for` 具有比 `v-if` 更高的优先级。 也就是说，Vuejs 会先执行 `v-for`, 再执行 `v-if` . 

下面是个完整的例子：

```
<html>
<head>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
	<div id='app'>
		<p> 全部的技术是： {{technologies}} </p>
		<p> v-for 与 v-if 的结合使用, 只打印出 以"n"开头的技术： <p>
		<ul>
			<li v-for="tech in technologies" v-if="tech.indexOf('n') === 0">
				{% raw %}{{{% endraw %}tech}}
			</li>
		</ul>
	</div>
	<script>
		var app = new Vue({
			el: '#app', 
			data: {	
				technologies: [
					"nvm", "npm", "node", "webpack", "ecma_script"
				]
			}
		})
	</script>
</body>
</html>
```

可以看到， 在下面的代码中， `v-if` 与 `v-for`结合使用了， 先是做了循环 `tech in technologies`，然后对当前的 循环对象 `tech` 做了判断： 

```
<li v-for="tech in technologies" v-if="tech.indexOf('n') === 0">
	{% raw %}{{{% endraw %}tech}}
</li>
```

用浏览器打开上面代码后，如下图所示： 

![v-for与 v-if的结合使用](./images/directive-v-for-and-v-if.png)


## v-bind

## v-on

`v-on` 指令用于触发事件。  例如： 

```
<html>
<head>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
	<div id='app'>
		{{ message }}
		<br/>
		<button v-on:click='highlight' style='margin-top: 50px'>真的吗</button>
	</div>

	<script>
		var app = new Vue({
			el: '#app', 
			data: {
				message: '学习Vuejs使我快乐~ '
			},
			methods:  {
				highlight: function() {
					this.message = this.message + '是的， 工资还会涨~!'
				}
			}

		})
	</script>
</body>
</html>
```

上面的代码中， 通过`v-on:click` 的声明，当 <button> 被点击(click)后，就会触发  `highlight` 这个方法。 

点击前的页面: 

![点击前](./images/directive-v-on-click-before.png)

点击后的页面: 

![点击后](./images/directive-v-on-click-after.png)


`v-on` 后面可以接HTML的标准事件， 例如： 

- click  （单击 鼠标左键）
- dblclick (双击鼠标左键)
- contextmenu (单机鼠标右键)
- mouseover  (指针移到有事件监听的元素或者它的子元素内)
- mouseout   (指针移出元素，或者移到它的子元素上)
- keydown   （键盘动作： 按下任意键) 
- keyup     (键盘动作： 释放任意键)

## v-model