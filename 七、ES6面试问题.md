<blockquote>
<p>作者：Alex</p>
<p>译者：前端小智</p>
<p>来源：dev.to</p>
</blockquote>

<hr>
<p>ECMAScript 6（以下简称ES6）是 JS 语言的下一代标准，已经在<code>2015</code>年<code>6</code>月正式发布了。它的目标，是使得 JS 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。接下来咱们来看看 20 道棘手的面试题，通过做题，顺带提升一下咱们的 JS 的技能。</p>
<h4 class="heading" data-id="heading-0">问题1：可以解释一下 <code>ES5</code> 和<code>ES6</code>的区别吗?</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p><strong>ECMAScript 5 (ES5)</strong>：ECMAScript 的第五版，于2009年标准化，该标准已在所有现代浏览器中完全支持。</p>
<p><strong>ECMAScript 6 (ES6)/ ECMAScript 2015 (ES2015)</strong>:ECMAscript 第 6 版，2015 年标准化。这个标准已经在大多数现代浏览器中部分实现。</p>
<p>以下是ES5和ES6之间的一些主要区别：</p>
<p><strong>箭头函数和字符串插值</strong></p>
<pre><code class="copyable">const greetings = (name) =&gt; {
  return `hello ${name}`;
}
<span class="copy-code-btn"></span></code></pre>
<p>也可以这样写：</p>
<pre><code class="copyable">const greetings = name =&gt; `hello ${name}`;    
<span class="copy-code-btn"></span></code></pre>
<p><strong>const</strong>：<code>const</code> 表示无法修改变量的原始值。需要注意的是，<code>const</code>表示对值的常量引用，咱们可以改变被引用的对象的属性值，但不能改变引用本身。</p>
<pre><code class="copyable">const NAMES = [];
NAMES.push("Jim");
console.log(NAMES.length === 1); // true
NAMES = ["Steve", "John"]; // error    
<span class="copy-code-btn"></span></code></pre>
<p><strong>块作用域</strong>：ES6 中 <code>let</code>, <code>const</code> 会创建块级作用域，不会像 <code>var</code> 声明变量一样会被提升。</p>
<p><strong>默认参数</strong>：默认参数使咱们可以使用默认值初始化函数。当参数省略或 <code>undefined</code> 时使用默认参数值。</p>
<pre><code class="copyable">function multiply (a, b = 2) {
   return a * b;
}
multiply(5); // 10    
<span class="copy-code-btn"></span></code></pre>
<p><strong>类定义与继承</strong></p>
<p>ES6 引入了对类(<code>class</code>关键字)、构造函数(<code>constructor</code>关键字)和 <code>extend</code> 关键字(用于继承)的语言支持。</p>
<p><strong>for-of 运算符</strong></p>
<p><code>for...of</code> 语句创建一个遍历可迭代对象的循环。</p>
<p><strong>展开操作符</strong></p>
<pre><code class="copyable">const obj1 = { a: 1, b: 2 }
const obj2 = { a: 2, c: 3, d: 4}
const obj3 = {...obj1, ...obj2}    
<span class="copy-code-btn"></span></code></pre>
<p><strong>Promises</strong>: Promises 提供了一种机制来处理异步操作的结果和错误。可以使用回调来完成相同的事情，但是<code>Promises</code> 通过方法链接和简洁的错误处理来提高可读性。</p>
<pre><code class="copyable">const isGreater = (a, b) =&gt; {
  return new Promise ((resolve, reject) =&gt; {
    if(a &gt; b) {
      resolve(true)
    } else {
      reject(false)
    }
    })
}
isGreater(1, 2)
  .then(result =&gt; {
    console.log('greater')
  })
 .catch(result =&gt; {
    console.log('smaller')
 })    
