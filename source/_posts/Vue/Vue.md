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

# 二、基本语法

vue的template：

~~~
<body>

<div id="app">{{message}}</div>
<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data:{
            message: "欢迎你！"
        }
    })
</script>

</body>
~~~

## 1.插值操作mustache

1. mustache语法

   * 解析双大括号的内容
   * 大括号内可不仅可以直接写变量，还可以写表达式

   ~~~
   直接写变量：{{message}}
   
   变量拼接：{{firstName + lastName}}
   变量中间加空格{{firstName + ' ' + lastName}}等同于{{firstName}} {{lastName}}
   变量显示两遍：{{counter * 2}}
   ~~~

2. v-once指令

   * html标签中使用了v-once时，当改变了data中的数据，页面显示不会变化

3. v-html指令

   * 当data中的数据为HTML语句时，可以让页面直接解析

4. v-text指令

   * 显示data中的数据

   ~~~
   <h2 v-text="message"></h2> 如果message值为2，则页面显示二号标签的2
   ~~~

5. v-pre指令

   * 大括号不再解析，而是直接显示标签中间的内容

   ~~~
   <h2 v-pre>{{message}}</h2> 页面直接显示{{message}}
   ~~~

6. v-blind指令

   * 基本使用：data的数据绑定到html的属性上
     * 如：绑定到图片的src中，链接标签的href中
   * 语法糖：`:`

## 2.动态绑定属性v-bind

1. bind动态绑定class（对象语法）
   * class后面跟的是一个对象
   * 用法
     * 通过大括号直接绑定一个类；可以传入多个值；和普通的类同时存在，并不冲突；复杂时，可以放在一个method或者computed中
2. bind动态绑定class（数组语法）
   * class后面跟的是一个数组
3. 绑定style（对象语法）
   * 如：动态绑定style中的font-size和color属性值
4. 绑定style（数组语法）
   * style后跟数组

## 3.计算属性computed

1. 基本使用
   * computed：
2. 复杂操作
   * 计算书的总价格

## 4.ES6补充

1. let/var

   * JavaScript中用关键字let修复了var的问题
   * 块级作用域
     * JS中使用var声明变量时，对于if/for等块定义来说是没有作用域的，往往会引发一些问题
     * 用函数function（）、或者使用let来声明变量可以避免问题的发生

2. const的使用

   * 被const修饰的标识符为常量，而且在声明的时候就必须赋值，但不可以被再次赋值
   * 建议：es6开发中，优先使用const，只有需要改变某一个标识符的时候才使用let

3. 对象增强写法

   ~~~
   //1.属性的简写
   let name = 'why'
   let age = 18
   
   //es6之前
   let obj1 = {
   	name:name,
   	age:age
   }
   console.log(obj1);
   
   //es6之后
   let obj2 = {
   	name,age
   }
   console.log(obj2);
   
   //2.方法的简写
   //es6之前
   let obj1 = {
   	test:function(){
   	console.log('obj1的test函数');
   	}
   }
   obj1.test()
   //es6之后
   let obj2 = {
   	test(){
   		console.log('obj2的test函数');
   	}
   }
   ~~~

## 5.事件监听v-on

1. 交互

   * 监听点击、拖拽、键盘事件等
   * v-on指令实现监听

