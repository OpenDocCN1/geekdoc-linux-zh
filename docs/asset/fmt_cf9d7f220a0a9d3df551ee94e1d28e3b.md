
### 步骤 4
在用户窗口中点击鼠标，并按下 `Ctrl+X>3`。步骤 3 中的窗口现在应该被垂直分割为两个，向你显示共三个 `newfile` 缓冲区窗口。

### 步骤 5
在帧的下方的窗口中重复步骤 4。你应该有四个显示 `newfile` 缓冲区内容的窗口。你的屏幕显示应该类似于图 3.11。如果你执行步骤 1-4 错误，始终可以使用 `File>Remove Other Windows`（文件>移除其他窗口）下拉菜单选择返回单窗口显示，然后重试。

### 步骤 6
在左上窗口点击鼠标并输入 `1 2 3 4 5`。然后选择下拉菜单 `File>Save As`（文件>另存为）。在屏幕上出现的 `Write file:` 对话框中，在 `Name:` 框中输入 `firstrow`，然后使用 `Name` 对话面板双击文件夹 `multi`。然后选择 `OK`。在名为 `multi` 的目录下创建了一个名为 `firstrow` 的新文件，你仍然看到该缓冲区的四个窗口。

### 步骤 7
在右上窗口点击鼠标，将光标置于 5 之后，使用 `<Backspace>` 或 `<Delete>` 键删除 1, 2, 3, 4 和 5。然后输入 `6 7 8 9 10`。然后选择下拉菜单 `File>Save As`。在屏幕上出现的 `Write file:` 对话框中，在 `Name:` 框中输入 `secondrow`。文件将保存在名为 `multi` 的目录下。

### 步骤 8
在左上窗口点击鼠标，选择下拉菜单 `File>New Window Below`。帧现在应该被水平分割，这样你有堆叠的窗口。

### 步骤 9
在左上窗口点击鼠标，选择下拉菜单 `File>New Window Below`。帧现在应该被水平分割，这样你有堆叠的窗口。

### 步骤 10
在左上窗口点击鼠标，选择下拉菜单 `File>New Window Below`。帧现在应该被水平分割，这样你有堆叠的窗口。

### 步骤 11
在左上窗口点击鼠标，选择下拉菜单 `File>New Window Below`。帧现在应该被水平分割，这样你有堆叠的窗口。

### 步骤 12
在左上窗口点击鼠标，选择下拉菜单 `File>New Window Below`。帧现在应该被水平分割，这样你有堆叠的窗口。

### 步骤 13
在左上窗口点击鼠标，选择下拉菜单 `File>New Window Below`。帧现在应该被水平分割，这样你有堆叠的窗口。

### 步骤 14
最后，当右下窗口处于激活状态时，选择下拉菜单 `File>Save As`。在 `Write file` 对话框中，在 `Name` 框中输入 `fourth`。覆盖旧缓冲区。然后不保存任何缓冲区直接退出 `Emacs`。

## GNU Emacs 编辑器

### 227

#### 表 3.5
更改 Emacs 行为的方法

| 自定义动作 | 按键序列 |
| --- | --- |
| 缩写 (Abbrevs) | |
| 添加全局缩写 | `<Ctrl+X> a g` |
| 添加模式局部缩写 | `<Ctrl+X> a l` |
| 为此缩写添加全局扩展 | `<Ctrl+X> a i` |
| 为此缩写添加模式局部扩展 | `<Ctrl+X> a l` |
| 显式展开缩写 | `<Ctrl+X> a e` |
| 动态展开上一个单词 | `<Alt+/>` |
| 宏 (Macros) | |
| 开始定义键盘宏 | `<Ctrl+X> or <F3>` |
| 结束键盘宏 | `<Ctrl+X> or <F4>` |
| 执行上一次定义的键盘宏 | `<Ctrl+X> e or <F4>` |
| 追加到上一个键盘宏 | `<Ctrl+U> <Ctrl+X>` |
| 为上一个键盘宏命名 | `<Alt+X> name-last-kbd-macro` |
| 将宏列表插入缓冲区 | `<Ctrl+X> insert-kbd-macro` |
| 自定义变量和面 | `<Alt+X> customize` |
| 使用 `<Alt+X> customize` 进行简单自定义 | `(global-set-key (kbd "<Ctrl+C g>") 'search-forward')` `(global-set-key (kbd "<Alt+#>") 'query-replace-regexp')` |

#### 表 3.6
键盘宏

