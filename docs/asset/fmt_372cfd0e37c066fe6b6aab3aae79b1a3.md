
该语句触碰了窗口 `pp` 中的所有位置，并检查是否有父窗口，以便在这些窗口中也触碰相同的更改位置。再次，`refresh(pp)` 命令会执行相同的操作，因此很少需要使用此命令。

## 示例程序

不适用。

# 另有参考

```
wnoutrefresh()
```

# `wsyncup()`

`wsyncup()` 函数触碰子窗口父窗口中在子窗口中已更改的位置。

# 手册页格式

```
void wsyncup(WINDOW *win);
```

## 格式参考

`win` 是一个 `WINDOW` 子窗口名称。

# 返回值

此函数没有返回值。

## 注意事项

每当 Ncurses 使用 `mvwin()` 函数重新定位子窗口时，都会在内部调用 `wsyncup()`。

当任何窗口发生变化时，此函数都可能被自动调用。更多信息请参见 `synock()`。鉴于子窗口与其父窗口共享内存，`wsyncup()` 似乎有些多余。

## 示例

```
wsyncup(baby);
```

该语句也触碰了所有父窗口中子窗口 `baby` 内部的所有已更改的位置。

## 示例程序

不适用。

# 另有参考

`synock()`, `refresh()`

# `wtimeout()`

参见 `timeout()`。

# `wtouchlin`

`wtouchlin()` 函数将特定窗口中的一个或多行标记为需要在屏幕上更新或不需要更新。（关于窗口部分如何被触碰并需要更新的更多信息请参考 `refresh()` 条目。）

# 手册页格式

```
int wtouchlin(WINDOW *win, int y, int n, int changed);
```

## 格式参考

- `win` 是一个 `WINDOW` 变量，指示 `wtouchlin()` 函数影响的窗口。
- `y` 是要标记为已触碰或未触碰的起始行。
- `n` 表示包含该行在内标记为已触碰或未触碰的行数。取值范围从 1 到该行与窗口底部之间的行数。
- `changed` 是 1 或 0。当 `changed` 为 1 时，指定的行被标记为已触碰，并在下一次调用 `wrefresh()` 时更新。当 `changed` 为 0 时，指定的行被标记为最新或未触碰。

# 返回值

该函数在失败时返回 `ERR`；成功时返回除 `ERR` 以外的 `int` 值。

## 注意事项

`wtouchlin()` 标记特定窗口中的一个或多行，为需要在屏幕上更新或不需要更新。

`wtouchlin()` 标记特定窗口中的一个或多行，为需要在屏幕上更新或不需要更新。（参考 `refresh()` 条目获取有关窗口部分如何被触碰并需要更新的更多信息。）

`wtouchlin()` 标记特定窗口中的一个或多行，为需要在屏幕上更新或不需要更新。

`wtouchlin()` 标记特定窗口中的一个或多行，为需要在屏幕上更新或不需要更新。（参考 `refresh()` 条目获取有关窗口部分如何被触碰并需要更新的更多信息。）

`wtouchlin()` 标记特定窗口中的一个或多行，为需要在屏幕上更新或不需要更新。

`w lin 0`

## 示例程序

```
#include <ncurses.h>

#include <stdlib.h>

int main(void)

  (

    initscr();

    addstr("I'm just an innocent little program
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

# `wrefresh()`

参见 `refresh()`。

# `wsyncdown()`

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

该语句触碰了窗口 `pp` 中的所有位置，并检查是否有父窗口，以便在这些窗口中也触碰相同的更改位置。再次，`refresh(pp)` 命令会执行相同的操作，因此很少需要使用此命令。

## 示例程序

不适用。

# 另有参考

```
wnoutrefresh()
```

# `wsyncup()`

`wsyncup()` 函数触碰子窗口父窗口中在子窗口中已更改的位置。

# 手册页格式

```
void wsyncup(WINDOW *win);
```

## 格式参考

`win` 是一个 `WINDOW` 子窗口名称。

# 返回值

此函数没有返回值。

## 注意事项

每当 Ncurses 使用 `mvwin()` 函数重新定位子窗口时，都会在内部调用 `wsyncup()`。

当任何窗口发生变化时，此函数都可能被自动调用。更多信息请参见 `synock()`。鉴于子窗口与其父窗口共享内存，`wsyncup()` 似乎有些多余。

## 示例

```
wsyncup(baby);
```
