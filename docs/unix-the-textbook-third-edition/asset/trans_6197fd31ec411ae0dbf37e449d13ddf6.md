

![](img/02e070097d401d3bf7de4bf1c470b267_160_0.png)

## 3.3.13 修改 Emacs 行为

本节描述了自定义和修改 GNU emacs 行为的基本方法。这包括以下操作：

- 使用 Options 菜单修改选项。
- 使用 Custom（基于 GUI 的界面）更改偏好和选项，并结合该界面，同时使用传统的键入 <Alt+X> customize 命令集。
- 使用 abbrev 编写击键缩写。
- 编写击键宏命令，如第 3.3.5 节所示。
- 重新定义键盘按键。
- 编写 emacs Lisp（elisp）代码来自定义 emacs 的行为，并将该代码直接输入到你的 ~/.emacs 启动配置文件中。

所有这些操作都可以对你的 ~/.emacs 启动配置文件进行更改，从而为你提供更定制化和个性化的 emacs 会话，根据你为特定应用程序输入文本的特定需求和方法进行定制。此外，正如将要看到的，elisp 代码是由你所执行的操作生成的。但你实际上不需要知道如何用 elisp 编程的任何细节就能实现所有这些操作！

以下小节描述并举例说明了所有给定的操作。此外，表 3.15 和表 3.16 总结了实现 <Alt+X> customize、击键缩写 abbrev 以及编写击键宏的重要击键。

## TABLE 3.15 Some Ways to Change Emacs Behavior

| Customization Action | Keystrokes |
|---|---|
| Abbrevs | |
| Add global abbrev | <Ctrl+X> a g |
| Add mode-local abbrev | <Ctrl+X> a l |
| Add global expansion for this abbrev | <Ctrl+X> a i g |
| Add mode-local expansion for this abbrev | <Ctrl+X> a i l |
| Explicitly expand abbrev | <Ctrl+X> a e |
| Expand previous word dynamically | <Alt+/> |
| Macros | |
| Start defining a keyboard macro | <Ctrl+X> ( or <F3> |
| End keyboard macro definition | <Ctrl+X> ) or <F4> |
| Execute last-defined keyboard macro | <Ctrl+X> e or <F4> |
| Append to last keyboard macro | <Ctrl+U> <Ctrl+X> ( |
| Name last keyboard macro | <Alt+X> name-last-kbd-macro |
| Insert Lisp definition in buffer | <Alt+X> insert-kbd-macro |
| Customize variables and faces | <Alt+X> customize |
| Simple customization with <Alt+X> customize | |
| (global-set-key (kbd "<Ctrl+<C> g")) | |
| 'search-forward' | |
| (global-set-key (kbd "<Alt+#>")) | |
| 'query-replace-regexp' | |

### 3.3.13.1 Using the Options Menu

自定义 emacs 行为最简单快捷的方法是使用 GNU emacs 下拉菜单中的 Options 选项，如图 3.19 所示。例如，如果你在 Highlight Matching Parentheses 选项旁边打上复选标记，缓冲区中所有匹配的左右括号在你输入时都会被高亮显示。

此选项仅对当前 emacs 会话有效。如果你想在所有未来的 emacs 会话中保留此选项，请做出 Options 菜单选择 Save Options。以下有效的 elisp 行将自动写入你的 ~/.emacs 文件中，位于 custom-set-variables 组下。

```
(show-paren-mode t)
```

### EXERCISE 3.10

显示你将使用的 emacs Help 设施击键序列，以查找 show-paren-mode 选项是什么。然后，列出 Help 设施对 show-paren-mode 选项描述的前几行。

你也可以从 Options 菜单按组进行自定义，如果你做出 Customize Emacs 选择，然后做出其下的任何子选择。例如，如果你做出 Options>Customize Emacs>Top-Level Customization Group 选择，一个新缓冲区将在屏幕上打开，并允许你从所有自定义变量的子组中进行选择。

下一节将展示如何以键入命令的方式实现这种自定义。

## TABLE 3.16 Keystroke Macros

| Keystrokes | Command Name | Action |
|---|---|---|
| <Ctrl+X> ( | kmacro-startmacro | Start macro definition. |
| <F3> | kmacro-startmacro-or-insertcounter | Start macro definition. If pressed while defining a macro, insert a counter. |
| <Ctrl+X> ) | kmacro-end-macro | End macro definition. |
| <F4> | kmacro-end-orcall-macro | End macro definition (if definition is in progress) or invoke last keyboard macro. |
| <Ctrl+X> e | kmacro-end-andcall-macro | Execute last keyboard macro defined. Can type e to repeat macro. |
| <Ctrl+X> <Ctrl+K> n | name-last-kbdmacro | Name the last macro you created (before saving it). |
| (none) | insert-kbd-macro | Insert the macro you named into a file. |
| (none) | macroname | Execute a named keyboard macro. |
| <Ctrl+X> q | kbd-macro-query | Insert a query in a macro definition. |
| <Ctrl+U> <Ctrl+X> q | (none) | Insert a recursive edit in a macro definition. |
| <Ctrl+Alt+C> | exit-recursive-edit | Exit a recursive edit. |
| <Ctrl+X> <Ctrl+K> b | kmacro-bind-tokey | Bind a macro to a key (<Ctrl+X> <Ctrl+K> 0-9 and A-Z are reserved for macro bindings). Lasts for current session only. |
| <Ctrl+X> <Ctrl+K> Space | kmacro-step-editmacro | Edit a macro while stepping through it. |
| <Ctrl+X> <Ctrl+K> l | kmacro-editlossage | Turn the last 100 keystrokes into a keyboard macro. |
| <Ctrl+X> <Ctrl+K> e | edit-kbd-macro | Edit a keyboard macro by typing <Ctrl+X> e for the last keyboard macro defined, <Alt+X> for a named macro, <Ctrl+X> l for lossage, or keystrokes for a macro bound to a key. |
| <Ctrl+X> <Ctrl+K> Enter | kmacro-editmacro | Edit the last keyboard macro. |
| <Ctrl+X> <Ctrl+K> <Ctrl+E> | kmacro-editmacro-repeat | Edit the last keyboard macro again. |
| <Ctrl+X> <Ctrl+K> <Ctrl+T> | kmacro-swap-ring | Transpose last keyboard macro with previous keyboard macro. |
| <Ctrl+X> <Ctrl+K> <Ctrl+D> | kmacro-deletering-head | Delete last keyboard macro from the macro ring. |
| <Ctrl+X> <Ctrl+K> <Ctrl+P> | kmacro-cycle-ringprevious | Move to the previous macro in the macro ring. |
| <Ctrl+X> <Ctrl+K> <Ctrl+N> | kmacro-cycle-ringnext | Move to the next macro in the macro ring. |
| <Ctrl+X> <Ctrl+K> <Ctrl+R> | apply-macro-toregion-lines | Apply this macro to each line in a region. |

