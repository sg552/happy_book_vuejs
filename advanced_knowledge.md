## 在vue中操作什么属性，在接口中就要存在该属性的key.

例如，vue页面，会在初始化时，请求一个接口：


{
  products: [
    {
      name: 'a'
      comment: 'lalala'
    },
    {
      name: 'b'
      comment: 'kakaka'
    }

  ]
}

如果在接口中，这个comment 不存在，那么我们在vue中怎么操作，
都不会把 'comment'放到  products中去。

## 发送层次很深的json 格式的参数


vuejs - 发送大量的请求时，使用 post + JSON.stringify(xx)的形式

2017-11-26 14:13
访问量: 1

分类： 技术
如题，我们从vuejs向接口发起请求时， 这样：

      this.$http.post(this.$configs.api + 'dish_orders/native_add_dish_order', {
        dishes: JSON.stringify(this.chosen_dishes),
      }).then((response) => {

服务器端会看到这样的日志：

{"socket_ips"=>"[{\"socketIPAddress\":\"192.168.1.181\",\"port\":9100,\"printType\":1,\"ticketTitle\":\"皇后镇餐厅总单\"
,\"categoryArray\":[1,2,3,4,5,6,11,12,13],\"categoryHashArray\":[{\"id\":1,\"name\":\"特色菜\"},
{\"id\":2,\"name\":\"凉菜\"},{\"id\":3,\"name\":\"热菜\"},{\"id\":4,\"name\":\"烧烤\"},
{\"id\":5,\"name\":\"面点、主食\"},{\"id\":6,\"name\":\"酒水饮料\"},{\"id\":11,\"name\":\"早点\"},
{\"id\":12,\"name\":\"铁锅炖\"},{\"id\":13,\"name\":\"餐具\"}]},
{\"socketIPAddress\":\"192.168.1.182\",\"port\":9100,
\"printType\":0,\"ticketTitle\":\"热菜、凉菜、特色菜、烧烤\", .....

然后，我们在rails端，这样解析：

dishes = ActiveSupport::JSON.decode(params[:dishes])
