# Lecture 02 HTML & CSS (Part 1)

## 目录

- [Lecture 03 CSS 进阶](#lecture-03-css-进阶)

- [Lecture 02 HTML&CSS](#lecture-02-htmlcss)
  - [2.0 How HTML, CSS, and JavaScript Work](#20-how-html-css-and-javascript-work)
  - [2.1 HTML Introduction](#21-html-introduction)
    - [2.1.1 HTML 基本结构](#211-html-基本结构)
    - [2.1.2 live server](#212-live-server)
    - [2.1.3 Headings of the context`<h1>`](#213-h1)
    - [2.1.4`<p>`](#214-p)
    - [2.1.5 `<strong>`和`<em>`](#215-strong和em)
    - [2.1.6 `<ol>`和`<ul>`](#216-ol和ul)
    - [2.1.7`<img>`](#217-img)
    - [2.1.8`<a>`](#218-a)
    - [2.1.9 HTML 语义化](#219-html-语义化)

# 课堂笔记

### Lecture 02 HTML&CSS

#### 2.0 How HTML, CSS, and JavaScript Work

- HTML, CSS, JavaScript 是现代 Web app 的三大基石
  - Html 是文本标记语言 提供了网站的基本结构并定义内容
  - CSS 用于控制表示、格式和布局
  - JavaScript 用于控制不同元素的行为，响应 user event

#### 2.1 HTML Introduction

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

#### 2.1.3 `<h1>`

- 从`<h1>` 到`<h6>` 由大到小有各种不同的 Heading，为页面创造视觉层级效果
  > 实际工作时，UI Design 会提供设计样本，Developer 只需要跟着样本开发即可

#### 2.1.4 `<p>`

- 补充:
  - `<p>`里面可以使用<br/>换行
    > 在 XHTML、XML 以及未来的 HTML 版本中，不允许使用没有结束标签（闭合标签）的 HTML 元素。
    > 即使 <br> 在所有浏览器中的显示都没有问题，使用 <br /> 也是更长远的保障。
  - 可以使用`<link rel = "icon" href = "" />`:设定 icon

#### 2.1.5 `<strong>`&`<em>`

- 使用对应 tag 包住要强调的元素进行加粗或者斜体

#### 2.1.6 有序和无序 list`<ol>`&`<ul>`

- 都由`<ol>`和`<ul>`作为 parent，`<li>` list item 作为 children

```html
<ol>
  <li></li>
  <li></li>
</ol>
```

- 补充: description list`<dl>`

```html
<dl>
  <dt>Coffee</dt>
  <dd>- black hot drink</dd>
  <dt>Milk</dt>
  <dd>- white cold drink</dd>
</dl>
```

#### 2.1.7 `<img>`

- NB:self-closing 的 tag，一定要定义 src 和 alt
- 标签包含以下参数
  - src：来源，如果文件在当前路径，直接使用 xxx.jpg, 若在其他地方的 img 文件夹里，更改相对路径至./source folder/xxx.jpg
  - alt: 若 img 加载不出来，提供图片描述
  - height, width 调节图片尺寸
- 补充: [Html 的文件路径](https://www.w3schools.com/html/html_filepaths.asp)

#### 2.1.8 `<a>`

- href：代表链接指向的网页
- target：\_blank 代表点击链接会跳转到一个新的 tab

#### 2.1.9 Plug-in for VScode

- [推荐的 VS Code 插件](https://github.com/Cameron933/JR-17th-Full-Stack-Bootcamp/blob/main/VS%20Code%20Extensions.md)
  > Tips:安装 Live-server 插件后，完成后点击右下角 Go-live 选项，会打开浏览器并实时更新做出修改的内容
