<div data-v-4cdf82d6="" data-id="5b73d90fe51d45667915a2ea" itemprop="articleBody" class="article-content"><p>首先，JavaScript是一个单线程的脚本语言。</p>
<p>所以就是说在一行代码执行的过程中，必然不会存在同时执行的另一行代码，就像使用<code>alert()</code>以后进行疯狂<code>console.log</code>，如果没有关闭弹框，控制台是不会显示出一条<code>log</code>信息的。</p>
<p>亦或者有些代码执行了大量计算，比方说在前端暴力破解密码之类的鬼操作，这就会导致后续代码一直在等待，页面处于假死状态，因为前边的代码并没有执行完。</p>

<p>所以如果全部代码都是同步执行的，这会引发很严重的问题，比方说我们要从远端获取一些数据，难道要一直循环代码去判断是否拿到了返回结果么？<em>就像去饭店点餐，肯定不能说点完了以后就去后厨催着人炒菜的，会被揍的。</em></p>
<p>于是就有了异步事件的概念，注册一个回调函数，比如说发一个网络请求，我们告诉主程序等到接收到数据后通知我，然后我们就可以去做其他的事情了。</p>
<p>然后在异步完成后，会通知到我们，但是此时可能程序正在做其他的事情，所以即使异步完成了也需要在一旁等待，等到程序空闲下来才有时间去看哪些异步已经完成了，可以去执行。</p>
<p><em>比如说打了个车，如果司机先到了，但是你手头还有点儿事情要处理，这时司机是不可能自己先开着车走的，一定要等到你处理完事情上了车才能走。</em></p>
<p></p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2018/8/15/1653c82e7835e1a9?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="650" data-height="405" src="https://user-gold-cdn.xitu.io/2018/8/15/1653c82e7835e1a9?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
<h2 class="heading" data-id="heading-0">微任务与宏任务的区别</h2>
<p>这个就像去银行办业务一样，先要取号进行排号。<br>
一般上边都会印着类似：“您的号码为XX，前边还有XX人。”之类的字样。</p>
<p>因为柜员同时职能处理一个来办理业务的客户，这时每一个来办理业务的人就可以认为是银行柜员的一个宏任务来存在的，当柜员处理完当前客户的问题以后，选择接待下一位，广播报号，也就是下一个宏任务的开始。<br>
所以多个宏任务合在一起就可以认为说有一个任务队列在这，里边是当前银行中所有排号的客户。<br>
<strong>任务队列中的都是已经完成的异步操作，而不是说注册一个异步任务就会被放在这个任务队列中，就像在银行中排号，如果叫到你的时候你不在，那么你当前的号牌就作废了，柜员会选择直接跳过进行下一个客户的业务处理，等你回来以后还需要重新取号</strong></p>
<p>而且一个宏任务在执行的过程中，是可以添加一些微任务的，就像在柜台办理业务，你前边的一位老大爷可能在存款，在存款这个业务办理完以后，柜员会问老大爷还有没有其他需要办理的业务，这时老大爷想了一下：“最近P2P爆雷有点儿多，是不是要选择稳一些的理财呢”，然后告诉柜员说，要办一些理财的业务，这时候柜员肯定不能告诉老大爷说：“您再上后边取个号去，重新排队”。<br>
所以本来快轮到你来办理业务，会因为老大爷临时添加的“<strong>理财业务</strong>”而往后推。<br>
也许老大爷在办完理财以后还想 <strong>再办一个信用卡</strong>？或者 <strong>再买点儿纪念币</strong>？<br>
无论是什么需求，只要是柜员能够帮她办理的，都会在处理你的业务之前来做这些事情，这些都可以认为是微任务。</p>
<p>这就说明：<s>你大爷永远是你大爷</s><br>
<strong>在当前的微任务没有执行完成时，是不会执行下一个宏任务的。</strong></p>
<p>所以就有了那个经常在面试题、各种博客中的代码片段：</p>
<pre><code class="hljs javascript copyable" lang="javascript">setTimeout(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-number">4</span>))

<span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-params">resolve</span> =&gt;</span> {
  resolve()
  <span class="hljs-built_in">console</span>.log(<span class="hljs-number">1</span>)
}).then(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
  <span class="hljs-built_in">console</span>.log(<span class="hljs-number">3</span>)
})