2. v-on

   * 作用：绑定事件监听器

   * 缩写：@

   * v-on基础

     ~~~
     <div id="app">
       <h2>{{counter}}</h2>
       <button @click="increment">+</button>
       <button @click="decrement">-</button>
     </div>
     
     <script src="../js/vue.js"></script>
     <script>
       const app = new Vue({
         el: '#app',
         data: {
           counter: 0
         },
         methods: {
           increment() {
             this.counter++
           },
           decrement() {
             this.counter--
           }
         }
       })
     </script>
     ~~~

   * v-on参数

     * 当通过methods中定义方法，以供@click调用时，需要注意参数问题
       1. 情况一：如果该方法不需要额外参数，那么方法后的()可以不添加。但是注意：如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去
       2. 情况二：如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件

     ~~~
     <div id="app">
       <!--1.事件调用的方法没有参数-->
       <button @click="btn1Click()">按钮1</button>
       <button @click="btn1Click">按钮1</button>
     
       <!--2.在事件定义时, 写方法时省略了小括号, 但是方法本身是需要一个参数的, 
       这个时候, Vue会默认将浏览器生产的event事件对象作为参数传入到方法-->
       <!--<button @click="btn2Click(123)">按钮2</button>-->
       <!--<button @click="btn2Click()">按钮2</button>-->
       <button @click="btn2Click">按钮2</button>
     
       <!--3.方法定义时, 我们需要event对象, 同时又需要其他参数-->
       <!-- 在调用方式, 如何手动的获取到浏览器参数的event对象: $event-->
       <button @click="btn3Click(abc, $event)">按钮3</button>
     </div>
     
     <script src="../js/vue.js"></script>
     <script>
       const app = new Vue({
         el: '#app',
         data: {
           message: '你好啊',
           abc: 123
         },
         methods: {
           btn1Click() {
             console.log("btn1Click");
           },
           btn2Click(event) {
             console.log('--------', event);
           },
           btn3Click(abc, event) {
             console.log('++++++++', abc, event);
           }
         }
       })
     
       // 如果函数需要参数,但是没有传入, 那么函数的形参为undefined
       // function abc(name) {
       //   console.log(name);
       // }
       //
       // abc()
     </script>
     ~~~

   * v-on修饰符

     * 处理获取到event的事件的修饰符
       1. `.stop`：调用event.stopPropagation()
       2. `.prevent`：调用event.preventDefault()
       3. `.{keyCode | keyAlias}`：只当事件是从特定键触发时才触发回调
       4. `.native`：监听组件根元素的原生事件
       5. `.once`：只触发一次回调

     ~~~
     <div id="app">
       <!--1. .stop修饰符的使用-->
       <div @click="divClick">
         aaaaaaa
         <button @click.stop="btnClick">按钮</button>
       </div>
     
       <!--2. .prevent修饰符的使用-->
       <br>
       <form action="baidu">
         <input type="submit" value="提交" @click.prevent="submitClick">
       </form>
     
       <!--3. .监听某个键盘的键帽-->
       <input type="text" @keyup.enter="keyUp">
     
       <!--4. .once修饰符的使用-->
       <button @click.once="btn2Click">按钮2</button>
     </div>
     
     <script src="../js/vue.js"></script>
     <script>
       const app = new Vue({
         el: '#app',
         data: {
           message: '你好啊'
         },
         methods: {
           btnClick() {
             console.log("btnClick");
           },
           divClick() {
             console.log("divClick");
           },
           submitClick() {
             console.log('submitClick');
           },
           keyUp() {
             console.log('keyUp');
           },
           btn2Click() {
             console.log('btn2Click');
           }
         }
       })
     </script>
     ~~~

## 6.条件判断v-if

1. v-if、v-else-if、v-else

   * 在dom中渲染/销毁元素组件
   * v-if后面的条件为false时，对应的元素以及其子元素不会渲染。也就是根本没有不会有对应的标签出现在DOM中

   ~~~
   <div id="app">
     <h2 v-if="score>=90">优秀</h2>
     <h2 v-else-if="score>=80">良好</h2>
     <h2 v-else-if="score>=60">及格</h2>
     <h2 v-else>不及格</h2>
   
     <h1>{{result}}</h1>
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         score: 99
       },
       computed: {
         result() {
           let showMessage = '';
           if (this.score >= 90) {
             showMessage = '优秀'
           } else if (this.score >= 80) {
             showMessage = '良好'
           }
           // ...
           return showMessage
         }
       }
     })
   </script>
   ~~~

