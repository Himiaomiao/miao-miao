# vue中的`watch`、`methods`、`computed`的区别

> `methods`和`watch`、`computed`都是以函数为基础的，但各自却都不同，从作用机制和性质上看，`methods`和`watch/computed`不太一样。
## 1、`methods`和（`watch/computed`）的对比
* 作用机制上
> 1、`watch`和`methods`都是以vue的依赖追踪机制为基础，它们都试图处理同一件事，当某个数据（称为它为依赖数据）发生变化时，所有依赖这个数据的“相关”数据“自动”发生变化，也就是自动调用相关的函数去实现数据的变动。
> 2、`methods`是用来定义函数的，对于其中的函数，需要手动去调用才能执行，和`computed、watch`不一样，`computed、watch`中的函数会自动执行。
> 【总结】`methods`里面定义的函数是需要手动调用的，而`computed、watch`中的函数是会自动执行的。

* 从性质上看

>1、`methods`里面定义的是函数，需要像"fuc()"这样去调用它(假设函数为fuc)
>
>2、`computed`是计算属性。事实上和data对象里的数据属性是同一类的（使用上）
>
>```  javascript
>computed:{  fullName: function () { return this.firstName + lastName }}
>
>```
>
>在取用的时候，用this.fullName去取用，就和取data一样（不要当成函数调用）
>
>3、`watch`类似于监听机制+事件机制：
>
>例如：
>
>```javascript
>watch: {
>  firstName: function (val) { this.fullName = val + this.lastName }
>}
>
>```
>
>firstName的改变是这个特殊“事件”被触发的条件，而firstName对应的函数就相当于监听到事件发生后执行的方法

## 2、`watch`和`computed`的对比

>对比`watch`和`computed`
>
>![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/00040f86bd4c4641ba2bb9e3d7ebfb14~tplv-k3u1fbpfcp-zoom-1.image)
>
>两个都是以vue的依赖追踪机制为基础的，它们的共同点是：都是希望在依赖数据发生改变的时候，被依赖的数据根据预先定义好的函数，发生“自动”的变化
>
>`watch`和`computed`有明显不同：
>
>+ `watch`擅长处理“一个数据影响多个数据”
>
>+ `computed`擅长处理“一个数据受多个数据影响”
>
>  ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5a59b5bc82fa47fb9bc21aec254cb23a~tplv-k3u1fbpfcp-zoom-1.image)
>
>![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/47272f5b2c2040a58c2302c09c4f3bb4~tplv-k3u1fbpfcp-zoom-1.image)
>
>参考文章 https://juejin.cn/post/6921944541205364743