<span class="hljs-built_in">console</span>.log(<span class="hljs-number">2</span>)
<span class="copy-code-btn"></span></code></pre><p><code>setTimeout</code>就是作为宏任务来存在的，而<code>Promise.then</code>则是具有代表性的微任务，上述代码的执行顺序就是按照序号来输出的。</p>
<p><strong>所有会进入的异步都是指的事件回调中的那部分代码</strong><br>
也就是说<code>new Promise</code>在实例化的过程中所执行的代码都是同步进行的，而<code>then</code>中注册的回调才是异步执行的。<br>
在同步代码执行完成后才回去检查是否有异步任务完成，并执行对应的回调，而微任务又会在宏任务之前执行。<br>
所以就得到了上述的输出结论<code>1、2、3、4</code>。</p>
<p><em>+部分表示同步执行的代码</em></p>
<pre><code class="hljs diff copyable" lang="diff"><span class="hljs-addition">+setTimeout(_ =&gt; {</span>
<span class="hljs-deletion">-  console.log(4)</span>
<span class="hljs-addition">+})</span>

<span class="hljs-addition">+new Promise(resolve =&gt; {</span>
<span class="hljs-addition">+  resolve()</span>
<span class="hljs-addition">+  console.log(1)</span>
<span class="hljs-addition">+}).then(_ =&gt; {</span>
<span class="hljs-deletion">-  console.log(3)</span>
<span class="hljs-addition">+})</span>

<span class="hljs-addition">+console.log(2)</span>
<span class="copy-code-btn"></span></code></pre><p>本来<code>setTimeout</code>已经先设置了定时器（相当于取号），然后在当前进程中又添加了一些<code>Promise</code>的处理（临时添加业务）。</p>
<p>所以进阶的，即便我们继续在<code>Promise</code>中实例化<code>Promise</code>，其输出依然会早于<code>setTimeout</code>的宏任务：</p>
<pre><code class="hljs javascript copyable" lang="javascript">setTimeout(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-number">4</span>))

<span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-params">resolve</span> =&gt;</span> {
  resolve()
  <span class="hljs-built_in">console</span>.log(<span class="hljs-number">1</span>)
}).then(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
  <span class="hljs-built_in">console</span>.log(<span class="hljs-number">3</span>)
  <span class="hljs-built_in">Promise</span>.resolve().then(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'before timeout'</span>)
  }).then(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
    <span class="hljs-built_in">Promise</span>.resolve().then(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
      <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'also before timeout'</span>)
    })
  })
})

