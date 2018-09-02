# 底部Tab

页面的底部Tab是非常重要的部分， 哪个页面都会用到。 

下面就是使用的步骤

## 1. 在首页中引用底部Tab

```
<template>
  <div class="background">
    <div class="home">
      <div class="m_layout">
        <!-- 轮播图-->
        <HomeBannerView></HomeBannerView>
      </div>
    </div>
    <!-- 这里就是底部Tab -->
    <NavBottomView :is_shops_index="is_shops_index"></NavBottomView>
  </div>
</template>
<script>

    // 这里就是底部Tab对应的vue文件
    import NavBottomView from '../../components/NavBottom.vue';
</script>
```

## 2. 增加对应的component文件

增加 /components/NavBottom.vue ：

```
<template>
  <div class="footer">
  	<footer class="fixBottomBox">
        <ul>
            <router-link tag="li" to="/" class="tabItem">
              <a href="javascript:;" class="tab-item-link" v-if="is_shops_index">
                <img src="../assets/footer01.png" alt="" class="tabbar-logo">
                <p class="tabbar-text" style="color: rgba(234, 49, 6, 0.66);">首页</p>
              </a>
              <a href="javascript:;" class="tab-item-link" else>
                <img src="../assets/footer001.png" alt="" class="tabbar-logo">
                <p class="tabbar-text">首页</p>
              </a>
            </router-link>
            <router-link tag="li" to="/shops/category" class="tabItem">
                <a href="javascript:;" class="tab-item-link" v-if="is_category">
                    <img src="../assets/footer02.png" alt="" class="tabbar-logo">
                    <p class="tabbar-text" style="color: rgba(234, 49, 6, 0.66);">分类</p>
                </a>
                <a href="javascript:;" class="tab-item-link" else>
                  <img src="../assets/footer002.png" alt="" class="tabbar-logo">
                  <p class="tabbar-text">分类</p>
                </a>
            </router-link>
            <router-link tag="li" to="/cart2" class="tabItem">
                <a href="javascript:;" class="tab-item-link" v-if="is_cart">
                  <img src="../assets/footer03.png" alt="" class="tabbar-logo">
                  <p class="tabbar-text" style="color: rgba(234, 49, 6, 0.66);">购物车</p>
                </a>
                <a href="javascript:;" class="tab-item-link" else>
                  <img src="../assets/footer003.png" alt="" class="tabbar-logo">
                  <p class="tabbar-text">购物车</p>
                </a>
            </router-link>
            <router-link tag="li" to="/mine" class="tabItem">
                <a href="javascript:;" class="tab-item-link" v-if="is_mine">
                  <img src="../assets/footer04.png" alt="" class="tabbar-logo">
                  <p class="tabbar-text" style="color: rgba(234, 49, 6, 0.66);">我的</p>
                </a>
                <a href="javascript:;" class="tab-item-link" else>
                  <img src="../assets/footer004.png" alt="" class="tabbar-logo">
                  <p class="tabbar-text">我的</p>
                </a>
            </router-link>
        </ul>
    </footer>
  </div>
</template>

 <script>
    export default{
      data () {
        return {
        }
      },
      props: {
        is_shops_index: Boolean,
        is_category: Boolean,
        is_cart: Boolean,
        is_mine: Boolean,
      },
      mounted () {
      },
      computed: {
      },
      methods: {
      }
    }
</script>

<style scoped>
.tabbar-logo {
  width: 25px;
  height: 25px;
  margin: 0 auto;
  margin-top: 4px;
}
.tabbar-text {
  margin-top: -4px;
  font-weight: 500;
}
.tabItem .tab-item-link {
  display: block;
}
.fixBottomBox .tabItem {
  width: 70px;
}
</style>

```

## 效果图

效果如下图所示：

![底部Tab](/images/real_project/bottom_tab.png)

## 总结

底部Tab 很简单，又很重要。 

在本节中，我们使用了一个component来实现它，然后在所有用到它的页面来使用。 是一个非常典型的重用过程。

需要注意的有几点：

1. 底部Tab务必抽取成component
2. 设计好要跳转到的页面（注意上面代码中的router-link)
3. 判断好当前页面对应的底部Tab的某个图标，是否要高亮.