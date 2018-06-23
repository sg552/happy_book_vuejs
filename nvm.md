# NVM

NVM, 全名为"Node Version Manager", 是非常好用的Node版本管理器。 

这个技术出现的原因，是因为很多时候，我们的不同的项目，node版本是不同的。 有的是 `5.0.1`, 有的是 `6.3.2`

如果node版本不对的话，运行某个应用时，很可能会遇到各种莫名其妙的问题。 

所以，我们需要在同一台机器上，同时安装多个版本的node .  所以NVM应用而生，很好的帮我们解决了这个问题。

官网：https://github.com/creationix/nvm

## 安装

1.下载nvm的源代码。 运行下面命令即可。

```
$ git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```

2.为脚本设置启动时加载：

把下面这行代码放到： `~/.bashrc`, 或  `~/.bash_profile`, 或 `~/.zshrc` 中。

```
$ source ~/.nvm/nvm.sh
```

（对于使用windows的同学，可以直接无视上面这两步，到官网下载exe安装文件就可以了）

## 运行

注意： 不能使用 `$ which nvm` 来验证安装是否成功。因为即使成功了也不会返回结果。

直接在命令行下， 输入 

```
$ nvm 
```

就可以了。  如果安装成功的话，会看到一些英文。如下所示：

```
Running version 1.1.6.

Usage:

  nvm arch                     : Show if node is running in 32 or 64 bit mode.
  nvm install <version> [arch] : The version can be a node.js version or "latest" for the latest stable version....
  nvm list [available]         : List the node.js installations. Type "available" at the end to see what can be ...
  nvm on                       : Enable node.js version management.
```

## 使用

1.列出所有可以安装的node版本：

```
$ nvm list-remote
```

对于windows的同学来说，可以跳过这一步。 因为Windows上的NVM功能是比较有限的。 不具备这个命令。

2.列出本地安装好了的版本：

```
$ nvm list
```

结果例如： 

```
$ nvm list

  * 10.5.0 (Currently using 64-bit executable)
    6.9.1
```

表示，我的系统中安装了两个node版本，一个是 6.9.1 , 一个是 10.5.0  . 默认的node版本是 10.5.0

3.安装

可以根据上面的 `nvm list-remote`的结果来安装。 对于windows的用户，也可以 `nvm install latest` 来安装最新版。

```
$ nvm install v10.5.0
```

安装好之后，退出命令行并重新进入即可。 

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

对于Linux, Mac, 直接手动删掉对应的配置文件（如果有的话）即可。

- `~/.nvm`
- `~/.npm` 
- `~/.bower` 

对于Windows, 则直接在控制面板中卸载软件就可以。 

## 国内安装速度太慢的办法

由于某些原因，在国内连接国外的服务器会比较慢，所以我们使用下面的命令，就可以在国内的镜像服务器下载node了。

```
$ NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/dist nvm install
```

## 用cnpm代替 npm 命令。

考虑到国内安装太慢，我们一般使用国内的镜像。 （感谢taobao提供）

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

对于Linux, Mac用户，可以通过直接创建一个 "alias" 命令： 

```
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
```

然后，就可以通过国内的淘宝服务器来安装node的包了，例如：

```
$ cnpm install vue-cli -g
```