<span class="hljs-built_in">console</span>.log(<span class="hljs-number">2</span>)
<span class="copy-code-btn"></span></code></pre><p>当然了，实际情况下很少会有简单的这么调用<code>Promise</code>的，一般都会在里边有其他的异步操作，比如<code>fetch</code>、<code>fs.readFile</code>之类的操作。<br>
而这些其实就相当于注册了一个宏任务，而非是微任务。</p>
<p><em>P.S. 在<a target="_blank" href="https://promisesaplus.com/#notes" rel="nofollow noopener noreferrer">Promise/A+的规范</a>中，<code>Promise</code>的实现可以是微任务，也可以是宏任务，但是普遍的共识表示(至少<code>Chrome</code>是这么做的)，<code>Promise</code>应该是属于微任务阵营的</em></p>
<p>所以，明白哪些操作是宏任务、哪些是微任务就变得很关键，这是目前业界比较流行的说法：</p>
<h3 class="heading" data-id="heading-1">宏任务</h3>
<table>
<thead>
<tr>
<th style="text-align:left">#</th>
<th style="text-align:center">浏览器</th>
<th style="text-align:center">Node</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left"><code>I/O</code></td>
<td style="text-align:center">✅</td>
<td style="text-align:center">✅</td>
</tr>
<tr>
<td style="text-align:left"><code>setTimeout</code></td>
<td style="text-align:center">✅</td>
<td style="text-align:center">✅</td>
</tr>
<tr>
<td style="text-align:left"><code>setInterval</code></td>
<td style="text-align:center">✅</td>
<td style="text-align:center">✅</td>
</tr>
<tr>
<td style="text-align:left"><code>setImmediate</code></td>
<td style="text-align:center">❌</td>
<td style="text-align:center">✅</td>
</tr>
<tr>
<td style="text-align:left"><code>requestAnimationFrame</code></td>
<td style="text-align:center">✅</td>
<td style="text-align:center">❌</td>
</tr>
</tbody>
</table>
<p><em>有些地方会列出来<code>UI Rendering</code>，说这个也是宏任务，可是在读了<a target="_blank" href="https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model" rel="nofollow noopener noreferrer">HTML规范文档</a>以后，发现这很显然是和微任务平行的一个操作步骤</em><br>
<em><code>requestAnimationFrame</code>姑且也算是宏任务吧，<code>requestAnimationFrame</code>在<a target="_blank" href="https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestAnimationFrame" rel="nofollow noopener noreferrer">MDN的定义</a>为，下次页面重绘前所执行的操作，而重绘也是作为宏任务的一个步骤来存在的，且该步骤晚于微任务的执行</em></p>
<h3 class="heading" data-id="heading-2">微任务</h3>
<table>
<thead>
<tr>
<th style="text-align:left">#</th>
<th style="text-align:center">浏览器</th>
<th style="text-align:center">Node</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left"><code>process.nextTick</code></td>
<td style="text-align:center">❌</td>
<td style="text-align:center">✅</td>
</tr>
<tr>
<td style="text-align:left"><code>MutationObserver</code></td>
<td style="text-align:center">✅</td>
<td style="text-align:center">❌</td>
</tr>
<tr>
<td style="text-align:left"><code>Promise.then catch finally</code></td>
<td style="text-align:center">✅</td>
<td style="text-align:center">✅</td>
</tr>
</tbody>
</table>
<h2 class="heading" data-id="heading-3">Event-Loop是个啥</h2>
<p>上边一直在讨论 宏任务、微任务，各种任务的执行。<br>
但是回到现实，<code>JavaScript</code>是一个单进程的语言，同一时间不能处理多个任务，所以何时执行宏任务，何时执行微任务？我们需要有这样的一个判断逻辑存在。</p>
<p>每办理完一个业务，柜员就会问当前的客户，是否还有其他需要办理的业务。<em><strong>（检查还有没有微任务需要处理）</strong></em><br>
而客户明确告知说没有事情以后，柜员就去查看后边还有没有等着办理业务的人。<em><strong>（结束本次宏任务、检查还有没有宏任务需要处理）</strong></em><br>
这个检查的过程是持续进行的，每完成一个任务都会进行一次，而这样的操作就被称为<code>Event Loop</code>。<em>(这是个非常简易的描述了，实际上会复杂很多)</em></p>
<p>而且就如同上边所说的，一个柜员同一时间只能处理一件事情，即便这些事情是一个客户所提出的，所以可以认为微任务也存在一个队列，大致是这样的一个逻辑：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-keyword">const</span> macroTaskList = [
  [<span class="hljs-string">'task1'</span>],
  [<span class="hljs-string">'task2'</span>, <span class="hljs-string">'task3'</span>],
  [<span class="hljs-string">'task4'</span>],
]

<span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> macroIndex = <span class="hljs-number">0</span>; macroIndex &lt; macroTaskList.length; macroIndex++) {
  <span class="hljs-keyword">const</span> microTaskList = macroTaskList[macroIndex]
  
  <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> microIndex = <span class="hljs-number">0</span>; microIndex &lt; microTaskList.length; microIndex++) {
    <span class="hljs-keyword">const</span> microTask = microTaskList[microIndex]

    <span class="hljs-comment">// 添加一个微任务</span>
    <span class="hljs-keyword">if</span> (microIndex === <span class="hljs-number">1</span>) microTaskList.push(<span class="hljs-string">'special micro task'</span>)
    
    <span class="hljs-comment">// 执行任务</span>
    <span class="hljs-built_in">console</span>.log(microTask)
  }

  <span class="hljs-comment">// 添加一个宏任务</span>
  <span class="hljs-keyword">if</span> (macroIndex === <span class="hljs-number">2</span>) macroTaskList.push([<span class="hljs-string">'special macro task'</span>])
}

