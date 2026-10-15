
```
If you have a two-button mouse, it is most likely of type 1, and if you have a three-button mouse, it can probably support both protocol 1 and 2. There are two main varieties of the latter type: mice with a switch to select the protocol, and mice that default to 1 and require a button to be held at boot-time to select protocol 2. Some mice can be convinced to do 2 by sending a special sequence to the serial port (see the ClearDTR/ClearRTS options).
```

```
Enter a protocol number:
```

这里只是询问你拥有什么类型的鼠标。请注意，如果你有一只带 PS/2 接口的 Microsoft 鼠标，应选择 PS/2 鼠标选项，而不是 Microsoft 选项。Microsoft 选项仅适用于 Microsoft 串行鼠标。Logitech 鼠标也同样适用。如果你有一只来自 Logitech 的 PS/2 鼠标，请选择 PS/2 鼠标选项。需要记住的规则是，如果你拥有任何品牌的 PS/2 风格鼠标，应选择 PS/2；所有 PS/2 鼠标或多或少都相同，你只需担心针对较老、更专有的鼠标类型的特定厂商命名驱动。

对于内置指向设备（轨迹点、触控板等）的笔记本电脑，这些几乎总是也是 PS/2。

然后你将被要求以下问题：

```
If your mouse has only two buttons, it is recommended that you enable Emulate3Buttons.
```

```
Please answer the following question with either 'y' or 'n'.
```

```
Do you want to enable Emulate3Buttons?
```

与倾向于仅使用左右鼠标按钮的 Microsoft Windows 不同，X 使用全部三个按钮。（中间按钮通常用于粘贴已复制到剪贴板上的文本。）如果你只有一只双按钮鼠标，X 可以通过同时点击左右两个按钮来模拟三按钮鼠标。实际上，这通常效果并不好，因此你可能只需购买一只三按钮鼠标。如果你有一只双按钮鼠标，这里只需回答 `y`；如果有一只三按钮鼠标，则回答 `n`。

```
Now give the full device name that the mouse is connected to, for example /dev/tty00. Just pressing enter will use the default, /dev/mouse.
```

```
Mouse device:
```

这里，你需要指定鼠标连接在哪个设备上。如果你有一只 PS/2 鼠标，该设备几乎总是 `/dev/psm0`。建议的默认值 `/dev/mouse` 只有在你为鼠标实际所在的设备创建了符号链接时才有效。如果没有这样做，你将需要指定鼠标实际所在的设备。

对于使用 COM1 或 COM2 端口的串行鼠标，分别使用 `/dev/cuaa0` 或 `/dev/cuaa1`。USB 鼠标将为 `/dev/ums0`。

请从以下键盘类型中选择一个更符合你键盘的描述。如果没有任何一项真正匹配，请选择 1（通用 101 键 PC）

- 1. 通用 101 键 PC
- 2. 通用 102 键（国际）PC
- 3. 通用 104 键 PC
- 4. 通用 105 键（国际）PC
- 5. Dell 101 键 PC
- 6. Everex STEPnote
- 7. Keytronic FlexPro
- 8. Microsoft Natural
- 9. Northgate OmniKey 101
- 10. Winbook Model XP5
- 11. 日本 106 键
- 12. PC-98xx 系列
- 13. 巴西 ABNT2

输入一个数字来选择键盘。

这里你需要选择你拥有的键盘类型。对于大多数现代系统，你将希望选择通用 104 键 PC。如果你的键盘没有位于 Alt 键旁边的 Windows 按钮，你可能只有 101 键键盘；如果是这样，你应选择此选项。注意，像 Microsoft Natural Keyboard 这样的人体工学键盘存在特殊选项。PC-98 是日本标准，在美国不使用。

- 1. 美国英语
- 2. 美国英语 w/ISO9995-3
- 3. 比利时
- 4. 保加利亚
- 5. 加拿大
- 6. 捷克斯洛伐克
- 7. 德语
- 8. 瑞士德语
- 9. 丹麦
- 10. 西班牙
- 11. 芬兰
- 12. 法语
- 13. 瑞士法语
- 14. 英国
- 15. 匈牙利
- 16. 意大利
- 17. 日语
- 18. 挪威

输入一个数字来选择国家。

按 Enter 进入下一页

在此处选择键盘的国家布局。条目多于一屏所能容纳，因此你可以按 Enter 查看更多。当你到达列表末尾时，再次按 Enter 将循环回到列表开头。

下一个问题要求你输入布局的变体名称。只需在此处按 Enter 接受默认值。

```
Please answer the following question with either 'y' or 'n'.
Do you want to select additional XKB options (group switcher,
group indicator, etc.)?
```

除非你熟悉 X 和 UNIX 程序，否则你可能希望在这里选择 `n`。如果选择 `y`，你将有机会重新映射键盘上的某些键并执行各种其他高级设置操作。例如，如果你是 Emacs 大师，你可能想要交换 Caps Lock 键和 Ctrl 键。（Emacs 大量使用 Ctrl 键，许多人发现 Caps Lock 位置更方便。）

你收到的下一条消息将告知你正在进入程序的显示器配置部分。按 Enter 继续下一个问题。

你必须指明显示器的水平同步范围。你可以从下面对应行业标准显示器类型的预定义范围中选择一个，也可以给出特定范围。

```
It is VERY IMPORTANT that you do not specify a monitor type with a horizontal sync range that is beyond the capabilities of your monitor. If in doubt,
choose a conservative setting.
```

`hsync` 单位为 kHz；具有特征模式的显示器类型

| 选择 | hsync | 描述 |
|---|---|---|
| 1 | 31.5 | 标准 VGA，640x480 @ 60 Hz |
| 2 | 31.5 - 35.1 | 超级 VGA，800x600 @ 56 Hz |
| 3 | 31.5, 35.5 | 8514 兼容，1024x768 @ 87 Hz 隔行（无 800x600） |
| 4 | 31.5, 35.5, 37.5 | 超级 VGA，1024x768 @ 87 Hz 隔行，800x600 @ 56 Hz |
| 5 | 31.5 - 37.9 | 扩展超级 VGA，800x600 @ 60 Hz，640x480 @ 72 Hz |
| 6 | 31.5 - 48.5 | 非隔行 SVGA，1024x768 @ 60 Hz，800x600 @ 72 Hz |
| 7 | 31.5 - 57.0 | 高频 SVGA，1024x768 @ 70 Hz |
| 8 | 31.5 - 64.3 | 可实现 1280x1024 @ 60 Hz 的显示器 |
| 9 | 31.5 - 79.0 | 可实现 1280x1024 @ 74 Hz 的显示器 |
| 10 | 31.5 - 82.0 | 可实现 1280x1024 @ 76 Hz 的显示器 |
| 11 | — | 输入你自己的水平同步范围 |

输入你的选择（1-11）：

这个问题涉及本小时开始时讨论的刷新率。再一次，你可能可以从显示器手册中获得此信息。

给你的选项相当通用，可能无法充分利用显示器的功能。如果你知道显示器可以在比列出更高的刷新率下显示所列分辨率，你可能希望选择允许你指定自己的水平同步范围的选项。如果这样做，你将被要求输入显示器的水平和垂直同步范围：
