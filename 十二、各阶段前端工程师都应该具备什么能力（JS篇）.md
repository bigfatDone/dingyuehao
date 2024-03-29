> 作为一名程序猿、攻城狮，要清楚自己的实力，自己所处的阶段，这样才能更好的扬长补短。常问自己几个问题：我最擅长什么，我比别人有哪些优势？我的短板在哪些方面？我在整个行业所处什么阶段，在这个阶段我该如何提升自己？
> 对于前端工程师等级的划分，每个人都可能有自己的理解，正所谓，一千个读者就有一千个哈姆雷特。下面是我对前端工程师划分的一些拙见。

### 一、入门菜鸟

这个阶段一般具备以下几点：
- 基础的JavaScript编程能力
- 基本能看懂别人写的代码
- 有一定的代码调试能力

举些例子：
#### 1、怎样对字符串进行截取操作，你会想到哪些方法？
substr() ,subString(), split(), slice() ...

#### 2、给你一段代码，你能知道这段代码实现了什么功能，别人为什么要这么写？
```javascript
var url = window.location.href;
if(url === 'http://www.xieliqun.com'){
	window.location.href = 'https://github.com/tsrot';
}else{
	window.location.href = '/404';
}
```
#### 3、给你一段简单的错误代码，你能知道错在哪里，怎样去改正它？
```javascript
var foo = 'hello world!';
var arr = [];
for(var i=0;i<foo.length;i++){
	var fooArr = arr.push(foo[i]);
	console.log(fooArr);
}
```

### 二、初级工程师

初级工程师应该能够：
- 解决一些例如特效方面的问题
- 能使用一些框架，例如jQuery、bootstrap、vue等
- 能使用ajax进行简单的前后通信
- 能DOM编程解决一些问题
- 能熟练使用浏览器的调试工具
- 了解一些HTML 5 API
- 了解ES5 规范

举些例子：
#### 1、怎样实现一个焦点图的效果？
在这个阶段只要能正确解决问题就好了。你可以自己去写代码实现，无论是原生，还是使用jQuery，你也可以百度去网上找一些焦点图的插件，或别人总结的方法。只要能够无错地完成需求，不考虑代码冗余之类的带来的性能问题。


#### 2、使用jQuery完成一个简单的动画？
假如完成一个可控制的球在水平面跳动的效果。你应该想怎样触发球，是hover还是click，球怎样跳动起来，是用css样式来控制，还是用jQuery的animate函数来执行动画。

#### 3、怎样使用ajax完成用户名验证？
你要完整的说出它的思路，首先用户输入完用户名，失去焦点（blur）后，然后通过ajax POST或者GET把用户名提交到后端，此时后端会给你一个接口，你把用户名传到这个接口，后端应该会返回一个true or false给你，根据返回的结果，作出相应的用户提示。

#### 4、如何动态的插入、删除、替换一个DOM元素？
原生方法：appendChild()、removeChild()、innerHTML、replaceChild() ...

jQuery方法：append()、empty()、html()、remove()、replaceAll() ...

#### 5、H5 新增了哪些API？
localStorage 、sessionStorage、ApplicationCache、postMessage、file、canvas ...

#### 6、ES6 比 ES5 有哪些新特性？
语法上更严格了，使用了let，const来声明，加强了作用域。

添加了更多的语法，例如箭头函数，模板字符串...


### 三 、中级工程师

中级工程师应该具备：
- 深入理解this、闭包、事件模型、原型和原型链、作用域链、继承等概念
- 尽量使用ES6编写代码
- 熟悉前后端通信方式
- 熟悉一些前端技术框架设计思想、优劣势等
- 熟悉模块化、面向对象、MVC等编程思想
- 能自己独立封装一些组件
- 编码时尽量考虑性能优化
- 了解常见的http状态码
- 了解前端工程化思想
- 了解一些最新的技术框架等
- 了解函数式编程思想

举些例子：自找答案
1. setTimeout中function里面的this指向什么？
2. 写一个最常见的闭包问题？
3. 如何深度克隆一个对象？
4. 前后端有哪些通信方式？
5. jQuery里的ready函数是怎样实现的，和原生的load有什么不同？
6. 谈谈commonJS和AMD的区别？
7. JavaScript是如何实现面向对象的？
8. 谈一谈JavaScript的性能优化问题？
9. bower、grunt、gulp、yeoman、webpack的了解？
10. JavaScript的异步编程？


### 四、高级工程师

高级前端工程师应该具备：
- 使用前端工程化思维开发
- JavaScript对DOM操作的各种方式与性能开销
- 熟悉RESTful架构、跨域等技术
- 能对代码进行良好的性能优化
- 了解常用框架功能原理的代码实现
- 熟悉前端开发的一些安全问题
- 熟悉常见跨浏览器问题
- 了解必要的计算机网络协议
- 熟悉JavaScript的前后端开发
- 熟悉各种开发设计模式
- 了解前端的一些测试方法

举些例子：自找答案
1. 如何解决回调层级过深的问题？
2. CORS跨域的原理？
3. 谈谈各种本地存储方案的优势与弊端？
4. JS延迟加载的方式有哪些？
5. 哪些操作会造成内存泄漏？
6. 写一个通用的事件侦听器函数？
7. 介绍一下XSS和CSRF的原理和防范？
8. 如何实现一个简易个模块管理库？
9. 介绍for in的技术细节与性能问题？
10. 谈谈JS的满加载和断点续调问题？
11. 如何实现JS的依赖注入？

> github地址：https://github.com/bigfatDone/dingyuehao.git 