<span class="hljs-comment">// &gt; task1</span>
<span class="hljs-comment">// &gt; task2</span>
<span class="hljs-comment">// &gt; task3</span>
<span class="hljs-comment">// &gt; special micro task</span>
<span class="hljs-comment">// &gt; task4</span>
<span class="hljs-comment">// &gt; special macro task</span>
<span class="copy-code-btn"></span></code></pre><p><em>之所以使用两个<code>for</code>循环来表示，是因为在循环内部可以很方便的进行<code>push</code>之类的操作（添加一些任务），从而使迭代的次数动态的增加。</em></p>
<p>以及还要明确的是，<code>Event Loop</code>只是负责告诉你该执行那些任务，或者说哪些回调被触发了，真正的逻辑还是在进程中执行的。</p>
<h2 class="heading" data-id="heading-4">在浏览器中的表现</h2>
<p>在上边简单的说明了两种任务的差别，以及<code>Event Loop</code>的作用，那么在真实的浏览器中是什么表现呢？<br>
首先要明确的一点是，宏任务必然是在微任务之后才执行的（因为微任务实际上是宏任务的其中一个步骤）</p>
<p><code>I/O</code>这一项感觉有点儿笼统，有太多的东西都可以称之为<code>I/O</code>，点击一次<code>button</code>，上传一个文件，与程序产生交互的这些都可以称之为<code>I/O</code>。</p>
<p>假设有这样的一些<code>DOM</code>结构：</p>
<pre><code class="hljs html copyable" lang="html"><span class="hljs-tag">&lt;<span class="hljs-name">style</span>&gt;</span><span class="css">
  <span class="hljs-selector-id">#outer</span> {
    <span class="hljs-attribute">padding</span>: <span class="hljs-number">20px</span>;
    <span class="hljs-attribute">background</span>: <span class="hljs-number">#616161</span>;
  }

  <span class="hljs-selector-id">#inner</span> {
    <span class="hljs-attribute">width</span>: <span class="hljs-number">100px</span>;
    <span class="hljs-attribute">height</span>: <span class="hljs-number">100px</span>;
    <span class="hljs-attribute">background</span>: <span class="hljs-number">#757575</span>;
  }
</span><span class="hljs-tag">&lt;/<span class="hljs-name">style</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-name">div</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"outer"</span>&gt;</span>
  <span class="hljs-tag">&lt;<span class="hljs-name">div</span> <span class="hljs-attr">id</span>=<span class="hljs-string">"inner"</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-name">div</span>&gt;</span>
<span class="copy-code-btn"></span></code></pre><pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-keyword">const</span> $inner = <span class="hljs-built_in">document</span>.querySelector(<span class="hljs-string">'#inner'</span>)
<span class="hljs-keyword">const</span> $outer = <span class="hljs-built_in">document</span>.querySelector(<span class="hljs-string">'#outer'</span>)

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handler</span> (<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'click'</span>) <span class="hljs-comment">// 直接输出</span>

  <span class="hljs-built_in">Promise</span>.resolve().then(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'promise'</span>)) <span class="hljs-comment">// 注册微任务</span>

  setTimeout(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'timeout'</span>)) <span class="hljs-comment">// 注册宏任务</span>

  requestAnimationFrame(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'animationFrame'</span>)) <span class="hljs-comment">// 注册宏任务</span>

  $outer.setAttribute(<span class="hljs-string">'data-random'</span>, <span class="hljs-built_in">Math</span>.random()) <span class="hljs-comment">// DOM属性修改，触发微任务</span>
}

<span class="hljs-keyword">new</span> MutationObserver(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'observer'</span>)
}).observe($outer, {
  <span class="hljs-attr">attributes</span>: <span class="hljs-literal">true</span>
})

