
`progressmeter` 标签是一个具有可访问性支持的只读标签。它提供进度指示。它是 `<progressmeter>` 标签，等待网页下载或等待大文件下载。`progressmeter` 的特殊属性为

```
mode value label
```

`mode` 指定 `<progressmeter>` 的类型。如果设置为 `undetermined`，进度条表示正在进行或已完成的任务。使用 Mozilla 主题，这显示为一个像理发杆的动画图像。如果 `mode` 匹配，则进度条被横向分成两部分。一部分部分的宽度匹配任务的完成进度；另一部分的宽度匹配任务的比例。它们共同构成了任务的 100%。`value` 属性具体指定了完成了多少任务（以百分比）。`label` 属性用于可访问性且不提供视觉内容。

`<progressmeter>` 标签不仅仅是相邻的两个 `<spacer>` 标签。Unix 版本的 `<progressmeter>` 在指定了 `mode="undetermined"` 和 `value` 时会变得有些困惑，如图 8.3 所示。该条也可以通过 `orient` 属性垂直排列，但它看起来很丑，需要额外的样式来修复其外观，并且会干扰页面布局。

要让 `<progressmeter>` larger，可以使用 `minheight` 和 `minwidth` 属性。

### 8.2.7.2 `<colorpicker>`

`<colorpicker>` 标签是 Mozilla 为颜色工具栏和偏好对话框标签页发明的功能。它允许你从颜色切换中选择 CSS2 颜色。这两个标签都使用其他逻辑使基础任务变得更完整。`<colorpicker>` 没有整洁的模块化实现。

如果你想尝试此标签，一个起点是注意每当点击选择器中显示的任何颜色块时，标签 DOM 对象的属性会被设置为一个值。除此之外的功能都与标签的应用逻辑混合在一起。如果需要，可以检查 `color-picker.xml` 定义。

`<colorpicker>` 生成 `DOMMenuItemActive` 事件以支持可访问性需求外，不包含特殊功能或组件。

## 8.2.7 笔记

尽管 Mozilla 的源代码表明可能存在 `<tkinter>` XUL 标签，但在 1.21 版本中并没有这这样的标签。

Mozilla 包含了 `<titlebar>` 标签的 XBL 定义。它被用于其他 XBL 定义中，但并不具备 XUL 标签的地位。它无非是一个包含 `<label>` 和 `<image>` 的 `<hbox>`。它的设计目的是为了放置由桌面窗口管理器添加到窗口的标题栏。如果你感兴趣，可以去探索一下。

文件选择器（FilePicker）对话框是一个 XUL 应用程序，可以通过对象创建，而不是由它自身的标签。

这标志着 XUL 最明显的用于用户导航的标签结束。

## 8.3 样式选项

导航小部件受益于 Mozilla 的几项样式扩展。

`t-moz-apparence` 样式扩展支持用于精美组件的原生主题。某些值应用于本章描述的 XUL 标签：

`toolbox toolbar statusbar statusbarpanel progressbar vertical progressunk progresschunk-vertical tab left-edge tab-right-edge tabpanis tabpanel scrollbartrack-horizontal scrollbartrack-vertical`

Mozilla 提供了 CSS2 `overflow` 样式属性非常实用的替代方案，如表 8.1 所示。

Mozilla 还支持 `scrollbar auto`。

表 8.1 CSS2 overflow: scroll 样式扩展

| overflow 属性的值 | 内容布局 | 滚动条外观 |
|---|---|---|
| scroll | 裁剪在可滚动框内 | 滚动条始终出现。 |
| -moz-scrollbars-none | 裁剪在可滚动框内 | 滚动条从不出现。 |
| -moz-scrollbars-horizontal | 裁剪在可滚动框内 | 出现水平滚动条。 |
| -moz-scrollbars-vertical | 裁剪在可滚动框内 | 出现垂直滚动条。 |

