# 日常bug

不要在vue内随便用箭头函数，会模糊this指向 导致this为怒defined

# 基础
## v-bind:   

## v-if

## v-on 监听dom事件
要是需要访问原始DOM，可以使用$event传入方法		 v-on:click="warn('Form cannot be submitted yet.', $event)"
## 修饰符

## computed

## watch

## [class/style](https://cn.vuejs.org/v2/guide/class-and-style.html ) 	
:class={} 可以填对象，也可以是计算属性 也可以是数组

:style=“{}” 对象。 2.3也可以添加数组


## v-if v-else会复用已有元素而不是从头渲染。若是不想复用，可以给重复部分添加key值

## v-show
会被渲染并保留在dom中

## v-for
v-if v-for避免用在一起
v-for 遍历对象 ，默认遍历值
v-for="value in object"
v-for="(value, name) in object"
v-for="(value, name, index) in object"

由于 JavaScript 的限制，Vue 不能检测数组和对象的变化。
template 也可以用v-for


## [事件修饰符](https://cn.vuejs.org/v2/guide/events.html)	


## v-model
v-model 为input textarea select双向数据绑定



## 组件

### 注册组件

### prop

### 自定义事件

### 插槽

### 动态组件

### 边界情况

组件data必须是函数 return值 为了实例化

全局注册和局部注册

通过prop向子组件传递数据
可以先注册props 然后传递至组件中
也可以使用v-bind动态传递参数

要是传的太多，就只穿一个对象，然后掉他的子对象

子件使用$emit(‘xxx’，xxx)调用父类传入的函数
父类使用$event接收子类传入的值

动态组件  is ？

组件注册 组件名简易全小写且必须包含一个连字符

Prop 可以以对象形式列出prop，列出名称和类型。
数字也要用v-bind复制
v-bind代表 赋值js表达式

单向数据流
不应该在子组件内改变prop

对象和数组是通过引用传入的，对于一个数组或者对象prop来说，子组件中改变会导致父组件改变

prop可以设置验证   prop在组件实例创建之前进行验证，所以实例的property如data，computed不能在default，validator中使用


在组件上使用v-model

v-model会将value绑定到prop和事件上，通过prop传入，事件传出



## 可复用性&组合
## 工具 
## 内在原理