$inner.addEventListener(<span class="hljs-string">'click'</span>, handler)
$outer.addEventListener(<span class="hljs-string">'click'</span>, handler)
<span class="copy-code-btn"></span></code></pre><p>如果点击<code>#inner</code>，其执行顺序一定是：<code>click</code> -&gt; <code>promise</code> -&gt; <code>observer</code> -&gt; <code>click</code> -&gt; <code>promise</code> -&gt; <code>observer</code> -&gt; <code>animationFrame</code> -&gt; <code>animationFrame</code> -&gt; <code>timeout</code> -&gt; <code>timeout</code>。</p>
<p>因为一次<code>I/O</code>创建了一个宏任务，也就是说在这次任务中会去触发<code>handler</code>。<br>
按照代码中的注释，在同步的代码已经执行完以后，这时就会去查看是否有微任务可以执行，然后发现了<code>Promise</code>和<code>MutationObserver</code>两个微任务，遂执行之。<br>
因为<code>click</code>事件会冒泡，所以对应的这次<code>I/O</code>会触发两次<code>handler</code>函数(<em>一次在<code>inner</code>、一次在<code>outer</code></em>)，所以会优先执行冒泡的事件(<em>早于其他的宏任务</em>)，也就是说会重复上述的逻辑。<br>
在执行完同步代码与微任务以后，这时继续向后查找有木有宏任务。<br>
需要注意的一点是，因为我们触发了<code>setAttribute</code>，实际上修改了<code>DOM</code>的属性，这会导致页面的重绘，而这个<code>set</code>的操作是同步执行的，也就是说<code>requestAnimationFrame</code>的回调会早于<code>setTimeout</code>所执行。</p>
<h3 class="heading" data-id="heading-5">一些小惊喜</h3>
<p>使用上述的示例代码，如果将手动点击<code>DOM</code>元素的触发方式变为<code>$inner.click()</code>，那么会得到不一样的结果。<br>
在<code>Chrome</code>下的输出顺序大致是这样的：<br>
<code>click</code> -&gt; <code>click</code> -&gt; <code>promise</code> -&gt; <code>observer</code> -&gt; <code>promise</code> -&gt;  <code>animationFrame</code> -&gt; <code>animationFrame</code> -&gt; <code>timeout</code> -&gt; <code>timeout</code>。</p>
<p>与我们手动触发<code>click</code>的执行顺序不一样的原因是这样的，因为并不是用户通过点击元素实现的触发事件，而是类似<code>dispatchEvent</code>这样的方式，我个人觉得并不能算是一个有效的<code>I/O</code>，在执行了一次<code>handler</code>回调注册了微任务、注册了宏任务以后，实际上外边的<code>$inner.click()</code>并没有执行完。<br>
所以在微任务执行之前，还要继续冒泡执行下一次事件，也就是说触发了第二次的<code>handler</code>。<br>
所以输出了第二次<code>click</code>，等到这两次<code>handler</code>都执行完毕后才会去检查有没有微任务、有没有宏任务。</p>
<p>两点需要注意的：</p>
<ol>
<li><code>.click()</code>的这种触发事件的方式个人认为是类似<code>dispatchEvent</code>，可以理解为同步执行的代码</li>
</ol>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-built_in">document</span>.body.addEventListener(<span class="hljs-string">'click'</span>, _ =&gt; <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'click'</span>))

<span class="hljs-built_in">document</span>.body.click()
<span class="hljs-built_in">document</span>.body.dispatchEvent(<span class="hljs-keyword">new</span> Event(<span class="hljs-string">'click'</span>))
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'done'</span>)

<span class="hljs-comment">// &gt; click</span>
<span class="hljs-comment">// &gt; click</span>
<span class="hljs-comment">// &gt; done</span>
<span class="copy-code-btn"></span></code></pre><ol start="2">
<li><code>MutationObserver</code>的监听不会说同时触发多次，多次修改只会有一次回调被触发。</li>
</ol>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-keyword">new</span> MutationObserver(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'observer'</span>)
  <span class="hljs-comment">// 如果在这输出DOM的data-random属性，必然是最后一次的值，不解释了</span>
}).observe(<span class="hljs-built_in">document</span>.body, {
  <span class="hljs-attr">attributes</span>: <span class="hljs-literal">true</span>
})

