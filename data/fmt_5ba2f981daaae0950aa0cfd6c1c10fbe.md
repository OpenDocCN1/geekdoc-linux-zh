
在 Tk 中，为事件注册过程以及运行事件循环的细节很大程度上是在后台处理的。在您创建小部件（widget）时，可以注册一个过程，当小部件被选中时对其进行评估，而当没有其他处理在进行时，事件循环就会运行。

## 8.1 创建小部件

创建 Tk 小部件的标准命令格式为：

```
Syntax: WidgetClass widgetName requiredArguments ?options?
```

`WidgetClass`: 原始小部件类型，如 `button`（按钮）、`label`（标签）或 `scrollbar`（滚动条）。

`widgetName`: 该小部件的名称。必须符合下一节描述的 Tk 命名规范。

- `requiredArguments`: Tk 小部件有必需参数。
- `?options?`: Tk 小部件支持大量选项，用于定义字体、颜色、小部件被选中时采取的动作等。

例如，这一行代码：

```
label .hello -text "Hello, World."
```

将创建一个名为 `.hello` 的标签小部件，文本为 "Hello, World."。

在创建小部件的过程中，Tcl 会创建一个名为 `widgetName` 的命令。小部件被创建后，您的脚本可以通过此命令与小部件进行交互。这与第 6 章中创建和操作树对象的方式类似。Tk 小部件支持用于设置和检索配置选项、查询小部件当前状态以及其他特定小部件的命令，例如滚动视图、选择项目和报告选择结果。

前一个示例中的标签将出现在默认窗口中。当 `wish` 解释器启动时，它会创建一个名为 `""` 的默认图形窗口。

## 8.2 规范

Tk 支持的小部件有一些种规范。这些规范包括小部件和颜色的命名规范，以及描述屏幕位置、大小和距离的规范。

### 8.2.1 小部件命名规范

小部件或窗口名称必须以点（`.`）开头，后面可以跟一个标签。标签可以以小写字母、数字或标点符号开头。在第一个字符之后，其他字符可以是大小写字母、数字或标点符号（点除外）。建议您使用小写字母开头标签。

Tk 图形小部件以树状方式命名。

某些小部件可以包含其他小部件。在这种情况下，小部件通过从顶部点到被引用的小部件的完整名称来标识。Tk 小部件必须使用绝对窗口命名。例如，`.root.button1`。

小部件名称是树状的。小部件是另一个小部件的路径。例如，`.hello.label1`。

小部件路径必须是唯一的。因此，在窗口中每个部件是唯一的。例如，`.main.widget1`。

### 8.2.2 颜色规范

颜色可以以十六进制表示，也可以使用名称（如 `red`、`green`、`blue` 等）。

颜色定义可以使用十六进制值，或者使用名称（如 `black`、`lavender`、`000`、`purple`、`deep red`、`golden`、`yellow`、`white`）。

### 8.2.3 尺寸规范

尺寸或位置可以使用像素、英寸、厘米或点来描述。这些值通常是正数。

## 8.3 常用选项

Tk 小部件支持许多显示和操作选项。这些选项具有默认值，因此您不需要为每个小部件定义它们。

这些是许多小部件支持的常用选项：

- `-background`: 小部件的背景颜色。
- `-borderwidth`: 绘制周围的边框宽度。
- `-font`: 小部件使用的字体。
- `-foreground`: 小部件的前景颜色。这是绘制在部件上的颜色。
- `-height`: 小部件请求的高度（像素）。
- `-highlightbackground`: 小部件无焦点时周围的矩形颜色。
- `-highlightcolor`: 小部件有焦点时周围的矩形颜色。
- `-padx -pady`: 在排列小部件时周围要求的额外空间（像素）。
- `-relief`: 小部件的三立体效果：可以是 `raised`、`sunken`、`flat`、`ridge`、`solid` 或 `groove`。
- `-text`: 显示在此部件中的文本。
- `-textvariable`: 与小部件关联的变量名称。变量的内容将反映小部件的内容。例如，与 `entry` 关联的 `textvariable` 将包含输入到该部件的字符。
- `-width`: 小部件请求的宽度（像素）。

