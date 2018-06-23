# 开发环境的搭建

npm: 3.10.8 (npm > 3.0)

node: v6.9.1 (node > 6.0)

vue: 2.0+


整体来讲，只要能安装上node 和 vuejs就可以。nvm在windows下可以不安装。

## 安装nvm 和 node 

```
$ 
```

# 安装git

## windows下使用 git客户端。　

在这里直接下载：

https://git-scm.com/download/win

## linux下可以直接安装。

ubuntu下可以直接：

```
$ apt-get install git
```

# 安装vuejs

要同时安装 `vue`和 `vue-cli`这两个node package.

`-g` 表示给他们安装成全局可以使用的包。

```
$ cnpm install vue vue-cli -g
```

## 试运行 vue

创建一个基于 webpack 模板的新项目:

```
$ vue init webpack my-project
```

注意： 我们使用Vue, 都是在 `webpack` 这个大前提下使用的。

安装依赖, :

```
$ cd my-project
$ cnpm install
```

在本地，以默认端口来运行：

```
$ npm run dev
```

然后就可以看到 在本地已经跑起来了。

```
$ npm run dev

> test_vue_0613@1.0.0 dev /workspace/test_vue_0613
> node build/dev-server.js

> Starting dev server...


 DONE  Compiled successfully in 12611ms   12:16:47 PM

> Listening at http://localhost:8080
```

打开 `http://localhost:8080` 就可以看到。

如下图：

![默认欢迎页](./images/vue_default_hello.jpg)
