#### <i class="fa fa-css3"></i> CSS on the Road

### CSS *Preprocessor* and *Postprocessor*

Firede

<small>
    <i class="fa fa-github"></i> [Github](https://github.com/firede)
    <i class="fa fa-weibo"></i> [Weibo](http://weibo.com/firede)
</small>

---

### CSS *Preprocessor* ?

**CSS 预处理器** 是以最终生成 CSS 为目的的 **领域特定语言 <small>DSL</small>**

[`Sass`](http://sass-lang.com/)、[`LESS`](http://lesscss.org/)、[`Stylus`](http://learnboost.github.io/stylus/) 是最主流的 **CSS 预处理器**

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>广义上讲，从 **源代码** 转为 **生产环境 CSS** 过程中，处理 **CSS** 的工具都是 **CSS 预处理器**</small>

---

### 例如 *LESS*

```less
.opacity(@opacity: 100) {
    opacity: @opacity / 100;
    filter: ~"alpha(opacity=@{opacity})";
}
.sidebar {
    .opacity(50);
}
```

<i class="fa fa-arrow-down"></i> 输入 **DSL 源代码**，输出 **CSS**

```css
.sidebar {
    opacity: 0.5;
    filter: alpha(opacity=50);
}
```

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>这个大家比我熟 <i class="fa fa-heart"></i></small>

---

### CSS *Preprocessor* 的实现原理

1. 取到 **DSL 源代码** 的 **分析树**
2. 将含有 **动态生成** 相关节点的 **分析树** 转换为 **静态分析树**
3. 将 **静态分析树** 转换为 **CSS** 的 **静态分析树**
4. 将 **CSS** 的 **静态分析树** 转换为 **CSS 代码**

---

### CSS *Postprocessor* ?

**CSS 后处理器** 是对目标 **CSS** 进行再处理的程序

[`Autoprefixer`](https://github.com/ai/autoprefixer)、[`clean-css`](https://github.com/GoalSmashers/clean-css) 都属于 **CSS 后处理器**

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>它本质上还是 **CSS 预处理器**，将两者分开便于之后的阐述</small>

---

### 例如 *Autoprefixer*

```css
.container {
    display: flex;
}
.item {
    flex: 1;
}
```

<i class="fa fa-arrow-down"></i> 由 **标准 CSS** 到 **生产环境 CSS**

```css
.container {
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
}
.item {
    -webkit-box-flex: 1;
    -webkit-flex: 1;
    -ms-flex: 1;
    flex: 1;
}
```

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>如果你用 **Sublime Text**，可以安装 **Autoprefixer** 插件体验一下</small>

---

### CSS *Postprocessor* 的实现原理

1. 将 **源代码** 做为 **CSS** 解析，获得 **分析树**
2. 对 **CSS** 的 **分析树** 进行 **后处理**
3. 将 **CSS** 的 **分析树** 转换为 **CSS 代码**

---

#### 新的工作流

### **DSL 源代码** <i class="fa fa-long-arrow-right"></i> **标准 CSS** <i class="fa fa-long-arrow-right"></i> **生产环境 CSS**

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>**标准 CSS** 到 **生产环境 CSS** 的转换过程是自动的</small>

---

### 未来趋势

+ 越来越多专注于 **单一功能** 的小型 **CSS 工具库**
+ **CSS 样式库** 从 **整体方案** 到 **模块化组合方案** 转变
+ 部分 **CSS 未来标准** 在 **CSS 预处理器** 中得到支持
+ **原生 CSS** 和 **CSS 后处理器** 的组合成为新选择

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>其中的佼佼者是 **Rework** 和 **PostCSS**</small>

---

### *Rework*

[`Rework`](https://github.com/visionmedia/rework) 是一个 **高效**、**简单**、**易扩展** 并且 **模块化** 的 **CSS预处理器**

<i class="fa fa-ellipsis-h state-weakest"></i>

实际上，它采用的是 **CSS 后处理器** 的模型

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>**Rework** 2012 年 9 月发布第一个版本，是 **Stylus** 的作者 *TJ Holowaychuk* 挖的新坑</small>

---

### *Rework* 特点及概况

+ **JavaScript** 中直接操作 **CSS 解析对象**，扩展方便
+ 可以 **自由组合模块**，按需定制 **CSS 工具库**
+ **CSS 后处理器** 的模型决定它的模块倾向 **CSS 未来标准**
+ 除 **服务器** 端外，也支持在 **浏览器** 环境运行
+ 很年轻的项目，还需更多时间积累


<i class="fa fa-ellipsis-h state-weakest"></i>

<small>一些参考 **CSS 未来标准** 的模块：[rework-vars](https://github.com/visionmedia/rework-vars)、[rework-font-variant](https://github.com/ianstormtaylor/rework-font-variant)、[rework-calc](https://github.com/klei-dev/rework-calc)、[rework-color-function](https://github.com/ianstormtaylor/rework-color-function)</small>

---

### *PostCSS*

[`PostCSS`](https://github.com/ai/postcss) 是一个 **CSS 后处理器** 框架，允许你通过 **JS** 对 **CSS** 进行修改

<i class="fa fa-ellipsis-h state-weakest"></i>

+ 它和 **Rework** 非常相似，但提供了更高级的 **API**，更易扩展
+ 它可以在现有 *Source Map* 的基础上生成新的 **Source Map**
+ 在 **原有 CSS 格式** 的保护方面做的更好，便于开发 **编辑器插件**
+ 比 **Rework** 更年轻，还只有 **Autoprefixer** 一个成功案例

<i class="fa fa-ellipsis-h state-weakest"></i>

<small>**PostCSS** 第一个版本发布于 2013 年 11 月，是从 **Autoprefixer** 项目中抽象出的框架</small>

---

## Q & A