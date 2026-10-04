

## 10.5 总结

- * 可以使用 `textName window create` 子命令将 Tk 小部件插入到文本小部件中。

  语法：`textName window create index ?options?`

- * 使用 `delete` 子命令从文本小部件中删除文本。

  语法：`textName delete startIndex ?endIndex?`

- *可以使用 `search` 子命令在文本小部件中搜索模式。

  语法：`textName search ?options? pattern startIndex ?endIndex?`

- * 使用 `mark set` 子命令放置标记。

  语法：`textName set markName index`

- * 使用 `mark unset` 子命令移除标记。

  语法：`textName unset markName ?markName2? ... ?markName?`

- * 可以使用 `mark names` 子命令获取标记列表。

  语法：`textName mark names`

- * 可以 `mark next` 和 `mark previous` 子命令遍历文本小部件中的标记。

  语法：`textName mark next`
  语法：`textName mark previous`

- * 可以在 `insert` 子命令或使用 `tag add` 子命令添加标签。

  语法：`textName tag add startIndex ?end1? ?start2? ... ?endN?`

- * 使用 `tag remove` 命令从位置移除标签。

  语法：`textName tag remove startIndex1 ?end1? ?start2? ... ?endN?`

- * 使用 `tag delete` 命令移除对标签的所有引用。

  语法：`tagName delete ?tagName2?`

- * 可以使用 `tag names` 命令获取标签名称列表。

  语法：`tagName names index`

- * 使用 `tag nextrange` 和 `tag prevrange` 命令遍历标签位置。

  语法：`tagName nextrange startIndex ?end?`

- * 使用 `tag bind` 命令将事件绑定到字符或字符串上的动作。

  语法：`tagName bind ?eventType? ?script?`

- * `html_library.tcl` 包提供了一过程，可以将 HTML 渲染为文本小部件。

- * 使用 `HMset_image` 和相关的 `HMgot_image` 将图像插入到 HTML 文档。

  语法：`HMset_image win src`
  语法：`HMgot_image handle`

- * 用户提供的 `HMLink_callback` 过程插入超链接。

  语法：`HMLink_callback win href`

## 第 10 章 text Widget 和 html_library

## Widgets

第 8 章描述的小部件是较小且简单的对象，用于单一目的。它们被设计组合应用程序中更大、更复杂的用户界面。

许多应用程序需要复杂的用户界面部件。例如，任何允许用户从磁盘保存或读取数据的程序都需要一个支持文件浏览的小部件，许多应用程序还需要一个 listbox 或文本小部件，当显示的行数超过小部件高度时显示滚动条。

这些复合小部件通常被称为 megawidget。

Tk 标准发行版工具包包含了一些 megawidget，Tk 扩展中还支持更多 megawidget，例如 [tix](http://www.xpi.com/tix/index.html)、wigwam 和 [MegaWidget](http://www.neosoft.com)。

## 第 11 章 Tk Megawidget

megawidget 可以仅使用 Tk 或使用 C 语言扩展创建。在本章中，我们将讨论标准发行版包含的 megawidget（它们是用 Tk 编写的），以及使用 Tk 构建自己的 megawidget 的方法。

## 11.1 标准对话框

Tk 8.0 发发提供了几个 megawidget 以简化应用程序的编写。这些部件扩展了 Tk 解释器的功能，并让脚本编写者无需重复造轮。

这些部件的实现取决于 Tcl 支持的平台。在 Unix 平台上，它们都是作为 TK_LIBRARY 目录下的 .tcl 脚本实现的。在 Windows 和 Macintosh 平台上，操作系统支持部分小部件，此时 Tk 使用原生实现。如果你希望应用程序使用 Motif 风格的小部件而不是原生小部件，可以将全局变量 `tk_strictMotif` 设置为 1，这将 Tk 对这些小部件使用 Unix 脚本而不是原生小部件。

- - tk_optionMenu

此菜单按钮小部件在按钮上显示选中项目的文本。小部件创建命令返回与脚本提供的按钮名称关联的菜单名称。

```
语法: tk_optionMenu buttonName varName val1?val2...valN?
```

创建一个用于选择项目的菜单。

要创建的按钮的名称。此名称不能属于已的小部件。当 `tk_optionMenu` 调用返回后，此名称可用于显示小部件。

与菜单关联的文本变量。选中的值将保在此变量中。

用户可以从菜单中选择的值。这些值将显示在按钮面上。

## 11.1 标准对话框

### 示例

```
tk_optionMenu .button varName Val1 Val2 Val3
pack .button
```

![](img/fdcc2919568b5b6c9f5301d50a10e87_412)

- - tk_chooseColor

此颜色选择器返回一个可用于颜色的格式化字符串。它会在屏幕上创建一个新窗口，并在完成前启用任务中的其他小部件。

语法：`tk_chooseColor`

### 示例

tk_chooseColor

![](img/fdcc2919568b5b6c9f5301d50a10e87_411)

- - tk_getOpenFile

此文件浏览器部件返回现有文件的名称。如果用户输入不存在的文件名，将显示错误消息对话框，并将焦点返回窗口，直到完成。

语法：`tk_getOpenFile`

```
tk_getOpenFile
```

创建一个文件浏览部件来查找文件。

- - extension

如果用户没有提供扩展名，则会将扩展字符串附加到用户的文件名。默认为空字符串。此选项在 Macintosh 上被忽略。

- - filetypes

此列表用于创建文件类型菜单。如果评估脚本的平台不支持文件类型，则忽略此选项。

- - initialdir 选择目录的初始目录。注意在 Macintosh 上，面板可能会覆盖应用程序默认值，导致此选项被忽略。

- - initialfile 指定出现在选择窗口中的默认文件名。

- - parentWindow 指定此小部件的父窗口。小部件将尝试放置在其父窗口上方，但可能会被窗口管理器放在其他地方。

- title 窗口的标题。某些窗口管理器可能会不带标题栏显示窗口。

### 示例

```
set typeList {
{{Include Files} .h}
{{Object Files} .o}
{{Source Files} .c}
{{All Files} *.}

tk_getOpenFile -initialdir /usr/src/TCL/8.0/library -filetypes typeList
```

| 目录: | /usr/src/TCL/8.0/unix | |
|---|---|---|
| UnixApp.c | UnixDraw.c | |
| Unixic.c | UnixEmbed.c | UnixScale.c |
| UnixId.c | UnixEvent.c | UnixScrib.c |
| UnixUtil.c | UnixFocus.c | UnixSelect.c |
| UnixColor.c | UnixFont.c | UnixSend.c |
| UnixCursor.c | UnixPage.c | |
| UnixDialog.c | UnixMenu.c | UnixXId.c |
| Source Files (*c) | | |

- tkSaveFile

此文件浏览器部件返回所选文件的名称。如果所选文件已存在，将提示用户确认他们愿意覆盖该文件。
它将创建一个与 `tk_getOpenFile` 创建的窗口完全相同的窗口。

**语法：** `tk_getSaveFile ?option value`

```
tk_getSaveFile
```

创建一个文件浏览部件来查找现有文件或输入不存在的文件名。
```
