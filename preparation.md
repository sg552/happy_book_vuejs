
开发环境

npm: 3.10.8 (npm > 3.0)

node: v6.9.1 (node > 6.0)

vue: 2.0.1


# 安装nvm

用nvm安装node, 官网：https://github.com/creationix/nvm

安装：

1. 下载

git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`

2. 启动时加载：

# 把下面这行代码放到： ~/.bashrc  ~/.bash_profile ~/.zshrc 中。
source ~/.nvm/nvm.sh

3. 运行： $ nvm

注意： 不能使用 $ which nvm 来验证安装是否成功。因为即使成功了也不会 有 $ which nvm 返回结果。

使用

1. 列出所有可以安装的版本：

$ nvm list-remote

2. 列出本地安装好了的版本：

$ nvm list

3. 安装：

$ nvm install v0.10.37

4.使用：

$ nvm alias default 0.10.32  # 把这句命令放到 ~/.bashrc 中。

官方的例子：

  nvm install v0.10.32                  Install a specific version number
  nvm use 0.10                          Use the latest available 0.10.x release
  nvm run 0.10.32 app.js                Run app.js using node v0.10.32
  nvm exec 0.10.32 node app.js          Run `node app.js` with the PATH pointing to node v0.10.32
  nvm alias default 0.10.32             Set default node version on a shell
删除

直接手动删掉：~/.nvm,  ~/.npm ~/.bower 即可。

## 通过nvm 安装node
安装好 nvm 后，　就可以安装node了。

$ nvm install v6.9.1

如果已经安装过了nvm, 可以直接切换版本:

$ nvm use 6.9.1

## nvm 国内安装速度太慢的办法

$ NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/dist nvm install

## 用cnpm安装vue, vue-cli, vue-router等等 ( vue-router > 2.0)

npm 是 node package manager.

考虑到国内安装太慢，我们一般使用国内的镜像。

$ npm install -g cnpm --registry=https://registry.npm.taobao.org
或者你直接通过添加 npm 参数 alias 一个新命令:

alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"

例如：

$ cnpm install vue-cli

# 安装git

## windows下使用 git客户端。　

https://git-scm.com/download/win

## linux下可以直接安装。

$ apt-get install git


# 安装vuejs

$ cnpm install vue

## 试运行 vue

全局安装 vue-cli:

$ npm install --global vue-cli

创建一个基于 webpack 模板的新项目:

$ vue init webpack my-project

安装依赖, :
$ cd my-project
$ cnpm install

运行：
$ npm run dev

然后就可以看到 在本地已经跑起来了。