## 8.4 动手实练：工具栏和标签

在本次“动手实练”环节中，我们为 NoteTaker 工具添加了导航功能。NoteTaker 最初是一个像 Classic Browser 那样的完整应用程序窗口，那么一个中央菜单栏和一组工具栏图标是一个显而易见的起点。然而，NoteTaker 是一个插件工具，它的导航与主机应用程序的导航混合在一起。我们别选择将其设计为一组组件。

该设计任务的一个问题是，我们还没有足够的技术来观察 NoteTaker 组件将如何连接到主机应用程序。我们将分别创建这些组件，并等到稍后的章节再对它们进行集成。

构成 NoteTaker 导航系统的组件如下：

- 1. 我们到目前为止处理过的对话框。
- 2. 主应用程序窗口中的笔记管理工具栏。
- 3. 主应用程序 Tools 菜单上的一个菜单项。
- 4. 在 Tools Web 页面上显示笔记内容的较小插入窗口。

某天可能还会有一个要添加到 Tools 菜单的 Note Manager 项，但本书中不会涉及。那个较小的插入窗口需要特殊处理。它将在第 10 章“窗口与窗格”中处理。我们在这里处理另外三点。

对话框只需要改进。我们将类 `<toolbarbutton>`、`<decr>` 和一些 `action()` 逻辑替换为简单的 `<tabbox>`。代码 Binding 8.6 显示了这段新代码，它非常直观。

> 列表 8.6 用于 NoteTaker 编辑对话框的 `<tabbox>` 控制。

```xml
<tabbox id="dialog.tabs">
<tabs>
<tab id="dialog.tab.edit" label="Edit" accesskey="E" selected="true"/>
<tab id="dialog.tab.keywords" label="Keywords" accesskey="K"/>
</tabs>
<tabpanel>
... 编辑面板内容位于此处 ...
</tabpanel>
<tabpanel>
<description>稍后添加的内容。</description>
</tabpanel>
</tabbox>
```

此更改后的结果如图 8.8 所示。

我们还必须更新 `action()` 函数，因为各个标签的 JavaScript 可以按键进行选择。我们需要从 JavaScript 控制 `<tabbox>`。查看 chrome 中 `toolkit.jar` get `ui.css`，我们看到对所有 `<tabbox>`、`<tabs>`、`<tab>` 和 `<tabpanel>` 的绑定。检查（同样在 chrome 中）包含这些 XBL 绑定的 `tabbox.xml` 文件，我们注意到 `tabbox` 有一个 `selected` 属性，`<tab>` 也有一个 `selected` 属性。再次，这些名称在用法上与 XML 属性和标准 DOM 2 HTML 属性匹配。我们将使用 `<selectbox>` 的 `selected` 属性。

## 8.4 动手实练：NoteTaker 工具栏和标签

![](img/319913ee3703286e2c03d285fbfc49c7_318_0.png)

`action()` 函数所需的更改显示在列表 8.7 中。

## 列表 8.7 使用 `<tab>` 的 NoteTaker 面板更改。

```javascript
var card = document.getElementById("dialog.") + task;
var deck = card.parentNode;

if (task == "edit") deck.selectedIndex = 0;
if (task == "keywords") deck.selectedIndex = 1;

// 新代码

var tabs = document.getElementById("dialog,tabs");
if (task == "edit") tabs.selectedIndex = 0;
if (task == "keywords") tabs.selectedIndex = 1;
```

显然 `<tabbox>` 和 `<delete>` 的操作方式相似，但 `<tab-box>` 的用户界面略好。得出的结论是对话框的更改。

NoteTaker 工具栏是一个出现在 Classic Browser 窗口中的 XUL `<toolbar>` 标签。它包含允许用户导航到 NoteTaker 编辑对话框的编辑按钮。它还为创建或删除笔记提供了几乎所有内容的默认值。它是用于替换 Classic Browser 工具栏的简便方案。
