
此类属性文件必须存储在 chrome 包的 locale 子目录中。因此，字符串包的完整 URL 为：

```
chrome://packagename/local/filename.properties
```

从纯 XUL 的角度来看，字符串包是无趣的。列表 3.2 显示了你用它们能做的一切。

### 3.2 从 XUL 声明的字符串包

```
<stringbundle id="menus" src="menus.properties"/>
<stringbundle id="tips" src="tips.properties"/>
<stringbundle id="status" src="status.properties"/>
</stringbundle>
```

这些标签没有一个显示任何可见内容。它们所做的仅仅是让 JavaScript 脚本可以使用字符串包。`<stringbundle>` 并不是一个真实的标签——它只是一个用户定义的容器，用于存放 `<stringbundle>` 标签。标签有默认样式，使其完全不可见。

这种 XUL 展示了该语言的一项重要特性。使用容器标签（通常名称以 -set 结尾）是一种常见的用法。将此类标签作为 `<stringbundle>` 使用并无影响，但将一组相似的语句（`<stringbundle>` 标签）收集是一个良好的编码习惯。它整洁且具有高度可读性。建议你始终这样收集你的不可见标签集，并将它们放在 XUL 文档的开头。

涉及字符串包时，JavaScript 完成了所有工作。脚本对此解释并提供了一个示例。也可以直接从代码访问字符串包，而无需使用任何 XUL 内容。

除了这些机制外，JavaScript 脚本和 RDF 文档还可以为 XUL 应用程序提供文本内容。那种内容不如字符串包静态。

## 3.2.2 图像和 `<image>`

HTML 有 `<IMG>` 标签；XUL 有 `<image>` 标签。它们是相同的。一个代码示例是：

```
<image src="myimage.jpg"/>
```

图像具有与显示图像匹配的最小宽度和高度。如果在 `<img>` 标签上应用 flex，图像将失去这些最小值并可以被压缩。为了保留这些最小值，请重新应用 width 和 height 属性。

有两种非常有用的图像技术。两者都与存储在 Mozilla 皮肤和主题中的装饰信息有关。尽管 XUL 有 `<img>` 标签，但在皮肤和主题使用的图像不应那样声明；它们应该在样式表中指定。包含图像 URL 的样式可以附加到如下的无内容标签上：

```
<description class="placeholder"/>
```

匹配的样式的示例是：

```
.placeholder { list-style-image: url(face.gif); }
```

第二，大量的图像可以减少到一个文件。CSS 的裁剪功能可以用于从大文件中显示，如下：

```
#foo { moz-image-region: rect(48px 16px 64px 0px); }
```

类似地：

```
#foo:hover { moz-image-region: rect(48px 32px 64px 16px); }
```

使用这种技术，可以实现由鼠标移动和其他 CSS 伪类引起的图像。过去这种一个图像替换另一个的情况需要单独的 JavaScript 代码，但 CSS 的进步使得这不再需要。这种技术在 Mozilla 自己的皮肤和主题中被常规使用。图 3.2 显示了带有裁剪图像和原始图像的 Composer。

![img/319913ee3703286e03285bfc49c7_115_0.png] 图 3.2 带有裁剪图像和原始图像的 Composer。

## 3.3 理解字体系统

带有经典皮肤的 Composer 和 chrome 文件负责许多可见图标。Mozilla 还对 Microsoft Windows .bmp 格式提供了新的支持。

## 3.2.3 边框装饰

Mozilla 支持基于 CSS 的大量边框装饰。这些在本章的“样式”部分有所介绍。有一个值得特别提及的完全标准的 CSS 是 overflow。该样式的典型用法是为静态文本提供滚动区域，例如许可免责声明。所有需要的只是

## 3.3 理解字体系统

遵循如下：程序将指令发送到专用的 X-server（如 Xfree86、VNC、X-Terminal 固件或 Reflection），然后由它在屏幕上进行绘制。基于 X 的应用程序本质上是由应用程序引导的 X-server 绘制的图片。服务器有一套可以接受的标准指令集。这套指令就是 X11 协议，它并不包含复杂的字体显示。X11 支持扩展（extensions），这些是服务器的可选功能。RENDER 扩展支持复杂的字体显示——这正是你需要的。大多数服务器（尚未）实现这一扩展。Mozilla 无法依赖服务器上是否存在该扩展来运行。然而，这里有一个回退方案。如果你的服务器支持 RENDER，请在命令行运行 `--cmdinfo`。

