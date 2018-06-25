# Hybrid App: 混合式App

目前App几乎是每个互联网公司的标配。 但是不是每个团队都具备开发原生app的能力。

于是出现了以 phonegap, titanium, xamarin, react native 等一系列的 混合式App. 

我们可以大概了解一下：

- phonegap: 出现的最早，使用了很多H5的技术来实现原生app的功能，例如拍照等。 很有新意。 不过完全没有实用价值。 响应速度特别慢。 卡顿非常明显。 

- titanium: 出现的比较早。性能不错。 跟小程序很类似，使用js,css的类似技术，在不同平台上只要稍加修改代码，就可以跨平台媲美原生App. 缺点是有学习曲线，特别是module很难写。 
公司被收购了。

- xamarin： 使用 .NET 来实现，跟titanium 很接近。 也有不小的使用群体。

- react native: 使用js 黑科技，直接生成 Android/IOS, 原理与titanium， xamarin一样。 但是是目前走的最远的 混合式开发方式。 性能也很高。 

## 共同的缺点

无论是Titanium, 还是 Xamarin, React native，包括 Weex , 都属于 使用 js/.net ，然后把代码改造成 可以被 Android/IOS 的 javascript virtual machine所能接受的情况。

也就是说，对原生的Android/IOS平台做了封装。 

这样的好处，为两个不同的编程语言增加了一个统一的编程入口。 

缺点也非常明显： 做一些普通的事情（展示页面，点击按钮）没问题， 但是一旦需要用到第三方应用（定制化的地图，定制化的身份证识别，人脸识别等等），就需要开发人员具备写“native module”
的能力。 这就要求开发人员 同时精通 Android / IOS （写这种 native module的要求比单纯使用的要求要高得多） 而这背离了 这些技术的初衷 （初衷是让不太懂 app 编程的人可以快速上手开发）。

## 原生的壳儿 + Webview的开发方式，只适用于IOS.

还有一种，就是原生的壳儿 + Webview的开发方式。

- 原生的壳儿，指的是： 外壳部分完全使用100%的 native app. 
- Webview: 所有的页面，都是放到了Webview中来展示。 

这个情况，经过我们的实践，对于 IOS 设备是可行的。 安卓是不行的。

IOS： 机器硬件性能好， 软件使用Object C 开发，所以用起来效果非常棒，跟native App的体验是一模一样的。 每个页面都可以瞬间打开，而且页面滑动非常流畅。
但是在开发层面上，几乎不用考虑页面的适配。 这个解决了很大的问题。

Android: 机器硬件性能稍差于苹果， 软件使用 java 开发，性能比 Object C差。 而且在 Android中， Webview的性能体验比 IOS的差太多。 每个页面打开速度是3-10秒。
而且卡顿严重。 

我们曾经试着在优化的路子上走了一段时间，发现对于Android + Webview(Vuejs) 的方式，前期开发成本低于原生， 后期维护成本远高于原生，而且一些问题在混合的架构下, 无解。 

所以，我们的结论： 

开发App,  IOS可以使用混合式开发, Android 务必使用原生开发。 