2. v-show

   * 与v-if相似
   * 区别
     * pv-if当条件为false时，压根不会有对应的元素在DOM中
     * v-show当条件为false时，仅仅是将元素的display属性设置为none而已
   * 选择
     * 当需要在显示与隐藏之间切片很频繁时，使用v-show
     * 当只有一次切换时，通过使用v-if

## 7.循环遍历v-for

1. v-for遍历数组

   * 如果在遍历的过程中不需要使用索引值：v-for="movie in movies"
   * 如果在遍历的过程中，我们需要拿到元素在数组中的索引值：v-for=(item, index) in items

   ~~~
   <div id="app">
     <!--1.在遍历的过程中,没有使用索引值(下标值)-->
     <ul>
       <li v-for="item in names">{{item}}</li>
     </ul>
   
     <!--2.在遍历的过程中, 获取索引值-->
     <ul>
       <li v-for="(item, index) in names">
         {{index+1}}.{{item}}
       </li>
     </ul>
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         names: ['why', 'kobe', 'james', 'curry']
       }
     })
   </script>
   ~~~

2. v-for遍历对象

   ~~~
   <div id="app">
     <!--1.在遍历对象的过程中, 如果只是获取一个值, 那么获取到的是value-->
     <ul>
       <li v-for="item in info">{{item}}</li>
     </ul>
   
   
     <!--2.获取key和value 格式: (value, key) -->
     <ul>
       <li v-for="(value, key) in info">{{value}}-{{key}}</li>
     </ul>
   
   
     <!--3.获取key和value和index 格式: (value, key, index) -->
     <ul>
       <li v-for="(value, key, index) in info">{{value}}-{{key}}-{{index}}</li>
     </ul>
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         info: {
           name: 'why',
           age: 18,
           height: 1.88
         }
       }
     })
   </script>
   ~~~

3. 组件的key属性

   * 官方推荐我们在使用v-for时，给对应的元素或组件添加上一个:key属性
   * 以节点中间插入节点说明我们需要使用key来给每个节点做一个唯一标识
   * 总之，key的作用主要是为了高效的更新虚拟DOM

4. 检测数组更新

   * Vue中包含了一组观察数组编译的方法，使用它们改变数组也会触发视图的更新
     * push()
     * pop()
     * shift()
     * unshift()
     * splice()
     * sort()
     * reverse()

## 8.高级函数

1. filter
2. map
3. reduce

~~~
1.filter函数的使用
// 10, 20, 40, 50
let newNums = nums.filter(function (n) {
  return n < 100
})
// console.log(newNums);

// 2.map函数的使用
// 20, 40, 80, 100
let new2Nums = newNums.map(function (n) { // 20
  return n * 2
})
console.log(new2Nums);

// 3.reduce函数的使用
// reduce作用对数组中所有的内容进行汇总
let total = new2Nums.reduce(function (preValue, n) {
  return preValue + n
}, 0)
console.log(total);
~~~



## 9.表单绑定v-model

1. 基本使用

   * 使用v-model指令实现表单元素和数据双向绑定

   ~~~
   <div id="app">
     <input type="text" v-model="message">
     {{message}}
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         message: '你好啊'
       }
     })
   </script>
   
   //也可以用于textarea
   <textarea v-model="message"></textarea>
   <p>输入的内容是：{{message}}</p>
   ~~~

2. v-model原理

   * v-model其实是一个语法糖，它的背后本质上是包含两个操作
     * v-bind绑定一个value属性
     * v-on指令给当前元素绑定input事件

   ~~~
   <input type="text" v-model="message">
   等同于
   <input type="text" v-bind:value="message" v-on:input="message = $event.target.value">
   
   ~~~

3. v-model：radio

   * 单选框

   ~~~
   <div id="app">
     <label for="male">
       <input type="radio" id="male" value="男" v-model="sex">男
     </label>
     <label for="female">
       <input type="radio" id="female" value="女" v-model="sex">女
     </label>
     <h2>您选择的性别是: {{sex}}</h2>
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         message: '你好啊',
         sex: '女'
       }
     })
   </script>
   ~~~

