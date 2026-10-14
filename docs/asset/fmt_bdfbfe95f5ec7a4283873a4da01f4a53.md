
## 另一个页面将是 Microsoft Internet Explorer 特有的

## 还有一个页面将是 Mosaic 特有的

图 6.6 显示了一个包含一个 JPEG 类型图形的简单网页。这种页面可以使用图形化浏览器（如 Mosaic）读取，但不能由基于文本浏览器（如 Lynx）读取。

**图 6.6：此基础网页包含一个 JPEG 风格的嵌入图形。**

创建包含一个嵌入图形的网页的 HTML 语句出现在列表 6.6 中。

### 列表 6.6 带有文本和一个嵌入 JPEG 图形的网页 (`maingraph.html`)

```
<HTML>
```

第 6 章 -- 使用动态页面

```
<HEAD><TITLE>欢迎！</TITLE></HEAD>

<BODY BGCOLOR="FFEBCD" TEXT="#8B4513">

<H1>欢迎访问我的网站！ </H1>

<p>

<IMG SRC="garden2.jpg">

<p>

本站点在打开此页面之前将测试您的浏览器。根据确定的浏览器类型，它将打开不同的页面。

<p>

<H2>其中一个页面将是纯文本。</H2>

<p>

<H2>另一个页面将是 Netscape 特有的。</H2>

<p>

<H2>另一个页面将是 Microsoft Internet Explorer 特有的</H2>

<p>

<H2>还有一个页面将是 Mosaic 特有的</H2>

</BODY>

</HTML>
```

图 6.7 是一个包含五个框架的复杂网页。四个顶部框架显示嵌入在框架中打开的文档中的 JPEG 风格图形；底部框架包含主文档。要读取此内容，浏览器必须支持框架。Netscape 2.x 或更高版本、Microsoft Explorer 3.x 或更高版本，以及任何基于 HTML3.0 的浏览器都可以读取框架。尝试在未启用框架的浏览器中打开此页面，将显示一条消息，说明浏览器无法读取框架。

**图 6.7：此基于框架的网页在顶部框架中打开了四个 JPEG 图片。**

创建包含 FRAMESET 文档的文档的 HTML 出现在列表 6.7 中。

### 列表 6.7 创建包含两行四列两个框架集的网页 (`frames.html`)

```
<HTML>
<HEAD>
<TITLE>Web 服务</TITLE>
</HEAD>
<FRAMES ROWS="30%, *">
<NOFRAMES>
<p>您正在使用的浏览器无法处理框架。</p>
</NOFRAMES>
<FRAMESET COLS="25%, 25%, 25%, 25%">
<FRAME SRC="cliff2.jpg" NAME="Logo" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
<FRAME SRC="flower2.jpg" NAME="Stars" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
<FRAME SRC="leaves2.jpg" NAME="Stars" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
<FRAME SRC="garden2.jpg" NAME="Stars" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
</FRAMESET>
<FRAME SRC="main.html" NAME="Space">
</FRAMESET>
</HTML>
```

最后，图 6.8 显示了一个基于框架的网页，其中包含专门为配合 Netscape 的 Live 插件开发的 VRML 文件。这仅为某一个浏览器开发，至少这次是这样。如果你尝试用另一个浏览器（如 Microsoft 的 Internet Explorer）打开此文档，文档的顶部部分将保留。

图 6.8：此基于框架的网页包含四个 VRML 文件，每个顶部行框架对应一个。

创建此文档的 HTML 仅针对一个浏览器出现，如列表 6.8 所示。代码与列表 6.7 几乎相同，只是对于 `.vRL` 扩展名，在顶部框架中打开而不是 JPEG 文件。

### 列表 6.8 包含五个带有 VRML 框架的 HTML 文档 (`netframes.html`)

```
<HTML>
<HEAD>
<TITLE>Web 服务</TITLE>
</HEAD>
<FRAMES ROWS="30%, *">
<NOFRAMES>
<p>您正在使用的浏览器无法处理框架。</p>
</NOFRAMES>
<FRAMESET COLS="25%, 25%, 25%, 25%">
<FRAME SRC="box.vrl" NAME="Logo" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
<FRAME SRC="graph.vrl" NAME="Stars" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
<FRAME SRC="station.vrl" NAME="Stars" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
<FRAME SRC="garden.vrl" NAME="Stars" MARGINWIDTH="0" MARGINHEIGHT="0" SCROLLING="no">
</FRAMESET>
<FRAME SRC="main.html" NAME="Space">
</FRAMESET>
</HTML>
```

`META` 元素包含在 HTML 文档的 `HEAD` 部分，它包含三个属性。一个 `META` 元素必须包含 `NAME` 或 `HTTP-EQUIV`，但不能两者兼有。`NAME` 属性由解析它的浏览器定义。其中一种是使用 `keywords` 单词作为名称；`CONTENT` 属性包含一个描述文档或网站的关键词列表。`HTTP-EQUIV` 属性与 `CONTENT` 属性结合使用，由浏览器解析以提供响应头。

该技术的一种流行用途是刷新摄像头站点，例如著名的 FishCam 网站。如果该网站每隔 30 秒截取一张静态照片，并为每张照片使用不同的 `name` 属性，那么每 30 秒刷新一次文档内容就会显示新图像，从而为 Web 页面提供动态内容。

将此概念更进一步，我们可以调用 CGI 程序来代替加载 HTML 文档；由 CGI 程序来创建要加载的文档。在程序的每次迭代中，该程序都可以提供不同的内容。

图 6.9 显示了一个简单的网页，该 Web 页面阅读器是首次访问的（至少对于当前会话而言）。30 秒后，会自动加载一个不同的页面，说明该人员已在第 1 页；下次迭代是 2，依此类推。图 6.10 显示了刷新操作两次后的 Web 页面。

图 6.9：此简单的网页包含一个页眉，其中包含一个 `META` 属性，用于在 30 秒后自动刷新页面。

图 6.10：此简单的网页由 CGI 程序生成，显示刷新的迭代次数，并包含其自身的 `META` 属性，以便在 30 秒后再次自动刷新。

第一个页面是标准的 HTML 文档，包含带有 `HTTP-EQUIV` 属性的 `META` 标签。30 秒后，将加载一个名为 `backagain.cgi` 的 CGI 程序。该 CGI 程序反过来创建一个新的 HTML 文档，其具有再次 30 秒自动刷新的属性。此外，迭代次数作为查询字符串位于应用程序调用的 URL 中。列表 6.10 显示了 HTML 文档语句，列表 6.11 显示了 CGI 程序。

### 列表 6.10 包含刷新响应的 HTML 文档 (`backagain.html`)

```
<HTML>
<HEAD><TITLE>First Time! </TITLE>
<META HTTP-EQUIV="refresh" CONTENT="30; URL=http://unix.yas.com/book-bin/backagain.cgi?i=1">
</HEAD>
<BODY>
<h1>This is your first time here!</h1>
</BODY>
```

### 列表 6.11 包含 HTTP-EQUIV 刷新响应的 CGI 程序 (`backagain.cgi`)

```perl
#!/usr/local/bin/perl

#
# backagain.cgi
#
# 该应用程序根据嵌入文档的
# 刷新响应头由服务器调用。
# 每次迭代都会捕获并打印在
# 生成的新文档头中。
#
```
