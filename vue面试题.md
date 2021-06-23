# vue面试题

## 1、生命周期

>创建前后、载入前后、更新前后、销毁前后
>
>1、创建前后：在beforeCreate阶段：实例的挂载元素和数据对象都为undefined，还未初始化，在created阶段，vue实例的数据对象有了data.
>
>2、载入前后：在beforeMount阶段，vue实例和data都初始化了，但是挂载之前为虚拟dom节点，data.message还未替换，在mounted阶段，vue实例挂载完成，data.message成功渲染。
>
>3、更新前后：当data变化时，会触发beforeUpdate和updated方法。
>
>4、销毁前后：在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在。