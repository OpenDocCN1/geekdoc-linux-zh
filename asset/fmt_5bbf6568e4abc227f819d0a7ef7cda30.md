
```c
#define XC_X_cursor 0
#define XC_arrow 2
#define XC_based_arrow_down 4
#define XC_based_arrow_up 6
#define XC_boat 8
#define XC_gosility 10
#define XC_bottom_left_corner 12
#define XC_bottom_right_corner 14
#define XC_bottom_side 16
#define XC_box_spiral 18
#define XC_center_ptr 22
#define XC_circle 24
#define XC_clock 26
#define XC_coffee_mug 28
#define XC_cross 30
#define XC_cross_reverse 32
#define XC_crosshair 34
#define XC_diamond_cross 36
#define XC_dot 38
#define XC_dot_box 38
#define XC_double_arrow 40
#define XC_draft_large 42
#define XC_draft_small 44
#define XC_boxed 46
#define XC_exchange 48
#define XC_fleur 50
#define XC_gobbler 52
#define XC_hand 54
#define XC_hand2 56
#define XC_heart 58
#define XC_icon 60
#define XC_iron 62
#define XC_cross_v2 64
#define XC_left 66
#define XC_left_ptr 68
#define XC_left_side 70
#define XC_left_tee 72
#define XC_leftbutton 74
#define XC_1_angle 76
#define XC_lr_angle 78
#define XC_ur_angle 80
#define XC_v_angle 82
#define XC_shuttle 84
#define XC_mouse 86
#define XC_pirate 88
#define XC_plus 90
#define XC_question 92
#define XC_right 94
#define XC_right_ptr 96
#define XC_right_side 98
#define XC_right_tee 100
#define XC_rightbutton 102
#define XC_sail 104
#define XC_box 106
#define XC_sb_down_arrow 108
#define XC_h_double_arrow 110
#define XC_sb_right_arrow 112
#define XC_sb_up_arrow 114
#define XC_v_double_arrow 116
#define XC_sizing 118
#define XC_spider 120
#define XC_star 122
#define XC_target 124
#define XC_trek 126
#define XC_watch 128
#define XC_cross_v3 130
#define XC_top_left_arrow 132
#define XC_top_left_corner 134
#define XC_top_right_corner 136
#define XC_top_side 138
#define XC_top_tee 140
#define XC_trek_v2 142
#define XC_ul_angle 144
#define XC_umbrella 146
#define XC_ur_angle 148
#define XC_watch_v2 150
```

## 附录 C 扩展

由于 X 可以通过扩展来演进，因此确保扩展不被视为二等公民是非常重要的。在某个时刻，你喜欢的扩展可能会被采纳为标准的额外部分。

因此，扩展的使用与核心协议的使用不应该有太大区别。为了避免在应用程序中手动初始化扩展，让扩展执行惰性评估（在第一次调用时自动初始化）也是同样重要的。

本附录描述了编写 Xlib 扩展的技术，这些扩展的运行方式与核心协议相同。

### 注意

预计一个特定的 X 扩展包含多个请求。将 10 个新功能定义为 10 个独立的扩展是不良的做法。相反，应该将它们封装进单个扩展中，并使用子操作码（minor opcodes）来区分这些请求。

用于编写 Xlib 存根（stubs）的符号和宏列在 `<X11/Xlibint.h>`。

### 基本协议支持程序

扩展的基础协议请求是 `XQueryExtension` 和 `XListExtensions`。

```c
Bool XQueryExtension(display, name, major_opcode_return, first_event_return, first_error_return);
```

`display` 指定到 X 服务器的连接。

`name` 指定扩展名称。

`major_opcode_return` 返回主操作码。

`first_event_return` 返回第一个事件代码（如果有）。

`first_error_return` 返回第一个错误代码（如果有）。

`XQueryExtension` 函数判断指定的扩展是否存在。如果扩展不存在，`XQueryExtension` 返回 False；否则，它返回 True。如果扩展存在，`XQueryExtension` 将扩展的主操作码返回给 `major_opcode_return`；否则返回 0。任何子操作码和请求格式都是扩展特定的。如果扩展包含了额外的事件类型，`XQueryExtension` 将基础事件类型代码返回给 `first_event_return`；否则，返回特定扩展的格式。如果扩展包含了额外的错误代码，`XQueryExtension` 将基础错误代码返回给 `first_error_return`；否则返回 0。错误中额外数据的格式是扩展特定的。

### 扩展

如果扩展名称不在主机可移植字符编码（Host Portable Character Encoding）中，结果取决于实现。大小写敏感敏感；字符串 ``thing``、``Thing`` 和 ``thinG`` 都被视为不同的名称。

```c
char **XListExtensions(display, extensions_return);
```

`display` 指定与 X 运行的连接。

`extensions_return` 返回列出的扩展数量。

`XListExtensions` 函数返回服务器支持的所有扩展的列表。服务器返回的数据采用拉丁可移植字符编码（Latin Portable Character Encoding），而返回的字符串则采用主机可移植字符编码。否则，结果取决于实现。

```c
XFreeExtensionList(list);
```

`list` 指定扩展名称列表。

`XFreeExtension` 函数释放由 `XListExtensions` 分配的内存。

### 挂钩到 Xlib

这些函数允许你挂钩（hook）到库中。应用程序程序员通常不会使用这些函数，但它们会被那些需要扩展核心 X 协议和 X 库接口的人员使用。这些为 X 生成协议请求的函数通常是存根函数（stub）。

在扩展中，存根函数首先应该检查是否已经在连接上进行了初始化。如果没有，它们应该调用 `XInitExtension` 尝试在连接上进行初始化。

如果扩展需要被告知 GC/字体的分配或释放，或者该扩展定义了新类型，这里描述的函数允许在这些事件发生时调用该扩展。

`XExtCodes` 结构返回来自 `XInitExtension` 的信息，定义在 `<X11/Xlib.h>` 中。

```c
typedef struct _XExtCodes { /* 扩展，不可更改 */
int extension; /* 扩展号 */
int major_opcode; /* 服务器分配的主操作码 */
int first_event; /* 扩展的第一个事件号 */
int first_error; /* 扩展的第一个错误号 */ /
} XExtCodes;
```

```c
XExtCodes *XInitExtension(display, name);
```
