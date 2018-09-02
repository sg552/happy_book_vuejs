# 轮播图

用户登录到首页之后， 第一个看到的内容，就是轮播图。 (见前面的原型图)

所以，我们接下来，要为首页增加它。  

## 1. 增加路由

路由文件(src/router/index.js)，对应位置，增加： 

```
import Index from '@/views/shops/index'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Home',
      component: Index
    }
  ]
```

## 2. 增加对应页面

src/views/shops/index.vue

```
<template>
  <div class="background">
    <div class="home">
      <div class="m_layout">
        <!-- 轮播图-->
        <HomeBannerView></HomeBannerView>
        <!--导航-->
        <HomeNavView></HomeNavView>
        
        <span class="divider" style="height: 4px;"></span>
        <div class="product_top">
          <div class="product_left">
            <div>商品列表</div>
          </div>
        </div>
        <span class="divider" style="height: 2px;"></span>
        <!-- 特产商品 -->
        <SpecialMarket :id="good.id" :name="good.name" :description="good.description" :image_url="good.image_url" v-for="good in goods"></SpecialMarket>
      </div>
    </div>
    <NavBottomView :is_shops_index="is_shops_index"></NavBottomView>
  </div>
</template>
<script>
    // 轮播图需要的js文件
    import {bindEvent,scrollPic} from '../../libs/index.js'
    // 轮播图需要的前台文件
    import HomeBannerView from '../../components/HomeBanner.vue';
    // 商品分类
    import HomeNavView from '../../components/HomeNav.vue';

    // 特产，商品的列表
    import SpecialMarket from '../../components/SpecialMarket.vue';

    // 底部4个TAB， 下一节会讲到
    import NavBottomView from '../../components/NavBottom.vue';

    export default{
      data () {
        return {
          goods: [],
          is_shops_index: true,
        }
      },
       components:{
        HomeHeaderView,
        HomeBannerView,
        HomeNavView,
        HomeMainView,
        SpecialMarket,
        NavBottomView
       },
       mounted () {
        //bindEvent();
        scrollPic();
        this.loadPage ();
       },
       computed:  {
       },
       methods: {
         loadPage () {
           this.$http.get(this.$configs.api + 'goods/get_goods').then((response)=>{
             console.info(response.body)
             this.goods= response.body.goods
           },(error) => {
             console.error(error)
           });
         },
       }
    }
</script>

```

上面的代码中， 

- 先是读取了一个API
- 渲染数据
- 实现首页的轮播图



## 3. 增加轮播图

我们做开发的核心方法论： 不要造轮子。 

一定要造轮子的话， 先搜索一下是否已经有了现成的轮子。 

轮播图是最最常见的组件， 所以一定会有别人写好的第三方包， 我们拿过来用就好。 

经过一番考察， 我们发现这个项目不错： 

所以， 直接拿过来用。  


3.1 轮播图的组件

我们需要在src/views/shops/index.vue中，增加： 

```
import {bindEvent,scrollPic} from '../../libs/index.js'
```

然后， 增加对应的文件（libs/index.js)

