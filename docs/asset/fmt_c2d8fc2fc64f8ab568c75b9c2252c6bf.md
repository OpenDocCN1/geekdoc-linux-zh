
`<window>` 标签的 `chromehidden` 属性对应用程序程序员无效。它由 `window.open()` 方法、经典浏览器的工具栏逻辑或 MacOS 上的工具栏部件设置。`<window>` 标签的 `windowtype` 属性接受字符串并用于窗口管理（参见“管理现有窗口”）。如果曾经存在 `<package>` 标签，它现在已经消失了。它偶尔出现在旧的 Mozilla 文档中。

## 10.6 混合文档

可以组合文档使它们的单独标签混合在一起，而无需将其隔离在 `<iframe>` 中。

### 10.6.1 混合 XML 文档类型

Mozilla 的一项强大功能是可以渲染包含多个标准标签文档。这意味着文档可以包含 HTML、SVG、MathML 和 XUL 内容，并混合在一起。这只需通过添加 XML 命名空间来实现。添加的命名空间的所有标签变得可用。然而，Mozilla 只识别正确 MIME 类型的 XUL 内容。

### 10.6.2 混合 XUL

`<overlay>` 标签类似于 C/C++ `#include` 指令的高级版本。它允许通过 `id` 属性无缝合并多个 XUL 文档。在第 12 章“叠加层与 Chrome”中有描述。

## 10.7 管理现有窗口

窗口创建后，应用程序可能希望管理它们。一个简单的例子是 DOM 检查器中的“文件 | 检查窗口”（File | Inspect a Window）菜单选项，它会选取一个窗口进行研究。另一个更简单的例子是大多数 Mozilla 应用程序窗口的下半部分，它可以在窗口之间移动焦点。

尝试管理多个窗口可能会导致非常糟糕的设计。在用户可以随时关闭窗口的情况下，这会清除该窗口的所有状态（Java applet 和共享的 XPCOM 对象除外）。当状态可以任意消失时，很难维持一个理性的设计。通而言之，一个应用程序应该有一个窗口，任何其他窗口都依赖于该窗口。`window.open()` 的依赖和模态功能是协调窗口的最简单的方法。如果需要桌面隐喻，则所有窗口都必须是相互独立的，或者必须实现一个注册系统来跟踪哪些窗口仍然可用。

Mozilla 提供了几个用于管理窗口的组件和接口。最简单的组合对是：

```
@mozilla.org/appshell/window-mediator:1 and nsWindowMediator
```

此接口提供了当前窗口的列表。它还没有完成（版本 1.2 的版本），可能会发生轻微变化。列表有多种形式，取决于使用了什么方法。使用 10.3 演示了如何获取当前打开窗口的静态列表。

列表 10.3 使用 `nsWindowMediator` 获取当前打开的窗口。

```
var C, obj, iface, mediator, enum, windows;
C = Components;
obj = Classes("@mozilla.org/appshell/window-mediator");
iface = C.Interfaces.nsWindowMediator;

mediator = obj.createInstance(iface);
enum = mediator.getEnumerator(null);
windows = {};

// 使用 nsSimpleEnumerator 方法记录所有窗口
while (enum.hasMoreElements()) {
  windows.push(enum.getNext());
}
// 对第一个窗口进行某些操作
windows[0].document.GetElementBy-
```

`getEnumerator()` 方法可以传递一个字符串，该字符串将过滤所检索的窗口列表。只有 `windowtype` 属性匹配字符串的 `<html>`、`<window>`、`<dialog>` 或 `<wizard>` 窗口会被返回。

## 样式选项

要仅返回 XUL 窗口，请改用 `getXULWindowEnumerator()`。该接口还可以报告当前打开窗口的堆叠顺序。图标化（最小化）的窗口位于堆叠顺序的底部。

窗口会打开和关闭，应用程序可能希望动态地跟踪这一点，正如前面提到的菜单那样。实现此点的方法之一向窗口协调器对象添加一个监听器。如果窗口打开、关闭或更改更改，建议使用此监听器（实现 `nsWindowMediatorListener`）。一种更高级且所需代码较少的解决方案是-直接在 XUL 中使用 `rdf:window-mediator` 数据源。RDF 和数据源在第 11 章“RDF”中进行了描述。