<span class="hljs-built_in">document</span>.body.setAttribute(<span class="hljs-string">'data-random'</span>, <span class="hljs-built_in">Math</span>.random())
<span class="hljs-built_in">document</span>.body.setAttribute(<span class="hljs-string">'data-random'</span>, <span class="hljs-built_in">Math</span>.random())
<span class="hljs-built_in">document</span>.body.setAttribute(<span class="hljs-string">'data-random'</span>, <span class="hljs-built_in">Math</span>.random())

<span class="hljs-comment">// 只会输出一次 ovserver</span>
<span class="copy-code-btn"></span></code></pre><p><em>这就像去饭店点餐，服务员喊了三次，XX号的牛肉面，不代表她会给你三碗牛肉面。</em><br>
<em>上述观点参阅自<a target="_blank" href="https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/#level-1-bossfight" rel="nofollow noopener noreferrer">Tasks, microtasks, queues and schedules</a>，文中有动画版的讲解</em></p>
<h2 class="heading" data-id="heading-6">在Node中的表现</h2>
<p>Node也是单线程，但是在处理<code>Event Loop</code>上与浏览器稍微有些不同，这里是<a target="_blank" href="https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/#event-loop-explained" rel="nofollow noopener noreferrer">Node官方文档</a>的地址。</p>
<p>就单从API层面上来理解，Node新增了两个方法可以用来使用：微任务的<code>process.nextTick</code>以及宏任务的<code>setImmediate</code>。</p>
<h3 class="heading" data-id="heading-7">setImmediate与setTimeout的区别</h3>
<p>在官方文档中的定义，<code>setImmediate</code>为一次<code>Event Loop</code>执行完毕后调用。<br>
<code>setTimeout</code>则是通过计算一个延迟时间后进行执行。</p>
<p>但是同时还提到了如果在主进程中直接执行这两个操作，很难保证哪个会先触发。<br>
因为如果主进程中先注册了两个任务，然后执行的代码耗时超过<code>XXs</code>，而这时定时器已经处于可执行回调的状态了。<br>
所以会先执行定时器，而执行完定时器以后才是结束了一次<code>Event Loop</code>，这时才会执行<code>setImmediate</code>。</p>
<pre><code class="hljs javascript copyable" lang="javascript">setTimeout(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'setTimeout'</span>))
setImmediate(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'setImmediate'</span>))
<span class="copy-code-btn"></span></code></pre><p>有兴趣的可以自己试验一下，执行多次真的会得到不同的结果。</p>
<p></p><figure><img class="lazyload inited loaded" data-src="https://user-gold-cdn.xitu.io/2018/8/15/1653c82abfac7543?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" data-width="510" data-height="854" src="https://user-gold-cdn.xitu.io/2018/8/15/1653c82abfac7543?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
<p>但是如果后续添加一些代码以后，就可以保证<code>setTimeout</code>一定会在<code>setImmediate</code>之前触发了：</p>
<pre><code class="hljs javascript copyable" lang="javascript">setTimeout(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'setTimeout'</span>))
setImmediate(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'setImmediate'</span>))

<span class="hljs-keyword">let</span> countdown = <span class="hljs-number">1e9</span>

<span class="hljs-keyword">while</span>(countdown--) { } <span class="hljs-comment">// 我们确保这个循环的执行速度会超过定时器的倒计时，导致这轮循环没有结束时，setTimeout已经可以执行回调了，所以会先执行`setTimeout`再结束这一轮循环，也就是说开始执行`setImmediate`</span>
<span class="copy-code-btn"></span></code></pre><p>如果在另一个宏任务中，必然是<code>setImmediate</code>先执行：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-built_in">require</span>(<span class="hljs-string">'fs'</span>).readFile(__dirname, _ =&gt; {
  setTimeout(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'timeout'</span>))
  setImmediate(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'immediate'</span>))
})

