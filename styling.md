# 使用样式

样式用起来特别简单.  直接写到 `<style>` 段落里面即可.

## 使用普通的css

```
<style >
td {
  border-bottom: 1px solid grey;
}
</style>
```

## 使用局部的css

```
<style scoped>
td {
  border-bottom: 1px solid grey;
}
</style>
```
这段CSS只对当前的 component 适用.

## 使用 sass等.

安装sass依赖sass-loader和node-sass：
```
$ npm i sass-loader node-sass -D
```




然后在webpack.base.conf.js中添加相关配置：

```
{
    test: /\.s[a|c]ss$/,
    loader: 'style!css!sass'
}
```

然后我们就可以在style标签中写 sass 了.
```
<style lang='sass'>
td {
  border-bottom: 1px solid grey;
}
</style>
```
