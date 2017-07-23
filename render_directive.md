# 视图中的循环v-for,判断v-if

Vuejs的视图,使用了"指令"(directive). 下面分别来说.

注意: 无论是`v-if` 还是`v-for`, 都要与某个标签结合使用. 这点跟JSP, PHP, Rails很不同.

## 循环: v-for

```
<tr v-for="blog in blogs">
  <td >{{blog.title }}</td>
</tr>
```

上面代码,会被渲染成:

```
<tr>
  <td>...</td>
  <td>...</td>
  <td>...</td>
</tr>
```

## 判断: v-if


```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

## v-if 与 v-for 的优先级

当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级。
