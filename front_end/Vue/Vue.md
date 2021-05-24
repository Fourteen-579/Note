# 回顾JavaScript

## 函数和标准对象

## BOM和DOM

#### 事件

- DOM事件：增删遍历，修改节点元素内容

- 浏览器事件：window document

- jQuery

#### 视图

- html

- css

#### 通信

- xhr
- ajax
- axios



# Vue：前端体系、前后端分离

## 概述

一套用于构建用户界面的渐进式框架

Vue的核心库只关注视图层

## 前端三要素

- HTML（结构）

- CSS（表现）

  - 无法嵌套书写
  - 没有变量和合理的样式复用机制

  - ***CSS预处理器***
    - 定义了一种新的语言。用一种专门的编程语言，为CSS增加了编程的特性
    - 用一种专门的编程语言，进行Web页面样式设计，再通过编译器转化为正常的Css文件
    - SASS
    - LESS

- JavaScript（行为）

  - jQuery
  - Angular 模块化开发+MVC模式
  - React 虚拟DOM
  - Vue 模块化开发+虚拟DOM（计算属性）
  - Axios 前端通信框架

## 三端统一

混合开发

- 云打包
- 本地打包

微信小程序

## 后端技术

NodeJs

## 主流前端框架

Vue.js



# 第一个Vue程序

## Vue模式

### MVVM实现

model：模型层，JavaScript对象

view：视图层，DOM

viewmodel

- 连接视图和数据的中间件
- 能够观察到数据的变化，并对视图对应的内容进行更新
- 能够监听到视图的变化，并能够通知数据发生变化
- 视图和状态都在viewmodel中

### 为什么要使用MVVM

- 低耦合
- 可复用
- 独立开发
- 可测试

```html
<div id="app">
    {{message}}
</div>
```

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: "hello!"
        }
    })
</script>
```

## 指令

带有v-前缀，以表示它们是Vue提供的特殊特性

### v-bind

```html
    <span v-bind:title="message">鼠标悬停几秒钟查看</span>
```

```html
    <span :title="message">鼠标悬停几秒钟查看</span>
```

### v-if

```html
    <h1 v-if="ok">Yes</h1>
    <h1 v-else>No</h1>
```

### v-for

```html
    <li v-for="(item,index) in items">
        {{item.message}}--{{index}}
    </li>
```

### 事件 v-on

```html
<div id="app">
    <button v-on:click="sayHi">there</button>
</div>
```

```html
<div id="app">
    <button @click="sayHi">there</button>
</div>
```

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: 'A'
        },
        methods: {
            sayHi: function () {
                alert(this.message)
            }
        }
    })
</script>
```

## Vue主要七大元素

- el
- data
- template
- methods
- render
- computed
- watch



# Vue：双向绑定

## 什么是双向绑定

数据发生变化，视图也发生变化

视图发生变化，数据也会同步变化

双向绑定是对于UI控件，非UI控件不会涉及到双向绑定

## 在表单中使用双向数据绑定

v-model

```html
<input type="text" v-model="message">{{message}}
```

```html
<select v-model="fourteen">
        <option>A</option>
        <option>B</option>
        <option>C</option>
    </select>
```

使用v-model之后会把checked、selected等属性忽略，所以需要增加一个空属性避免这种情况

```html
    <select v-model="fourteen">
        <option value="" disabled>--请选择--</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
    </select>
```



# 第一个Vue组件

## 什么是组件

组件是可复用的Vue实例，即是一组可以重复使用的模板，跟jstl的自定义标签等框架有异曲同工之妙。通常一个应用会以一颗嵌套的组件树的形式来组织。

## 自定义一个组件

```html
<div id="app">
    <!--组件：传递给组件中的值：props-->
    <fourteen v-for="item in items" v-bind:values="item">
    </fourteen>
</div>
```

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    <!--定义一个Vue组件component-->
    Vue.component("fourteen", {
        props: ['values'],
        template: "<li>{{values}}</li>"
    });
    var vm = new Vue({
            el: "#app",
            data: {
                items: ["java", "python", "c"]
            }
        })
    ;
</script>
```



# Vue：Axios异步通信

## 什么是Axios

一个开源的可以用在浏览器端和NodeJs的异步通信框架

- 从浏览器创建XMLHttpRequests
- 从node.js创建http请求
- 支持Promise API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御XSRF

## 为什么要使用Axios

因为Vue.js是一个视图层框架 并且作者严格遵守SoC（关注度分离原则）

## 第一个Axios应用程序

```html
    <!--    解决闪烁问题-->
    <style>
        [v-clock] {
            display: none;
        }
    </style>
```

```html
<div id="vue" v-cloak>
    <div>{{info.name}}</div>
    <div>{{info.address.street}}</div>
    <a v-bind:href="info.url">跳转</a>
</div>
```

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script src=https://unpkg.com/axios/dist/axios.min.js></script>
<script type="text/javascript"></script>
<script>
    var vm = new Vue({
        el: "#vue",
        //data:属性:vm
        //data:方法
        data() {
            return {
                //请求的返回参数格式，必须和json字符串一样
                info: {
                    name: null,
                    address: {
                        street: null,
                        city: null,
                        country: null
                    },
                    url:null
                }
            }
        },
        mounted() {//钩子函数 链式编程 ES6新特性
            axios.get('../data.json').then(response => (this.info = response.data));
        }
    });
</script>
```



# Vue生命周期

Vue实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模板、挂载DOM、渲染->更新->渲染、卸载等一系列过程。

![](Vue_Life.png)



# Vue计算属性

计算属性突出在属性两个字上，首先他是个属性，其次这个属性有计算的能力，这里的计算就是个函数；简单来说，他就是一个能够计算结果缓存起来的属性（将行为转化成了静态的属性），仅此而已；可以想象为缓存。

计算出来的结果，保存在属性中，在内存中运行。

调用方法时，每次都需要进行计算，既然有计算过程则必定产生系统开销，那如果这个结果是不经常变化的呢？此时就可以考虑将这个结果缓存起来，采用计算属性可以很方便的做到这一点，计算属性的主要特性就是为了将不经常变化的计算结果进行缓存，以节约我们的系统开销。

```html
<div id="app">
    <p>{{currentTime1()}}</p>
    <p>{{currentTime2}}</p>
</div>
```

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: "hello!"
        },
        methods: {
            currentTime1: function () {
                return Date.now();
            }
        },
        computed: {//计算属性 重名之后只会调用methods中的方法
            currentTime2: function () {
                this.message;
                return Date.now();
            }
        }
    });
</script>
```



# 插槽Slot

<slot>元素作为承载分发内容的出口，可以应用在组合组建的场景中。

```html
<div id="app">
    <fourteen>
        <fourteen-title slot="fourteen-title" :title="title"></fourteen-title>
        <fourteen-items slot="fourteen-items" v-for="item in items" :item="item"></fourteen-items>
    </fourteen>
</div>
```

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>

    Vue.component("fourteen", {
        template: "<div>\
            <slot name='fourteen-title'></slot>\
            <ul>\
            <slot name='fourteen-items'></slot>\
            </ul>\
            </div>"
    });

    Vue.component("fourteen-title", {
        props: ["title"],
        template: "<div>{{title}}</div>"
    });
    Vue.component("fourteen-items", {
        props: ["item"],
        template: "<li>{{item}}</li>"
    });

    var vm = new Vue({
        el: "#app",
        data: {
            title:"列表",
            items: ['java', 'python', 'c', '前端']
        }
    });
</script>
```

