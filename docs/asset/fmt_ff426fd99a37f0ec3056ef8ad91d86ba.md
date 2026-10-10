
从列表中选择你的键盘，由于代码较旧，请选择最接近的匹配，右键点击按键弹出菜单并选择 `Edit`（编辑）。“`Edit Key`”对话框如图 7.1 (`img/a06369af5597deead612a49ccaa3_126.png`) 所示。与相关修饰符相关的 `Keysym`，在这种情况下，按下控制键后修饰符将 `Control`。对于 `F3`，选择一个字符集，然后对所有合适的按键执行 `Repeat`（重复）。图 7.2 显示了编辑 `F13` 键定义的对话框。图 7.3 显示了显示输出的消息框。从命令行或启动脚本的一部分运行 `xmodmap -n` 来调用键盘更改。(`img/a06369af5597deead612a49ccaa3_127.png`)

| 代码的 `Keysym` | 修饰符 | 字符集 | `Keysym` |
|---|---|---|---|
| `Keysym 1`: `F13` | `Shift` | `Latin1` | `F10` |
| `Keysym 2`: `F13` | `Ctrl+Shift+Alt` | `Latin2` | `F11` |
| `Keysym 3`: `F13` | `Control` | `Latin3` | `F12` |
| `Keysym 4`: `NoSymbol` | | `Latin4` | `F13` |
| `Keysym 5`: `NoSymbol` | `mod2` | `Arabic` | `F14` |
| `Keysym 6`: `NoSymbol` | `mod3` | `Greek` | `F15` |
| `Keysym 7`: `NoSymbol` | `Cyrillic` | `F16` |
| `Keysym 8`: `NoSymbol` | `mod5` | `Technical` | `F17` |

`AutoRepeat`: `Yes`

虽然 `XKeyCaps` 并不是一个美的应用程序，但它可以将键盘重映射到你需要的或想要的任何内容。你对键映射的这种全局更改将影响所有在图形模式下运行的程序。

### 7.1.4 应用程序本地化键映射更改

`xterm` 存在一种应用程序本地化方法，可以使用其键映射和翻译仅在 `xterm` 内部重映射按键。`xterm` 将一组物理按键按下翻译为另一个按键序列在文本流中的输入。一个为你执行映射的脚本允许创建一个新命令 `vmstream`，以便使用正确的键映射连接到 `VMS` 机器，而不影响任何其他程序。这种方法是首选的，并在 `xterm` FAQ (`http://dickey.com/xterm/xterm.faq.html`) 中充分讨论，那里还列出了与以下不同的脚本。然而，你应该注意某些相似之处，因为执行此过程的方法只有几种。此脚本将映射表 7.1 所示的按键。(`img/a06369af5597deead612a49ccaa3_127_1.png`)

#### 表 7.1 键映射脚本

| 键 | 映射 |
|---|---|
| `Shift F3` | `F13` |
| `Shift F4` | `F14` |
| `Shift F5` | `F15 (Help)` |
| `Shift F6` | `F16 (Do)` |
| `Shift F7` | `F17` |
| `Shift F8` | `F18` |
| `Shift F9` | `F19` |
| `Shift F10` | `F20` |
| `Shift F11` | `F21` |
| `Shift F12` | `F22` |
| `Shift F13` | `F23` |
| `Shift F14` | `F24` |
| `Shift F15` | `F25` |
| `Shift F16` | `F26` |
| `Shift F17` | `F27` |
| `Shift F18` | `F28` |
| `Shift F19` | `F29` |
| `Shift F20` | `F30` |
| `Insert` | `Insert` |
| `Delete` | `Delete` |
| `Home` | `Home` |
| `End` | `End` |
| `Page Up` | `Page Up` |
| `Page Down` | `Page Down` |
| `Up` | `Up` |
| `Down` | `Down` |
| `Left` | `Left` |
| `Right` | `Right` |
| `Print Screen` | `Print Screen` |
| `Backspace` | `Backspace` |
| `Enter` | `Enter` |
| `Tab` | `Tab` |
| `Space` | `Space` |
| `/` | `/` |
| `\` | `\` |
| `-` | `-` |
| `*` | `*` |
| `+` | `+` |
| `'` | `'` | `"` |
| `<` | `<` |
| `>` | `>` |
| `=` | `=` |
| `,` | `,` |
| `.` | `.` |
| `;` | `;` |
| `[` | `[` |
| `]` | `]` |
| `{` | `{` |
| `}` | `}` |
| `0` | `0` |
| `1` | `1` |
| `2` | `2` |
| `3` | `3` |
| `4` | `4` |
| `5` | `5` |
| `6` | `6` |
| `7` | `7` |
| `8` | `8` |
| `9` | `9` |
| `F1` | `F1` |
| `F2` | `F2` |
| `F3` | `F3` |
| `F4` | `F4` |
| `F5` | `F5` |
| `F6` | `F6` |
| `F7` | `F7` |
| `F8` | `F8` |
| `F9` | `F9` |
| `F10` | `F10` |
| `F11` | `F11` |
| `F12` | `F12` |
| `F13` | `F13` |
| `F14` | `F14` |
| `F15` | `F15` |
| `F16` | `F16` |
| `F17` | `F17` |
| `F18` | `F18` |
| `F19` | `F19` |
| `F20` | `F20` |

#### 表 7.1 键映射脚本（续）

| 键 | 映射 |
|---|---|
| `KP_0` | `0` |
| `KP_1` | `1` |
| `KP_2` | `2` |
| `KP_3` | `3` |
| `KP_4` | `4` |
| `KP_5` | `5` |
| `KP_6` | `6` |
| `KP_7` | `7` |
| `KP_8` | `8` |
| `KP_9` | `9` |
| `KP_Enter` | `Enter` |
| `KP_Minus` | `-` |
| `KP_Multiply` | `*` |
| `KP_Add` | `+` |
| `KP_Divide` | `/` |
| `KP_Decimal` | `.` |
| `KP_Up` | `Up` |
| `KP_Down` | `Down` |
| `KP_Left` | `Left` |
| `KP_Right` | `Right` |
| `KP_Insert` | `Insert` |
| `KP_Delete` | `Delete` |
| `KP_Home` | `Home` |
| `KP_End` | `End` |
| `KP_PageUp` | `Page Up` |
| `KP_PageDown` | `Page Down` |

```
#!/bin/sh

xterm -title "VMStream" -geometry 80x24

xmodmap -e "clear lock"

xmodmap -e "clear shift"

xmodmap -e "add mod4 = F13"

xmodmap -e "add mod5 = F14"

xmodmap -e "add mod6 = F15"

xmodmap -e "add mod7 = F16"

xmodmap -e "add mod8 = F17"

xmodmap -e "add mod9 = F18"

xmodmap -e "add mod10 = F19"

xmodmap -e "add mod11 = F20"

xmodmap -e "add mod12 = F21"

xmodmap -e "add mod13 = F22"

xmodmap -e "add mod14 = F23"

xmodmap -e "add mod15 = F24"

xmodmap -e "add mod16 = F25"

xmodmap -e "add mod17 = F26"

xmodmap -e "add mod18 = F27"

xmodmap -e "add mod19 = F28"

xmodmap -e "add mod20 = F29"
```
