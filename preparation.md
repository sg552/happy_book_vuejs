# 开发环境的搭建

npm: 3.10.8 (npm > 3.0)

node: v6.9.1 (node > 6.0)

vue: 2.0+

总的来说，只要能安装上node 和 vuejs就可以。

## 安装NVM 和 node 

请看对应章节。

## 安装git

请看对应章节。

## 安装vuejs

要同时安装 `vue`和 `vue-cli`这两个node package.

运行下面这个命令：

```
$ npm install vue vue-cli -g
```

`-g` 表示这个包安装后可以被全局使用。 

## 运行 vue

创建一个基于 webpack 模板的新项目:

```
$ vue init webpack my-project
```

注意： 我们使用Vue, 都是在 `webpack` 这个大前提下使用的。

安装依赖:

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
> test_vue_0613@1.0.0 dev /workspace/test_vue_0613
> node build/dev-server.js

> Starting dev server...


 DONE  Compiled successfully in 12611ms   12:16:47 PM

> Listening at http://localhost:8080
```

我们打开 `http://localhost:8080` 就可以看到刚才创建的项目欢迎页, 如下图所示：

![默认欢迎页](./images/vue_default_hello.jpg)
