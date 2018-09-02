# 微信支付

微信支付，最难的地方不在于技术，而是在于微信有一套自己的技术规范。 

建议每位同学都要从官方文档看起。 虽然市面上有一些集成工具，例如 Ping++ , 但是往往这些产品不是特别方便，收费也比较高昂。 出了问题不好调试。

所以，我们对于核心技术，一定要亲自掌握。 

## 申请微信账号和配置

这里就不详述了。 我们假设全部的账号都已经做好了。 

## 1. 添加支付页面的路由


```
import Pay from '@/components/pay'

Vue.use(Router)

export default new Router({
  routes: [
    { 
      path: '/shops/pay',
      name: 'Pay',
      component: Pay
    },
  ]

})
```

## 2. 添加vue页面

```
<template>
  <div class="background">
    <header class="top_bar">
      <a onclick="window.history.go(-1)" class="icon_back"></a>
      <h3 class="cartname">订单支付</h3>
    </header>

    <div class="tast_list_bd" style="background-color: #F3F3F3; padding-top: 0; padding-bottom: 80px;">
      <div class="goods_detail" style="">

        <main class="detail_box">
            <span class="divider"></span>

            <form style="margin-top: 45px;">
                <div class="column is-12">
                    <label class="label">收货人</label>
                    <p class="control has-icon has-icon-right">
                    <input name="name" v-model="mobile_user_name" v-validate="'required|required'" :class="{'input': true, 'is-danger': errors.has('name') }" type="text" placeholder="例如: 张三" autofocus="autofocus"/>
                    <span v-show="errors.has('name')" class="help is-danger">收货人不能为空</span>
                    </p>
                </div>

                <div class="column is-12">
                    <label class="label">收货地址</label>
                    <p class="control has-icon has-icon-right">
                    <input name="url" v-model="mobile_user_address" v-validate="'required|required'" :class="{'input': true, 'is-danger': errors.has('url') }" type="text" placeholder="例如: 北京市朝阳区大望路西西里小区4栋2单元201"/>
                    <span v-show="errors.has('url')" class="help is-danger">收货地址不能为空</span>
                    </p>
                </div>

                <div class="column is-12">
                    <label class="label">收货电话</label>
                    <p class="control has-icon has-icon-right">
                    <input name="phone" v-model="mobile_user_phone" v-validate="'required|numeric'" :class="{'input': true, 'is-danger': errors.has('phone') }" type="text" placeholder="例如: 18888888888"/>
                    <span v-show="errors.has('phone')" class="help is-danger">电话号码不能为空</span>
                    </p>
                </div>
            </form>

        <span class="divider"></span>

        <section class="product_info clearfix" v-if="single_pay">
          <div>
            <div class="fu_li_zhuan_qu" >
              <img :src="good_images[0]" class="logo_image"/>
              <div class="content" >
                <div class="title">
                  {{good.name}}
                </div>
                <div class="logo_and_shop_name">
                  <div class="product_pric">
                    <span>￥</span>
                    <span class="rel_price">{{good.price}}</span>
                    <span> &nbsp x {{buy_count}}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section class="product_info clearfix" v-else v-for="product in cartProducts">
          <div>
            <div class="fu_li_zhuan_qu" >
              <img :src="product.image" class="logo_image"/>
              <div class="content" >
                <div class="title">
                  {{product.title}}
                </div>
                <div class="logo_and_shop_name">
                  <div class="product_pric">
                    <span>￥</span>
                    <span class="rel_price">{{product.price}}</span>
                    <span> &nbsp x {{product.quantity}}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section>
          <span class="divider" style="height: 15px;"></span>
          <div class="extra_cost" style=" ">
            <span style="float: left; margin-left: 15px;"> 卖家留言:</span>
            <input v-model="guest_remarks" id="extra_charge" type="text" name="cost" placeholder="选填: 对本次交易的说明" style="border: 0; background-color: white;
            font-size: 15px; color: #48484b; outline: none; width: 60%;"></input>
          </div>
        </section>

        <section>
          <span class="divider"></span>
          <div class="extra_cost" style=" ">
            <span style="float: left; margin-left: 15px;"> 应付金额:</span>
            <div v-if="single_pay" class="rel_price" type="text" name="cost" style="border: 0; background-color: white;
            font-size: 20px; color: #ff621a; font-weight: bold; outline: none; text-align: right; padding-right: 20px;"> {{total_cost | currency }}</div>
            <div v-else class="rel_price" type="text" name="cost" style="border: 0; background-color: white;
            font-size: 20px; color: #ff621a; font-weight: bold; outline: none; text-align: right; padding-right: 20px;"> {{ total | currency }}</div>

          </div>
        </section>
        </main>

        <span class="divider"></span>

        <div style="height: 55px;  display: flex; width: 100%; padding: 0px 10px; background-color: #fff;" @click="">
          <div style="flex: 1; display: flex;">
            <div style="margin-top: 10px;">
              <img src="../../assets/微信icon@3x.png" style="width: 35px;"/>
            </div>
            <span style="margin-top: 8px; font-size: 18px; line-height:40px; margin-left: 10px;">微信支付</span>
          </div>

          <div style=" padding: 14px 10px;" @click="user_wechat">
            <img src="../../assets/选中3x.png" style="width: 28px;"/>
          </div>
        </div>
      </div>
    </div>

    <div class="shop_layout-scroll-absolute" style="">
      <div class="queding" @click="buy">
        立即支付
      </div>
    </div>

  </div>
</template>
<script>
   import { go } from '../../libs/router'
   import { mapGetters } from 'vuex'
   export default{
        data(){
            return {
                good_images: [],
                good: "",
                buy_count: this.$route.query.buy_count,
                good_id: this.$route.query.good_id,
                open_id: this.$store.state.userInfo.open_id,
                mobile_user_address: '',
                mobile_user_name: '',
                mobile_user_phone: '',
                guest_remarks: '',
                is_use_wechat: false,
            }
        },
        watch:{
        },
        mounted(){
          if (this.single_pay) {
              this.$http.get(this.$configs.api + 'goods/goods_details?good_id=' + this.good_id).then((response)=>{
                  console.info(this.good_id)
                  console.info(response.body)
                  this.good = response.body.good
                  this.good_images = response.body.good_images
              },(error) => {
                  console.error(error)
              });
          }
        },
        computed:  {
            total () {
              return this.cartProducts.reduce((total, p) => {
                return (total + p.price * p.quantity)
              }, 0)
            },
            single_pay () {
               return this.good_id && this.buy_count
            },
            total_cost () {
              return this.good.price * this.buy_count
            },
            ...mapGetters({
              cartProducts: 'cartProducts',
              checkoutStatus: 'checkoutStatus'
            })
        },
        methods:{
            validateBeforeSubmit() {
               //拦截异步操作
               return new Promise((resolve, reject) => {
                   this.$validator.validateAll().then(result => {
                       console.info(result)
                       if (result) {
                           console.info("============表单验证成功===")
                           resolve(true);
                       } else {
                           alert('请填写完整的收货信息!');
                           resolve(false);
                       }
                    });
               })
            },
            plus () {
              this.buy_count = this.buy_count + 1
            },
            minus () {
              if(this.buy_count > 1) {
                this.buy_count = this.buy_count - 1
              }
            },
            user_wechat () {
              if (this.is_use_wechat === false) {
                this.is_use_wechat = true
              } else {
                this.is_use_wechat = false
              }
            },
            buy (){
                let result = this.validateBeforeSubmit().then((resolve)=>{
                    if (resolve) {
                        console.info('true ==== ')
                        let params
                        if (this.single_pay) {
                            params = {
                                good_id: this.good_id,
                                buy_count: this.buy_count,
                                total_cost: this.total_cost,
                                guest_remarks: this.guest_remarks,
                                mobile_user_address: this.mobile_user_address,
                                mobile_user_name: this.mobile_user_name,
                                mobile_user_phone: this.mobile_user_phone,
                                open_id: this.open_id
                            }
                        } else {
                            console.info(this.total)
                            params = {
                                goods: this.cartProducts,
                                total_cost: this.total,
                                guest_remarks: this.guest_remarks,
                                mobile_user_address: this.mobile_user_address,
                                mobile_user_name: this.mobile_user_name,
                                mobile_user_phone: this.mobile_user_phone,
                                open_id: this.open_id
                            }
                        }
                        this.$http.post(this.$configs.api + 'goods/buy', params
                        ).then((response) => {
                            let order_number =  response.body.order_number
                            this.purchase(order_number)
                        }, (error) => {
                            console.error(error)
                        });
                    } else {
                        console.info('== 请填写完整的收货信息')
                    }
                });
            },
            purchase (order_number) {
              //调起微信支付界面
              if (typeof WeixinJSBridge == "undefined"){
                if( document.addEventListener ){
                  document.addEventListener('WeixinJSBridgeReady', this.onBridgeReady, false);
                }else if (document.attachEvent){
                  document.attachEvent('WeixinJSBridgeReady', this.onBridgeReady);
                  document.attachEvent('onWeixinJSBridgeReady', this.onBridgeReady);
                }
              }else{
                this.onBridgeReady(order_number);
              }
            },
            onBridgeReady (order_number) {
              let that = this
              let total_cost
              if (this.single_pay) {
                total_cost = this.total_cost
              } else {
                total_cost = this.total
              }
              this.$http.post(this.$configs.api + 'payments/user_pay',
              {
                open_id: this.$store.state.userInfo.open_id,
                total_cost: total_cost,
                order_number: order_number
              }).then((response) => {
                WeixinJSBridge.invoke(
                    'getBrandWCPayRequest', {
                        "appId": response.data.appId,
                        "timeStamp": response.data.timeStamp,
                        "nonceStr": response.data.nonceStr,
                        "package": response.data.package,
                        "signType": response.data.signType,
                        "paySign":  response.data.paySign
                    },
                    function(res){
                        // 下面代码仅用于调试
                        // alert("res.err_msg: " + res.err_msg + ", err_desc: " + res.err_desc)
                        if(res.err_msg == "get_brand_wcpay_request:ok" ) {
                          // 使用以上方式判断前端返回,微信团队郑重提示：res.err_msg将在用户支付成功后返回    ok，但并不保证它绝对可靠。
                          that.$router.push({ path: '/shops/paysuccess?order_id=' + order_number });
                        } else {
                          // 显示取消支付或者失败
                          that.$router.push({ path: '/shops/payfail?order_id=' + order_number });
                        }
                    }
                );
              }, (error) => {
                console.error(error)
              });
            }
          },
    }
</script>
```