## 样式选项

XUL 和 HTML 的窗口方面受益于对 CSS2 系统的微小和系统性增强。

微小增强如下：

`<tooltip>` 标签显示弹出内容，正如第 7 章“表单与菜单”中的“样式选项”部分讨论 `<menupopup>` 标签的那样。行内显示工具提示比使用菜单更有用，尽管后者可以快速视觉检查以确认所有视觉元素都有此类提示。

`-moz-appearance` 样式属性用于支持原生（桌面）主题，还支持以下值：

原生主题也存在系统性增强。这对于窗口以及让对话框看起来完全像由原生桌面（例如 Windows 或 GTK）创建的窗口是非常有用的。对话框如果不包含奇怪的颜色和形状，对用户来说是不会干扰的。Mozilla 包含了颜色和名称扩展，帮助对话框（以及其他）模拟桌面产生的对话框。这些颜色和字体名称可以用样式中任何普通颜色或字体名称出现的地方。

除了这些自定义颜色和字体外，Mozilla 还支持 CSS2 标准第 18.2 节指定的面向桌面的颜色和字体。

在 XUL 应用程序中广泛且仔细地使用这些样式，可以消除该应用程序基于 Mozilla 的任何暗示。以这种方式设计良好的应用程序可能与传统的桌面应用程序无异，例如 Windows 上的 Visual Basic 或 UNIX 上基于 GTK 的应用程序。

Mozilla 支持的附加原生匹配颜色名称见表 10.2。通过检查源文件 `nsCSSProps.cpp` 可以找到这些颜色的最新更新。

## 表 10.2 CSS2 颜色名称扩展

| 原生颜色名称 | 匹配此原生项目 | 额外的 Macintosh 特有颜色名称 |
|---|---|---|
| `-moz-field` | 字段背景 | `-moz-mac-focusring` |
| `-moz-fieldtext` | 字段内文本前景 | `-moz-mac-menueslect` |
| `-moz-dialog` | 对话框背景 | `-moz-mac-menushadow` |
| `-moz-dialogtext` | 对话框内文本前景 | `-moz-mac-accentselect` |
| `-moz-dragtargetextension` | 拖过拖拽目标时的突出颜色 | `-moz-mac-accentregularhighlight` |
| `-moz-hyperlinktext` | 可点击的链接文本，例如 Windows 桌面链接 | `-moz-mac-accentregularshadow` |
| `-moz-visitedhyperlinktext` | 已访问链接的可点击链接文本 | `-moz-mac-accentdarkshadow` |
| | | `-moz-mac-accentdarkestshadow` |

同样，Mozilla 支持 10.3 中列出的字体名称，但这些字体名称似乎没有起任何作用。版本 1.4 的特殊字体名称 `-moz-fixed` 提供固定宽度字体并可用于显示字体。

## 表 10.3 Mozilla 字体扩展

| 原生字体名称 |
|---|
| `-moz-window` |
| `-moz-document` |
| `-moz-workspace` |
| `-moz-desktop` |
| `-moz-info` |
| `-moz-dialog` |
| `-moz-button` |
| `-moz-pull-menu` |
| `-moz-list` |
| `-moz-field` |

## 10.9 动手实践：对话框

在本次“动手实践”中，我们将利用 XUL 的窗口特性来进一步编辑 Noteaker。我们还将协调应用程序和编辑对话框以便它们协同工作。这两个项目包括若干小任务：

- 将编辑对话框中的 `<window>` 替换为 `<dialog>`。
- 将 `<button>` 处理器替换为 `<dialog>` 处理器。
- 在主窗口上实现 `notetaker-open-dialog` 命令，以便使用 `window.open()` 显示框。
- 实现 `notetaker-close-dialog` 命令。
- 为处理多窗口的数据找到策略。
- 确定 Noteaker 是什么类型的窗口。

首先，我们查看编辑对话框。将 `<window>` 标签替换为 `<dialog>` 是很容易的，新标签也可以这样做。新标签将是
