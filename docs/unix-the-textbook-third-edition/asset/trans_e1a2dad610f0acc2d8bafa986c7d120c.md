
## 图 3.19 选项菜单选项。

![](img/02e070097d401d3bf7de4bf1c470b267_163_0.png)

![](img/02e070097d401d3bf7de4bf1c470b267_163_1.png)

## 图 3.20 Emacs 定制组。

## 3.3.13.2 使用 Custom 和 <Alt+X> customize 命令更改 Emacs 变量

Emacs 有许多可更改的设置。大多数设置都可以通过更改变量的设置来进行定制，这些变量也称为用户选项。可定制的变量数量庞大，控制着 Emacs 行为的方方面面。另有一类设置此处不涉及，即决定字体、颜色和其他文本属性的 faces。

要浏览和更改设置（包括变量和 faces），请在 Emacs 命令提示符下输入 `<Alt+X> customize`。这会创建一个定制缓冲区，使你可以浏览按逻辑组织的设置列表，编辑并设置这些设置的值，然后永久保存。

定制设置按定制组进行组织。这些组再汇聚成更大的组，直到形成一个名为 Emacs 的主组，如图 3.20 中缓冲区顶部附近所示。

`<Alt+X> customize` 创建的定制缓冲区与图 3.20 类似。

如果你已经知道某个特定设置或定制组的名称并希望定制它，可以使用命令 `<Alt+X> customize-option`、`<Alt+X> customize-face` 或 `<Alt+X> customize-group` 直接前往。

图 3.20 中缓冲区的主要部分显示了“Emacs”定制组，其中包含多个其他子组（如“Editing”“Convenience”等）。每个子组的内容显示在该组的单行描述中。

组的状态显示该组中的设置是否已被编辑、设置或保存。

定制缓冲区的大部分内容不可更改，但它包含许多可编辑字段。例如，在定制缓冲区顶部有一个用于搜索设置的可编辑字段，旁边有一个 Search 按钮。还有一些按钮和链接，你可以通过单击鼠标或移动光标到该处并按 `<Enter>` 来激活。例如，像“[Editing]”这样的组名就是链接；激活其中一个链接会打开该组的另一个定制缓冲区。

在任何特定的定制缓冲区中，你可以按 `<Tab>`（widget-forward）前进到下一个按钮或可编辑字段。按 `<Shift+Tab>`（widget-backward）返回到上一个按钮或可编辑字段。

### 3.3.13.2.1 浏览和搜索设置：

在由 `<Alt+X> customize` 创建的顶层定制缓冲区中，你可以通过链接进入“Emacs”定制组的子组。这些子组可能包含可供你定制的设置；也可能包含更深层的子组，处理 Emacs 中更加专门的子系统。当你在图形界面中浏览定制组的层级结构时，你会发现一些需要根据自己的个人偏好以及想要高效编辑的文本文档的性质来定制的设置。

### 3.3.13.2.2 更改变量：

下面是一个变量（或用户选项）在特定定制缓冲区中的示例。要访问该变量，可以从顶层 emacs 组逐级进入 Editing>Killing 组，然后左键单击指向“Kill Ring Max”文本的小菱形：

```
Kill Ring Max: 60
[State]: STANDARD.
Maximum length of kill ring before oldest elements are thrown away.
```

第一行显示变量名为 kill-ring-max，为了便于查看格式化为“Kill Ring Max”。它的值是 60。在我们的图形显示中，变量名后面的行指示该变量的定制状态；在此示例中，STANDARD 表示你尚未更改该变量，因此其值为默认值。[State] 按钮提供一个用于定制该变量的操作菜单。

定制状态下方是该变量的说明文档。要为 Kill Ring Max 输入新值，只需点击该值右侧并编辑即可。当你开始修改文本时，[State] 行将变为：

```
[State]: EDITED, shown value does not take effect until you set or save it.
```
