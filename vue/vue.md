# Vue
### 创建一个 Vue 实例
### 数据与方法
    -当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时 data 中存在的属性才是响应式的。

### 实例生命周期钩子
    - 生命周期钩子的 this 上下文指向调用它的 Vue 实例
    - created 钩子可以用来在一个实例被创建之后执行
### v-if

   - 如果想切换多个元素,可以把一个 <template> 元素当做不可见的包裹元素，并在上面使用 v-if。
   - 这两个元素是完全独立的，不要复用它们”。只需添加一个具有唯一值的 key 属性
   - v-show：
      - 带有 v-show 的元素始终会被渲染并保留在 DOM 中。v-show 只是简单地切换元素的 CSS 属性 display。
      - v-show 不支持 <template> 元素，也不支持 v-else。
   - v-if和v-show的区别：
      - v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
      - v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
      - 相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
      - 一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。
      - 不推荐同时使用 v-if 和 v-for，v-for 具有比 v-if 更高的优先级。

### v-text---指定解决{{}}表达式闪烁的问题
    <span v-text="msg"></span>
    <!-- 和下面的一样 -->
    <span>{{msg}}</span>
    //使用{{}}的比较多，如果都使用v-text又比较麻烦，所以Vue提供了一个指令v-cloak
### v-cloak 
    <div id="app" v-cloak>
       <h1>{{msg}}</h1>
    </div>
    <style>
        [v-cloak]{
          display:none;
        }
    </style>
    //浏览器在解析的过程中，发现具有v-cloak的属性隐藏不显示，所以你就看不到这个{{}}闪烁问题了
    //当Vue解析替换完之后，Vue会自动把v-cloak样式移除
 ### v-pre---告诉vue不要解析这个节点内部的内容，让浪费时间
 ### v-if---会根据条件进行渲染和不渲染
     - true 渲染DOM
     - false 不渲染DOM   
     - 需要非常频繁的切换，使用v-show较好；
       如果在运行时条件很少改变，使用v-if较好
- 在模板中放太多的逻辑会让模板过重难以维护
- 想在模板中多次引用此处功能时，就会更加难以处理。
- 所以，对于任何复杂逻辑，使用计算属性
- 1.使用方法可以把这种复杂逻辑封装起来(每使用一次就调用一次，重复使用效率不高)
- 2.使用计算属性（不要让模板逻辑太乱，解决性能问题）
   - 本质是一个方法，不是方法，当属性来用，不能用于事件处理函数
- 为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一key属性：
### 自定义指令
  - 什么是：除了使用vue提供的内置指令，我们可以自定义一些自己的指令
  - 什么时候需要：当你需要不可避免的DOM的时候，使用自定义指令来解决
  - 怎么使用？
    - 注册
      - 全局注册：在任何组件中都可以使用
      - 局部注册：只能在当前组件中使用
      - 如果多个组件中使用---定义成全局的
    - 使用
      - 要加上v-前缀 
      - 驼峰命名，在使用是需要把驼峰转小写用横杆连接

### 在客户端存储数据 （本地存储）
- localStorage-没有时间限制的数据存储
  - getItem('key')---取值
  - setItem('key','value')---赋值
      - setItem('key',JSON.stringify({foo:'bar'}))
  - removeItem()---删除
- sessionStorage-针对一个session的数据存储
   
```
<div v-for="item in items" v-bind:key="item.id">
  <!-- 内容 -->
</div>
```
- 变异方法---会改变原始数组
   - push()、pop()、shift()、unshift()、splice()、sort()、reverse()
- 替换数组（非变异数组）---不会改变原始数组，而总是返回一个新数组
   - filter()、concat() 和 slice()
箭头函数的this定义：箭头函数的this是在定义函数时绑定的，不是在执行过程中绑定的。简单的说，函数在定义时，this就继承了定义函数的对象。



vuejs知识
1、认识vue.js
+ CDN 开发环境 生产环境  选择就近的服务器
+ 下载和引入
+ npm install vue



2、vue基础语法
3、组件化开发
4、vue-cli 基于webpack  
   webpack 
   vue-cli
   vue-cli2
   vue-cli3
5、vue-router 前端路由
6、vuex  vue状态管理
7、网络封装 
   axios的使用
8、项目实战
9、项目部署 
   NGINX服务器
   远程Linux上的NGINX部署
10、vuejs原来相关 
   响应式原理(双向绑定)
   源码
   
   

vue的mvvm：
view===dom
viewModel===vue实例  数据绑定（model数据绑定在view里,响应式，最新）   vue指令事件响应绑定到model,对dom界面做监听，回调model函数
model===js


方法、函数 
方法：methods
函数：function
定义在类里面是方法，定义外面函数


release/debug
生命周期(钩子函数hook)：事务诞生到消亡的过程
vue生命周期：
beforeCreate(){
}
created(){  //做网络请求,赋值data,渲染dem
}
mounted(){
}

代码规范：缩进4个空格，2个空格

cli->editconfig 2空格

{{}}======mustache语法