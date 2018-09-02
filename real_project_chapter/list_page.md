# 商品列表页

商品列表， 在我们的首页有一部分， 在“列表页”（第二个Tab)也会存在。 

所以我们可以直接把抽取成为组件。 

下面以首页中引用为例：

## 1. 在首页中添加代码 

```
<template>
  <div class="background">
    <div class="home">
      <div class="m_layout">
        <div class="product_top">
          <div class="product_left">
            <div>商品列表</div>
          </div>
        </div>
        <span class="divider" style="height: 2px;"></span>
        <!-- 这里循环显示特产商品列表 -->
        <SpecialMarket :id="good.id" :name="good.name" :description="good.description" :image_url="good.image_url" v-for="good in goods"></SpecialMarket>
      </div>
    </div>
    <NavBottomView :is_shops_index="is_shops_index"></NavBottomView>
  </div>
</template>
<script>
    // 在这里引入 特产component
    import SpecialMarket from '../../components/SpecialMarket.vue';
</script>    
```

上面的核心代码按如下：

```
<!-- 这里循环显示特产商品列表 -->
<SpecialMarket :id="good.id" :name="good.name" :description="good.description" :image_url="good.image_url" v-for="good in goods"></SpecialMarket>
```

使用了v-for 和 componment的组合，来显示列表。

## 2. 在component中添加该文件

新增文件 src/components/SpecialMarket.vue: 

```
<template>
  <div>
    <div @click="show_goods_details" class="fu_li_zhuan_qu" >
      <img :src="image_url" class="logo_image"/>
      <div class="content" >
        <div class="title">
          {{name}}
        </div>
        <div class="logo_and_shop_name">
          <span v-html="description"></span>
        </div>
      </div>
    </div>
    <span class="divider" style="height: 2px;"></span>
  </div>
</template>
<script>
import { go } from '../libs/router'

    export default{
        data(){
            return {
            }
        },
        props: {
          id: Number,
          name: String,
          description: String,
          image_url: String,
        },
        mounted(){
        },
        methods:{
         show_goods_details () {
           go("/shops/goods_details?good_id=" + this.id, this.$router)
         },
        },
        components:{
        },
    }
</script>

```

可以看到，该段代码会接受一个数组，然后循环显示。 点击任意一个按钮， 跳转到详情页面。

## 总结

这里算是最简单的地方了。 