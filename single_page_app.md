# 单页应用框架对比


## 不要用Angular
angular: 老牌框架. 源于google. 难学, 难用. 文档垃圾.

13年7月做项目. angular 1. 它的文档: directive. 被无数人(老外)骂: 看不懂. 'The worst document that I've ever read'
3 个月没变. (很多留言都是一年以前的)

所以说最大的教训:
1. google 也有很多很烂的东西.
2. 关注度特别高的框架,不一定适合自己. 小王都认为很好, 但是我自己试过,我觉得不好.

优酷: app 置换系统, 就是我做的.用angular + python(pyramid 框架)



## React

也是 twitter 推出的. 开源框架

不错. 比 angular 简单些. 但, 最大的弱点:

html代码居然要写在js 文件中. 无法调试.

content = function(){ "<div> ... </div>" }

大家不习惯,把前后端代码写在一起的风格.

`````````````
//前端代码

....


// 后端代码

....

`````````````

所有传统web框架过的人( java, rails, php) 都觉得奇怪.

最大的优点:  react native.  可以把js代码转换成: native app(android, ios). (效果会打折扣,也不会100% 能转化).能力有限.


## Vuejs

最大的优点:  好学,  好用.

angular; 学一个月
react; 学2个星期.
vue: 3天.

做的事儿都一样.

"途铃服务" 这个公众账号, 就是用vue来做的.

而且:  vuejs, 作者是 中国人(目前在美国google工作)  核心文档,2种语言:  中文/ 英文.

而且, 使用vue 的人,越来越多.  关注度: 28317  (2016-9-29)

angular:  52451 (但是他特别老牌,比vue提前2年出现)
react: 50376


## 为什么用vue , 不用 react, angular?


https://www.quora.com/How-does-Vue-js-compare-to-React-js

https://laracasts.com/discuss/channels/vue/vuejs-or-reactjs-which-should-i-choose-to-make-frontend/?page=1

而且vuejs 有中文文档：  cn.vuejs.org

对于小弟们上手足够快乐(了）