4. v-model：checkbox

   * 单个勾选框
     * v-model即为布尔值
     * 此时input的value并不影响v-model的值

   * 多个勾选框
     * 因为可以选中多个，所以对应的data中属性是一个数组
     * 当选中某一个时，就会将input的value添加到数组中

   ~~~
   <div id="app">
     <!--1.checkbox单选框-->
     <!--<label for="agree">-->
       <!--<input type="checkbox" id="agree" v-model="isAgree">同意协议-->
     <!--</label>-->
     <!--<h2>您选择的是: {{isAgree}}</h2>-->
     <!--<button :disabled="!isAgree">下一步</button>-->
   
     <!--2.checkbox多选框-->
     <input type="checkbox" value="篮球" v-model="hobbies">篮球
     <input type="checkbox" value="足球" v-model="hobbies">足球
     <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
     <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
     <h2>您的爱好是: {{hobbies}}</h2>
   
     <label v-for="item in originHobbies" :for="item">
       <input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
     </label>
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         message: '你好啊',
         isAgree: false, // 单选框
         hobbies: [], // 多选框,
         originHobbies: ['篮球', '足球', '乒乓球', '羽毛球', '台球', '高尔夫球']
       }
     })
   </script>
   ~~~

5. v-model：select

   * 单选下拉菜单
     * v-model绑定的是一个值
     * 当我们选中option中的一个时，会将它对应的value赋值到mySelect中
   * 多选下拉菜单
     * v-model绑定的是一个数组
     * 当选中多个值时，就会将选中的option对应的value添加到数组mySelects中

   ~~~
   <div id="app">
     <!--1.选择一个-->
     <select name="abc" v-model="fruit">
       <option value="苹果">苹果</option>
       <option value="香蕉">香蕉</option>
       <option value="榴莲">榴莲</option>
       <option value="葡萄">葡萄</option>
     </select>
     <h2>您选择的水果是: {{fruit}}</h2>
   
     <!--2.选择多个-->
     <select name="abc" v-model="fruits" multiple>
       <option value="苹果">苹果</option>
       <option value="香蕉">香蕉</option>
       <option value="榴莲">榴莲</option>
       <option value="葡萄">葡萄</option>
     </select>
     <h2>您选择的水果是: {{fruits}}</h2>
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         message: '你好啊',
         fruit: '香蕉',
         fruits: []
       }
     })
   </script>
   ~~~

6. 值绑定

   * 动态的给value赋值
     * 我们前面的value中的值，都是在定义input的时候直接给定的
     * 但是真实开发中，这些input的值可能是从网络获取或定义在data中的
     * 所以我们可以通过v-bind:value动态的给value绑定值
     * 这就是v-bind在input中的应用

7. 修饰符

   * lazy修饰符
     * 默认情况下，v-model默认是在input事件中同步输入框的数据的。
     * 也就是说，一旦有数据发生改变对应的data中的数据就会自动发生改变。
     * lazy修饰符可以让数据在失去焦点或者回车时才会更新
   * number修饰符
     * 默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当做字符串类型进行处理
     * 但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理。
     * number修饰符可以让在输入框中输入的内容自动转成数字类型
   * trim修饰符
     * 如果输入的内容首尾有很多空格，通常我们希望将其去除
     * trim修饰符可以过滤内容左右两边的空格

   ~~~
   <div id="app">
     <!--1.修饰符: lazy-->
     <input type="text" v-model.lazy="message">
     <h2>{{message}}</h2>
   
   
     <!--2.修饰符: number-->
     <input type="number" v-model.number="age">
     <h2>{{age}}-{{typeof age}}</h2>
   
     <!--3.修饰符: trim-->
     <input type="text" v-model.trim="name">
     <h2>您输入的名字:{{name}}</h2>
   </div>
   
   <script src="../js/vue.js"></script>
   <script>
     const app = new Vue({
       el: '#app',
       data: {
         message: '你好啊',
         age: 0,
         name: ''
       }
     })
   
     var age = 0
     age = '1111'
     age = '222'
   </script>
   ~~~