<span class="copy-code-btn"></span></code></pre>
<p><strong>模块导出</strong></p>
<pre><code class="copyable">const myModule = { x: 1, y: () =&gt; { console.log('This is ES5') }}
export default myModule;   
<span class="copy-code-btn"></span></code></pre>
<p><strong>和导入</strong></p>
<pre><code class="copyable">import myModule from './myModule';
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-1">问题 2：什么是 IIFE (立即调用的函数表达式)</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p><code>IIFE</code>是一个立即调用的函数表达式，它在创建后立即执行</p>
<pre><code class="copyable">(function IIFE(){
    console.log( "Hello!" );
})();
// "Hello!"
<span class="copy-code-btn"></span></code></pre>
<p>常常使用此模式来避免污染全局命名空间，因为在<code>IIFE</code>中使用的所有变量(与任何其他普通函数一样)在其作用域之外都是不可见的。</p>
<h4 class="heading" data-id="heading-2">问题 3：何时在 ES6 中使用箭头函数？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p>以下是一些经验分享：</p>
<ul>
<li>
<p>在全局作用域内和<code>Object.prototype</code>属性中使用 <code>function</code> 。</p>
</li>
<li>
<p>为对象构造函数使用 <code>class</code>。</p>
</li>
<li>
<p>其它情况使用箭头函数。</p>
</li>
</ul>
<p>为啥大多数情况都使用<strong>箭头函数</strong>？</p>
<ul>
<li>
<p><strong>作用域安全性</strong>:当箭头函数被一致使用时，所有东西都保证使用与根对象相同的<code>thisObject</code>。如果一个标准函数回调与一堆箭头函数混合在一起，那么作用域就有可能变得混乱。</p>
</li>
<li>
<p><strong>紧凑性</strong>:箭头函数更容易读写。</p>
</li>
<li>
<p>清晰度:使用箭头函数可明确知道当前 <code>this</code> 指向。</p>
</li>
</ul>
<h4 class="heading" data-id="heading-3">问题 4:将 Symbol 引入ES6 的目的是什么？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p><code>Symbol</code> 是一种新的、特殊的对象，可以用作对象中惟一的属性名。使用 <code>Symbol</code> 替换<code>string</code> 可以避免不同的模块属性的冲突。还可以将<code>Symbol</code>设置为私有，以便尚无直接访问<code>Symbol</code>权限的任何人都不能访问它们的属性。</p>
<p><code>Symbol</code> 是JS新的基本数据类型。与<code>number</code>、<code>string</code>和<code>boolean</code> 原始类型一样，<code>Symbol</code> 也有一个用于创建它们的函数。与其他原始类型不同，<code>Symbol</code>没有字面量语法。创建它们的唯一方法是使用以下方法中的<code>Symbol</code>构造函数</p>
<pre><code class="copyable">let symbol = Symbol();    
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-4">问题 5: 在 ES6 中使用展开(spread)语法有什么好处? 它与剩余(rest)语法有什么不同?</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p>ES6 的展开语法在以函数形式进行编码时非常有用，因为咱们可以轻松地创建数组或对象的副本，而无需求助于<code>Object.create，slice</code>或库函数。<code>Redux</code> 和<code>rx.js</code>项目中经常使用此特性。</p>
<pre><code class="copyable">function putDookieInAnyArray(arr) {
  return [...arr, 'dookie'];
}

const result = putDookieInAnyArray(['I', 'really', "don't", 'like']); 
// ["I", "really", "don't", "like", "dookie"]

const person = {
  name: 'Todd',
  age: 29,
};

const copyOfTodd = { ...person };  
<span class="copy-code-btn"></span></code></pre>
<p>ES6 的 rest 语法提供了一种捷径，其中包括要传递给函数的任意数量的参数。</p>
<p>就像展开语法的逆过程一样，它将数据放入并填充到数组中而不是展开数组，并且它在函数变量以及数组和对象解构分中也经常用到。</p>
<pre><code class="copyable"> function addFiveToABunchOfNumbers(...numbers) {
  return numbers.map(x =&gt; x + 5);
}

const result = addFiveToABunchOfNumbers(4, 5, 6, 7, 8, 9, 10); 
// [9, 10, 11, 12, 13, 14, 15]

const [a, b, ...rest] = [1, 2, 3, 4]; // a: 1, b: 2, rest: [3, 4]

const { e, f, ...others } = {
  e: 1,
  f: 2,
  g: 3,
  h: 4,
}; // e: 1, f: 2, others: { g: 3, h: 4 }   
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-5">问题 6: ES6 类和 ES5 函数构造函数有什么区别？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<pre><code class="copyable">// ES5 Function Constructor
function Person(name) {
  this.name = name;
}

// ES6 Class
class Person {
  constructor(name) {
    this.name = name;
  }
}  
<span class="copy-code-btn"></span></code></pre>
<p>对于简单的构造函数，它们看起来非常相似。</p>
<p>构造函数的主要区别在于使用继承。如果咱们创建一个继承<code>Person</code>类的<code>Student</code>子类并添加一个<code>studentId</code>字段，以下是两种方式的使用：</p>
<pre><code class="copyable">// ES5 Function Constructor
function Student(name, studentID) {
  // 调用你类的构造函数以初始化你类派生的成员。
  Person.call(this. name)
  // 初始化子类的成员。
  this.studentId = studentId
}

