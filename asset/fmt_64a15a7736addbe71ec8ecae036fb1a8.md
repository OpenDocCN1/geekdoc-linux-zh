
`win->_idock`

`win->_immed`

`win->_sync`

`win->_use_keypad`

`win->_delay`

```
对于所有布尔元素，值 `TRUE` 会设置相应的位和下述的条件。
`_notimeout` 是一个布尔值，设置时指示 NCurses 不要为 Esc 键按下设置超时时间。此值由 `notimeout()` 函数控制。

`_clear` 是一个布尔值，设置时告诉 NCurses 窗口中的信息需要从头重绘。此设置由 `clearok()` 函数控制。

`_leaveok` 是一个布尔值，设置时告诉 NCurses 不要更新该窗口的光标位置。此设置由 `leaveok()` 函数控制。

`_scroll` 是一个布尔值，设置时告诉 NCurses 窗口内容可以滚动。此设置由 `scroll()` 函数控制。

`_idlock` 是一个布尔值，设置时告诉 NCurses 使用硬件插入/删除行函数。此设置由 `idlock()` 函数控制。

`_idock` 是一个布尔值，设置时告诉 NCurses 使用硬件插入/删除字符函数。此设置由 `idock()` 函数控制。

`_immed` 是一个布尔值，设置时告诉 NCurses 每窗口数据变化时自动调用 `refresh()` 函数。此设置由 `immedok()` 函数控制。

`_sync` 是一个布尔值，设置时告诉 NCurses 每当父窗口数据变化时自动更新子窗口的数据。此设置由 `sync()` 函数控制。

`_use_keypad` 是一个布尔值，设置时告诉 NCurses 解析键盘的小数字区、功能键、光标和其他特殊键。此设置由 `keypad()` 函数控制。

`_delay` 是一个 `int` 值，设置键盘输入延迟。小于0的值将 `getch()` 变为非阻塞调用。大于0的值设置毫秒级延迟。此设置由 `nodelay()` 和 `timeout()` 函数控制。
```

## 窗口数据

```
win->line
```

`_line` 指向一个特殊结构的指针，该结构持有窗口的实际数据，NCurses 开发人员并不希望你干扰这些数据，因此 `WINDOW` 结构中的此元素未被文档。

## 窗口滚动区域

```
win->regtop
win->regbottom
```

变量 `_regtop` 和 `_regbottom` 是两个 `NCURSES_SIZE_T` 值，用于设置窗口内文本滚动区域的顶部和底部。由 `setscrreg()` 函数设置。

## 子窗口数据

```
win->_parx
win->_pary
win->_parent
```

对于子窗口，`_parx` 和 `_pary` 是整数，表示子窗口相对于父窗口的左上角坐标。这些坐标通过 `getparentxy()` 函数返回。
`_parent` 是一个 `WINDOW` 指针，指示父窗口。此值为父窗口结构的地址，而非其名称。参见示例。

## 填充页 Pad 数据

填充页的数据在 `WINDOW` 结构中的 `pdata` 结构中。`pdata` 结构命名为 `_pad` 并按如下所示引用：

```
win->_pad..pad_y
win->_pad..pad_x
win->_pad..pad_top
win->_pad..pad_left
win->_pad..pad_bottom
win->_pad..pad_right
```

窗口中的填充页对应于表 A-20 所示的 `prefetch()` 函数使用的参数。

表 A-20：WINDOW 填充页数据列出的 `prefetch()` 函数参数

| PREFETCH() 参数 | WINDOW 填充页结构元素 |
| :--- | :--- |
| pminrow | _pad..pad_y |
| pmincol | _pad..pad_x |
| sminrow | _pad..pad_top |
| smincol | _pad..pad_left |
| smaxrow | _pad..pad_bottom |
| smaxcol | _pad..pad_right |

## 返回值

不适用。

## 注意事项

显然，通过属性来更改属性是优的。
窗口中的填充页对应于表 A-20 所示的 `prefetch()` 函数使用的参数。

