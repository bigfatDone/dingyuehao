<div data-v-0526462d="" data-id="5de05ff4e51d4532da11c15b" itemprop="articleBody" class="article-content"><p>在我们的日常前端开发中，使用最频繁的莫过于使用<code>console.log</code>在浏览器的控制台中打印出我们需要调试的信息，但是大部分人可能跟之前的我一样，没有意识到其实<code>console</code>除了<code>log</code>方法以外，还有很多实用的方法，这些方法可以使我们的调试过程更加容易，也表达得更加直观，更加丰富多彩，下面我们就来看看有哪些实用的方法吧！</p>
<h3 class="heading" data-id="heading-0">1、console.log()</h3>
<p>我们经常会使用<code>console.log</code>来打印出某个变量的值或者某个实体对象，也可以传入多个变量参数，它会按照传入顺序进行打印：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-number">1.</span> 传入一个变量
<span class="hljs-keyword">const</span> a = <span class="hljs-number">1</span>;
<span class="hljs-built_in">console</span>.log(a); <span class="hljs-comment">// -&gt; 1</span>

<span class="hljs-number">2.</span> 传入一个对象
<span class="hljs-keyword">const</span> foo = {<span class="hljs-attr">a</span>: <span class="hljs-number">1</span>};
<span class="hljs-built_in">console</span>.log(foo); <span class="hljs-comment">// -&gt; {a: 1}</span>

<span class="hljs-number">3.</span> 传入多个变量
<span class="hljs-built_in">console</span>.log(a, foo); <span class="hljs-comment">// -&gt; 1 {a: 1} </span>
<span class="copy-code-btn">复制代码</span></code></pre><p>除此之外，它还支持<strong>格式化打印</strong>的功能，传入特定的<strong>占位符</strong>来对参数进行格式化处理，常见的占位符有以下几种：</p>
<ol>
<li><code>%s</code>：字符串占位符</li>
<li><code>%d</code>：整数占位符</li>
<li><code>%f</code>：浮点数占位符</li>
<li><code>%o</code>：对象占位符(注意是字母<code>o</code>，不是数字<code>0</code>)</li>
<li><code>%c</code>: CSS样式占位符</li>
</ol>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-keyword">const</span> string = <span class="hljs-string">'Glory of Kings'</span>;
<span class="hljs-keyword">const</span> number = <span class="hljs-number">100</span>;
<span class="hljs-keyword">const</span> float = <span class="hljs-number">9.5</span>;
<span class="hljs-keyword">const</span> obj = {<span class="hljs-attr">name</span>: <span class="hljs-string">'daji'</span>};

<span class="hljs-number">1</span>、%s 字符串占位符
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'I do like %s'</span>, string); <span class="hljs-comment">// -&gt; I do like Golry of Kings.</span>

<span class="hljs-number">2</span>、%d 整数占位符
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'I won %d times'</span>, number); <span class="hljs-comment">// -&gt; I won 100 times.</span>

<span class="hljs-number">3</span>、%f 浮点数占位符
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'My highest score is %f'</span>, float); <span class="hljs-comment">// -&gt; My highest score is 9.5</span>

<span class="hljs-number">4</span>、%o 对象占位符
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'My favorite hero is %o'</span>, obj); <span class="hljs-comment">// -&gt; My favorite hero is {name: 'daji'}.</span>

