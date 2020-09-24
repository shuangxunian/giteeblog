---
title: Vue高频面试题
excerpt: 此篇是Vue3.0以下的高频面试题，3.0的内容还不是很充分
categories:
- 技术文章
tags:
- js
- vue
- 面试
---

## 前言
欢迎大家私聊我进行补充~这里只放一些比较简介的问题和答案，想看前端面试题请移步[前端必会面试题]()。

## 内容
**为什么操作真实 dom 有性能问题**
因为 DOM 是属于渲染引擎中的东西，而 JS 又是 JS 引擎中的东西。当我们通过 JS 操作 DOM 的时候，其实这个操作涉及到了两个线程之间的通信，那么势必会带来一些性能上的损耗。操作 DOM 次数一多，也就等同于一直在进行线程之间的通信，并且操作 DOM 可能还会带来重绘回流的情况，所以也就导致了性能上的问题。

**说一下 MVVM**
MVVM是双向数据绑定
- M: Model 数据层
- V: View 视图层
- VM: ViewModel 视图层和数据层中间的桥，视图层和数据层通信的桥梁

view 层通过事件去绑定 Model 层， Model 层通过数据去绑定 View 层

**Vue 的响应式原理**
Vue 内部使用了 Object.defineProperty() 来实现数据响应式，通过这个函数可以监听到 set 和 get 的事件。
1. 首先利用 Object.defineProperty() 给 data 中的属性去设置 set, get 事件
2. 递归的去把 data 中的每一个属性注册为被观察者
3. 解析模板时，在属性的 get 事件中去收集观察者依赖
4. 当属性的值发生改变时，在 set 事件中去通知每一个观察者，做到全部更新

**Vue 的模板如何被渲染成 HTML? 以及渲染过程**
1. vue 模板的本质是字符串，利用各种正则，把模板中的属性去变成 js 中的变量，vif,vshow,vfor 等指令变成 js 中的逻辑
2. 模板最终会被转换为 render 函数
3. render 函数执行返回 vNode
4. 使用 vNode 的 path 方法把 vNode 渲染成真实 DOM

**Vue 的整个实现流程**
1. 先把模板解析成 render 函数，把模板中的属性去变成 js 中的变量，vif,vshow,vfor 等指令变成 js 中的逻辑
2. 执行 render 函数，在初次渲染执行 render 函数的过程中 绑定属性监听，收集依赖，最终得到 vNode，利用 vNode 的 Path 方法，把 vNode 渲染成真实的 DOM
3. 在属性更新后，重新执行 render 函数，不过这个时候就不需要绑定属性和收集依赖了，最终生成新的 vNode
4. 把新的 vNode 和 旧的 vNode 去做对比，找出真正需要更新的 DOM，渲染

**什么是 diff 算法，或者是 diff 算法用来做什么**
- diff 是linux中的基础命令，可以用来做文件，内容之间的对比
- vNode 中使用 diff 算法是为了找出需要更新的节点，避免造成不必要的更新

**Vuex是什么**
vuex 就像一个全局的仓库，公共的状态或者复杂组件交互的状态我们会抽离出来放进里面。

vuex的核心主要包括以下几个部分：
- state：state里面就是存放的我们需要使用的状态，他是单向数据流，在 vue 中不允许直接对他进行修改，而是使用 mutations 去进行修改
- mutations: mutations 就是存放如何更改状态的一些方法
- actions： actions 是来做异步修改的，他可以等待异步结束后，再去使用 commit mutations 去修改状态
- getters: 相当于是 state 的计算属性

使用：
- 获取状态在组件内部 computed 中使用 this.$store.state 得到想要的状态
- 修改的话可在组件中使用 this.$store.commit 方法去修改状态
- 如果在一个组件中，方法，状态使用太多。 可以使用 mapState，mapMutations 辅助函数

**Vue 中组件之间的通信**
父子组件：父组件通过 Props 传递子组件，子组件通过 $emit 通知父组件 兄弟组件：可以使用 vuex 全局共享状态，或 eventBus

**如何解决页面刷新后 Vuex 数据丢失的问题**
可以通过插件 vuex-persistedstate 来解决 插件原理：利用 HTML5 的本地存储 + Vuex.Store 的方法，去同步本地和 store 中的数据，做到同步更新

**前端路由的两种实现原理**
两种路由模式分为 hash 模式 和 history 模式

- hash 模式：
hash 模式背后的原理是 onhashchange 事件，可以在window对象上监听这个事件，在hash 变化时，浏览器会记录历史，并且触发事件回调，在 hash 模式中，地址栏中会带一个 #

- history 模式：
前面的 hashchange，你只能改变 # 后面的 url 片段，而 history api 则给了前端完全的自由；history api可以分为两大部分，切换和修改，参考 MDN

使用 history 需要服务端的支持，在hash模式下，前端路由修改的是#中的信息，而浏览器请求时是不带着的，所以没有问题.但是在history下，你可以自由的修改path，当刷新时，如果服务器中没有相应的响应或者资源，会刷出一个404来



## 后记
这些问题我都会写文章补上，也欢迎大家给我提供我这里没有的问题哦~