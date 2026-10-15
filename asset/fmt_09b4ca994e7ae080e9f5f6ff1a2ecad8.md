
`border` 属性被认为是表现性的，因为它可以用于装饰。通过提供一个大于 0 的值，边框大小会改变，无论图片是否被链接。理想情况下，你将使用 CSS 而不是 `border` 属性来修改边框。CSS 也被用于在内容内对齐或浮动图片。你将在第 11 章“Margins, Borders, and Padding”以及第 12 章“Positioning, Floats, and Z-index”中学习更多知识。

## 链接音频或视频文件

如果你想为你的网站提供媒体链接，可以像链接图片一样轻松实现。音频和视频有许多文件类型，如今最流行的是 MP3、QuickTime、Real 和 Windows Media 文件。

你首先将媒体文件放入子目录。与图片一样，这是一个有助于你保持所有文件组织的约定。在这种情况下，我将子目录命名为 `sub-media` 并在其中放置了两个文件，一个是 MP3 音频文件，另一个是 `.avi` 视频文件。示例 3-5 显示了我的文档以及我如何链接我的媒体文件。

**示例 3-5** 链接音频和视频

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN"
  "http://www.w3.org/TR/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
  <title>Chapter 3</title>
</head>

<body>
  <a href="media/audio.mp3">audio</a>
  <a href="media/video.avi">video</a>
</body>
</html>
```

*(注：由于原文提供的代码块内容不完整，此处根据逻辑补全了翻译结构。)*

# 但是法官大人，我提议！

好的，整个最后一个章节都充满了谎言。并不是说我试图误导你——我正试图做完全相反的事情。如果你希望标记是存在于 HTML 和 XHTML 有效世界中的，那么就应该使用 `object` 元素来处理所有外部媒体。

然而，使用 `object` 元素有一个巨大的障碍，那就是它在不同浏览器和平台上的支持并不一致。从纯粹主义的角度来看，这非常令人不安，因为在规范内部没有其他替代方案。

## 量子飞跃：XHTML 2.0 中的对象处理

在 HTML 2.0 中，`object` 元素变得无处不在。换句话说，任何其他外部对象的元素（包括 `img`）都过时了。显然，使用 XHTML 2.0 是初步的，因为你的结果将限于少数支持 `img` 的 `object` 的浏览器。但它能让你对 XHTML 的发展方向有一个良好的了解。

简单来说，核心就是：如果你想让多媒体在所有浏览器中保持一致，你就必须转向一种专用元素，即 `embed` 元素。这个元素从未出现在任何正式规范中，但大多数浏览器都支持它；如果你的页面使用了 `embed` 元素导致验证错误，它们将会崩溃。

常规做法是结合使用 `object` 和 `embed`。因此，如果你对上述描述的 Flash 文件使用这种方法，你将得到示例 3-8 所示的标记。

### 示例 3-8 使用 `<object>` 和 `<embed>` 将 Flash 文件 (SWF) 嵌入页面

```html
<object class="cid=d27cdc66-ae6d-11cf-96b8-444535545000" width="100"
height="100" codebase="http://archive.macromedia.com/flash6/cas/
flash.cabversion="6,0,0">
<param name="movie" value="ava.swf" />
<param name="play" value="true" />
<param name="loop" value="true" />
<param name="quality" value="high" />
<embed src="media/ava.swf" width="100" height="100" play="true"
loop="true" quality="high"></embed>
</object>
```

该 Flash 电影现在将在几乎每个浏览器中内联播放。

# 添加脚本

为你的页面增加交互性和趣味的另一种方法是向它们添加脚本。通常，这指的是 JavaScript 或所知的动态 HTML（DHTML），它是多种技术的组合，包括 HTML、CSS、JavaScript 和文档对象模型（DOM）。结合这些技术可以为你提供丰富的功能，如下拉菜单和交互式游戏。

## 量子飞跃：文档对象模型

文档对象模型（也称为 DOM）是浏览器内部的接口，允许你将脚本附加到特定元素上。DHTML 引起争议并产生问题的部分原因在于，由于浏览器实现了非标准的 DOM，这导致了糟糕的一致性。当你在寻找 HTML 脚本时，请确保你使用的是那些提供最强跨浏览器支持的脚本。DOM 是标准化的，所有现代基于标准的浏览器都在使用它来高效地实现 DOM 标准。

你可以通过两种主要方式向文档中添加脚本。一种是将脚本放置在文档的 `head` 部分，这被称为嵌入脚本。另一种方法是将你的脚本放置在文档外部，这被称为链接脚本。

# 嵌入脚本

要在文档的 `head` 部分嵌入 JavaScript，你使用 `script` 元素来包含脚本（参见示例 3-9）。

### 示例 3-9 将脚本嵌入文档的 head 部分

```html
<head>
  <script type="text/javascript">
    function newWindow() {window.open("images/photo.jpg",
      "foodwin", "width=250,height=188")
  }
  </script>
</head>
```

该脚本的目的是设置文档，在点击特定链接时在新窗口中打开图片 `photo.jpg`。你还需要在文档实际链接中放置一点脚本，如下所示：

```html
<a href="javascript:newWindow()">美味的越南式午餐</a>
```

图 3-12 展示了点击链接如何让弹出窗口带完整的图片出现。

![](img/516568206e0e220ce5a120446a34b48d_60_0.png)

# 链接到脚本

从最佳实践的角度来看，在脚本和样式方面，你越能从文档中提取并放入外部文件，就越好。你可以让许多页面指向一个脚本，如果你需要更改脚本，只需对那一个脚本文件进行修改，而不是对许多带有嵌入脚本的文档进行修改。

要链接到脚本，首先将脚本代码（不包含任何 HTML）放入单独的文件中，并以 `.js` 扩展命名文件，例如 `popup.js`。你可以将该文件放在名为 `scripts` 的子目录下（就像你处理图像和媒体时那样），然后使用脚本将其链接到文档（参见示例 3-10）。

### 示例 3-10 链接到脚本

```html
<head>
<script src="scripts/script.js" type="text/javascript"></script>
</head>
```

将链接代码原样留在文档的 `body` 中，结果将与演示的完全相同。

# 脚本和浏览器问题

在最佳实践方面，在脚本和样式方面，你越能从文档中提取并放入外部文件，就越好。你可以让许多页面指向一个脚本，如果你需要更改脚本，只需对那一个脚本文件进行修改，而不是对许多带有嵌入脚本的文档进行修改。

> 注意
>
> JavaScript 和 HTML 的伟大之处之一在于有许多免费脚本。当然，拥有许多免费脚本的缺点是，许多可能不符合标准，或者出现了新的、更好的脚本。因此，请谨慎使用并仔细阅读细则。我喜欢的几个网站包括 http://javascriptkit.com/、http://simplythebest.net/scripts/HTML_scripts/、http://www.javascript.com/ 和 http://www.dynamic-drive.com/。

# 针对旧浏览器的脚本隐藏

在某些情况下，旧浏览器会尝试显示 `script` 元素内部的内容。

为了避免这种情况，许多人养了“注释掉”脚本的习惯——也就是说，使用注释语法来防止脚本显示（参见示例 3-11）。

### 示例 3-11 使用注释隐藏脚本

```html
<head>
<script type="text/javascript">
  <!-- 为旧浏览器隐藏的脚本 -->
  function newWindow() {window.open("images/photo.jpg",
    "foodwin", "width=250,height=188")
  // 结束对浏览器的隐藏 -->
</script>
</head>
```
