# 整理一波关于Vue的核心面试题
## 一、对于MVVM模型的理解？
> MVVM 是 Model-View-ViewModel 的缩写。
Model代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑。
View 代表UI 组件，它负责将数据模型转化成UI 展现出来。
ViewModel 监听模型数据的改变和控制视图行为、处理用户交互，简单理解就是一个同步View 和 Model的对象，连接Model和View。
在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。
ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

## 二、Vue的生命周期

**beforeCreate**（创建前） 在数据观测和初始化事件还未开始

**created** 创建后） 完成数据观测，属性和方法的运算，初始化事件，el属性还没有显示出来

**beforeMount**（载入前）在挂载开始之前被调用，相关的render函数首次被调用。实例已完成以下的配置：编译模板（在内存中编译模板），把data里面的数据和模板生成html。注意此时还没有挂载html到页面上。

**mounted**（载入后）在el 被新创建的 vm.el 替换，并挂载到实例上去之后调用。实例已完成以下的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html页面中。此过程中进行ajax交互。

**beforeUpdate**（更新前）在数据更新之前调用，发生在虚拟DOM重新渲染和打补丁之前。可以在该钩子中进一步地更改状态，不会触发附加的重渲染过程。

**updated**（更新后）在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。

**beforeDestroy**（销毁前）在实例销毁之前调用。实例仍然完全可用。

**destroyed**（销毁后） 在实例销毁之后调用。调用后，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。

## 3、三、 Vue实现数据双向绑定的原理：Object.defineProperty() 和 Proxy

*1.x ~ 2.x* vue实现数据双向绑定主要是：采用数据劫持结合发布者-订阅者模式的方式，通过**Object.defineProperty（）**来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应监听回调。当把一个普通 Javascript 对象传给 Vue 实例来作为它的 data 选项时，Vue 将遍历它的属性，用 Object.defineProperty 将它们转为 getter/setter。用户看不到 getter/setter，但是在内部它们让 Vue 追踪依赖，在属性被访问和修改时通知变化。

*3.x* vue使用了**proxy**代替了**Object.defineProperty（）** 进行数据代理，可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。

vue的数据双向绑定 将MVVM作为数据绑定的入口，整合Observer，Compile和Watcher三者，通过Observer来监听自己的model的数据变化，通过Compile来解析编译模板指令（vue中是用来解析 {{}}），最终利用watcher搭起observer和Compile之间的通信桥梁，达到数据变化 —>视图更新；视图交互变化（input）—>数据model变更双向绑定效果。

**js实现简单的双向绑定Object.defineProperty()**
```
<body><divid="app"><inputtype="text"id="txt"><pid="show"></p></div></body><scripttype="text/javascript">var obj = {}
    Object.defineProperty(obj, 'txt', {
        get: function () {
            return obj
        },
        set: function (newValue) {
            document.getElementById('txt').value = newValue
            document.getElementById('show').innerHTML = newValue
        }
    })
    document.addEventListener('keyup', function (e) {
        obj.txt = e.target.value
    })
</script>
```
**js实现简单的双向绑定Proxy**
```
<!--html-->
<div id="app">
    <h3 id="paragraph"></h3>
    <input type="text" id="input"/>
</div>

<!-- js -->
//获取段落的节点
const paragraph = document.getElementById('paragraph');
//获取输入框节点
const input = document.getElementById('input');
    
//需要代理的数据对象
const data = {
    text: 'hello world'
}

const handler = {
    //监控 data 中的 text 属性变化
    set: function (target, prop, value) {
        if ( prop === 'text' ) {
                //更新值
                target[prop] = value;
                //更新视图
                paragraph.innerHTML = value;
                input.value = value;
                return true;
        } else {
            return false;
        }
    }
}

//添加input监听事件
input.addEventListener('input', function (e) {
    myText.text = e.target.value;   //更新 myText 的值
}, false)

//构造 proxy 对象
const myText = new Proxy(data,handler);

//初始化值
myText.text = data.text;    
```
## 四、Vue组件间的参数传递

### 父子组件相互通信方法详情

