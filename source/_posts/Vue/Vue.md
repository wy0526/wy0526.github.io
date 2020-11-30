---
date: 2020-11-28
categories: Vue
---



# 一、邂逅Vuejs

1. 简单认识

   * 渐进式框架
   * Vue核心库以及其生态系统（如：Core+Vue-router+Vuex）可以满足更多的业务逻辑
   * 特点功能
     * 解耦视图和数据
     * 可复用的组件
     * 前端路由技术
     * 状态管理
     * 虚拟DOM

2. Vue.js安装

   1. CDN引入
      * 开发环境版本
      * 生产环境版本
   2. 下载和引用
   3. NPM安装

3. Hello Vuejs

   * javascript代码创建了一个Vue对象
   * 创建对象的时候传入了一些options：{}
     * el属性：决定了vue对象挂载到哪一个元素上
     * data属性：通常会存储一些数据
       * 数据可以直接定义
       * 或者来自网络，从服务器加载

4. Vue列表显示

   * html代码中使用v-for指令
   * 是响应式的
   * 不需要在JavaScript中完成dom的拼接了

5. 案例：计数器

   * methods属性：用于vue对象中定义新方法
   * @click指令：监听某个元素的点击事件，通常执行的是methods中定义的方法

6. Vue中的MVVM

   * View层
     * 视图层
     * 前端开发中通常就是dom层
     * 给用户展示各种信息
   * Model层
     * 数据层
     * 数据可能是固定的死数据，更多来自服务器，网络请求下来的数据
   * VueModel层
     * 视图模型层
     * view和model沟通的桥梁
     * 一方面实现了DataBinding，数据绑定，将Model的改变实时反映到view中
     * 另一方面实现了DomListener，DOM监听，当Dom发生一些事件是可以监听到，并在需要的情况下改变对应的data

7. 计数器的MVVM

   * 计数器的MVVM
     * view依旧是dom
     * model是抽离出来的obj
     * viewModel就是我们创建的vue对象实例
   * 工作流程
     * viewModel通过DataBinding让obj中的数据实时显示在dom中
     * 其次viewModel通过DOMListener监听Dom时间，通过methods操作改变obj中的数据

   ~~~
   <body>
   <div id="app">
       <h2>当前计数：{{counter}}</h2>
       <!--<button v-on:click="counter++">+</button>
       <button v-on:click="counter&#45;&#45;">-</button>-->
       <button v-on:click="add">+</button>
       <button v-on:click="sub">-</button>
   <script src="../js/vue.js"></script>
   <script>
       const obj = {
           counter:0,
       }
       const app = new Vue({
           el:'#app',
           data:obj,
           methods:{
               add:function () {
                   console.log('add被执行');
                   this.counter++
               },
               sub:function () {
                   console.log('sub被执行');
                   this.counter--
               }
           }
       })
   </script>
   </body>
   ~~~

8. 创建vue实例传入的options

   * el
   * data
   * methods

9. vue的生命周期

   