<span class="hljs-comment">// 如果使用一个设置了延迟的setTimeout也可以实现相同的效果</span>
<span class="copy-code-btn"></span></code></pre><h3 class="heading" data-id="heading-8">process.nextTick</h3>
<p>就像上边说的，这个可以认为是一个类似于<code>Promise</code>和<code>MutationObserver</code>的微任务实现，在代码执行的过程中可以随时插入<code>nextTick</code>，并且会保证在下一个宏任务开始之前所执行。</p>
<p>在使用方面的一个最常见的例子就是一些事件绑定类的操作：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Lib</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">require</span>('<span class="hljs-title">events</span>').<span class="hljs-title">EventEmitter</span> </span>{
  <span class="hljs-keyword">constructor</span> () {
    <span class="hljs-keyword">super</span>()

    <span class="hljs-keyword">this</span>.emit(<span class="hljs-string">'init'</span>)
  }
}

<span class="hljs-keyword">const</span> lib = <span class="hljs-keyword">new</span> Lib()

lib.on(<span class="hljs-string">'init'</span>, _ =&gt; {
  <span class="hljs-comment">// 这里将永远不会执行</span>
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'init!'</span>)
})
<span class="copy-code-btn"></span></code></pre><p>因为上述的代码在实例化<code>Lib</code>对象时是同步执行的，在实例化完成以后就立马发送了<code>init</code>事件。<br>
而这时在外层的主程序还没有开始执行到<code>lib.on('init')</code>监听事件的这一步。<br>
所以会导致发送事件时没有回调，回调注册后事件不会再次发送。</p>
<p>我们可以很轻松的使用<code>process.nextTick</code>来解决这个问题：</p>
<pre><code class="hljs javascript copyable" lang="javascript"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Lib</span> <span class="hljs-keyword">extends</span> <span class="hljs-title">require</span>('<span class="hljs-title">events</span>').<span class="hljs-title">EventEmitter</span> </span>{
  <span class="hljs-keyword">constructor</span> () {
    <span class="hljs-keyword">super</span>()

    process.nextTick(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> {
      <span class="hljs-keyword">this</span>.emit(<span class="hljs-string">'init'</span>)
    })

    <span class="hljs-comment">// 同理使用其他的微任务</span>
    <span class="hljs-comment">// 比如Promise.resolve().then(_ =&gt; this.emit('init'))</span>
    <span class="hljs-comment">// 也可以实现相同的效果</span>
  }
}
<span class="copy-code-btn"></span></code></pre><p>这样会在主进程的代码执行完毕后，程序空闲时触发<code>Event Loop</code>流程查找有没有微任务，然后再发送<code>init</code>事件。</p>
<p><em>关于有些文章中提到的，循环调用<code>process.nextTick</code>会导致报警，后续的代码永远不会被执行，这是对的，参见上边使用的双重循环实现的<code>loop</code>即可，相当于在每次<code>for</code>循环执行中都对数组进行了<code>push</code>操作，这样循环永远也不会结束</em></p>
<h2 class="heading" data-id="heading-9">多提一嘴async/await函数</h2>
<p>因为，<code>async/await</code>本质上还是基于<code>Promise</code>的一些封装，而<code>Promise</code>是属于微任务的一种。所以在使用<code>await</code>关键字与<code>Promise.then</code>效果类似：</p>
<pre><code class="hljs javascript copyable" lang="javascript">setTimeout(<span class="hljs-function"><span class="hljs-params">_</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(<span class="hljs-number">4</span>))

<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">main</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-number">1</span>)
  <span class="hljs-keyword">await</span> <span class="hljs-built_in">Promise</span>.resolve()
  <span class="hljs-built_in">console</span>.log(<span class="hljs-number">3</span>)
}


<span class="hljs-built_in">console</span>.log(<span class="hljs-number">2</span>)
<span class="copy-code-btn"></span></code></pre><p><strong>async函数在await之前的代码都是同步执行的，可以理解为await之前的代码属于<code>new Promise</code>时传入的代码，await之后的所有代码都是在<code>Promise.then</code>中的回调</strong></p>
<h2 class="heading" data-id="heading-10">小节</h2>
<p>JavaScript的代码运行机制在网上有好多文章都写，本人道行太浅，只能简单的说一下自己对其的理解。<br>
并没有去生抠文档，一步一步的列出来，像什么查看当前栈、执行选中的任务队列，各种balabala。<br>
感觉对实际写代码没有太大帮助，不如简单的入个门，扫个盲，大致了解一下这是个什么东西就好了。</p>