| 按键序列 | 命令名称 | 动作 |
| --- | --- | --- |
| `<Ctrl+X> (<F3>)` | `kmacro-startmacro` | 开始宏定义 |
| | `kmacro-startmacro-or-insertcounter` | 开始宏定义。如果在定义宏期间按下，则插入计数器。 |
| `<Ctrl+X> (<F4>)` | `kmacro-endmacro` | 结束宏定义 |
| | `kmacro-end-callmacro` | 结束宏定义（如果正在定义中）或调用键盘宏。 |
| `<Ctrl+X> e` | `kmacro-endandcallmacro` | 执行上一次定义的键盘宏。可以输入或重复宏。 |
| `<Ctrl+X> <Ctrl+K> n` | `name-last-kbdmacro` | 为你创建的最后一个宏命名（保存之前）。 |
| (无) | `insert-kbd-macro` | 将你命名的宏插入文件 |
| (无) | `macrome` | 执行命名的键盘宏。 |
| `<Ctrl+X> q` | `kbd-macro-query` | 在宏定义中插入一个查询。 |

#### 表 3.6（续）

| 按键序列 | 命令名称 | 动作 |
| --- | --- | --- |
| `<Ctrl+u><Ctrl+X> q` | (无) | 在宏定义中插入递归编辑。 |
| `<Ctrl+u><Alt+C>` | `exit-recursive-edit` | 退出递归编辑。 |
| `<Ctrl+X><Ctrl+K> b` | `kmac-bind-tokey` | 将宏绑定到键上 (`<Ctrl+X=<Ctrl+K> 0-9` 和 `A-Z` 留用于宏绑定)。仅对当前会话有效。 |
| `<Ctrl+X><Ctrl+K> Space` | `kmac-step-editmacro` | 在单步执行时编辑宏。 |
| `<Ctrl+X><Ctrl+X> l` | `kmac-editlossage` | 将最后 100 次按键转换为键盘宏。 |
| `<Ctrl+X><Ctrl+X> e` | `edit-kbd-macro` | 通过输入 `<Ctrl+X>=`（命名宏）、`<Ctrl+H-1`（丢失的宏）或绑定到键的按键序列来编辑键盘宏。 |
| `<Ctrl+X><Ctrl+K> Enter` | `kmac-editmacro` | 编辑上一个键盘宏。 |
| `<Ctrl+X><Ctrl+K> E` | `kmac-macro-repeat` | 再次编辑上一个键盘宏。 |
| `<Ctrl+X><Ctrl+K><Ctrl+T>` | `kmac-swap-ring` | 将上一个键盘宏与上一个键盘宏交换。 |
| `<Ctrl+X><Ctrl+K><Ctrl+D>` | `kmac-deleting-head` | 从宏环中删除最后一个键盘宏。 |
| `<Ctrl+X><Ctrl+K><Ctrl+P>` | `kmac-cycle-ringprevious` | 移动到宏环中的上一个宏。 |
| `<Ctrl+X><Ctrl+K><Ctrl+N>` | `kmac-cycle-ringnext` | 移动到宏环中的下一个宏。 |
| `<Ctrl+X><Ctrl+K><Ctrl+R>` | `kmac-apply-toregion-lines` | 将此宏应用到区域中的每一行。 |

### 3.6.1 使用选项菜单

自定义 Emacs 行为最简单且快速的方法是使用 GNU Emacs 中 `Options`（选项）下的下拉菜单选择，如图 3.14 所示。例如，在 **`Matching Parentheses`**（匹配括号，一个默认选项）旁边打勾时，所有匹配的左右括号都将为你高亮。

你额外添加的勾选仅对当前 Emacs 会话有效。例如，如果你在 `Debug on Error`（错误时调试）选项上打勾，并希望在以后所有的 Emacs 会话中保留该选项，请选择选项菜单中的 **`Save Options`**（保存选项）。第一次执行此选项菜单选择时，以下 `elisp` 值将自动写入：

这些子组可能包含供你自定义的设置；它们也可能包含更多的子组，处理 Emacs 中更专门的子系统。当你通过图形界面导航自定义组的层级结构时，你会发现一些想要根据自己的个人偏好以及你正在高效编辑的文本文档性质进行自定义的设置。

### 3.16.2.2 修改变量

这里是一个变量（或用户选项）在特定自定义缓冲区中的示例。通过进入 `Editing>Killing` 组的顶部 Emacs 组，然后左键点击指向 `Kill Ring Max:` 的小圆形形状可以访问此变量：

`Kill Ring Max:` 60

`[State]: STANDARD.`

在丢弃旧元素之前剪环（kill ring）的最大长度。
