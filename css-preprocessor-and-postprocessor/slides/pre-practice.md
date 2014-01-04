### CSS *Preprocessor* 实践

从 **CSS 样式库** 的设计说起

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>整体以移动端样式库 **Archer** 为例</small>

---

### CSS 样式库的功能

+ 浏览器兼容
+ 语法糖
    + 简写
    + 常见组合封装
+ 单位转换
+ 响应式支持
+ UI 样式库

---

### 浏览器兼容

在移动端，通过 **Autoprefixer** 解决大多数问题

<i class="fa fa-ellipsis-h state-weakest"></i>

在PC端，不仅仅是加 **Prefix**，情况更复杂，以 [`est`](ecomfe.github.io/est/) 为例

<div class="multi-column-container with-gap">

<div class="multi-column-item">
<h4>opacity</h4>
<pre>
```
.opacity(@opacity: 100) {
    opacity: @opacity / 100;
    filter: ~"alpha(opacity=@{opacity})";
}
```
</pre>
</div>

<div class="multi-column-item">
<h4>inline-block</h4>
<pre>
```
.inline-block() {
    display: inline-block;
}
.ie-inline-block() {
    *display: inline;
    *zoom: 1;
}
.inline-block() when (@support-old-ie) {
    .ie-inline-block;
}
```
</pre>
</div>

</div>

---

### 语法糖

提高书写效率，增强代码 **可读性**，延缓 **代码腐化** 速度

---

### 语法糖 - 简写

<div class="multi-column-container with-gap">

<div class="multi-column-item grid-2">
<h4>Stylus</h4>
<pre>
```
.toolbar
    size: 320px 40px
    fixed: 30px 0 _
    padding: _ 20px
    transition: all .5s ease-in-cubic
```
</pre>
</div>

<div class="multi-column-item grid-3">
<h4>CSS</h4>
<pre>
```
.toolbar {
    width: 320px;
    height: 40px;
    position: fixed;
    top: 30px;
    left: 0;
    right: 0;
    padding-left: 20px;
    padding-right: 20px;
    transition: all .5s cubic-bezier(0.550, 0.055, 0.675, 0.190);
}
```
</pre>
</div>

</div>

<small>**顺时针规则** 来自 [CSS Shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)，**下划线占位符** 来自 [clockhand-stylus](https://github.com/jasonkuhrt/clockhand-stylus)，**缓动函数** 来自 [easings](http://easings.net/zh-cn)</small>

---

### 语法糖 - 常见组合封装

<div class="multi-column-container with-gap">

<div class="multi-column-item">
<h4>Stylus</h4>
<pre>
```
.logo
    size: 120px 36px
    ir: './img/sprite.png' 0 -40px
```
</pre>
</div>

<div class="multi-column-item">
<h4>CSS</h4>
<pre>
```
.logo {
    width: 120px;
    height: 36px;
    text-indent: 101%;
    white-space: nowrap;
    overflow: hidden;
    background-image: url(img/sprite.png);
    background-position: 120px 36px;
    background-repeat: no-repeat;
    background-size: 300px 400px;
}
```
</pre>
</div>

</div>

<small>**Stylus** 可以 **扩展** 出具备后端能力的 *Function*、*Mixin*，如 [`nib`](http://visionmedia.github.io/nib/) 中 **渐变** 可为 **古董浏览器** 生成图片等</small>

---

### 单位转换

<div class="multi-column-container with-gap">

<div class="multi-column-item">
<h4>Stylus</h4>
<pre>
```
// 默认配置
$base_font_size ?= 16px

.title
    font-size: rem(20)
.desc
    font-size: rem(12)
```
</pre>
</div>

<div class="multi-column-item">
<h4>CSS</h4>
<pre>
```
.title {
    font-size: 1.25rem;
}
.desc {
    font-size: 0.75rem;
}
```
</pre>
</div>

</div>

<small>**默认配置** 在 *`normalize()`* 后生效，会转换为 **百分比**，为 *`html`* 设置 *`font-size`*</small>

---

### 响应式支持

<div class="multi-column-container with-gap">

<div class="multi-column-item">
<h4>Stylus</h4>
<pre>
```
$breakpoint-slicer = 0 400px 600px 800px 1050px

.header
    background: black
    +below(1)
        background: red
    +between(2, 4)
        background: yellow
    +above(4)
        background: blue
```
</pre>
</div>

<div class="multi-column-item">
<h4>Stylus</h4>
<pre>
```
.header { background: black; }
@media only screen and (max-width: 400px) {
    .header { background: red; }
}
@media only screen and (min-width: 400px) and (max-width: 1050px) {
    .header { background: yellow; }
}
@media only screen and (min-width: 1050px) {
    .header { background: blue; }
}
```
</pre>
</div>

</div>

    Breakpoint:   0                 400px     600px     800px       1050px
               ├───────────────────┼─────────┼─────────┼───────────┼─────────>
    Slice #:                1              2         3          4          5


<i class="fa fa-ellipsis-h state-weakest"></i>

<small>**Stylus** 的实现有 [`rupture`](https://github.com/jenius/rupture)，**Sass** 的实现有 [`breakpoint-slicer`](https://github.com/lolmaus/breakpoint-slicer)、[`breakpoint`](https://github.com/Team-Sass/breakpoint)</small>

---

### UI 样式库

基于基础 **工具库**，搭建针对特定 **业务类型** 的 **UI 样式库**<br/><br/>

<i class="fa fa-angle-right"></i> 布局&nbsp;&nbsp;&nbsp;&nbsp;
<i class="fa fa-angle-right"></i> 排版&nbsp;&nbsp;&nbsp;&nbsp;
<i class="fa fa-angle-right"></i> 组件

<small>

+ 需要 **快速成型** 的项目以 **显式定义 Class** 为主，类似 **Bootstrap**
+ 需要 **精耕细作** 的项目以 **Mixin** 风格为主，**语义化**、**可维护性** 更好

</small>


---

## Thanks

<small class="state-weaken">2013-12-25, Baidu EFE</small>