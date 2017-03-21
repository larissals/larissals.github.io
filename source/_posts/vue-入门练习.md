---
title: vue 入门练习
date: 2017-03-13 14:18:41
tags:
- vue
- 练习笔记

---
学习vue.js 参照这个笔记进行练习：  
练习要达到以下效果： 

1. 理解各个结构、组件及vue框架本身的运作原理；
2. 理解用法，掌握用法
3. 对比未用框架的项目和使用vue.js框架的项目；

<!---more--->

[Vue 爬坑之路（二）—— 组件之间的数据传递](http://www.cnblogs.com/wisewrong/p/6266038.html#)  

[Vue 爬坑之路（三）—— 使用 vue-router 跳转页面](http://www.cnblogs.com/wisewrong/p/6277262.html)   
 
>[vue-router官方文档](https://router.vuejs.org/zh-cn/essentials/getting-started.html)
>[HTML5 history 模式](https://router.vuejs.org/zh-cn/essentials/history-mode.html)

[Vue 爬坑之路（四）—— 与 Vuex 的第一次接触](http://www.cnblogs.com/wisewrong/p/6344390.html#3635013)  

[Vue 爬坑之路（五）—— 组件进阶](http://www.cnblogs.com/wisewrong/p/6380903.html)  

[ Vue 爬坑之路（六）—— 使用 Vuex + axios 发送请求](http://www.cnblogs.com/wisewrong/p/6402183.html)

##学习总结
1. 完成了《（二）组件间数据传递》  
 问题：不理解template，script内变量传递的方向，谁识别谁，如何编译。
2.怎么理解vue中的state view actions  

	new Vue({
	  // state
	  data () {
	    return {
	      count: 0
	    }
	  },
	  // view
	  template: `
	    <div>{{ count }}</div>
	  `,
	  // actions
	  methods: {
	    increment () {
	      this.count++
	    }
	  }
	})


- state，驱动应用的数据源；
- view，以声明方式将state映射到视图；
- actions，响应在view上的用户输入导致的状态变化。

###之前很好奇，为什么state被翻译成数据源。下面这段话解释的很好。
> Vuex 应用的核心就是 store（仓库）。"store" 基本上就是一个容器，它包含着你的应用中大部分的状态(state)。
  
###Vuex 和单纯的全局对象有以下两点不同：

>1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。    

  
可以理解为实时增量渲染

>2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交(commit) mutations。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。  

控制store改变的入口，从而能够可以跟踪变化。尤其是在大型项目中，这点尤为重要。

- Vuex 使用 单一状态树 —— 是的，用一个对象就包含了全部的应用层级状态。
- Vuex 通过 store 选项，提供了一种机制将状态从根组件『注入』到每一个子组件中（需调用 Vue.use(Vuex)）：


学习vue.js一段时间了，今天参考demo开始写一个小项目。 

参照的地址是：
[https://github.com/bailicangdu/vue2-happyfri](https://github.com/bailicangdu/vue2-happyfri)

同时，这项目也作为我熟悉git操作的一个项目。