Student.prototype = Object.create(Person.prototype)
Student.prototype.constructor = Student

// ES6 Class
class Student extends Person {
  constructor(name, studentId) {
    super(name)
    this.studentId = studentId
  }
}
<span class="copy-code-btn"></span></code></pre>
<p>在 ES5 中使用继承要复杂得多，而且 ES6 版本更容易理解和记住。</p>
<h4 class="heading" data-id="heading-6">问题 7: <code>.call</code> 和 <code>.apply</code> 区别是啥？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p><code>.call</code>和<code>.apply</code>均用于调用函数，并且第一个参数将用作函数中<code>this</code>的值。但是，<code>.call</code>将逗号分隔的参数作为下一个参数，而<code>.apply</code>将参数数组作为下一个参数。简单记忆法：<strong>C</strong>用于<code>call</code>和逗号分隔，<strong>A</strong>用于<code>apply</code>和参数数组。</p>
<pre><code class="copyable"> function add(a, b) {
  return a + b;
}

console.log(add.call(null, 1, 2)); // 3
console.log(add.apply(null, [1, 2])); // 3   
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-7">问题 8: 为什么要使用 ES6 类？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p>选择使用类的一些原因：</p>
<ul>
<li>
<p>语法更简单，更不容易出错。</p>
</li>
<li>
<p>使用新语法比使用旧语法更容易(而且更不易出错)地设置继承层次结构。</p>
</li>
<li>
<p><code>class</code>可以避免构造函数中使用new的常见错误（如果构造函数不是有效的对象，则使构造函数抛出异常）。</p>
</li>
<li>
<p>用新语法调用父原型方法的版本比旧语法要简单得多，用<code>super.method()</code>代替<code>ParentConstructor.prototype.method.call(this)</code> 或<code>Object.getPrototypeOf(Object.getPrototypeOf(this)).method.call(this)</code></p>
</li>
</ul>
<p>考虑下面代码：</p>
<p></p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/11/16e57ba14be021fe?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="800" data-height="603" src="https://user-gold-cdn.xitu.io/2019/11/11/16e57ba14be021fe?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
<p>使用 ES6 实现上述功能：</p>
<p></p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/11/16e57ba288475156?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="619" data-height="800" src="https://user-gold-cdn.xitu.io/2019/11/11/16e57ba288475156?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
<h4 class="heading" data-id="heading-8">问题 9: 在 JS 中定义枚举的首选语法是什么</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p>可以 <code>Object.freeze</code> 来实现枚举</p>
<pre><code class="copyable">var DaysEnum = Object.freeze({
    "monday": 1,
    "tuesday": 2,
    "wednesday": 3,
    ...
})
<span class="copy-code-btn"></span></code></pre>
<p>或者</p>
<pre><code class="copyable">var DaysEnum = {
    "monday": 1,
    "tuesday": 2,
    "wednesday": 3,
    ...
}
Object.freeze(DaysEnum)
<span class="copy-code-btn"></span></code></pre>
<p>但是，这阻止咱们把值分配给变量：</p>
<pre><code class="copyable">let day = DaysEnum.tuesday
day = 298832342 // 不会报错
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-9">问题 10: 解释一下 <code>Object.freeze()</code> 和 <code>const</code> 的区别</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐</p>
</blockquote>
<p><code>const</code>和<code>Object.freeze</code>是两个完全不同的概念。</p>
<p><code>const</code> 声明一个只读的变量，一旦声明，常量的值就不可改变：</p>
<pre><code class="copyable">const person = {
    name: "Leonardo"
};
let animal = {
    species: "snake"
};
person = animal; // ERROR "person" is read-only    
<span class="copy-code-btn"></span></code></pre>
<p><code>Object.freeze</code>适用于值，更具体地说，适用于对象值，它使对象不可变，即不能更改其属性。</p>
<pre><code class="copyable">let person = {
    name: "Leonardo"
};
let animal = {
    species: "snake"
};
Object.freeze(person);
person.name = "Lima"; //TypeError: Cannot assign to read only property 'name' of object
console.log(person); 
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-10">问题 11: JS 的提升是什么</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐</p>
</blockquote>
<p>提升是指 JS 解释器将所有变量和函数声明移动到当前作用域顶部的操作，提升有两种类型</p>
<ul>
<li>变量提升</li>
<li>函数提升</li>
</ul>
<p>只要一个<code>var</code>(或函数声明)出现在一个作用域内，这个声明就被认为属于整个作用域，并且可以在任何地方访问。</p>
<pre><code class="copyable">var a = 2
foo() // 正常运行, foo 已被提升