```

function $id(id) {
    return document.getElementById(id);
}

function bindEvent() {
    var sea = $id("my_search");
    /*banner对象*/
    var banner = $id("my_banner");
    /*高度*/
    var height = banner.offsetHeight;
    window.onscroll = function() {
        var top = document.body.scrollTop;
        /*当滚动高度大于banner的高度时候颜色不变*/
        if (top > height) {
            sea.style.background = "rgba(201,21,35,0.85)";
        } else {
            var op = top / height * 0.85;
            sea.style.background = "rgba(201,21,35," + op + ")";
        }
    };
}

function scrollPic() {
    var imgBox = document.getElementsByClassName("banner_box")[0];
    var width = $id("my_banner").offsetWidth;
    var pointBox = document.getElementsByClassName("point_box")[0];
    var ols = pointBox.children;
    var indexx = 1;
    var timer = null;
    var moveX = 0;
    var endX = 0;
    var startX = 0;
    var square = 0;

    function addTransition() {
        imgBox.style.transition = "all .3s ease 0s";
        imgBox.style.webkitTransition = "all .3s ease 0s";
    }

    function removeTransition() {
        imgBox.style.transition = "none";
        imgBox.style.webkitTransition = "none";
    }

    function setTransfrom(t) {
        imgBox.style.transform = 'translateX(' + t + 'px)';
        imgBox.style.webkitTransform = 'translateX(' + t + 'px)';
    }

    // 开始动画部分
    pointBox.children[0].className = "now";
    for (var i = 0; i < ols.length; i++) {
        ols[i].index = i; // 获得当前第几个小li 的索引号
        ols[i].onmouseover = function() {
            // 所有的都要清空
            for (var j = 0; j < ols.length; j++) {
                ols[j].className = "";
            }
            this.className = "now";
            setTransfrom(-indexx * width);
            square = indexx; 
        }
    }
    timer = setInterval(function() {
        indexx++;
        addTransition();
        setTransfrom(-indexx * width);
        // 小方块
        square++;
        if (square > ols.length - 1) {
            square = 0;
        }
        // 先清除所有的
        for (var i = 0; i < ols.length; i++) 
        {
            ols[i].className = "";
        }
        // 留下当前的
        ols[square].className = "now"; 
    }, 3000);

    imgBox.addEventListener('transitionEnd', function() {
        if (indexx >= 9) {
            indexx = 1;
        } else if (indexx <= 0) {
            indexx = 8;
        }
        removeTransition();
        setTransfrom(-indexx * width);
    }, false);

    imgBox.addEventListener('webkitTransitionEnd', function() {
        if (indexx >= 9) {
            indexx = 1;
        } else if (indexx <= 0) {
            indexx = 8;
        }
        removeTransition();
        setTransfrom(-indexx * width);
    }, false);

    /**
     * 触摸事件开始
     */
    imgBox.addEventListener("touchstart", function(e) {
        console.log("开始");
        var event = e || window.event;
        //记录开始滑动的位置
        startX = event.touches[0].clientX;
    }, false);

    /**
     * 触摸滑动事件
     */
    imgBox.addEventListener("touchmove", function(e) {
        console.log("move");
        var event = e || window.event;
        event.preventDefault();

        //清除定时器
        clearInterval(timer);
        //记录结束位置
        endX = event.touches[0].clientX;
        //记录移动的位置
        moveX = startX - endX;
        removeTransition();
        setTransfrom(-indexx * width - moveX);
    }, false);

    /**
     * 触摸结束事件
     */
    imgBox.addEventListener("touchend", function() {
        console.log("end");
        //如果移动的位置大于三分之一，并且是移动过的
        if (Math.abs(moveX) > (1 / 3 * width) && endX != 0) {
            //向左
            if (moveX > 0) {
                indexx++;
            } else {
                indexx--;
            }
            //改变位置
            setTransfrom(-indexx * width);
        }
        //回到原来的位置
        addTransition();
        setTransfrom(-indexx * width);
        //初始化
        startX = 0;
        endX = 0;

        clearInterval(timer);
        timer = setInterval(function() {
            indexx++;
            square++;
            if (square > ols.length - 1) {
                square = 0;
            }
            // 先清除所有的
            for (var i = 0; i < ols.length; i++) 
            {
                ols[i].className = "";
            }
            // 留下当前的
            ols[square].className = "now"; 
            addTransition();
            setTransfrom(-indexx * width);

        // 每3秒钟轮播图变化一次。
        }, 3000);
    }, false);
};

module.exports = {
    bindEvent,
    scrollPic
}

```


3.2 轮播图的视图层

```
<!-- 轮播图-->
<HomeBannerView></HomeBannerView>   
```

上面的代码， 会直接生成一个轮播图。


我们创建这个component, 增加： src/components/HomeBanner.vue, 

```
<template>
	<div class="home_ban">
		<div class="m_banner clearfix" id="my_banner">
	        <ul class="banner_box">
	            <!-- 更改这里就可以替换轮播图的图片了 -->
	            <li><img src="http://siweitech.b0.upaiyun.com/image/silulegou/2FgHsjCz7qfpSQr0.jpeg" alt="" /></li>
	            <li><img src="http://siweitech.b0.upaiyun.com/image/silulegou/uJawxX6H3PBRcfMO.jpeg" alt="" /></li>
	        </ul>
	        <ul class="point_box" >
	            <li></li>
	            <li></li>
	        </ul>
        </div>
	</div>
</template>
```

这个component的内容非常简单。 它只是一个轮播图组件的View. 我们只需要更换上面代码中的两个图片文件就好了。

## 4. 增加物品分类

```
<!--商品分类-->
<HomeNavView></HomeNavView>
```

上面的代码， 会直接生成一个物品分类区域

我们创建这个component: 增加： src/components/HomeNav.vue

```
<template>
	<div class="home_n">
		<nav class="m_nav">
                <ul>
                    <li class="nav_item">
                        <a href="#" class="nav_item_link">
                            <img src="../assets/images/nav0.png" alt="">
                            <span>草原特色肉</span>
                        </a>
                    </li>
                    <li class="nav_item">
                        <a href="#" class="nav_item_link">
                            <img src="../assets/images/nav1.png" alt="">
                            <span>特色干果</span>
                        </a>
                    </li>
                    <li class="nav_item">
                        <a href="#" class="nav_item_link">
                            <img src="../assets/images/nav9.png" alt="">
                            <span>特色瓜子</span>
                        </a>
                    </li>
                    <li class="nav_item">
                        <a href="#" class="nav_item_link">
                            <img src="../assets/images/nav8.png" alt="">
                            <span>特色大米</span>
                        </a>
                    </li>
                </ul>
            </nav>
	</div>
</template>

```

之所以这样写， 是考虑到前期的商品分类不多。 在下一个版本会改成读取后台的接口。 


## 看效果  

默认页面效果如下：

![图1](/images/real_project/slider_1.png)

三秒钟之后， 轮播图发生了滚动：

![图2](/images/real_project/slider_2.png)

## 总结

我们使用了 现成的轮播图组件。 可以看到， 非常简单。 步骤是：

1. 复制对应组件的js 文件到src/lib下。
2. 复制对应组件的vue文件到src/components下
3. 在对应的vue文件中使用它们。