<span class="hljs-number">5</span>、%c CSS样式占位符
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'I do like %c%s'</span>, <span class="hljs-string">'padding: 2px 4px;background: orange;color: white;border-radius: 2px;'</span>, string);
<span class="copy-code-btn">复制代码</span></code></pre><p>其中CSS样式占位符效果如下：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea881b595088b6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="919" data-height="56" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea881b595088b6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
<h3 class="heading" data-id="heading-1">2、console.warn()</h3>
<p>你可以完全使用<code>console.warn</code>来代替<code>console.log</code>方法，但前提是该条打印信息是属于警告级别而不是普通信息级别，因此浏览器遇到一条警告级别的信息会区别对待，最明显的是它的左侧会有一个警告图标，并且背景色和文字颜色也会不一样。
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea88c5e12cf8c0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="478" data-height="186" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea88c5e12cf8c0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
相比于普通信息，警告信息会出现在上图左侧的<code>warning</code>面板中，而不是<code>info</code>面板中，这样也有助于我们在一堆打印信息中快速筛选出警告信息，方便查看。<p></p>
<h3 class="heading" data-id="heading-2">3、console.dir()</h3>
<p>在大多数情况下，<code>console.dir</code>方法的作用和<code>console.log</code>作用相似，但是有一点细微的差别。
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea89629fb7b425?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="272" data-height="207" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea89629fb7b425?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
在上图中，我们可以看到，<code>console.log</code>方法会将打印结果的详细信息显示完整，但是<code>console.dir</code>方法只会打印出对象，不会展开详细信息，当然点击之后看到的信息和前者一样。
唯一差异比较大的地方是当我们打印HTML文档中的节点时，会有完全不一样的表现形式。例如我们使用<code>console.log</code>来打印<code>body</code>标签：
<figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea89df4709d106?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="602" data-height="198" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea89df4709d106?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
我们会方便地看到DOM结构，并且鼠标移上去能够帮我们自动定位到对应的DOM节点。但是在某些情况下，其实这并不是你想要看到的效果，或许你想看到的是该DOM节点下的所有属性信息，那么你可以尝试使用<code>console.dir</code>方法来试试：
<figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8a3cfb043504?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="700" data-height="448" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8a3cfb043504?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
<h3 class="heading" data-id="heading-3">4、console.table()</h3>
<p>在我们的项目开发中经常会遇到对象数组形式的列表数据，在调试过程中我们可能会使用<code>console.log</code>方法打印出这些数据来进行查看，但比起前者，还可以使用一种比较可视化的方式来进行打印。例如，这里准备一些列表数据：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-keyword">const</span> response = [
  {
      <span class="hljs-attr">id</span>: <span class="hljs-number">1</span>,
      <span class="hljs-attr">name</span>: <span class="hljs-string">'Marry'</span>,
      <span class="hljs-attr">age</span>: <span class="hljs-number">18</span>,
      <span class="hljs-attr">sex</span>: <span class="hljs-number">0</span>
  },
  {
     <span class="hljs-attr">id</span>: <span class="hljs-number">2</span>,
     <span class="hljs-attr">name</span>: <span class="hljs-string">'John'</span>,
     <span class="hljs-attr">age</span>: <span class="hljs-number">20</span>,
     <span class="hljs-attr">sex</span>: <span class="hljs-number">1</span>
  }
];
<span class="copy-code-btn">复制代码</span></code></pre><p>然后我们使用<code>console.log</code>来进行打印：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8af8d685935e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="340" data-height="340" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8af8d685935e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
可以看出，我们打印出的结果并不够直接，没有给人一种一目了然的效果，接着换着使用<code>console.table</code>来打印：
<figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8b2dd34942b1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="1280" data-height="92" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8b2dd34942b1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
可以看到，我们的列表数据被清晰完整地展现在了表格当中，同时<code>console.table</code>提供第二个可选参数用于筛选表格需要显示的列，默认为全部列都显示。
<figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8b9d200c2772?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="1273" data-height="152" src="https://user-gold-cdn.xitu.io/2019/11/27/16ea8b9d200c2772?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
上图我们通过添加第二个参数，数组中为需要在表格中显示的字段名，这样就很方便地在结果数据中过滤掉我们不需要关心的信息。<p></p>
<h3 class="heading" data-id="heading-4">5、console.assert()</h3>
<p><code>assert</code>即断言，该方法接收多个参数，其中第一个参数为输入的表达式，只有在该表达式的值为<code>false</code>时，才会将剩余的参数输出到控制台中。
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ead604510212d1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="550" data-height="88" src="https://user-gold-cdn.xitu.io/2019/11/27/16ead604510212d1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
上图中的第二行因为<code>arr.length &gt; 5</code>值为<code>false</code>，因此打印出后面的信息。如果在某些场景下你需要评估当前的数据是否满足某个条件，那么不妨使用<code>console.assert()</code>方法来在控制台中查看断言信息。<p></p>
<h3 class="heading" data-id="heading-5">6、console.trace()</h3>
<p>该方法用于在控制台中显示当前代码在堆栈中的调用路径，通过这个调用路径我们可以很容易地在发生错误时找到原始错误点，示例如下：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">foo</span>(<span class="hljs-params">data</span>) </span>{
  <span class="hljs-keyword">if</span> (data === <span class="hljs-literal">null</span>) {
    <span class="hljs-built_in">console</span>.trace();
    <span class="hljs-keyword">return</span> [];
  }
  <span class="hljs-keyword">return</span> [data.a, data.b];
}

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">bar1</span>(<span class="hljs-params">data</span>) </span>{
  <span class="hljs-keyword">return</span> foo(data);
}

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">bar2</span>(<span class="hljs-params">data</span>) </span>{
  <span class="hljs-keyword">return</span> foo(data);
}

