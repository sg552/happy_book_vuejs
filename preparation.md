# 开发环境的搭建

npm: 3.10.8 (npm > 3.0)

node: v6.9.1 (node > 6.0)

vue: 2.0+


整体来讲，只要能安装上node 和 vuejs就可以。nvm在windows下可以不安装。

# 安装nvm (windows下的同学可以略过）

用nvm安装node, 官网：https://github.com/creationix/nvm


## 1. 下载

```
git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```

## 2. 启动时加载：

```
# 把下面这行代码放到： ~/.bashrc  ~/.bash_profile ~/.zshrc 中。
source ~/.nvm/nvm.sh
```

## 3. 运行： $ nvm

注意： 不能使用 `$ which nvm` 来验证安装是否成功。因为即使成功了也不会 有
`$ which nvm` 返回结果。

## 使用

1. 列出所有可以安装的版本：

```
$ nvm list-remote
```

2. 列出本地安装好了的版本：

```
$ nvm list
```

3. 安装：

```
$ nvm install v0.10.37
```

4.使用：

```
$ nvm alias default 0.10.32  # 把这句命令放到 ~/.bashrc 中。
```

## 官方的例子：

```
  nvm install v0.10.32                  Install a specific version number
  nvm use 0.10                          Use the latest available 0.10.x release
  nvm run 0.10.32 app.js                Run app.js using node v0.10.32
  nvm exec 0.10.32 node app.js          Run `node app.js` with the PATH pointing to node v0.10.32
  nvm alias default 0.10.32             Set default node version on a shell
```

## 删除

直接手动删掉对应的配置文件：~/.nvm,  ~/.npm ~/.bower 即可。

## 通过nvm 安装node
安装好 nvm 后，　就可以安装node了。

```
$ nvm install v6.9.1
```

如果已经安装过了nvm, 可以直接切换版本:

```
$ nvm use 6.9.1
```

## nvm 国内安装速度太慢的办法

使用下面的命令，就可以在国内下载node了。

```
$ NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/dist nvm install
```

## 用cnpm安装vue, vue-cli, vue-router等等 ( vue-router > 2.0)

npm 是 node package manager.

考虑到国内安装太慢，我们一般使用国内的镜像。

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

或者直接通过添加 npm 参数 alias 一个新命令:

```
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
```

然后，就可以通过国内（淘宝服务器）来安装node的包了，例如：

```
$ cnpm install vue-cli -g
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
