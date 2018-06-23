# Component (组件) 进阶

Component 是非常常见的，在我们的Web开发中，只要是生产环境的项目，就一定会有Component. 

下面就是我们的一个实际项目中的例子， 这个项目我们只做了两个月，里面就发展到了32个component. 如下图所示：

![实际项目中的component](./images/components_in_real_project.png)

很多时候，我们甚至会看到 一个 component 中嵌套着另一个， 这个component再嵌套另外5个.... 

例如： 

`popup-picker` 这个component中，看起来是这样的: 

```
<template>
  <div>
      <popup
	      class="vux-popup-picker"
	      :id="`vux-popup-picker-${uuid}`"
	      @on-hide="onPopupHide"
	      @on-show="onPopupShow">

          <picker
	          v-model="tempValue"
	          @on-change="onPickerChange"
	          :columns="columns"
	          :fixed-columns="fixedColumns"
	          :container="'#vux-popup-picker-'+uuid"
	          :column-width="columnWidth">
          </picker>
      </popup>
  </div>
</template>
<script>
import Picker from '../picker'
import Popup from '../popup'
...
</script>
```

可以看到，这个component中，还包含了另外两个，一个是`popup`, 一个是 `picker`.  

这个时候，新人往往会眼花缭乱。 如果看到 `this.$emit` ， 就更晕了。 

所以，要做好实际项目，同学们一定要学好本章。 