# 三、组件化开发

## 1.认识组件化

1. 什么是组件化
   * 我们将一个完整的页面分成很多个组件
   * 每个组件都用于实现页面的一个功能块
   * 而每一个组件又可以进行细分
2. vue组件化思想
   * 任何的应用都会被抽象成一颗组件树

## 2.注册组件

* 创建组件构造器
* 注册组件
* 使用组件

~~~
<div id="app">
  <!--3.使用组件-->
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>

  <div>
    <div>
      <my-cpn></my-cpn>
    </div>
  </div>
</div>

<my-cpn></my-cpn>

<script src="../js/vue.js"></script>
<script>
  // 1.创建组件构造器对象
  const cpnC = Vue.extend({
    template: `
      <div>
        <h2>我是标题</h2>
        <p>我是内容, 哈哈哈哈</p>
        <p>我是内容, 呵呵呵呵</p>
      </div>`
  })

  // 2.注册组件
  Vue.component('my-cpn', cpnC)

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    }
  })
</script>
~~~

## 3.局部组件和全局组件

* 调用Vue.component()注册组件时，组件的注册是全局的
* 这意味着该组件可以在任意Vue示例下使用
* 如果我们注册的组件是挂载在某个实例中, 那么就是一个局部组件

~~~
<script src="../js/vue.js"></script>
<script>
  // 1.创建组件构造器
  const cpnC = Vue.extend({
    template: `
      <div>
        <h2>我是标题</h2>
        <p>我是内容,哈哈哈哈啊</p>
      </div>
    `
  })

  // 2.注册组件(全局组件, 意味着可以在多个Vue的实例下面使用)
  // Vue.component('cpn', cpnC)

  // 疑问: 怎么注册的组件才是局部组件了?

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      // cpn使用组件时的标签名
      cpn: cpnC
    }
  })

  const app2 = new Vue({
    el: '#app2'
  })
</script>
~~~

## 4.父组件和子组件

~~~
<div id="app">
  <cpn2></cpn2>
  <!--<cpn1></cpn1>-->
</div>

<script src="../js/vue.js"></script>
<script>
  // 1.创建第一个组件构造器(子组件)
  const cpnC1 = Vue.extend({
    template: `
      <div>
        <h2>我是标题1</h2>
        <p>我是内容, 哈哈哈哈</p>
      </div>
    `
  })


  // 2.创建第二个组件构造器(父组件)
  const cpnC2 = Vue.extend({
    template: `
      <div>
        <h2>我是标题2</h2>
        <p>我是内容, 呵呵呵呵</p>
        <cpn1></cpn1>
      </div>
    `,
    components: {
      cpn1: cpnC1
    }
  })

  // root组件
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn2: cpnC2
    }
  })
</script>
~~~

* 父子组件错误用法：以子标签的形式在Vue实例中使用

## 5.注册组件语法糖

* 省去了调用Vue.extend()的步骤，而是可以直接使用一个对象来代替

~~~
<script src="../js/vue.js"></script>
<script>
  // 1.全局组件注册的语法糖
  // 1.创建组件构造器
  // const cpn1 = Vue.extend()

  // 2.注册组件
  Vue.component('cpn1', {
    template: `
      <div>
        <h2>我是标题1</h2>
        <p>我是内容, 哈哈哈哈</p>
      </div>
    `
  })

  // 2.注册局部组件的语法糖
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      'cpn2': {
        template: `
          <div>
            <h2>我是标题2</h2>
            <p>我是内容, 呵呵呵</p>
          </div>
    `
      }
    }
  })
</script>
~~~

