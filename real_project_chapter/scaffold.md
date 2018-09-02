# 整体项目的搭建

## 为新项目生成骨架 

创建一个基于 webpack 模板的新项目:

```
$ vue init webpack shop_h5
```

安装依赖:

```
$ cd shop_h5
$ cnpm install
```

在本地，以默认端口来运行：

```
$ npm run dev
```

然后就可以看到 在本地已经跑起来了。

在这个阶段， 我们只需要修改它的标题就可以：


打开  根目录下的 index.html , 修改<title>字段: 
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>公益爱农</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

用浏览器打开后， 就可以看到一个没有内容的 Vuejs应用已经跑起来了。