bar1({<span class="hljs-attr">a</span>: <span class="hljs-number">1</span>, <span class="hljs-attr">b</span>: <span class="hljs-number">2</span>}); <span class="hljs-comment">// -&gt; [1, 2]</span>
bar2(<span class="hljs-literal">null</span>); <span class="hljs-comment">// -&gt; []</span>
<span class="copy-code-btn">复制代码</span></code></pre><p>在上面代码中，我们分别在<code>bar1</code>和<code>bar2</code>函数中调用<code>foo</code>函数并传入不同的参数，很显然<code>bar2</code>函数在执行时会进入<code>if</code>语句并执行<code>console.trace()</code>方法，以下是控制台中打印结果：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/27/16ead80a57f49d7f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="300" data-height="100" src="https://user-gold-cdn.xitu.io/2019/11/27/16ead80a57f49d7f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
可以看到自下而上的一条调用路径，并可以快速判定是在<code>bar2</code>函数中传入了不合适的参数<code>null</code>而导致出错，方便我们跟踪发生错误的原始位置。<p></p>
<h3 class="heading" data-id="heading-6">7、console.count()</h3>
<p>该方法相当于一个计数器，用于记录调用次数，并将记录结果打印到控制台中。其接收一个可选参数<code>console.count(label)</code>，<code>label</code>表示指定标签，该标签会在调用次数之前显示，示例如下：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">1</span>;i &lt;= <span class="hljs-number">5</span>;i++) {
    <span class="hljs-keyword">if</span> (!(i % <span class="hljs-number">2</span>)) {
        <span class="hljs-built_in">console</span>.count(<span class="hljs-string">'even'</span>);
    } <span class="hljs-keyword">else</span> {
        <span class="hljs-built_in">console</span>.count(<span class="hljs-string">'odd'</span>);
    }
}
<span class="copy-code-btn">复制代码</span></code></pre><p>代码中如果<code>i</code>是偶数，则会对<code>even</code>计数器进行计数，否则对<code>odd</code>计数器进行计数，执行后我们会在控制台中看到如下列表：</p>
<pre><code class="hljs javascript copyable" lang="javascript">odd: <span class="hljs-number">1</span>
even: <span class="hljs-number">1</span>
odd: <span class="hljs-number">2</span>
even: <span class="hljs-number">2</span>
odd: <span class="hljs-number">3</span>
<span class="copy-code-btn">复制代码</span></code></pre><h3 class="heading" data-id="heading-7">8、console.time() &amp; console.timeEnd()</h3>
<p>这两个方法一般配合使用，是JavaScript中用于跟踪程序执行时间的专用函数，<code>console.time</code>方法是作为计算的起始时间，<code>console.timeEnd</code>是作为计算的结束时间，并将执行时长显示在控制台。如果一个页面有多个地方需要使用到计算器，则可以为方法传入一个可选参数<code>label</code>来指定标签，该标签会在执行时间之前显示。在以往我们计算程序的执行时间时，我们一般会采用如下方式：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-keyword">const</span> startTime = performance.now();
<span class="hljs-keyword">let</span> sum = <span class="hljs-number">0</span>;
<span class="hljs-keyword">for</span>(<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>;i &lt; <span class="hljs-number">100000</span>;i++) {
    sum += i;
}
<span class="hljs-keyword">const</span> diffTime = performance.now() - startTime;
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">`Execution time: <span class="hljs-subst">${ diffTime }</span>`</span>);
<span class="copy-code-btn">复制代码</span></code></pre><p>这是一种比较传统的做法，我们还可以使用<code>console.time</code>来实现：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-built_in">console</span>.time(<span class="hljs-string">'sum'</span>);
<span class="hljs-keyword">let</span> sum = <span class="hljs-number">0</span>;
<span class="hljs-keyword">for</span>(<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>;i &lt; <span class="hljs-number">100000</span>;i++) {
    sum += i;
}
<span class="hljs-built_in">console</span>.timeEnd(<span class="hljs-string">'sum'</span>);
<span class="copy-code-btn">复制代码</span></code></pre><p>控制台效果如下：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/28/16eada4e93e9cb52?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="300" data-height="142" src="https://user-gold-cdn.xitu.io/2019/11/28/16eada4e93e9cb52?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
相比于第一种实现方式，我们没有设置任何临时变量并且没有做任何计算。<p></p>
<h3 class="heading" data-id="heading-8">9、console.group() &amp; console.groupEnd()</h3>
<p>顾名思义，对数据信息进行分组，其中<code>console.group()</code>方法用于设置分组信息的起始位置，该位置之后的所有信息将写入分组，<code>console.groupEnd()</code>方法用于结束当前的分组，示例如下：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">MyClass</span> </span>{
  <span class="hljs-keyword">constructor</span>() {
    <span class="hljs-built_in">console</span>.group(<span class="hljs-string">'Constructor'</span>);
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'Constructor executed'</span>);
    <span class="hljs-keyword">this</span>.init();
    <span class="hljs-built_in">console</span>.groupEnd();
  }

  init() {
    <span class="hljs-built_in">console</span>.group(<span class="hljs-string">'init'</span>);
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'init executed'</span>);
    <span class="hljs-built_in">console</span>.groupEnd();
  }
}
<span class="hljs-keyword">const</span> myClass = <span class="hljs-keyword">new</span> MyClass();
<span class="copy-code-btn">复制代码</span></code></pre><p>控制台效果如下：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/28/16eadb68788d1ac3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="240" data-height="106" src="https://user-gold-cdn.xitu.io/2019/11/28/16eadb68788d1ac3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
该方法的作用主要是让我们在控制台打印的日志更加清晰可读。<p></p>
<h3 class="heading" data-id="heading-9">10、浏览器转为编辑器</h3>
<p>在大部分情况下，我们在浏览器中调试DOM结构或者编辑一些文本时，会在Chrome Developer Tools的Elements选项中对DOM节点进行编辑，但是一旦节点过多，会很容易增加调试过程的困难，这里我们可以使用一种方式来将浏览器直接转换为编辑器模式：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-built_in">document</span>.body.contentEditable = <span class="hljs-literal">true</span>;
<span class="copy-code-btn">复制代码</span></code></pre><p>在控制台中输入以上代码后，可以将浏览器中的所有内容变为可编辑状态，效果图如下：</p>
<p></p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/29/16eb33c999c1bfd2?imageslim" data-width="854" data-height="588" src="https://user-gold-cdn.xitu.io/2019/11/29/16eb33c999c1bfd2?imageslim"><figcaption></figcaption></figure><p></p>
<h3 class="heading" data-id="heading-10">11、Chrome Command Line API</h3>
<p>Google的Chrome Command Line API包含了一个用于执行以下常见任务的便捷函数集合：选择和检查DOM元素，以可读格式显示数据，停止和启动分析器，以及监控DOM事件。</p>
<blockquote>
<p>注意：此API只能通过浏览器控制台获取，无法通过网页脚本来进行访问。</p>
</blockquote>
<h4 class="heading" data-id="heading-11">11.1 选择DOM元素</h4>
<p>当我们使用jQuery的时候，我们可以通过各种选择器例如<code>$('#id')</code>和<code>$('.class')</code>来选择匹配的DOM元素，但是如果我们没有引入jQuery时，我们仍然可以在Chrome的控制台中进行同样的操作。Chrome Command Line API提供了以下几种选择DOM元素的方式：</p>
<ul>
<li><code>$(selector)</code>：返回匹配指定CSS选择器的DOM元素的第一个引用，相当于<code>document.querySelector()</code>函数。</li>
<li><code>$$(selector)</code>：返回匹配指定CSS选择器的DOM元素数组，相当于<code>document.querySelectorAll()</code>函数。</li>
<li><code>$x(path)</code>：返回一个与给定XPath表达式匹配的DOM元素数组。
<figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/28/16eade035c9d0f6e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="800" data-height="230" src="https://user-gold-cdn.xitu.io/2019/11/28/16eade035c9d0f6e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure></li>
</ul>
<blockquote>
<p>$x('//p[a]')表示返回包含<code>&lt;a&gt;</code>元素的所有<code>&lt;p&gt;</code>元素。</p>
</blockquote>
<h4 class="heading" data-id="heading-12">11.2 检索最后一个结果的值</h4>
<p>在控制台中我们经常会进行一些计算，某些情况下你可能需要跟踪你之前的计算结果来用于后面的计算，使用<code>$_</code>标记可用于返回最近评估的表达式的值，示例如下：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-number">1</span> + <span class="hljs-number">2</span> + <span class="hljs-number">3</span> + <span class="hljs-number">4</span> <span class="hljs-comment">// -&gt; 10</span>