1. 模板的分离写法

   * 将其中的HTML分离出来写，然后挂载到对应的组件上，使结构变得更清晰
   * Vue提供了两种方案来定义HTML模块内容
     * 使用`<script>`标签
     * 使用`<template>`标签

   ~~~
   <!--1.script标签, 注意:类型必须是text/x-template-->
   <!--<script type="text/x-template" id="cpn">-->
   <!--<div>-->
     <!--<h2>我是标题</h2>-->
     <!--<p>我是内容,哈哈哈</p>-->
   <!--</div>-->
   <!--</script>-->
   
   <!--2.template标签-->
   <template id="cpn">
     <div>
       <h2>我是标题</h2>
       <p>我是内容,呵呵呵</p>
     </div>
   </template>
   
   <script src="../js/vue.js"></script>
   <script>
   
     // 1.注册一个全局组件
     Vue.component('cpn', {
       template: '#cpn'
     })
   
     const app = new Vue({
       el: '#app',
       data: {
         message: '你好啊'
       }
     })
   </script>
   ~~~

## 6.组件数据存放

* vue组件中的数据不可以访问vue实例数据，所以组件应该有自己保存数据的地方
* 组件对象也有一个data属性(也可以有methods等属性）
* 这个data属性必须是一个函数
  * 首先，如果不是一个函数，Vue直接就会报错
  * 其次，原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响
* 而且这个函数返回一个对象，对象内部保存着数据

~~~
template id="cpn">
  <div>
    <h2>{{title}}</h2>
    <p>我是内容,呵呵呵</p>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>

  // 1.注册一个全局组件
  Vue.component('cpn', {
    template: '#cpn',
    data() {
      return {
        title: 'abc'
      }
    }
  })

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      // title: '我是标题'
    }
  })
</script>
~~~

## 7.父子组件通信

1. 父级向子级传递

   * 在组件中，使用选项props来声明需要从父级接收到的数据
   * props的值有两种方式
     * 方式一：字符串数组，数组中的字符串就是传递时的名称
     * 方式二：对象，对象可以设置传递时的类型，也可以设置默认值等

   ~~~
   <div id="app">
     <!--<cpn v-bind:cmovies="movies"></cpn>-->
     <!--<cpn cmovies="movies" cmessage="message"></cpn>-->
   
     <cpn :cmessage="message" :cmovies="movies"></cpn>
   </div>
   
   
   
   <template id="cpn">
     <div>
       <ul>
         <li v-for="item in cmovies">{{item}}</li>
       </ul>
       <h2>{{cmessage}}</h2>
     </div>
   </template>
   
   <script src="../js/vue.js"></script>
   <script>
     // 父传子: props
     const cpn = {
       template: '#cpn',
       // props: ['cmovies', 'cmessage'],
       props: {
         // 1.类型限制
         // cmovies: Array,
         // cmessage: String,
   
         // 2.提供一些默认值, 以及必传值
         cmessage: {
           type: String,
           default: 'aaaaaaaa',
           required: true
         },
         // 类型是对象或者数组时, 默认值必须是一个函数
         cmovies: {
           type: Array,
           default() {
             return []
           }
         }
       },
       data() {
         return {}
       },
       methods: {
   
       }
     }
   
     const app = new Vue({
       el: '#app',
       data: {
         message: '你好啊',
         movies: ['海王', '海贼王', '海尔兄弟']
       },
       components: {
         cpn
       }
     })
   </script>
   ~~~

   * props数据验证
     * 在前面，我们的props选项是使用一个数组
     * 我们说过，除了数组之外，我们也可以使用对象，当需要对props进行类型等验证时，就需要对象写法了
     * 验证都支持哪些数据类型呢？
       * String
       * Number
       * Boolean
       * Array
       * Object
       * Date
       * Function
       * Symbol
     * 当我们有自定义构造函数时，验证也支持自定义的类型

2. 子级向父级传递

   * 通过自定义事件来完成
   * 自定义事件的流程
     * 在子组件中，通过$emit()来触发事件
     * 在父组件中，通过v-on来监听子组件事件

