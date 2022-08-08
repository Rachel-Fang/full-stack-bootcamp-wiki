# Lecture 02 HTML & CSS (Part 1)

## 目录

- [Lecture 03 CSS 进阶](#lecture-03-css-进阶)

- [Lecture 02 HTML&CSS](#lecture-02-htmlcss)
  - [2.0 How HTML, CSS, and JavaScript Work](#20-how-html-css-and-javascript-work)
  - [2.1 HTML 介绍](#21-html-introduction)
    - [2.1.1 HTML 基本结构](#211-html-基本结构)
    - [2.1.2 HTML5 Semantic](#212-html5-semantic)
    - [2.1.3 标题`<h1>`](#213-标题h1)
    - [2.1.4 段落`<p>`](#214-段落p)
    - [2.1.5 `<strong>`和`<em>`](#215-加粗斜体strong和em)
    - [2.1.6 有序和无序 List`<ol>`和`<ul>`](#216-有序和无序-listol和ul)
    - [2.1.7 插入图片`<img>`](#217-插入图片img)
    - [2.1.8 超链接`<a>`](#218-超链接a)
    - [2.1.9 Plug-in for VScode](#219-plug-in-for-vscode)
  - [2.2 CSS](#22-css)
    - [2.2.1 What is CSS](#221-what-is-css)
    - [2.2.2 三种 CSS 的应用方式](#222-三种-css-的应用方式)
    - [2.2.3 选择器 Selector](#223-选择器-selector)
    - [2.2.4 RGB/RGBA Model](#224-rgbrgba-model)
    - [2.2.5 继承-inheritance](#225-继承-inheritance)
    - [2.2.6 CSS box-modal](#226-css-box-modal)
      - [2.2.6.1 margin](#2261-margin)
      - [2.2.6.2 padding](#2262-padding)
    - [2.2.7 Dev tool(Chrome)](#227-dev-toolchrome重要)
    - [2.2.8 Flexbox](#228-flexbox)

# 课堂笔记

### Lecture 02 HTML&CSS

#### 2.0 How HTML, CSS, and JavaScript Work

- HTML, CSS, JavaScript 是现代 Web app 的三大基石
  - Html 是文本标记语言 提供了网站的基本结构并定义内容
  - CSS 用于控制表示、格式和布局
  - JavaScript 用于控制不同元素的行为，响应 user event

#### 2.1 HTML 介绍

HTML 基本结构： open tag + content + closing tag

- 网页开发中，一开始创建的墨守成规一般叫 index.html
  > Tips：在 VS Code 中 ! + tab 可以自动生成 Html 文件的基本部分
  > 同学们要试着使用 tab 键和 auto-completion 的提示来加快自己的代码完成速度

#### 2.1.1 HTML 基本结构

```html
<!-- Html文件头部，告诉文件类型 -->
<!DOCTYPE html>
  <html>
    <!-- `<head>`、`<title>`、`<body>`有且只有一个 -->
    <!-- Head 中的部分不会被浏览器渲染 -->
    <head>
      <title> Title </title>
    </heade>

    <!-- Body 中的部分会被浏览器所渲染 -->
    <body>
    </body>

  </html>
```

- 补充：`<head>` 中一般要有的内容

```html
<meta charset="UTF-8" />
<meta name="description" content="Free Web tutorials" />
<meta name="keywords" content="HTML, CSS, JavaScript" />
<meta name="author" content="John Doe" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

#### 2.1.2 HTML5 Semantic

- 语义化是什么？
  - 语义化是指根据内容的结构化（内容语义化），选择合适的标签（代码语义化）
    > 便于开发者阅读和写出更优雅的代码的同时，让浏览器的爬虫和机器很好的解析
- 为什么要语义化？
  - 有利于服务器搜索优化（SEO）
  - 语义化的 HTML 在没有 CSS 的情况下也能呈现较好的内容结构与代码结构
  - 方便其他设备的解析
  - 便于团队开发和维护
- 举例
  - article 和 header 应该怎么放？这是一个很主观的东西，以下是一个例子
  ```html
  <section>
    <article>
      <header>
        <h1>Title</h1>
      </header>
      <p>This is paragraph</p>
    </article>
  </section>
  ```

#### 2.1.3 标题`<h1>`

- 从`<h1>` 到`<h6>` 由大到小有各种不同的 Heading，为页面创造视觉层级效果
  > 实际工作时，UI Design 会提供设计样本，Developer 只需要跟着样本开发即可

#### 2.1.4 段落`<p>`

- 补充:
  - `<p>`里面可以使用`<br/>`换行
    > 在 XHTML、XML 以及未来的 HTML 版本中，不允许使用没有结束标签（闭合标签）的 HTML 元素。
    > 即使 `<br>` 在所有浏览器中的显示都没有问题，使用 `<br />` 也是更长远的保障。
  - 可以使用`<link rel = "icon" href = "" />`:设定 icon

#### 2.1.5 加粗&斜体`<strong>`和`<em>`

- 使用对应 tag 包住要强调的元素进行加粗或者斜体
  - NB: 使用语义话表达的`<strong>`&`<em>`代替`<b>`&`<i>`

#### 2.1.6 有序和无序 list`<ol>`和`<ul>`

- 都由`<ol>`和`<ul>`作为 parent，`<li>` list item 作为 children

```html
<ol>
  <li></li>
  <li></li>
</ol>
```

- 补充: [Description list](https://www.w3schools.com/html/html_lists.asp) `<dl>`

```html
<dl>
  <dt>Coffee</dt>
  <dd>- black hot drink</dd>
  <dt>Milk</dt>
  <dd>- white cold drink</dd>
</dl>
```

#### 2.1.7 插入图片`<img>`

```html
<img src="../images/picture.jpg" alt="Mountain" />
```

- NB:self-closing 的 tag，一定要定义 src 和 alt
- 标签包含以下参数
  - src：来源，如果文件在当前路径，直接使用 xxx.jpg, 若在其他地方的 img 文件夹里，更改相对路径至./source folder/xxx.jpg
  - alt: 若 img 加载不出来，提供图片描述
  - height, width 调节图片尺寸
- 补充: [Html 的文件路径](https://www.w3schools.com/html/html_filepaths.asp)
  - absolute path: file or directory from the root
  - relative path: 把 current working directory 加进考虑
    > . (代表 current directory)
    > ..（代表 parent directory）
    > pwd 会把 current working directory 给显示出来
    > cd chang directory 帮助在 file system 中 navi

#### 2.1.8 超链接`<a>`

```html
<a href="https://www.w3schools.com" target="_blank">Visit W3Schools.com!</a>
```

- href：代表链接指向的网页
- target：
  - \_self 在当前页面打开
  - \_blank 代表点击链接会跳转到一个新的 tab

#### 2.1.9 Plug-in for VScode

- [推荐的 VS Code 插件](https://github.com/Cameron933/JR-17th-Full-Stack-Bootcamp/blob/main/VS%20Code%20Extensions.md)
  > Tips:安装 Live-server 插件后，完成后点击右下角 Go-live 选项，会打开浏览器并实时更新做出修改的内容

#### 2.2 CSS

#### 2.2.1 What is CSS

CSS describes how HTML elements should be displayed.

```css
/* 其中p是选择器，{}内是declaration */
p {
  color: red;
  /* Color是property，red是value */
  text-align: center;
}
```

- Css 构成如上 Selector + Declaration block + Property + Value + Declaration / Style
- CSS Rule
  - 选择器指向要设置样式的 HTML 元素
  - 声明块包含一个或多个用分号分隔的声明
  - 每个声明包括一个 CSS 属性名和一个值，用冒号分隔
  - 多个 CSS 声明用分号分隔，声明块用花括号包围

#### 2.2.2 三种 CSS 的应用方式

1. External style:

   External style(推荐方式): head 里加 link 标签

2. Internal style:

   Internal style: 也是不推荐，会让 html 显得很长

3. Inline style:

   Inline style（最不推荐）: 省略了找 node 的过程，但是非常不推荐，不可复用，无单一性原则

#### 2.2.3 选择器 Selector

写 CSS 的时候，表明他要附着在什么上面：
NB: Always use class over id

1. All element `<p>` item 选择

```css
/* 其中p是选择器，{}内是declaration */
p {
  color: red;
  /* Color是property，red是value */
  text-align: center;
}
```

2. Class Selector 可复用，可叠加，一般最常用

```css
.className {
  text-align: center;
  color: red;
}
```

3. Element 和 class 组合

```css
p.class1 {
  text-align: center;
  color: red;
}
```

4. Id Selector 只能用在一个 element 里，用一次，所以不是很常用

```css
#id1 {
  text-align: center;
  color: red;
}
```

5. Universal Selector

```css
* {
  text-align: center;
  color: blue;
}
```

6. Grouping Selector

```css
h1,
h2,
p {
  text-align: center;
  color: red;
}
```

- 补充： 选择所有的`<li>`的第一个：
  - 在 Html 中使用 inline css: 加入 class=“first-li”
  - 或在 CSS 里使用 li:first-child\*li:nth-child(3)
  - 或在 CSS 中更具体的指定哪一个 element:article p: first-child

#### 选择`<a>`的属性

- a:link 代表带 href 这个 attribute 的`<a>`
- a:visited 代表链接点过之后的 style
- a:hover 代表鼠标移到链接上面的 style

- 补充:此处作用与常用的[TextEffect](https://www.w3schools.com/css/css3_text_effects.asp)和[Tooltips](https://www.w3schools.com/css/css_tooltip.asp)相似

#### 当多个选择器作用于同一个 element 时，哪个会生效？

冲突优先级:
![comflicting selector 1](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD%E7%AC%AC16%E6%9C%9F%E7%AC%94%E8%AE%B0/img/%E5%9B%BE4.PNG)
![comflicting selector 2](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD%E7%AC%AC16%E6%9C%9F%E7%AC%94%E8%AE%B0/img/%E5%9B%BE5.PNG)

#### 2.2.4 RGB/RGBA Model

每种颜色都可以用 Red、Green、Blue(+Transparency)的结合来表示

> rgb（0，255，255） -----##00fffff（0ff）

- RGB Model 中的 Transparency 被 hardcode 成 1

> rgba（0，255，255，0.3） （最后一项为透明度）

#### 2.2.5 继承 Inheritance

除了跟 text 相关的，其他都不会被继承:
![img6](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD%E7%AC%AC16%E6%9C%9F%E7%AC%94%E8%AE%B0/img/%E5%9B%BE6.PNG)

#### 2.2.6 CSS Box modal

![img7](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD%E7%AC%AC16%E6%9C%9F%E7%AC%94%E8%AE%B0/img/%E5%9B%BE7.PNG)

- Final element width = left border + left padding + width + right padding + right border
- top border + top padding + height + bottom padding + bottom border

#### 2.2.6.1 margin

margin: 跟外界的距离，border 的外面，跟着上和左走;

- 两个 div margin 叠加的时候，系统取中间最大值；e.g.一个 margin 50，另一个 60，系统会取 60
  > margin：auto
  > 把左边 margin 和右边 margin 能找到的最大空间做一个对半分

#### 2.2.6.2 padding

padding : 25px(top), 50px(right),50px(bottom),25px(left)
margin 的简写规则和 padding 一致

#### 2.2.7 Dev tool（Chrome）重要！！

快捷键：cmd+shif+i/ctrl+shift+i

- 直接在调试窗口更改 css，以显示效果
- Console: 查报错，也可以直接写代码，比如

```js
document.querySelectorAll("h1");
```

- Sources: 看源文件
- Network：看加载过程中的请求和文件
- Performance：看 performance，比如页面加载时间
- Memory: 看页面 memory 使用情况，不常用
- Application：用来看 cookie，storage 使用情况
- Lighthouse:也是用来做 performance，整体的 performance，SEO，Accessibility 等的分析
- Accessibility
  - devtools axe-core extension，根据分数给网站调优
    > 小技巧：可以直接在 Dev Tool 中看一些源码，借鉴到自己项目

#### 2.2.8 Flexbox

注意注释位置的设置

```html
<head>
<style>
.flex-container {
    /* A Flexible Layout must have a parent element with the <em>display</em> property set to <em>flex</em> */
  display: flex;
  background-color: DodgerBlue;
}

.flex-container > div {
  background-color: #f1f1f1;
  margin: 10px;
  padding: 20px;
  font-size: 30px;
}
</style>
</head>
<body>

<h1>Create a Flex Container</h1>

<!-- Direct child elements(s) of the flexible container automatically becomes flexible items -->
<div class="flex-container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
</body>
</html>
```
