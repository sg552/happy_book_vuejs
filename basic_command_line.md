# 基本命令

这个命令都是 `vue-cli` 提供的. 可以认为是 "webpack + vuejs"的结合。 

## 建立新项目

```
$ vue init webpack my_blog
```

这个命令会建立好一个文件夹。 具体的说明，见《Webpack下的Vuejs项目文件结构》 章节。

## 安装所有的第三方包

```
$ npm install
```

这个命令是根据 "package.json" 文件中定义的内容，来安装所有用到的第三方js库。  所有的文件都会安装到 "node_module"目录下。 

着急的同学还可以 输入 `--verbose` 命令，来查看运行细节：

```
$ npm install --verbose 
```

运行结果如下： 
```
$ npm install --verbose
npm info it worked if it ends with ok
npm verb cli [ 'D:\\nodejs\\node.exe',
npm verb cli   'D:\\nodejs\\node_modules\\npm\\bin\\npm-cli.js',
npm verb cli   'install',
npm verb cli   '--verbose' ]
npm info using npm@6.1.0
npm info using node@v10.5.0
npm verb npm-session d1e752145cbb60ba
npm info lifecycle test_vue_0613@1.0.0~preinstall: test_vue_0613@1.0.0
npm timing stage:loadCurrentTree Completed in 1609ms
npm timing stage:loadIdealTree:cloneCurrentTree Completed in 12ms
npm timing stage:loadIdealTree:loadShrinkwrap Completed in 681ms
...
```

这样出现问题的时候，就很容易知道卡在哪里了。

## 在本地运行

使用下列命令：

```
$ npm run dev
```

默认就会在  localhost 的 8080端口，启动一个小型的web 服务器。 性能可以完全满足开发使用，还具备代理转发等功能。 

源代码发生改变的时候，服务器也会自动重启。 （偶尔需要手动重启）

运行的输入如下所示：

```
dashi@i5-16g MINGW64 /d/workspace/vue_js_lesson_demo (master)
$ npm run dev

> test_vue_0613@1.0.0 dev D:\workspace\vue_js_lesson_demo
> node build/dev-server.js

[HPM] Proxy created: /api  ->  http://siwei.me
[HPM] Proxy rewrite rule created: "^/api" ~> ""
> Starting dev server...
 DONE  Compiled successfully in 2373ms10:55:18

> Listening at http://localhost:8080

 WAIT  Compiling...11:02:14

 DONE  Compiled successfully in 213ms11:02:14

 WAIT  Compiling...11:06:09

 DONE  Compiled successfully in 117ms11:06:09

 WAIT  Compiling...11:06:26

 DONE  Compiled successfully in 103ms11:06:26
 ... 
```

## 打包编译

```
$ npm run build
```

该命令用来把 "src" 目录下的所有文件，都打包成 "webpack"的标准文件，供部署使用。 具体的内容见 《打包和部署》 这一章节。