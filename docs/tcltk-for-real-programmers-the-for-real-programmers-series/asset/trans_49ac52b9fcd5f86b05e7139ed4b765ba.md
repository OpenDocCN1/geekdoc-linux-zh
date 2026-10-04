

# 第 11 章. Tk 大组件 (Megawidgets)

option value?

tk_getSaveFile 大组件支持与 tk_getOpenFile 控件相同的选项。

- *tk_messageBox*
在几种定义的样式之一创建一个对话框窗口。返回被点击按钮的名称。
该组件会创建一个新窗口，该窗口将获取焦点，直到与此组件的交互完成为止。

语法: tk_messageBox ?option value?

tk_dialog
创建一个带有消息的新窗口。当按钮被点击时，窗口将由于销毁，并且被点击的按钮的值将返回给创建此组件的脚本。该组件的选项包括：
- -message 要在框中显示的消息。
- -title 显示在窗口边框中的标题。
- -type 要创建的消息框类型。消息框的类型将决定创建哪些按钮。可选类型有：
- abortretry 显示三个按钮：取消（abort）、重试（retry）和忽略（ignore）。
- ok 显示一个按钮：确定（ok）。
- okcancel 显示两个按钮：确定（ok）和取消（cancel）。
- retrycancel 显示两个按钮：重试（retry）和取消（cancel）。
- yesno 显示两个按钮：是（yes）和否（no）。
- yesnocancel 显示三个按钮：是（yes）、否（no）和取消（cancel）。

## 11.1 标准对话框控件

tk_dialog
创建一个对话框，并等待行中提供的文本标签的一个或多个按钮。当用户点击按钮时，第一个按钮编号为 "0"。如果用户销毁窗口，则返回 "-1"。该组件会在屏幕中心创建一个新窗口，并禁用调用它的任务中的其他窗口。

语法: tk_dialog win title bitmap default string
- -win 对话框的名称。
- -title 放置在新窗口边框中的字符串。窗口是否带边框显示取决于你使用的窗口管理器。
- -text 在消息框中显示的文本。
- -bitmap 如果此非空字符串，则必须是一个位图对象或文件名（而不是图像对象）以供显示。
- -default 描述该窗口默认按钮选择的数值。按钮从 0 开始编号。
- -string 放置在按钮中的字符串。

- tk_megawidget 在显示器的给定位置（不局限于窗口内）创建一个弹出菜单窗口。菜单带有撕离（tearoff）条目出现并获取焦点。注意，这不是一个模态组件。tk_popup 之后的命令将立即执行；它不会等待用户从此组件中选择项目。以下示例显示了绑定到左键的弹出菜单，根据文本组件的内容显示问题。

**语法：** tk_popup menu x y entry（注：此处原文为 entry 似乎是笔误，根据上下文应为坐标值，但按要求保留原文或翻译逻辑，此处保持原样） -> 修正：**语法：** tk_popup menu x y entry

tk_popup
在显示器的某处创建一个弹出菜单。这不需要在 Tcl/Tk 窗口内。
- -menu 之前定义的菜单对象。
- -x 屏幕坐标中菜单的 x 和 y 坐标。
- -entry 定义菜单中位置的数值。定义的位置将被选中（激活），且菜单将带有条目放置在请求的 x, y 位置。

示例
```tcl
proc question {} {
  global var
# Remove any existing .m menu.
# Use catch in case there is no previous .m menu.
catch (destroy .m)
# Create a menu for this popup selector
menu .m
.m add radiobutton \
  -label "This dialog is from Abbot & Costello's 'Who's on First?' routine" \
  -variable var -value 1
.m add radiobutton \
  -label "This dialog is from War_and_Peace_" \
  -variable var -value 2
.m add radiobutton -label \
  "This dialog is from Monty Python's Parrot sketch" \
  -variable var -value 3

# Get the size and location of this window with the "winfo"
# command, which returns the geometry as
# WIDTHHEIGHT+XPOS+YPOS
# The scan command is similar to the C standard library "sscanf" function.
scan [winfo geometry .] "%dx%d+%d+%d" \
  width height xpos ypos

# Put the popup near the bottom, right hand edge of the parent window.
tk_popup .popup [expr $xpos + ($width/2) + 50] \
  [expr $ypos + $height - 40] 1

# Create a text window, display it, and insert some text from a famous dialog.
text .t -height 12 -width 75
pack .t
set dialog {
  "C: Tell me the names of the ballplayers on this team.\n"
  "A: We have Who's on first, What's on second, I'm third.\n"
  "C: I'm asking you who is on first.\n"
  "A: Who's on first.\n"
  "C: I'm asking you who is on second.\n"
  "A: What's on second.\n"
  "C: I'm asking you who is on third.\n"
  "A: I'm third.\n"
  "C: I don't understand who is on first.\n"
  "A: That's right.\n"
  "C: Give me the name of first.\n"
  "A: Who's on first.\n"
  "C: Give me the name of second.\n"
  "A: What's on second.\n"
  "C: Give me the name of third.\n"
  "A: I'm third.\n"
  "C: Now you tell me who is on first.\n"
  "A: Who's on first.\n"
  "C: Now you tell me who is on second.\n"
  "A: What's on second.\n"
  "C: Now you tell me who is on third.\n"
  "A: I'm third.\n"
}
insert .t 0.0 $dialog
```

## 11.2 Tk 大组件

- tk_messageBox 在几种定义的样式之一创建一个对话框窗口。返回被点击按钮的名称。
- tk_dialog 创建一个新窗口，该窗口将获取焦点，直到与此组件的交互完成为止。
- tk_megawidget 在显示器的给定位置创建一个弹出菜单窗口。

### 11.2.1 在应用程序窗口显示
标准发行包含的许多组件组件加载到应用程序窗口时非常有用，但某些作为顶层窗口显示更好。

### 11.2.2 模态与非模态操作
标准发行中的大多数大组件以模态方式运行，在用户完成交互之前冻结其他活动。在某些情况下这是恰当的而在其他情况下则不是。

### 11.2.3 控件访问约定
大组件可以构建为模拟标准控件的行为（如本章后续示例所示），也可以遵循它们自己的约定。

### 11.2.4 控件框架
大组件有一个包含其子控件的父框架。该框架可以由创建命令创建，也可以由调用过程提供。

### 11.2.5 配置
当你设计大组件时选择的默认值可能并不是下一个使用该库的人所需要的。

