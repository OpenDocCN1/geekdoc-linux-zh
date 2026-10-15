
如果你已经知道某个特定设置或定制组的名称并希望定制它，可以使用命令 `<Alt+X> customize-option`、`<Alt+X> customize-face` 或 `<Alt+X> customize-group` 直接前往。

图 3.20 中缓冲区的主要部分显示了“Emacs”定制组，其中包含多个其他子组（如“Editing”“Convenience”等）。每个子组的内容显示在该组的单行描述中。

组的状态显示该组中的设置是否已被编辑、设置或保存。

定制缓冲区的大部分内容不可更改，但它包含许多可编辑字段。例如，在定制缓冲区顶部有一个用于搜索设置的可编辑字段，旁边有一个 Search 按钮。还有一些按钮和链接，你可以通过单击鼠标或移动光标到该处并按 `<Enter>` 来激活。例如，像“[Editing]”这样的组名就是链接；激活其中一个链接会打开该组的另一个定制缓冲区。

在任何特定的定制缓冲区中，你可以按 `<Tab>`（`widget-forward`）前进到下一个按钮或可编辑字段。按 `<Shift+Tab>`（`widget-backward`）返回到上一个按钮或可编辑字段。

### 3.3.13.2.1 浏览和搜索设置

在由 `<Alt+X> customize` 创建的顶层定制缓冲区中，你可以通过链接进入“Emacs”定制组的子组。这些子组可能包含可供你定制的设置；也可能包含更深层的子组，处理 Emacs 中更加专门的子系统。当你在图形界面中浏览定制组的层级结构时，你会发现一些需要根据自己的个人偏好以及想要高效编辑的文本文档的性质来定制的设置。

### 3.3.13.2.2 更改变量

下面是一个变量（或用户选项）在特定定制缓冲区中的示例。要访问该变量，可以从顶层 emacs 组逐级进入 `Editing>Killing` 组，然后左键单击指向“Kill Ring Max”文本的小菱形：

```
Kill Ring Max: 60
[State]: STANDARD.
Maximum length of kill ring before oldest elements are thrown away.
```

第一行显示变量名为 `kill-ring-max`，为了便于查看格式化为“Kill Ring Max”。它的值是 60。在我们的图形显示中，变量名后面的行指示该变量的定制状态；在此示例中，`STANDARD` 表示你尚未更改该变量，因此其值为默认值。`[State]` 按钮提供一个用于定制该变量的操作菜单。

定制状态下方是该变量的说明文档。要为 Kill Ring Max 输入新值，只需点击该值右侧并编辑即可。当你开始修改文本时，`[State]` 行将变为：

```
[State]: EDITED, shown value does not take effect until you set or save it.
```

编辑值并不会立即生效。要使其生效，必须通过左键单击 `[State]` 按钮并选择 `Set for Current Session` 来设置变量。

然后变量的状态变为：

`[State]: SET for current session only.`

此时，你可以进行菜单选择 `Save for Future Sessions`。

此外，你不必担心指定一个无效的值；`Set for Current Session` 操作会检查有效性，并且不会安装不可接受的值。

当你设置一个变量时，新值仅在当前 emacs 会话中生效。要将值保存到未来会话，请使用 `[State]` 按钮并选择 `Save for Future Sessions` 操作。保存自定义设置是通过将 elisp 代码写入文件来实现的，最常见的是你的 `~/.emacs` 文件。未来的 emacs 会话在启动时会自动读取此文件，从而再次调用并建立自定义设置。

你也可以通过使用 `[State]` 按钮并选择 `Erase Customization` 菜单选项来将变量恢复为其标准值。重置操作有四种，如下所示。

- `Undo edits`: 如果你已修改但尚未设置变量，则此操作会将自定义缓冲区中的文本恢复为与实际值相匹配。
- `Reset to saved`: 这会将变量的值恢复为上次保存的值，并相应地更新文本。
- `Erase customization`: 这会将变量设置为其标准值。你已有的任何保存值也会被删除。
- `Set to backup value`: 这会将变量设置为在此会话中在自定义缓冲区中设置过的一个先前值。如果你自定义了一个变量然后将其重置，从而丢弃了自定义值，你可以使用此操作再次取回被丢弃的值。

