---
title: markdown语法
date: 2014-07-11 14:56:44
tags: markdown 语法
---

## 快速入门

用 Markdown 语法写作是很容易的。在编辑界面的左侧就是你写作的地方。在你认为需要的时候，可以使用以下这些语法来格式化你的内容。例如下面这个无序列表：

    * Item number one
      * Item number two
    * A nested item
    * A final item

还可以是有序列表：

    1. Remember to buy some milk
    2. Drink the milk
    3. Tweet that I remembered to buy the milk, and drank it

### 链接

     如果要链接其它页面，可以直接把页面的 URL 粘贴过来，例如 http://johnyn.com - 会被自动识别为链接。但是，如果你想自定义链接文本，可以像这样： [后会有期](http://johnyn.com)。很简单吧！

### 图片

插入图片也没问题！前提是你事先知道图片的 URL，然后像下面这样：

      {<1>}![The](http://johnyn.com/img/author.jpg)


### 引用

有些时候我们需要引用别人说的话，可以这样：

     > Wisdomous - it's definitely a word.

### 代码

或许你是个码农，需要贴一些代码到文章里，可以通过两个引号（Tab 键上面的那个键）加入行内代码 `<code>`。如果需要加入大段的代码，可以在代码前加 4 个空格缩进，这就是 Markdown 的语法。

    .awesome-thing {
        display: block;
        width: 100%;
    }

### 分割线

在任一新行输入 3 个或更多的短横线（减号）就是一条分隔线了。

---

### 高级用法

Markdown 还有一个特别用法，就是在你需要的时候可以直接书写 HTML 代码。

      <input type="text" placeholder="这是个输入框！" />

只要掌握了上面的这些介绍，你就已经入门了！继续写作吧！
