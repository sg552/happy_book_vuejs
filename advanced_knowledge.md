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
