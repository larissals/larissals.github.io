---
title: 熟悉vue.js语法
date: 2017-03-13 15:37:45
tags:

---

1. Vue 的根实例

	var vm = new Vue({
	  // 选项
	})

**在实例化 Vue 时，需要传入一个选项对象，它可以包含数据、模板、挂载元素、方法、生命周期钩子等选项。**全部的选项可以在 API 文档中查看。

2. 可以扩展 Vue 构造器，从而用预定义选项创建可复用的组件构造器：

	var MyComponent = Vue.extend({
	  // 扩展选项
	})
	// 所有的 `MyComponent` 实例都将以预定义的扩展选项被创建
	var myComponentInstance = new MyComponent()

尽管可以命令式地创建扩展实例，不过在多数情况下建议将组件构造器注册为一个自定义元素，然后声明式地用在模板中。我们将在后面详细说明组件系统。**现在你只需知道所有的 Vue.js 组件其实都是被扩展的 Vue 实例。  **
3. 每个 Vue 实例都会代理其 data 对象里所有的属性：
注意只有这些被代理的属性是响应的。如果在实例创建之后添加新的属性到实例上，**它不会触发视图更新**。我们将在后面详细讨论**响应系统**。  
4. 除了 data 属性， Vue 实例暴露了一些有用的**实例属性与方法。这些属性与方法都有前缀 $，以便与代理的 data 属性区分**。  
5.  注意，不要在实例属性或者回调函数中（如 vm.$watch('a', newVal => this.myMethod())）使用箭头函数。因**为箭头函数绑定父上下文**，所以 this 不会像预想的一样是 Vue 实例，而是 this.myMethod 未被定义。
6.  每个 Vue 实例在被创建之前都要经过一系列的初始化过程。
实例也会调用一些 生命周期钩子 ，这就给我们提供了执行自定义逻辑的机会。例如，created 这个钩子在实例被创建之后被调用：

	var vm = new Vue({
	  data: {
	    a: 1
	  },
	  created: function () {
	    // `this` 指向 vm 实例
	    console.log('a is: ' + this.a)
	  }
	})
	// -> "a is: 1"
其他生命周期钩子：
mounted、 updated 、destroyed 。
***钩子的 this 指向调用它的 Vue 实例***。一些用户可能会问 Vue.js 是否有*“控制器”*的概念？答案是，没有。组件的自定义逻辑可以分布在这些钩子中。
7. 生命周期
![生命周期](http://cn.vuejs.org/images/lifecycle.png)

8. Date.now() 不是响应式依赖：
- 在这个示例中，使用 watch 选项允许我们执行异步操作（访问一个 API），限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这是计算属性无法做到的。
-     // _.debounce 是一个通过 lodash 限制操作频率的函数
    // 学习更多关于 _.debounce function (and its cousin
    // _.throttle), 参考: https://lodash.com/docs#debounce
- Date.now()
-  注意， v-show 不支持 <template> 语法，也不支持 v-else。
-  v-if vs v-show

v-if 是“真正的”条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

相比之下， v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

一般来说， v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件不太可能改变，则使用 v-if 较好。
	 缩写 v-bind 缩写
	
	<!-- 完整语法 -->
	<a v-bind:href="url"></a>
	<!-- 缩写 -->
	<a :href="url"></a>
	
	v-on 缩写
	
	<!-- 完整语法 -->
	<a v-on:click="doSomething"></a>
	<!-- 缩写 -->
	<a @click="doSomething"></a>