`attrs` 元素是一个 `attr_t` 类型变量，指示应用于窗口中（非空格字符）的属性。`_attrs` 中的位域根据设置的属性进行填充。参见 `attrset()`。`_bkgd` 是一个 `ctype()` 变量，指示分配给窗口的当前背景 ctype（字符和属性）。此值由 `bkgd()` 函数设置。（注：页面 534-536 的 OCR 文本高度重复/损坏。我处理了提供文本中的可用逻辑部分）。

## 示例

```
wnoutrefresh(alpha);
woutrefresh(beta);
woutrefresh(gamma);
doupdate();
```

三个 `wnoutrefresh()` 函数更新来自 alpha、beta 和 gamma 三个窗口的信息。然后 `update()` 函数更新终端。这四条语句比三个对应的 `wrefresh()` 函数更高效。

```
wnoutrefresh(stdscr);
```

在这里，标准屏幕更新到虚拟屏幕。随后的 `doupdate()` 调用将更新终端。

## 示例程序

参见 `doupdate()` 和 `mvwin()` 的条目以获取示例程序和输出。

## 格式参考

`win` 是一个 `WINDOW` 变量，表示屏幕上的一个窗口。
`beg_line` 是一个 `int` 值，指定要更新的屏幕上的某行。取值范围从顶部的 0 开始，一直到 `beg_line` 与窗口底部之间剩余的行数。
`num_lines` 是要更新的行数，从 1 到 `beg_line` 与窗口底部之间所有可用的行数。

# 返回值

失败时返回 `ERR`，成功时返回 `ERR` 以外的数值（通常为 `OK`，但并非总是如此）。

## 注意事项

`wdrawln()` 实际上并不会刷新屏幕。下一次 `refresh()` 命令仅确保被 `wdrawln()` 触碰（touched）的行在屏幕上被完全更新。
`wdrawln()` 替换的行会被完全替换。
`redrawwin()` 用于强制重写整个屏幕。
它等同于 `wdrawln(win, 0, n)`，`win` 是窗口名称，`n` 是窗口的底部行。
我还没有见过这个函数按照描述的那样工作。尽管它看起来确实执行了某些操作，而不仅仅是广告宣传的那样。更好的解决方案是使用以下内容替换 `wdrawln()`：

```
touchwin(stdscr);
touchwin(curscr);
refresh(curscr);
```

## 示例

`wdrawln(stdscr, 0, 11);`

该语句描述标准屏幕的前 12 行需要完全刷新的。

## 示例程序

```
1 #include <ncurses.h>
2 #include <stdlib.h>
3 
4 int main(void)
5   (
6     initscr();
7
8     addstr("I'm just an innocent little program
```

示例输出：

I'm just an innocent little program,
minding my own business...

按 Enter 键在程序输出处写入文本：

RANDOM DATA innocent little program,
minding my own business...

按 Enter 键恢复程序输出：

I'm just an innocent little program,
minding my own business...

（再次说明：这在我尝试过的任何终端或平台上都不起作用，它可能是一个未来会修复的 bug。在此之前，将第 17 行改为 `refresh(curscr)` 可以修复程序，但并未解决 `wdrawln()` 是否正常工作的问题。）

# 另有参考

`wdrawln()`, `refresh()`

# wrefresh()

参见 `refresh()`。

# wsyncdown()

调用 `wsyncdown()` 函数是为了确保在 `win` 中触碰的位置在任何子窗口中也被触碰。

# 手册页格式

```
void wsyncdown(WINDOW *win);
```

## 格式参考

`win` 是一个 `WINDOW` 变量，表示屏幕上的一个窗口。

# 返回值

该函数没有返回值。

## 注意事项

此函数由 `wnoutrefresh()` 函数在内部调用。手动调用此函数通常是不寻常的。

`wsyncdown()` 函数递归地调用指定窗口的所有父窗口。因此，请指定最小的子窗口以同步刷新到所有父窗口。

此函数与 `wsyncup()` 函数无关。

## 示例

```
wsyncdown(pp);
```