1. 子组件通过 $emit 调用父组件的 method
```
// 父组件中定义 @updateInfo 调用的方法
<template>
  <user-popup @updateInfo="updateInfo"></user-popup>
</template>
 
methods: {
  updateInfo() {
    xxxxxx
  },
},
 
// 子组件在某个方法中进行调用，例如
saveInfomation() {
  this.$emit('updateInfo');
}
```
2. 父组件通过 prop 向子组件进行传值
```
// 父组件内定义传递给子组件的值 userInformation
<template>
  <child :userInformation="userInfo"></child>
</template>
 
data() {
  return {
    userInfo: {
      type: Object,
      required: true,
    },
  };
},
 
// 子组件内通过 prop 获取父组件传递的值 userInformation
<template>
  <label>姓名：</label><span>{{userInformation.username}}</span>
</template>
 
props: {
  userInformation: {
    type: Object,
    required: true,
  }
}
```
3. 父组件通过 $refs 调用子组件的 method
```

<template>
  <child ref="son"></child>
</template>
 
method: {
  parentMethod(param) {
    this.$refs.son.childMethod(param);
  },

```
### 非父子组件相互通信方法详情

> 原理：通过new一个新的vue实例化对象，作为中间件传递数据

情景描述：brother.vue 和 sister.vue 两姊妹要通信，sister 要知道 brother 被点击了多少次，由于它们师兄和师妹的关系（平级），所以需要一个新的中间件 globalBus 来进行消息的传递。

globalBus.js

```
import Vue from 'vue';
export const globalBus = new Vue();
```
> 这里 import 了一个 vue 类，然后实例化并且将它 export, 实际上是创建了一个与 DOM 和程序的其他部分完全解耦的组件，它仅仅是一个组件所以非常的轻量。

brother.vue

```
<template>
  <button @click="clickCount"></button>
</template>
 
import { globalBus } from './globalBus';
 
export default {
  data() {
    return {
      counts: 0,
    };
  },
  method: {
    clickCount() {
      this.counts++;
      globalBus.$emit('countNumber', this.counts);
    },
  },
}
```
> 触发了 globalBus 的 countNumber 事件，返回参数 this.counts。
sister.vue
```
import { globalBus } from './globalBus';
 
export default {
  created() {
    this.total();
  },
  method: {
    total() {
      globalBus.$on('countNumber', (number) => {
        console.log(`brother 被点击了 ${number} 次。`);
      });
    },
  },
}
```
> 监听 globalBus 的 countNumber 方法

## 五、Vue的路由实现：hash模式 和 history模式

> vue-router 默认使用 hash 模式，所以在路由加载的时候，项目中的 url 会自带 #。如果不想使用 #， 可以使用 vue-router 的另一种模式 history
```
new Router({
  mode: 'history',
  routes: [ ]
})
```
> 需要注意的是，当我们启用 history 模式的时候，由于我们的项目是一个单页面应用，所以在路由跳转的时候，就会出现访问不到静态资源而出现 404 的情况，这时候就需要服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面

## 六、vue路由的钩子函数

首页可以控制导航跳转，beforeEach，afterEach等，一般用于页面title的修改。一些需要登录才能调整页面的重定向功能。

**beforeEach**主要有3个参数to，from，next：

**to**：route即将进入的目标路由对象

**from**：route当前导航正要离开的路由

**next**：function一定要调用该方法resolve这个钩子。执行效果依赖next方法的调用参数。可以控制网页的跳转。

## 七、vuex是什么？怎么使用？哪种功能场景使用它？

只用来读取的状态集中放在store中； 改变状态的方式是提交mutations，这是个同步的事物； 异步逻辑应该封装在action中。

在main.js引入store，注入。新建了一个目录store，….. export 。