function foo() {
  a = 3
  console.log(a)   // 3
  var a                        
}

console.log( a )   // 2
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-11">问题 12: 解释一下原型设计模式(Prototype Pattern)</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐</p>
</blockquote>
<p>原型模式会创建新的对象，而不是创建未初始化的对象，它会返回使用从原型或样本对象复制的值进行初始化的对象。原型模式也称为属性模式。</p>
<p>原型模式有用的一个例子是使用与数据库中的默认值匹配的值初始化业务对象。原型对象保留默认值，这些默认值将被复制到新创建的业务对象中。</p>
<p>传统语言很少使用原型模式，但是JavaScript作为一种原型语言，在构建新对象及其原型时使用这种模式。</p>
<h4 class="heading" data-id="heading-12">问题 13: ES6 中的临时死区是什么</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐</p>
</blockquote>
<p>在 ES6 中，<code>let</code> 和<code>const</code> 跟 <code>var</code>、<code>class</code>和<code>function</code>一样也会被提升，只是在进入作用域和被声明之间有一段时间不能访问它们，这段时间是<strong>临时死区(TDZ)</strong>。</p>
<pre><code class="copyable">//console.log(aLet)  // would throw ReferenceError

let aLet;
console.log(aLet); // undefined
aLet = 10;
console.log(aLet); // 10
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-13">问题 14: 什么时候不使用箭头函数? 说出三个或更多的例子</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐</p>
</blockquote>
<p>不应该使用箭头函数一些情况：</p>
<ul>
<li>
<p>当想要函数被提升时(箭头函数是匿名的)</p>
</li>
<li>
<p>要在函数中使用<code>this/arguments</code>时，由于箭头函数本身不具有<code>this/arguments</code>，因此它们取决于外部上下文</p>
</li>
<li>
<p>使用命名函数(箭头函数是匿名的)</p>
</li>
<li>
<p>使用函数作为构造函数时(箭头函数没有构造函数)</p>
</li>
<li>
<p>当想在对象字面是以将函数作为属性添加并在其中使用对象时，因为咱们无法访问 <code>this</code> 即对象本身。</p>
</li>
</ul>
<h4 class="heading" data-id="heading-14">问题 15: ES6 中的 WeakMa p的实际用途是什么？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐</p>
</blockquote>
<p><strong>WeakMaps</strong> 提供了一种从外部扩展对象而不影响垃圾收集的方法。当咱们想要扩展一个对象，但是因为它是封闭的或者来自外部源而不能扩展时，可以应用<code>WeakMap</code>。</p>
<p><strong>WeakMap</strong>只适用于 ES6 或以上版本。<strong>WeakMap</strong>是键和值对的集合，其中键<strong>必须是对象</strong>。</p>
<pre><code class="copyable">var map = new WeakMap();
var pavloHero = {
    first: "Pavlo",
    last: "Hero"
};
var gabrielFranco = {
    first: "Gabriel",
    last: "Franco"
};
map.set(pavloHero, "This is Hero");
map.set(gabrielFranco, "This is Franco");
console.log(map.get(pavloHero)); //This is Hero
<span class="copy-code-btn"></span></code></pre>
<p><strong>WeakMaps</strong>的有趣之处在于，它包含了对<code>map</code>内部键的弱引用。弱引用意味着如果对象被销毁，垃圾收集器将从<code>WeakMap</code>中删除整个条目，从而释放内存。</p>
<h4 class="heading" data-id="heading-15">问题 16: 说明下列方法为何不能用作 IIFE，要使其成为 IIFE，需要进行哪些更改？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐</p>
</blockquote>
<pre><code class="copyable">function foo(){ }();
<span class="copy-code-btn"></span></code></pre>
<p><code>IIFE</code> 代表立即调用的函数表达式。JS解析器读取函数<code>foo(){}();</code>作为函数<code>foo(){}</code>和<code>();</code>，前者是一个函数声明，后者(一对括号)是尝试调用一个函数，但没有指定名称，因此它抛出<code>Uncaught SyntaxError: Unexpected token</code> 异常。</p>
<p>咱们可以使用<code>void</code>操作符:<code>void function foo(){ }();</code>。不幸的是，这种方法有一个问题。给定表达式的求值总是<code>undefined</code>的，所以如果IIFE 函数有返回值，则不能使用它，如下所示：</p>
<pre><code class="copyable">const foo = void
function bar() {
    console.log('前端小智')
    return 'foo';
}();

