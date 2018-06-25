# Vuejs的生命周期

每个 Vuejs 的实例，都会经历下图的生命周期。

![生命周期图](./images/vuejs_lifecycle.png)

可以看出，基本周期是：

1. created       (创建好DOM)
2. mounted       (页面基本准备好了。)
3. updated       (update 可以理解成人肉手动操作触发)
4. destroyed    （销毁)
 
上面步骤中的 1,3,4都是自动触发。 每个步骤都有对应的 beforeXyz方法

所以, 我们一般使用 `mounted` 作为页面初始化时执行的方法


