# Webpack下的Vuejs项目文件结构



我们看一下全局的文件结构：

```
▸ build/                // 编译用到的脚本
▸ config/               // 各种配置
▸ dist/                 // 打包后的文件夹
▸ node_modules/         // node第三方包
▸ src/                  // 源代码
▸ static/               // 静态文件, 暂时无用
  index.html            // 最外层文件
  package.json          // node项目配置文件
```


## build

保留各种打包脚本。不可或缺，不要随意修改。

展开后如下：

```
▾ build/
    build.js
    check-versions.js
    dev-client.js
    dev-server.js
    utils.js
    vue-loader.conf.js
    webpack.base.conf.js
    webpack.dev.conf.js
    webpack.prod.conf.js
```

- build.js:

打包使用，  不要修改。

- check-versions.js:

检查npm的版本， 不要修改。

- dev-client.js 和 dev-server.js:

是在开发时使用的服务器脚本。不要修改。（借助于node这个后端语言，我们
在做vuejs开发时，可以通过 `$npm run dev `这个命令，打开一个小的server, 运行vuejs. )

- utils.js

不要修改。 做一些css/sass 等文件的生成。

- vue-loader.conf.js

非常重要的配置文件，不要修改。内容是用来辅助加载vuejs用到的css source map等内容。

- webpack.base.conf.js
- webpack.dev.conf.js
- webpack.prod.conf.js

这三个都是基本的配置文件。不要修改。

## config

跟部署和配置相关。

```
▾ config/
    dev.env.js
    index.js
    prod.env.js
```

- dev.env.js
开发模式下的配置文件，一般不用修改。

- prod.env.js
生产模式下的配置文件，一般不用修改。

- index.js
很重要的文件， 定义了 开发时的端口（默认是8080），定义了图片文件夹（默认static)，
定义了开发模式下的 代理服务器. 我们修改的还是比较多的。

## dist

打包之后的文件所在目录，如下。

```
▾ dist/
  ▾ static/
    ▾ css/
        app.d41d8cd98f00b204e9800998ecf8427e.css
        app.d41d8cd98f00b204e9800998ecf8427e.css.map
    ▾ js/
        app.c482246388114c3b9cf0.js
        app.c482246388114c3b9cf0.js.map
        manifest.577e472792d533aaaf04.js
        manifest.577e472792d533aaaf04.js.map
        vendor.5f34d51c868c93d3fb31.js
        vendor.5f34d51c868c93d3fb31.js.map
    index.html
```

可以看到，对应的css, js, map, 都在这里。

这个文件夹不要放到git中。

## node_modules

node项目所用到的第三方包，特别多，特别大。  `$ npm install` 所产生。

这个文件夹不要放到git中。

## src

最最核心的源代码所在的目录。

```
▾ src/
  ▾ assets/
      logo.png
  ▾ components/
      Book.vue
      BookList.vue
      Hello.vue
  ▾ router/
      index.js
    App.vue
    main.js
```

- assets: 用到的图片
- components: 用到的"视图"和"组件"所在的文件夹。（最最核心）
- router/index.js  路由文件。 定义了各个页面对应的url.
- App.vue
如果index.html 是一级页面模板的话，这个App.vue就是二级页面模板。
所有的其他vuejs页面，都作为该模板的 一部分被渲染出来。
- main.js
废代码。没有实际意义，但是为了支撑整个vuejs框架，存在很必要。