console.log(foo); // undefined
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-16">问题 17: 能否比较模块模式与构造函数/原型模式的用法？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐</p>
</blockquote>
<p>模块模式通常用于命名空间，在该模式中，使用单个实例作为存储来对相关函数和对象进行分组。这是一个不同于原型设计的用例,它们并不是相互排斥,咱们可以同时使用它们(例如，将一个构造函数放在一个模块中，并使用<code>new MyNamespace.MyModule.MyClass(arguments)</code> )。</p>
<p>构造函数和原型是实现类和实例的合理方法之一。它们与模型并不完全对应，因此通常需要选择一个特定的<code>scheme</code>或辅助方法来实现原型中的类。</p>
<h4 class="heading" data-id="heading-17">问题 18: ES6 Map 和 WeakMap 有什么区别？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐⭐</p>
</blockquote>
<p>当它们的键/值引用的对象被删除时，它们的行为都不同，以下面的代码为例:</p>
<pre><code class="copyable">var map = new Map()
var weakmap = new WeakMap()

(function() {
    var a = {
        x: 12
    };
    var b = {
        y: 12
    };

    map.set(a, 1);
    weakmap.set(b, 2);
})()
<span class="copy-code-btn"></span></code></pre>
<p>执行上面的 IIFE，就无法再引用<code>{x：12}</code>和<code>{y：12}</code>。垃圾收集器继续运行，并从 <code>WeakMa</code>中删除<code>键b</code>指针，还从内存中删除了<code>{y：12}</code>。</p>
<p>但在使用 <code>Map</code>的情况下，垃圾收集器不会从<code>Map</code>中删除指针，也不会从内存中删除<code>{x：12}</code>。</p>
<p><code>WeakMap</code> 允许垃圾收集器执行其回收任务，但<code>Map</code>不允许。对于手动编写的 <code>Map</code>，数组将保留对键对象的引用，以防止被垃圾回收。但在<code>WeakMap</code>中，对键对象的引用被“弱”保留，这意味着在没有其他对象引用的情况下，它们不会阻止垃圾回收。</p>
<h4 class="heading" data-id="heading-18">问题 19: 举一个柯里化函数的例子，并说明柯里化的好处？</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐⭐</p>
</blockquote>
<p>柯里化是一种模式，其中一个具有多个参数的函数被分解成多个函数，当被串联调用时，这些函数将一次累加一个所需的所有参数。这种技术有助于使用函数式编写的代码更容易阅读和编写。需要注意的是，要实现一个函数，它需要从一个函数开始，然后分解成一系列函数，每个函数接受一个参数。</p>
<pre><code class="copyable">function curry(fn) {
  if (fn.length === 0) {
    return fn;
  }

  function _curried(depth, args) {
    return function(newArgument) {
      if (depth - 1 === 0) {
        return fn(...args, newArgument);
      }
      return _curried(depth - 1, [...args, newArgument]);
    };
  }

  return _curried(fn.length, []);
}

function add(a, b) {
  return a + b;
}

var curriedAdd = curry(add);
var addFive = curriedAdd(5);

var result = [0, 1, 2, 3, 4, 5].map(addFive); // [5, 6, 7, 8, 9, 10]
<span class="copy-code-btn"></span></code></pre>
<h4 class="heading" data-id="heading-19">问题 20: 如何在 JS 中“深冻结”对象</h4>
<blockquote>
<p>主题: JavaScript
难度: ⭐⭐⭐⭐⭐</p>
</blockquote>
<p>如果咱们想要确保对象被深冻结，就必须创建一个递归函数来冻结对象类型的每个属性：</p>
<p><strong>没有深冻结</strong></p>
<pre><code class="copyable">let person = {
    name: "Leonardo",
    profession: {
        name: "developer"
    }
};
Object.freeze(person); 
person.profession.name = "doctor";
console.log(person); //output { name: 'Leonardo', profession: { name: 'doctor' } }
<span class="copy-code-btn"></span></code></pre>
<p><strong>深冻结</strong></p>
<pre><code class="copyable">function deepFreeze(object) {
    let propNames = Object.getOwnPropertyNames(object);
    for (let name of propNames) {
        let value = object[name];
        object[name] = value &amp;&amp; typeof value === "object" ?
            deepFreeze(value) : value;
    }
    return Object.freeze(object);
}
let person = {
    name: "Leonardo",
    profession: {
        name: "developer"
    }
};
deepFreeze(person);
person.profession.name = "doctor"; // TypeError: Cannot assign to read only property 'name' of object
