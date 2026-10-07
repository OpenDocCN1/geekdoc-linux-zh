

## 第 18 章：自定义 DocBook

### 其他样式表

除了 DocBook 自带的样式表外，还有几种样式表可以免费获取。KDE、GNOME、Debian、FreeBSD 以及网络上的其他几个项目都提供了自定义的 DocBook 样式表。虽然你可能仍然需要对它们进行进一步自定义（特别是如果你编写的内容不是这些项目之一的话），但你可能会发现其中某个组织提供的外观和感觉比默认的 DocBook 样式表更佳。查看它们的源代码也会让你比只看 DocBook 样式表更清晰地理解这些概念。

## 编写本地样式表

自定义 DocBook 样式表，你可以直接修改现有样式表，也可以创建一个本地化的驱动文件，通过该文件进行你的修改，并依赖未修改的 DocBook 默认样式表来处理其余部分。

编写本地样式表要明智得多，因为它更容易管理。你不需要费力研究包含在内的样式表，只需编写一个与样式表配合的插件即可，这个文件要小得多，也更容易管理。

开始之前，你需要一个文档声明，就像普通的 DocBook 文档一样。它看起来应该像这样：

```
<DOCTYPE style-sheet PUBLIC "-//Zonker's Stylish Sheet//EN" [
  <ENTITY dbstyle PUBLIC "-//Norman Walsh//DOCUMENT DocBook Print
Stylesheets//EN" CDATA DTD>
```

这没什么你没见过的东西，至少在某种程度上如此。你使用的不是 DocBook 元素，而是样式表进行声明，并在正式公共标识符（Formal Public Identifier）中填入你的信息。

然后你通过对 DocBook 样式表进行修改来填充文档主体：

```
<DOCTYPE style-sheet PUBLIC "-//Zonker's Stylish Sheet//EN" [
  <ENTITY dbstyle PUBLIC "-//Norman Walsh//DOCUMENT DocBook Print
Stylesheets//EN" CDATA DTD>
  <style-sheet>
  <style-specification use="docbook">
  <style-specification-body>
```

## 自定义 DocBook DTD

```
(define %output-dir "index.html")

<style-specification-body>
</style-specification>
<external-specification id="docbook" document="dbstyle">
</style-sheet>
```

这是一个简单的改动。事实上，在所有这些文本中，你只做了一个改动：

`(define %output-dir "index.html")`

如果你曾经处理过将 DocBook 文档转换为 HTML，你可能已经注意到它会写入与你处理的 SGML 或 XML 文件同名的目录。例如，`book.sgml` 变成 `book/`，生成的文档文件具有像 `book.html` 和 `x231.html` 这样奇怪的名字。此修改的目的是让 HTML 输出为 `index.html`。

## XML 与样式表

XML 有自己的样式表语言，所以如果 DTD 不是你的菜，你会很高兴知道你有一个替代方案。

对于在线文档，XML 可以使用扩展样式表语言（XSL）或级联样式表（CSS）。简而言之，样式表的工作原理是独立于元素本身来定义元素的格式。例如，其中一个样式表可能会声明 HTML 段落元素中的所有文本都应是 14 磅字体，并使用无衬线字体。一个针对老年人网站的样式表可能想将其增加到 22 磅。第一种样式表看起来如下：

```
<style type="text/css">
  body (font-size: 14pt; font-family: sans-serif)
</style>
```

如果你做过任何种 Web 开发，你可能已经对 CSS 有了很好的理解。

SL 实际上利用了 CSS，但不仅于此。我将在本章的剩余部分讨论 XSL。如果你想了解更多关于 CSS 的信息，可能想访问 W3C 的 CSS 首页：http://www.w3.org/css/