有时记录特定自定义的注释很有用。使用 `[State]` 菜单中的 `Add Comment` 项来创建输入注释的字段。

### 3.3.13.2.3 Globally Saving Customizations for a Group

在任何组的自定义缓冲区的顶部，你可以通过选择 `[Apply]` 或 `[Apply and Save]` 按钮来保存该组缓冲区中显示的所有自定义设置。 `[Apply]` 仅为当前会话保存，而 `[Apply and Save]` 通过在 `~/.emacs` 文件中放入 elisp 代码来相应地修改 `~/.emacs` 文件，从而为未来会话保存。

### 3.3.13.2.4 More about Emacs Variables

变量是一个具有值的 elisp 符号。符号的名称是变量名。变量名可以包含可在文件中出现的任何字符，但大多数变量名由用连字符分隔的普通单词组成。

变量的名称描述了其在 emacs 环境中的作用。大多数变量还具有文档字符串，描述了变量的用途、应具有的值类型以及将如何使用该值。

你可以使用帮助命令 `<Ctrl+H> v Describe variable: somevariablename` in the minibuffer 来查看变量的文档，例如 `somevariablename`。要使用此功能，输入命令 `<Ctrl+H> v`；系统会在 minibuffer 中提示你 `Describe variable:`；然后输入变量名，例如 `somevariablename`，并按 `<Enter>`。

Elisp 使用变量进行内部记录，但如前所述，对不会专门编写 elisp 程序的用户而言最有趣的变量是那些供用户更改的变量——这些称为可自定义变量或用户选项。

Elisp 允许任何变量（有少数例外）具有任何类型的值。然而，许多变量只有在赋予特定类型的值时才有意义。例如，如第 3.3.13.2.2 节所示，只有数字才是 `kill-ring-max` 的有意义值，它指定 kill ring 的最大长度；如果你将 `kill-ring-max` 分配一个文本字符串作为值，则诸如 `<Ctrl+Y>`（yank）之类的命令会发出错误。另一方面，一些变量并不关心你分配给它们的值的类型或种类；例如，如果一个变量对 `nil` 值有一种效果，对非 `nil` 值有另一种效果，那么任何不是符号 `nil` 的值都会引发第二种效果，而不管其类型如何（按惯例，我们通常使用值 `t`——代表“真”的符号——来指定非 `nil` 值）。如果你使用自定义缓冲区设置变量，就不必担心赋予它无效的类型：自定义缓冲区通常只允许你输入有意义的值。如有疑问，请使用 `<Ctrl+H> v Describe variable: somevariablename` 来检查变量的文档字符串，以了解它期望的值类型。

### 3.3.13.2.5 Examining and Setting Variables

以下是如何检查和设置用户选项值的一些示例。此语法的第一个一般形式是：

```
<Ctrl+H> v variablename <Enter>
```

此一般形式使用 emacs 帮助函数，带 `v` 选项，并显示变量 `variablename` 的值和文档。

第二个一般形式实现了变量值的更改：

```
<Alt+X> set-variable <ENTER> var <ENTER> value <ENTER>
```

这会将变量 `var` 的值更改为 `value`。

它读取你在 minibuffer 中输入的变量名，并提供补全，并显示变量的值和文档。例如：

```
<Ctrl+H> v fill-column <ENTER>
```

一个新的缓冲区打开并显示以下内容：

```
fill-column is a variable defined in 'C source code'.
```

其值为 70

设置后会自动变为缓冲区本地变量。

如果满足以下谓词，则该变量可作为文件本地变量安全使用

其值

为 `'integerp'`.

文档：

自动换行应发生的列。

交互式地，你可以用 `<Ctrl+X> f` 设置本地值

你可以自定义此变量。

点击下划线文字 customize，你可以使用一个缓冲区来更改此变量的值。

设置特定可定制变量最方便的按键方法是输入 `<Alt+X> set-variable`。这会使用 minibuffer（带补全）读取变量名，然后再次在 minibuffer 中读取你输入的新值的 elisp 表达式（你可以通过 `<Alt+N>` 将旧值插入 minibuffer 进行编辑）。例如：