$_ <span class="hljs-comment">// -&gt; 10</span>

$_ * $_ <span class="hljs-comment">// -&gt; 100</span>

<span class="hljs-built_in">Math</span>.sqrt($_) <span class="hljs-comment">// -&gt; 10</span>

$_ <span class="hljs-comment">// -&gt; 10</span>
<span class="copy-code-btn">复制代码</span></code></pre><h4 class="heading" data-id="heading-13">11.3 查找与指定DOM元素关联的事件</h4>
<p>当我们需要查找DOM中与某个元素关联的所有事件时，控制台提供了<code>getEventListeners</code>方法来帮助我们找到这些关联的事件。<br>
<code>getEventListeners($('selector'))</code>返回在指定DOM元素上注册的事件监听器。返回值是一个对象，对象的<code>key</code>为对应的事件类型(例如<code>click</code>，<code>focus</code>)，对象的<code>value</code>为一个数组，其包含了对应事件类型下的所有事件监听器。例如，下面列出了在<code>document</code>上注册的所有事件监听器：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/28/16eadfdd064b207e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="900" data-height="514" src="https://user-gold-cdn.xitu.io/2019/11/28/16eadfdd064b207e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
如果我们需要找到某个特定的事件监听器，可以通过如下方式进行访问：<p></p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-comment">// eventName表示对应的事件类型</span>
<span class="hljs-comment">// index表示该事件类型下的事件监听器数组的索引</span>
getEventListeners($(<span class="hljs-string">'selector'</span>)).eventName[index].listener

