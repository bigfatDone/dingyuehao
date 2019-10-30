# 面试官：你能实现多少种水平垂直居中的布局（定宽高和不定宽高）
>我们在日常的开发中，经常会遇到这样一个问题，就是如何实现居中水平垂直居中对齐。并且在面试中也会出现这样的问题，但是我们往往回答的不是很全部，而导致没有得到面试加分。接下来我们通过不同的方式来实现，让我们成功破解这道面试。

## 1、定宽高
### 一、绝对定位和负magin值
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
    position: absolute;
    width: 100px;
    height: 100px;
    background: yellow;
    left: 50%;
    top: 50%;
    margin-left: -50px;
    margin-top: -50px; 
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e1329b5f303d54?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 二、绝对定位 + transform
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
    position: absolute;
    width: 100px;
    height: 100px;
    background: yellow;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%); 
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e13316fc4b2195?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 三、绝对定位 + left/right/bottom/top + margin
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
    position: absolute;
    display: inline;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0px;
    background: yellow;
    margin: auto;
    height: 100px;
    width: 100px;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e132c5f1e528b3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 四、flex布局
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: flex;
    justify-content: center;
    align-items: center;
}
.children-box {
    background: yellow;
    height: 100px;
    width: 100px;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e132f6069d5925?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 五、grid布局
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: grid;
}
.children-box {
    width: 100px;
    height: 100px;
    background: yellow;
    margin: auto;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15efd5798514e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 六、table-cell + vertical-align + inline-block/margin: auto
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box"></div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: table-cell;
    text-align: center;
    vertical-align: middle;
}
.children-box {
    width: 100px;
    height: 100px;
    background: yellow;
    display: inline-block;// 可以换成margin: auto;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15f27ba1b946c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
## 2、不定宽高
### 一、绝对定位 + transform
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    position: relative;
}
.children-box {
   position: absolute;
   background: yellow;
   left: 50%;
   top: 50%;
   transform: translate(-50%, -50%);
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15f695baa85de?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 二、table-cell
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: table-cell;
    text-align: center;
    vertical-align: middle;
}
.children-box {
   background: yellow;
   display: inline-block;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15fa1472b762e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 三、flex布局
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: flex;
    justify-content: center;
    align-items: center;
}
.children-box {
    background: yellow;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15fb58a8f283e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 四、flex变异布局
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: flex;
}
.children-box {
    background: yellow;
    margin: auto;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15fc6d1a68d63?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 五、grid + flex布局
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: grid;
}
.children-box {
    background: yellow;
    align-self: center;
    justify-self: center;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15fe57fc3aa56?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 六、gird + margin布局
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">11111111</div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    display: grid;
}
.children-box {
    background: yellow;
    margin: auto;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e15ff5b608854a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 七、writing-mode属性布局
```
<template>
    <div id="app">
        <div class="box">
            <div class="children-box">
                <p>11111</p>
            </div>
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    writing-mode: vertical-lr;
    text-align: center;
}

.box>.children-box {
    writing-mode: horizontal-tb;
    display: inline-block;
    text-align: center;
    width: 100%;
}

.box>.children-box>p {
    display: inline-block;
    margin: auto;
    text-align: left;
    background: yellow;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e1604266e841fe?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
>writing-mode 属性定义了文本在水平或垂直方向上如何排布。 兼容性上还有些小瑕疵，但大部分浏览器已经支持。


## 3、番外(图片定高|不定高水平垂直居中)
### 一、table-cell
```
<template>
    <div id="app">
        <div class="box">
            <img src="https://ss1.baidu.com/70cFfyinKgQFm2e88IuM_a/forum/pic/item/242dd42a2834349b406751a3ceea15ce36d3beb6.jpg">
        </div>
        </div>
</template>
<style type="text/css">
.box {
     height: 200px;
    width: 200px;
    display: table-cell;
    text-align: center;
    border: 1px solid #ccc;
    vertical-align: middle;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e161e067566752?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 二、 ::after
```
<template>
    <div id="app">
        <div class="box">
            <img src="https://ss1.baidu.com/70cFfyinKgQFm2e88IuM_a/forum/pic/item/242dd42a2834349b406751a3ceea15ce36d3beb6.jpg">
        </div>
    </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid red;
    text-align: center;
}

.box::after {
    content: '';
    display: inline-block;
    vertical-align: middle;
    height: 100%;
}
img {
    vertical-align: middle;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e161a999569181?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 三、 ::before
```
<template>
    <div id="app">
        <div class="box">
            <img src="https://ss1.baidu.com/70cFfyinKgQFm2e88IuM_a/forum/pic/item/242dd42a2834349b406751a3ceea15ce36d3beb6.jpg">
        </div>
        </div>
</template>
<style type="text/css">
.box {
    width: 200px;
    height: 200px;
    border: 1px solid #ccc;

    text-align: center;
    font-size: 0;
}

.box::before {
    display: inline-block;
    vertical-align: middle;
    content: '';
    height: 100%;
}

img {
    vertical-align: middle;
}
</style>
```
![](https://user-gold-cdn.xitu.io/2019/10/29/16e161d1fcad7abc?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
### 四、总结
>这里总结了很多种垂直水平居中的方法，但是肯定不是最完全的，还有很多其他中方式。但是总体的思路可以总结为以下几点。

#### 一、内联元素居中布局

水平居中

行内元素可设置：text-align: center;

flex布局设置父元素：display: flex; justify-content: center;

垂直居中

单行文本父元素确认高度：height === line-height

多行文本父元素确认高度：disaply: table-cell; vertical-align: middle;

#### 二、块级元素居中布局

水平居中

定宽: margin: 0 auto;

不定宽： 参考上诉例子中不定宽高例子。

垂直居中

position: absolute设置left、top、margin-left、margin-to(定高)；

position: fixed设置margin: auto(定高)；

display: table-cell；

transform: translate(x, y)；

flex(不定高，不定宽)；

grid(不定高，不定宽)，兼容性相对比较差；
>作者：<a href="https://juejin.im/post/5db706d5f265da4d31073959">蜗牛的北极星之旅（掘金）</a>