核心代码如下：

```
onBridgeReady (order_number) {
  //....
  this.$http.post(this.$configs.api + 'payments/user_pay',
  {
    open_id: this.$store.state.userInfo.open_id,
    total_cost: total_cost,
    order_number: order_number
  }).then((response) => {
    WeixinJSBridge.invoke(
        'getBrandWCPayRequest', {
            "appId": response.data.appId,
            "timeStamp": response.data.timeStamp,
            //....
        },
        function(res){
            //...
        }
    );
  }, (error) => {
    console.error(error)
  });
}
```

上面的代码是用来给页面一准备好( WeixinJSBridge 准备好了)的时候，页面就要调用的。 


```
purchase (order_number) {
  //调起微信支付界面
  if (typeof WeixinJSBridge == "undefined"){
    if( document.addEventListener ){
      document.addEventListener('WeixinJSBridgeReady', this.onBridgeReady, false);
    }else if (document.attachEvent){
      document.attachEvent('WeixinJSBridgeReady', this.onBridgeReady);
      document.attachEvent('onWeixinJSBridgeReady', this.onBridgeReady);
    }
  }else{
    this.onBridgeReady(order_number);
  }
},
```            

上面的代码用于调用出 “微信支付页面”.  其中的变量 `WeixinJSBridge` 是微信浏览器自带的变量， 不必声名，直接拿过来用就行。


从上面的代码可以看到：

1. 支付的细节处理，都交给了后台服务器端。 只要我们H5端把参数准备好，直接访问  http://shopweb.siwei.me/api/payments/user_pay 就可以了。 
2. 支付，分成单笔商品支付和多笔商品支付两种情况. 区别就是把参数重新组织一下即可。
3. 新手对于 WeixinJSBridge 这个变量很难掌握， 一定要多看文档。 这个文档是 “微信公众号内支付”的文档， 不是微信APP ， 或者微信普通H5的文档。 一定要梳理好逻辑。 另外，对于后端API的同学这里更难，建议多查多试。 
4. 在微信的后台，要配置不同的支付目录。 安卓和IOS 的粗略是不一样的。 建议大家百度一下。
5. 微信的支付场景对应的支付方式和实现方式是不一样的。 本例是“微信的公众号内支付”。

微信的官方文档中， 提供的例子都是基于经典的WEB页面（整体刷新的那种）的，目前还没有看到SPA的例子。 但是大家的问题很多。 我的个人博客也记录了一些内容： http://siwei.me/blog/posts/--27

由于篇幅限制，微信相关的内容不再赘述。