<span class="hljs-comment">// 例如获取document下click事件监听器数组的第一项</span>
getEventListeners(<span class="hljs-built_in">document</span>).click[<span class="hljs-number">0</span>].listener
<span class="copy-code-btn">复制代码</span></code></pre><h4 class="heading" data-id="heading-14">11.4 监控事件</h4>
<p>如果你希望在执行绑定到DOM中特定元素的事件时监视它们，控制台提供了<code>monitorEvents</code>方法来帮助你使用不同的命令来监控其中的一些或者所有事件：</p>
<ul>
<li><code>monitorEvents($('selector'))</code>：将监视与选择器匹配的元素关联的所有事件，当这些事件被触发时会将它们打印到控制台。例如<code>monitorEvents($('#content'))</code>将监视<code>id</code>为<code>content</code>的元素关联的所有事件。</li>
<li><code>monitorEvents($('selector'), 'eventName')</code>：将监视选择器匹配的元素的某个特定的事件。 例如，<code>monitorEvents($('#content'), 'click')</code>将监视<code>id</code>为<code>content</code>的元素关联的<code>click</code>事件。</li>
<li><code>monitorEvents($('selector'), [eventName1, eventName2, ...])</code>：将监视选择器匹配的元素的某些特定的事件。与上述不同的是，第二项可以传入一个字符串数组，包含所有需要监听的事件类型名称，以此达到自定义监听的目的。例如<code>monitorEvents($('#content'), ['click', 'focus'])</code>将监视<code>id</code>为<code>content</code>的元素关联的<code>click</code>和<code>focus</code>事件。</li>
<li><code>unmonitorEvents($('selector'))</code>：将停止监视选择器匹配的元素关联的所有事件。例如<code>unmonitorEvents($('#content'))</code>将停止监视<code>id</code>为<code>content</code>的元素关联的所有事件。</li>
</ul>
<p>效果图如下：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/29/16eb305a50a68c88?imageslim" data-width="860" data-height="400" src="https://user-gold-cdn.xitu.io/2019/11/29/16eb305a50a68c88?imageslim"><figcaption></figcaption></figure><p></p>
<h4 class="heading" data-id="heading-15">11.5 检查DOM元素</h4>
<p>控制台提供了<code>inspect()</code>方法让我们可以直接从控制台中检查一个DOM元素。</p>
<ul>
<li><code>inspect($('selector'))</code>：将检查与选择器匹配的元素，并且会自动跳转到Chrome Developer Tools的Elements选项卡中。例如<code>inspect($('#content'))</code>将检查<code>id</code>为<code>content</code>的元素。</li>
</ul>
<p>效果图如下：
</p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/29/16eb31a55f112adb?imageslim" data-width="620" data-height="240" src="https://user-gold-cdn.xitu.io/2019/11/29/16eb31a55f112adb?imageslim"><figcaption></figcaption></figure><p></p>
<h3 class="heading" data-id="heading-16">交流</h3>
<p>这篇主要是分享了几个笔者觉得不错的console调试技巧，希望在你的前端代码调试过程中能对你有所帮助，觉得文章不错的话，欢迎关注笔者的公众号，每周都会原创和整理一些前端技术干货，希望和大家一起互相交流学习，共同进步。</p>
<p><strong>文章已同步更新至<a target="_blank" href="https://github.com/qq591468061/xwfe" rel="nofollow noopener noreferrer">Github博客</a>，若觉文章尚可，欢迎前往star！</strong></p>
<p><strong>你的一个点赞，值得让我付出更多的努力！</strong></p>
<p><strong>逆境中成长，只有不断地学习，才能成为更好的自己，与君共勉！</strong></p>
<p></p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2019/11/2/16e2b919cdf81336?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="900" data-height="500" src="https://user-gold-cdn.xitu.io/2019/11/2/16e2b919cdf81336?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
</div>