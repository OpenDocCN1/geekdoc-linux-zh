
```text
!!
!! $HOME/.mwmrc
!! Modified system.wmrc for personal changes.
!!
!!
!! Root Description
!!
Menu DefaultRoot
{
 "Root Menu" f.title
 "New Window" f.exec "xterm &"
 "Shuffle Up" f.circle_up
 "Shuffle Down" f.circle_down
 "Refresh" f.refresh
 "Pack Icons" f.pack_icons
! "Toggle Behavior..." f.set_behavior
 no-label f.separator
 "Restart..." f.restart
! "Quit..." f.quit_mwm
}
MenuMenu_1
{
 "Root Menu" f.title
 "New Window" f.exec "xterm &"
 "Shuffle Up" f.circle_up
 "Shuffle Down" f.circle_down
 "Refresh" f.refresh
 "Pack Icons" f.pack_icons
! "Toggle Behavior" f.set_behavior
 no-label f.separator
 "Restart..." f.restart
}
!!
!! Window Description
!!
MenuWindow
{
 "Restore_R" Alt<Key>F5
 "Move_M" Alt<Key>F7
 "Size_S" Alt<Key>F8
 "Minimize_n" Alt<Key>F9
 "Maximize_x" Alt<Key>F10
 "Lower_L" Alt<Key>F3
 no-label f.separator
 "Close_C" Alt<Key>F4
}
!!
!! Key Binding Description
!!
Keys DefaultBindings
{
 Shift<Key>Escape window|f.post_wmenu
 Alt<Key>space window|f.post_wmenu
 Alt<Key>Tab root|f.next_key
 Alt Shift<Key>Tab root|f.prev_key
 Alt<Key>Escape root|f.circle_down
 Alt Shift<Key>Escape root|f.circle_up
 Alt Shift<Key>exclam root|f.set_behavior
 Alt<Key>F6 window.next_key
 Alt Shift<Key>F6 window.prev_key
 Alt<Key>F10 icon f.post_wmenu
 Alt Shift<Key>Delete root|f.restart
}
!!
!! Button Description(s)
!!
Buttons DefaultBindings
{
 <Btn1Down> icon|frame f.raise
 <Btn3Down> icon|frame f.post_wmenu
 <Btn3Down> root f.DefaultRoot
}
Buttons ExplicitButtonBindings
{
 <Btn1Down> icon|frame f.raise
 <Btn3Down> icon|frame f.post_wmenu
 <Btn3Down> root f.DefaultRoot
 <Btn1Up> icon|f.restore
 Alt<Btn1Down> window|f.lower
 Alt<Btn2Down> window|f.resize
 Alt<Btn3Down> window|f.move
}
Buttons PointerButtonBindings
{
 <Btn1Down> icon|frame f.raise
 <Btn3Down> icon|frame f.post_wmenu
 <Btn3Down> root f.DefaultRoot
 <Btn1Down> window f.raise
! <Btn1Up> icon|f.restore
 Alt<Btn1Down> window|f.lower
 Alt<Btn2Down> window|f.resize
 Alt<Btn3Down> window|f.move
}
!!
!! END OF mwm RESOURCE FILE
```

这里有几个关键特性：键绑定、按钮绑定和菜单项。绑定是用户操作与函数之间的映射。键绑定将按键映射到动作，按钮绑定将按钮按下和释放映射到动作。菜单显示菜单项并允许你将动作项组织成节。

所有项的格式为：

```text
Section_type Section_Title
{
.. definitions..
.. definitions..
}
```

其中 `Section_type` 可以是 `Menu`、`Keys` 或 `Buttons`。`Section_Title` 是定义变量名的字符串。它是一个可以在文件其他部分引用此节的名字。

示例文件中显示的函数以 `f.` 关键字开头。有些动作显而易见：`f.move`、`f.resize`、`f.maximize`、`f.minimize`、`f.title`、`f.lower` 等。有些动作并不直观：`f.separator`（在菜单项上显示线条）、`f.circle_up`（向上调整窗口堆叠顺序）、`f.circle_down`（向下调整窗口堆叠顺序）。记住窗口就像堆在画布上的纸。（参见“堆叠顺序”部分）。

查看表 1.1 获取所有可用功能。

**表 1.1. 有效的窗口管理器函数。**

| Function | Description |
| :--- | :--- |
| `f.menu mm` | 将 `mm` 与菜单关联。 |
| `f.minimize` | 将窗口变为图标。 |
| `f.move` | 启用窗口的交互移动。 |
| `f.nop` | 无操作——仅作为占位符。 |
| `f.normalize` | 将窗口恢复到原始大小。 |
| `f.pack_icons` | 重新排列桌面上的图标。 |
| `f.pass_keys` | 切换启用和禁用键绑定。 |
| `f.quit_mwm` | 终止 `mwm`。 |
| `f.raise` | 将窗口置于栈顶端。 |
| `f.refresh` | 重绘所有窗口。 |
| `f.resize` | 启用窗口的交互缩放。 |
| `f.restart` | 重启 `MWM`。 |
| `f.separator` | 绘制线条。 |
| `f.title nn` | 为菜单命名。 |

```text
{
  "Kamran Games" f.title
  no-label f.separator
  "Tetris" f.exec "xtetris &"
  "Mahhjong" f.exec "xmahjong &"
  "Chess" f.exec "xchess &"
}
```

`f.title` 动作指定子菜单的标题。`f.separator` 动作在标题下方绘制一条线。`f.exec` 动作会启动双引号中显示的命令。

**提示：** 注意 `f.exec` 中的安符号 `&`，它用于在后台启动这些任务。不要启动可能永远不会返回的任务，否则可能会导致你的 `MWM` 会话挂起。

现在，你可以通过在 `DefaultRootMenu` 定义中添加以下行，将此新菜单添加到根菜单：

`"Utils" f.menu MyGames`

## 更多关于按钮和按键绑定

按键和按钮绑定的工作方式与菜单相同。第一个明显的区别是额外的一列，包含 `icon`、`frame`、`window` 和 `root` 词。这些词强制绑定到上下文。`root` 指针在根窗口上的任何位置；`frame` 或 `window` 关键字仅当指针在窗口或其边框内时应用绑定；`icon` 绑定则适用于图标。

在你的 `.Xresource` 或 `.Xresources` 文件中，你将如下引用类为 `mwm` 的这些按键绑定：

`Mwm\*keyBindings: DefaultKeyBindings`

以下是按键绑定中的一些描述：

```text
| Shift<Key>Escape window|icon f.post_wmenu |
| Alt<Key>space window|icon f.post_wmenu |
| Alt<Key>Tab root f.menu DefaultRootMenu |
```

击键绑定的语法为：

`modifier<Key>key`

其中 `modifier` 是 Alt、Control 或 Shift。按键可以是组合键或功能键。前两个声明描述相同的动作——显示窗口菜单——但使用了不同的按键。第三个按键绑定显示了显示根菜单的方法。

按钮绑定是你的按钮的绑定。这里有三个重要的绑定需要记住：
