# 注册微信的相关账号并下载开发者工具

## 三个平台账号

微信的H5页面会涉及到一些功能（登录，分享等）， 所以我们需要事先了解一下微信的产品家族。 

- 微信公众平台： 包括服务号， 订阅号。  网址： https://mp.weixin.qq.com
- 微信开放平台:  给“手机App”提供登录分享等操作。  网址： https://open.weixin.qq.com/
- 微信商户平台： 提供微信支付的功能。 https://pay.weixin.qq.com

几乎无论是新手，还是老手，都会在这里发蒙。 所以大家务必做好必要的笔记。 另外，每申请一个账号， 就要把用户名和密码记录下来。 上面三个平台的账号都是独立的。
并且每个账号中几乎都有自己的secret等 独立密码。

对于公司来说，需要准备好相关的证照 ，并且在对应的时间内使用公司账号打款给微信。 由于过程比较繁琐，所以申请的步骤略。 

各位同学不要打退堂鼓，我们在真实的项目中，几乎每个互联网公司，都是一定会用到微信公众号的功能的。 

下面的内容，我们假设已经成功的申请到了微信的相关账户， 公众平台上的是“服务号”。 （具有支付功能）


## 微信开发者工具

由于微信自带浏览器的特殊性（一定会自带weixin openid等微信独有的信息） ， 这就导致我们平时使用的普通浏览器，在开发微信相关功能的时候（授权， 分享，支付等）是无法使用的。 
所以我们需要下载微信的开发者工具。 地址： https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

如果上述地址有变化，我们也可以自行百度搜索: "微信开发者工具"。

下载页面如下图所示：

![开发者工具下载页面](/images/real_project/developer_tool_download_page.png)

下载后，双击开始安装， 安装后会出现登录页面， 如下图所示：

![开发者工具登录页面](/images/real_project/developer_tool_login_page.png)

扫描后，可以看到有两个入口， 一个是微信小程序， 另一个是公众号网页项目， 如下图所示：

![开发者工具登录后选择入口页面](/images/real_project/developer_tool_choose_item.png)

打开后，可以看到，几乎跟chrome developer tool是一模一样的。 除了： 

- 左上角提供了wifi的信号选择. 
- 右上角提供了 “清缓存” 这个功能。
- 左上角可以看到当前登录的微信用户的图标

如下图所示：

![开发者工具界面](/images/real_project/developer_tool_default_page.png)

目前虽然网上有一些Linux的开源组件， 但是基本没有windows和mac上的好用。 所以建议Linux的开发同学， 暂时回到windows的开发环境。 