## 8.4 确定与设置

选项可以在创建小部件时设置，也可以在小部件创建后使用 `cget configure` 命令进行查询和修改。

`cget` 命令将返回小部件选项的值。

**Syntax:** `widgetName cget option`

- `widgetName`: 小部件的名称。
- `cget`: 返回单个配置选项的值。
- `option`: 要返回值的选项名称。

`configure` 命令将返回单个配置选项值、返回小部件可用的所有配置选项，或者允许您设置一个或多个配置选项。

**Syntax:** `widgetName configure ?opt1? ?val1? ?opt2? ?val2?`

- `widgetName`: 被设置/查询的小部件。
- `configure`: 返回或设置配置值。
- `opt1`: 第一个设置/查询的选项。
- `?val1?`: 为 `opt1` 设置的值。

如果评估 `configure` 时没有选项，则返回所有可用选项和值。

如果使用单个选项对 `configure` 进行评估，它将返回一个包含以下内容的列表：选项名称、在窗口系统资源文件中定义该选项名称和类、选项的默认值以及该选项的当前值。

如果 `configure` 使用选项值对进行评估，它将把选项设置为定义的值。

下面的示例创建了一个按钮，它使用 `configure` 命令在被点击时更改其标签。我们将在本章稍后介绍 `-command` 选项和 `pack` 命令。

## 示例 8.4-1

示例脚本

```tk
set click [button .bl -text "Please Click Me" -command {\.bl configure -text "I've been Clicked!"}]
pack .bl
```

脚本结果

| 点击前 | 点击后 |
| --- | --- |
| ![Please Click Me]()() | ![I've been Clicked!]()() |

## 8.5 基础小部件

Tk 8.0 分发版支持这些原始小部件：

- `- button`：一个可点击的按钮，在选中时可能会评估一个命令。
- `-radiobutton`：一组开启/关闭按钮和标签，其中一个可以被选中。
- `-checkbox`：一组开启/关闭按钮和标签，其中多个可以被选中。

## 8.6 介绍小部件：label, button, and entry

### entry
一个可用于接受单行文本输入的小部件。

### message
创建一个带有文本消息的新窗口。

### label
一个包含只读文本的小部件。

### scale
一个滑块小部件，当选定值改变时可以调用过程。

### menubutton
一个点击时会显示下拉菜单的按钮。

### menu
菜单项的容器。它附着在 `menubutton` 上。

### listbox
创建一个显示选项列表的小部件，其中一个或多个选项可以被选中。`listbox` 可以滚动。

### scrollbar
将滚动条附着在其以支持滚动。当滚动条被修改时会调用过程。

### frame
用于存放其他小部件的容器小部件。

### toplevel
一个带有窗口管理器提供的所有边界和装饰的窗口。

### text
用于显示和可选编辑大段文本的小部件。

### canvas
用于显示图形和图像的绘制小部件。

## 8.6 介绍小部件：label, button, and entry

`label`、`button` 和 `entry` 小部件是最容易使用的小部件。`label` 仅显示一行文本，`button` 小部件在选中时评估 Tcl 脚本，而 `entry` 小部件接受用户输入。

所有 Tcl 小部件创建命令都会返回它们创建的小部件的名称。一种良好的编码技术是将该名称保存在变量中，并通过该变量访问小部件，而不是在代码中硬编码小部件名称。

## 第 8 章 Tk 图形学简介

语法：`label labelName ?option1? ?option2? ...`
`label` 创建一个 `label` 小部件。
`lblName` 该小部件的名称。
`option` `label` 的有效选项包括：

- `-font fontDescriptor`：定义用于此类显示的字体。字体描述符将在第 10 章中讨论。
- `-textvariable varName`：包含显示文本的变量。
- `-text displayText`：要显示的文本。如果也使用了 `-textvariable`，则在小部件创建时该变量将设置为此值。

注意在下面的示例中，选项可以以任何顺序定义。

## 示例 8.6-1

```tk
示例脚本
set txt [label .11 -relief raised -text \
  "Labels can be configured with text"]
pack $txt
set var [label .12 -textvariable label2Var -relief sunken]
```