性能问题的引入是因为 `--enable-xft` 版本的 Mozilla 无论如何都会使用 RENDER。Mozilla 客户端并没有告诉服务器去执行渲染，而是自己内置了 RENDER。它使用额外信息将每个字形（glyph）渲染为一张渲染过的位图（图像），并由 X-server 设置标准的 X11 指令。RENDER 不再每个字符占用几个字节，而是每个字符超过 100 字节，大字符甚至多达 1,000 字节。这就是性能所在所在。

这种从字符到图像的转变并不总是致命的。X-Windows 系统本身存在性能问题，与 Mozilla 可能增加的问题相比微不足道。对 X11 特性的介绍将帮助你判断 Mozilla 中的 RENDER 支持是否值得拥有。

现代基于 X 的应用程序（如 Mozilla、GIMP 和 OpenOffice）包含许多用于图标和其他用户界面元素的图像。X11 系统最初是为显示器设计的（每个像素 1 位），但现在的显示器是每像素 8 位、24 位或 32 位。因此，图像变得更加常见且体积巨大。X-server 与 X-client 之间的通信流量由图像主导，就像大多数带宽消耗在 Web 图像上一样。如果 Mozilla 工作的环境本身就是如此，那么添加图像不会产生多大影响。在这种情况下，如果你喜欢，可以使用 RENDER 支持也所谓。一个典型的例子是：当你所有的技术都运行在一台 UNIX 或 Linux 计算机上，或者当你使用 KDE 或 GNOME 时。

当 X11 系统使用的图像较少，或者在慢连接上运行时，带有 RENDER 支持的 Mozilla 会导致真实问题，并在此时应避免使用。最常见的场景是 X-server 是远程的。在这里指的是 Reflection。如果你在家里（在 PC 或 XTerminal 上）运行 X-server 并拨号到工作地的主机应用程序，也是如此。VNC 则并非如此。VNC 服务器对于 VNC 客户端是远程的，而服务器包含一个 X-server。Mozilla 不影响 VNC 性能。

对于桌面集成，Mozilla 1.0–1.4 基于位于 X-Windows 之上的 GTK 1.4 库。现有的 X 增强功能将在 GNOME 2.0 或 KDE 或更高版本下运行，因为这些新版本也存在旧的 GTK 库。因此，选择使用启用 RENDER 的 Mozilla 版本不会为你的当前桌面带来升级问题。

如果这些 UNIX 字体引起了你的兴趣，会有很多可以学习的内容。你可以在多个地方搜索：`fonts HOWTO` 文件是大多数 Linux 系统附带的标准 FAQ；深层架构问题适用于 Mozilla 字体显示、Microsoft Windows 以及一般的图形显示；www.config.org 上的内容解释了 X 字体渲染系统的基础知识；而且 Window 可以自定义的。

最后，3.3 节对 Mozilla 的默认版本过于刻薄。`Linux fonts HOWTO` 文档包含了许多字体的指针。Mozilla 即使使用简单的位图字体（最原始、最无脑的字体）也可以看起来非常漂亮。所需要的只是在字体出现的每个点为每个字体安装一个 X 安装的位图。所有要求就是为每个字体在每个点安装一个 X 安装的位图。如果你的服务器支持 RENDER，请在命令行运行 `--cmdinfo`。

## 3.4 样式选项（此处为后续翻译，原文未提供完整）

## 3.5 实际操作：NoteTaker 模板代码

| 属性 | 值 | 用途 |
|---|---|---|
| 任意属性 | `-moz-initial` | 将此属性设置为在没有缩放上下文或继承时应具有的值。 |
| 大多数属性 | `inherit` | 与 HTML/XHTML 一致 |
| 任意字体属性 | Desktop fonts | 参见第 10 章“样式选项”中的“窗口与窗格” |
| 任意颜色属性 | Desktop colors | 参见第 10 章“样式选项”中的“窗口与窗格” |
| `-moz-binding` | | 将指定的 XBL 附加到标签上。参阅 XBL。 |