场景有：单页应用中，组件之间的状态、音乐播放、登录状态、加入购物车
![](https://user-gold-cdn.xitu.io/2019/2/14/168e9bf1a6278fbb?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

**state**
Vuex 使用单一状态树,即每个应用将仅仅包含一个store 实例，但单一状态树和模块化并不冲突。存放的数据状态，不可以直接修改里面的数据。

**mutations**
mutations定义的方法动态修改Vuex 的 store 中的状态或数据。

**getters**
类似vue的计算属性，主要用来过滤一些数据。

**action**
actions可以理解为通过将mutations里面处里数据的方法变成可异步的处理数据的方法，简单的说就是异步操作数据。view 层通过 store.dispath 来分发 action。

```
conststore = new Vuex.Store({ 
  //store实例
  state: {count: 0},
  mutations: {
    increment(state) {
      state.count++
    }
  },
  actions: { 
    increment(context) 
      {
        context.commit('increment')
      }
  }
})
```
**modules** 项目特别复杂的时候，可以让每一个模块拥有自己的state、mutation、action、getters,使得结构非常清晰，方便管理。
```
  constmoduleA = {
    state: { ... },
    mutations: { ... },
    actions: { ... },
    getters: { ... }
  }
  constmoduleB = {
    state: { ... },
    mutations: { ... },
    actions: { ... }
  }
  conststore = new Vuex.Store({
    modules: {
      a: moduleA,
      b: moduleB
    }
  })
```
## 八、vue-cli如何新增自定义指令？

1. 创建局部指令
```
var app = new Vue({
    el: '#app',
    data: {    
    },
    // 创建指令(可以多个)
    directives: {
        // 指令名称
        dir1: {
            inserted(el) {
                // 指令中第一个参数是当前使用指令的DOMconsole.log(el);
                console.log(arguments);
                // 对DOM进行操作
                el.style.width = '200px';
                el.style.height = '200px';
                el.style.background = '#000';
            }
        }
    }
})
```
2. 全局指令
```
Vue.directive('dir2', {
    inserted(el) {
        console.log(el);
    }
})
```
3. 指令的使用
```
<divid="app"><divv-dir1></div><divv-dir2></div></div>
```
## 九、vue如何自定义一个过滤器？

html代码：
```
<divid="app"><inputtype="text"v-model="msg" />
     {{msg| capitalize }}
</div>
```
JS代码：
```
var vm=new Vue({
    el:"#app",
    data:{
        msg:''
    },
    filters: {
      capitalize: function (value) {
        if (!value) return''value = value.toString()
        returnvalue.charAt(0).toUpperCase() + value.slice(1)
      }
    }
})
```
全局定义过滤器
```
Vue.filter('capitalize', function (value) {
  if (!value) return''value = value.toString()
  returnvalue.charAt(0).toUpperCase() + value.slice(1)
})
```
过滤器接收表达式的值 (msg) 作为第一个参数。capitalize 过滤器将会收到 msg的值作为第一个参数。

## 十、对keep-alive 的了解？

**keep-alive**是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。
在vue 2.1.0 版本之后，keep-alive新加入了两个属性: include(包含的组件缓存) 与 exclude(排除的组件不缓存，优先级大于include) 。

使用方法
```
<!-- 该组件是否缓存取决于include和exclude属性 -->
<keep-alive include='include_components' exclude='exclude_components'>
  <component>
  </component>
</keep-alive>

```
参数解释

include - 字符串或正则表达式，只有名称匹配的组件会被缓存

exclude - 字符串或正则表达式，任何名称匹配的组件都不会被缓存

include 和 exclude 的属性允许组件有条件地缓存。二者都可以用“，”分隔字符串、正则表达式、数组。当使用正则或者是数组时，要记得使用v-bind 

使用示例
```
<!-- 逗号分隔字符串，只有组件a与b被缓存。 -->
<!-- 正则表达式 (需要使用 v-bind，符合匹配规则的都会被缓存) -->
<keep-alive include="a,b">
  <component></component>
</keep-alive>

<keep-alive :include="/a|b/">
  <component></component>  <!-- Array (需要使用 v-bind，被包含的都会被缓存) -->
</keep-alive>

<keep-alive :include="['a', 'b']">
  <component></component>
</keep-alive>
```
## 十一、一句话就能回答的面试题

<h5 id='k1'>1. 说一下Vue的双向绑定数据的原理</h5>

> `vue` 实现数据双向绑定主要是：采用数据劫持结合发布者-订阅者模式的方式，通过 `Object.defineProperty()` 来劫持各个属性的 `setter`，`getter`，在数据变动时发布消息给订阅者，触发相应监听回调

<h5 id='k2'>2. 解释单向数据流和双向数据绑定</h5>

> 单向数据流： 顾名思义，数据流是单向的。数据流动方向可以跟踪，流动单一，追查问题的时候可以更快捷。缺点就是写起来不太方便。要使UI发生变更就必须创建各种 `action` 来维护对应的 `state`

> 双向数据绑定：数据之间是相通的，将数据变更的操作隐藏在框架内部。优点是在表单交互较多的场景下，会简化大量业务无关的代码。缺点就是无法追踪局部状态的变化，增加了出错时 `debug` 的难度

<h5 id='k3'>3. Vue 如何去除url中的 #</h5>

`vue-router` 默认使用 `hash` 模式，所以在路由加载的时候，项目中的 `url` 会自带 `#`。如果不想使用 `#`， 可以使用 `vue-router` 的另一种模式 `history`

```js
new Router({
  mode: 'history',
  routes: [ ]
})
```

> 需要注意的是，当我们启用 `history` 模式的时候，由于我们的项目是一个单页面应用，所以在路由跳转的时候，就会出现访问不到静态资源而出现 `404` 的情况，这时候就需要服务端增加一个覆盖所有情况的候选资源：如果 `URL` 匹配不到任何静态资源，则应该返回同一个 `index.html` 页面

<h5 id='k4'>4. 对 MVC、MVVM的理解</h5>

> MVC


特点：
1. `View` 传送指令到 `Controller`
2. `Controller` 完成业务逻辑后，要求 `Model` 改变状态
3. `Model` 将新的数据发送到 `View`，用户得到反馈

**所有通信都是单向的**

> MVVM


特点： 
1. 各部分之间的通信，都是双向的
2. 采用双向绑定：`View` 的变动，自动反映在 `ViewModel`，反之亦然

具体请移步 [这里](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)

<h5 id='k5'>5. 介绍虚拟DOM</h5>

[参考这里](https://www.jianshu.com/p/616999666920)

<h5 id='k6'>6. vue生命周期的理解</h5>

> vue实例有一个完整的生命周期，生命周期也就是指一个实例从开始创建到销毁的这个过程

- `beforeCreate()` 在实例创建之间执行，数据未加载状态
- `created()` 在实例创建、数据加载后，能初始化数据，`dom`渲染之前执行
- `beforeMount()` 虚拟`dom`已创建完成，在数据渲染前最后一次更改数据
- `mounted()` 页面、数据渲染完成，真实`dom`挂载完成
- `beforeUpadate()` 重新渲染之前触发
- `updated()` 数据已经更改完成，`dom` 也重新 `render` 完成,更改数据会陷入死循环
- `beforeDestory()` 和 `destoryed()` 前者是销毁前执行（实例仍然完全可用），后者则是销毁后执行

<h5 id='k7'>7. 组件通信</h5>

> 父组件向子组件通信

子组件通过 props 属性，绑定父组件数据，实现双方通信

> 子组件向父组件通信

将父组件的事件在子组件中通过 `$emit` 触发

> 非父子组件、兄弟组件之间的数据传递

```js
/*新建一个Vue实例作为中央事件总嫌*/
let event = new Vue();

/*监听事件*/
event.$on('eventName', (val) => {
    //......do something
});

/*触发事件*/
event.$emit('eventName', 'this is a message.')
```

> Vuex 数据管理

<h5 id='k8'>8. vue-router 路由实现</h5>

> 路由就是用来跟后端服务器进行交互的一种方式，通过不同的路径，来请求不同的资源，请求不同的页面是路由的其中一种功能

参考 [这里](https://zhuanlan.zhihu.com/p/37730038)

<h5 id='k9'>9. v-if 和 v-show 区别</h5>

> 使用了 `v-if` 的时候，如果值为 `false` ，那么页面将不会有这个 `html` 标签生成。

> `v-show` 则是不管值为 `true` 还是 `false` ，`html` 元素都会存在，只是 `CSS` 中的 `display` 显示或隐藏

<h5 id='k10'>10. $route和$router的区别</h5>

> `$router` 为 `VueRouter` 实例，想要导航到不同 `URL`，则使用 `$router.push` 方法

> `$route` 为当前 `router` 跳转对象里面可以获取 `name` 、 `path` 、 `query` 、 `params` 等

<h5 id='k11'>11. NextTick 是做什么的</h5>

> `$nextTick` 是在下次 `DOM` 更新循环结束之后执行延迟回调，在修改数据之后使用 `$nextTick`，则可以在回调中获取更新后的 `DOM`

具体可参考官方文档 [深入响应式原理](https://cn.vuejs.org/v2/guide/reactivity.html)

<h5 id='k12'>12. Vue 组件 data 为什么必须是函数</h5>

> 因为js本身的特性带来的，如果 `data` 是一个对象，那么由于对象本身属于引用类型，当我们修改其中的一个属性时，会影响到所有Vue实例的数据。如果将 `data` 作为一个函数返回一个对象，那么每一个实例的 `data` 属性都是独立的，不会相互影响了

<h5 id='k13'>13. 计算属性computed 和事件 methods 有什么区别</h5>

我们可以将同一函数定义为一个 `method` 或者一个计算属性。对于最终的结果，两种方式是相同的

不同点：

> computed: 计算属性是基于它们的依赖进行缓存的,只有在它的相关依赖发生改变时才会重新求值

> 对于 `method` ，只要发生重新渲染，`method` 调用总会执行该函数

<h5 id='k14'>14. 对比 jQuery ，Vue 有什么不同</h5>

> jQuery 专注视图层，通过操作 DOM 去实现页面的一些逻辑渲染； Vue 专注于数据层，通过数据的双向绑定，最终表现在 DOM 层面，减少了 DOM 操作

> Vue 使用了组件化思想，使得项目子集职责清晰，提高了开发效率，方便重复利用，便于协同开发

<h5 id='k15'>15. Vue 中怎么自定义指令</h5>

> 全局注册

```js
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```

> 局部注册

```js
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```

参考 [官方文档-自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

<h5 id='k16'>16. Vue 中怎么自定义过滤器</h5>

> 可以用全局方法 `Vue.filter()` 注册一个自定义过滤器，它接收两个参数：过滤器 `ID` 和过滤器函数。过滤器函数以值为参数，返回转换后的值

```js
Vue.filter('reverse', function (value) {
  return value.split('').reverse().join('')
})
```

```html
<!-- 'abc' => 'cba' -->
<span v-text="message | reverse"></span>
```

过滤器也同样接受全局注册和局部注册

<h5 id='k17'>17. 对 keep-alive 的了解</h5>

> `keep-alive` 是 `Vue` 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染

```html
<keep-alive>
  <component>
    <!-- 该组件将被缓存！ -->
  </component>
</keep-alive>
```

> 可以使用API提供的props，实现组件的动态缓存

具体参考 [官方API](https://cn.vuejs.org/v2/api/#keep-alive)

<h5 id='k18'>18. Vue 中 key 的作用</h5>

> `key` 的特殊属性主要用在 `Vue` 的虚拟 `DOM` 算法，在新旧 `nodes` 对比时辨识 `VNodes`。如果不使用 `key`，`Vue` 会使用一种最大限度减少动态元素并且尽可能的尝试修复/再利用相同类型元素的算法。使用 `key`，它会基于 `key` 的变化重新排列元素顺序，并且会移除 `key` 不存在的元素。

> 有相同父元素的子元素必须有独特的 `key`。重复的 `key` 会造成渲染错误

具体参考 [官方API](https://cn.vuejs.org/v2/api/#key)

<h5 id='k19'>19. Vue 的核心是什么</h5>

> 数据驱动 组件系统

<h5 id='k20'>20. vue 等单页面应用的优缺点</h5>

> 优点：

- 良好的交互体验 
- 良好的前后端工作分离模式
- 减轻服务器压力

> 缺点：

- SEO难度较高
- 前进、后退管理 
- 初次加载耗时多 

<h5 id='k21'>21. vue-router 使用params与query传参有什么区别</h5>

`vue-router` 可以通过 `params` 与 `query` 进行传参

```js
// 传递
this.$router.push({path: './xxx', params: {xx:xxx}})
this.$router.push({path: './xxx', query: {xx:xxx}})

// 接收
this.$route.params

this.$route.query
```

- `params` 是路由的一部分,必须要有。`query` 是拼接在 `url` 后面的参数，没有也没关系
- `params` 不设置的时候，刷新页面或者返回参数会丢，`query` 则不会有这个问题