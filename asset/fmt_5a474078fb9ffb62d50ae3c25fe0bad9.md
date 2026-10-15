
## 列表 14.28 带有模板重建的 NoteTaker 工具栏命令列表

```javascript
function action(task) {
  if (task == "notetaker-open-dialog") {
    window.openDialog("editDialog.xul","_blank",modal=yes);
    refresh_toolbar();
  }
```

## 14.9 调试角：模板生存指南

```javascript
if ( task == "notetaker-display" ) {
    display_note();
}
if ( task == "notetaker-save" ) {
    refresh_toolbar();
}
if ( task == "notetaker-delete" ) {
    refresh_toolbar();
}
```

这就完成了工具栏模板的管理。对于对话框，我们需要为关键字面板（Keywords pane）中的模板实现类似的效果。我们选择将其放在 `notetaker-load` 命令中。在处理该命令的 `action()` ) 函数中，我们添加了对 `refresh_dialog()` 的调用，并如列表 14.29 所示实现了 `refresh_dialog()`。

NoteMaker 编辑对话框的测试重建。

```javascript
function refresh_dialog() {
  var listbox = window.document.getElementById('dialog.keywords');
  listbox.setAttribute('ref', window.opener.note.url);
  listbox.builder.rebuild();

  var tree = window.document.getElementById('dialog.keywords');
  tree.setAttribute('ref', window.opener.note.url);
  tree.builder.rebuild();
}
```

这与工具栏下拉菜单的模板更新相同。

## 14.9 调试角：模板生存指南

当模板表述和使用正确时，一切都能正常工作。没有所谓的语法错误或不可用的功能可以归咎。大多数问题源于应用程序代码中的语法错误。

在 Microsoft Windows 上，请确保在关闭最后一个窗口时，Mozilla 平台已完全关闭。如果使用了格式不正确的模板，Mozilla进程可能会滞留，并在后的测试中被重用，这会非常困惑。当发生这种情况时，最常见的症状是对 XUL 代码或 JavaScript 的最新更改似乎没有生效。最安全的方法是每次测试时都启动平台的新实例。如果你让 Mozilla 启动界面保留，可以将其作为提示，提醒你新实例已启动。

第二个平台缺陷涉及递归查询。仅在配合 `<menu>` 或 `<tree>` 小部件时尝试让这些运行；其他结果是不可预测的并可能导致崩溃。

RDF 文档与 XUL 模板的结合是强大的，但复杂的。

![](img/319913ee3703286e2c03d285fbfc49c7_589_0.png)

# 第 15 章

## XBL 绑定

![](img/319913ee3703286e2c03d285fbfc49c7_590_0.png)

563

# 第 15 章 XBL 绑定

本章将解释如何使用 XBL（XML 绑定语言）通过新标签和新行为来增强 XUL 语言。

XBL 是一种基于 XML 的语言，允许向 XUL、HTML 和 XML 中添加新的、功能全标签。它是一个创建新 GUI 控件（widgets）的高效系统。它是 Mozilla 特有的。

原生的 XUL 允许程序员创建诸如 `<tag>` 这样的自定义标签，但这些标签并没有什么用。它们可以设置样式，但与 XBL 相比，它们仅仅是区块；而 XBL 用于创建具有独特外观和行为的控件。XBL 组件的内容是由基于 XBL 的 XUL、HTML 和其他标签的绘制而成的。XBL 不如 Java 程序或插件那样灵活。它不能从一个空白的矩形画布开始，并使用复杂的图形库在平面上绘图。XBL 只能组合现有的标签。

XBL 不创建新元素；它创建绑定（bindings）。一个*绑定*是标签和脚本的集合，提供了类似控件的事件处理器功能和显示内容。这个集合就是一个绑定，并且它是一个对象。在 Mozilla 中，绑定通过 Mozilla 特有的 CSS 类型——`binding` 与自定义标签匹配。当绑定与标签匹配后，它们就被认为已“绑定（bound）”。列表 15.1 显示了一个简易的绑定。这是一个 XUL 文档的片段，实现了一个仅仅是笑脸（表情符号）的控件。

- 列表 15.1 XBL 绑定的简单示例。

```xml
<binding id="smiley">
<content>
<xul:image src="face.png"/>
</content>
<handlers>
<handler event="click" action="alert('have a day')"/>
</handlers>
</binding>
```

可以通过像下面的一行 CSS 代码将此类绑定附加到自定义标签 `<smiley/>` 上：

```css
--moz-binding: url("smiley.xml");
```

每当 `<smiley/>` 标签在 XUL 文档中使用时，它都会显示一个脸。如果点击该脸，就会弹出一个警告框鼓励你度过愉快的一天。这是一个具有自身交互性的简单控件。XUL 或 HTML 都没有提供 `<smiley tag>`。

XBL 绑定被构建在 Mozilla 平台的 C/C++ 核心中，但绑定本身仅使用 JavaScript 和 XML 编写。这种完全解释型的环境使得绑定的创建和管理像 XUL 或 HTML 一样简单。这种用法在 Mozilla 中已经得到了充分利用。许多 XBL 绑定为 Mozilla 应用做出贡献，例如 Classic Mail & News 和 Classic Browser。几乎所有的 XUL 标签都有一个 XBL 绑定。

## 15.1 绑定概念

在本书中，提到了 `toolkit-jar` 文件中的 `.xml` 文件。这些 `.xml` 文件就是 XBL 绑定，通常每个文件有几个。书中记录的某些 XUL 标签仅仅是正在工作中的 XBL 绑定。良好的例子是高度专门的标签，如 `<tabbrowser>` 和 `<colorpicker>`，它们完全定义在 XBL 中。即使是像 `<button>` 这样简单的标签也有其 XBL 绑定。

在 Mozilla 之外，类似于 XBL 的技术是 PostScript 语言。PostScript 主要用于打印，也可以手动创建 PostScript 脚本。这使得创建大型文档变得容易。L 和 Tk 等列表处理语言提供了构建 GUI 的解释性方法，它们比基于 XBL 的更具程序化。T/Tk 可能是 Linux 世界中 XBL 最大的竞争对手。在 Windows 世界中，.NET 和许多简单的浏览器是 XBL 的竞争对手。

XBL 绑定具有定义定义的接口和唯一标识，使 XBL 一个轻量级组件系统。XPCOM 为 D3 组件设计，而 XBL 为 XML 组件设计。XBL 的模型比 COM 更简单。

由于 XBL 绑定由 XML 和 JavaScript 制成，绑定元素可以与 HTML 或 XUL 混合使用。HTML 混合是不常见的，因为 HTML 中使用的标签集是固定的且标准的。在 XUL 应用中使用 XBL 要常见得多。

本章开头的 NPA 图显示了 XBL 在 Mozilla 平台中的范围。尽管其状态是一个组件系统，但 XBL 是一种前端技术。在加载 XUL 文档期间，XBL 绑定会被识别并单独提取到文档内容中。这种包含过程是通过叠加系统实现的。在 XBL 绑定加载后，它们提供了对捕捉事件的特殊支持。它使用与 XUL `<key>` 标签几乎相同的捕捉系统来处理特定标签。

本章将继续概述 XBL 绑定，然后深入：

XBL 扩展 XML 扩展 Web Web环境的方式。它在一个起始没有对象特性的系统之上提供了对象特性。

### 15.1.1 示例绑定

每个 XBL 文档都是一个绑定的列表，每个绑定都用 `<binding>` 标签声明。构造绑定类似于构造对象。

列表 15.2 显示了一个简单的 XBL 绑定：
