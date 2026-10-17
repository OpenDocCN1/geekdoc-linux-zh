
调用 `raw` 会关闭特殊字符处理，因为此时通过输入特殊字符序列将无法产生信号或流控制。调用 `nocbreak` 将输入模式设回行编辑模式，但保持特殊处理不变；调用 `noraw` 则同时恢复行编辑模式和特殊字符处理。

# 键盘输入

读取键盘非常简单。主要的函数有：

```c
#include <curses.h>

int getch(void);
int getstr(char *string);
int getstr(char *string, int number_of_characters);
int scanf(char *format, ...);
```

这些函数的作用与它们对应的非 `curses` 版本如 `getchar` 非常相似。请注意，`getstr` 没有提供限制返回字符串长度的方法，因此你应该谨慎地使用它。如果你的 `curses` 版本支持 `getstr`（它允许你限制读取的字符数），你应该优先使用它而不是 `getstr`。这与我们在第 3 章中看到的 `fgets` 行为非常相似。

这里有一个短示例程序 `ipmode`，用于展示如何处理键盘。

# 尝试一下——键盘模式与输入

- 1. 首先，我们设置了程序、`<unistd.h>` 以及初始的 `curses` 调用。

```c
#include <unistd.h>
#include <stdlib.h>
#include <curses.h>
#include <string.h>

#define PW_LEN 25
#define NAME_LEN 256

int main() {
    char name[NAME_LEN];
    char password[PW_LEN];
    char *real_password = "xyzzy";
    int i = 0;

    initscr();
    move(5, 10);
    printw("%s", "Please login:");

    move(7, 10);
    printw("%s", "User name: ");
    getstr(name);

    move(9, 10);
    printw("%s", "Password: ");
    refresh();
```

- 2. 当用户输入密码时，我们需要停止密码在屏幕上的回显。然后我们检查 `xyzzy` 之后的密码。

```c
cbreak();
noecho();

memset(password, '0', sizeof(password));
while (i < PW_LEN) {
    password[i] = getch();
    move(9, 20 + 1);
    addch('*');
    refresh();
    if (password[i] == '\n') break;
    if (strcmp(password, real_password) == 0) break;
    ++i;
}
```

- 3. 最后，我们重新启用键盘回显并打印成功或失败。

```c
echo();
nobreak();

move(11, 10);
if (strcmp(password, real_password) == 0) printw("%s", "Correct");
else printw("%s", "Wrong");
refresh();

endwin();
exit(EXIT_SUCCESS);
```

## 工作原理

创建窗口后，我们如何向其写入内容？答案是，我们见过的几乎所有函数都有可以在指定窗口上操作的版本。窗口独立于屏幕，我们可以一次创建多个窗口。

## 窗口

窗口独立于屏幕，我们可以一次创建多个窗口。

```c
#include <curses.h>

int newwin(int width, int height, int y, int x);
int delwin(WINDOW *window);
```

窗口独立于屏幕，我们可以一次创建多个窗口。

# 结构

```c
intrefresh(int y, int x);
int wrefresh(WINDOW *window);
```

窗口独立于屏幕，我们可以一次创建多个窗口。

# 通用函数

我们已经使用了 `addch` 和 `addw` 函数向屏幕添加字符。对于许多其他函数，这些函数也可以加上前缀，例如 `w` 表示窗口（window），`mv` 表示移动（move），或 `mvw` 表示移动和窗口。如果你使用 `curses` 头文件，你会发现我们目前见过的许多函数只是调用这些更通用函数的宏。

## 使用 curses 管理文本的屏幕

```c
int wrefresh(WINDOW *window_ptr);
int wclear(WINDOW *window_ptr);
int werase(WINDOW *window_ptr);
int touchwin(WINDOW *window_ptr);
int scrollock(WINDOW *window_ptr, bool scroll_flag);
int scroll(WINDOW *window_ptr);
```

`mwin` 函数在屏幕上移动窗口。由于窗口的所有部分都必须位于屏幕内，如果你尝试移动窗口以导致其任何部分超出屏幕范围，那么 `mwin` 将执行失败。

`refresh`、`wclear` 和 `werase` 函数仅仅是我们之前遇到过的函数的泛化版本；它们只是使用 `WINDOW` 指针，以便引用特定的窗口，而不是 `stdscr`。

`touchwin` 函数相当特殊。它通知 `curses` 库，其参数所指向的窗口内容已经发生变化。这意味着当下一次调用 `wrefresh` 时，`curses` 总是会重绘该窗口，即使你实际上并没有更改窗口的内容。当你在屏幕上堆叠了多个重叠的窗口时，这个函数对于安排显示哪个窗口非常有用。

两个 `scroll` 函数控制窗口的滚动。当向 `scrollock` 传递布尔值 `true`（通常非零）时，允许窗口滚动。默认情况下，窗口是不可滚的。`scroll` 函数简单地将窗口向上滚动一行。某些滚动实现还带有 `wscroll` 函数，它接受一个滚动的行数作为参数，该数字可以是负数。我们将在本章稍后的部分重新讨论滚动。

## 尝试一下——多窗口

现在我们已经知道了如何管理多个窗口，让我们在程序 `miwl.c` 中这些这些新函数的用场吧。为了简洁起见，省略了错误检查。

- 1. 像往一样，让我们先获取定义：

```c
#include <unistd.h>
#include <stdlib.h>
#include <curses.h>

int main() {
    WINDOW *new_window_ptr;
    WINDOW *popup_window_ptr;
    int x_loop;
    int y_loop;
    char a_letter = 'a';

    initscr();
```

- 2. 然后我们用字符填充基础窗口，一旦逻辑屏幕填充完毕就刷新实际屏幕。

```c
move(5, 5);
printw("%s", "Testing multiple windows");
refresh();
```

```c
for (y_loop = 0; y_loop < LINES; y_loop++) {
  for (x_loop = 0; x_loop < COLS - 1; x_loop++) {
    mvaddch(stdscr, y_loop, x_loop, a_letter);
    a_letter++;
    if (a_letter > 'z') a_letter = 'a';
  }
}
/* 更新屏幕 */
refresh();
sleep(2);
```

- 3. 现在我们创建一个 10 x 20 的窗口，并在将其绘制到屏幕上之前添加一些文本。

```c
new_window_ptr = newwin(10, 20, 5, 5);
mwprintw(new_window_ptr, 2, 2, "%s", "Hello World");
mwprintw(new_window_ptr, 5, 2, "%s",
  "Notice how very long lines wrap inside the window");
wrefresh(new_window_ptr);
sleep(2);
```

- 4. 我们现在更改背景窗口的内容，当我们刷新屏幕时，`new_window_ptr` 指向的窗口被遮挡了。

```c
a_letter = '0';
for (y_loop = 0; y_loop < LINES - 1; y_loop++) {
  for (x_loop = 0; x_loop < COLS - 1; x_loop++) {
    mvaddch(stdscr, y_loop, x_loop, a_letter);
    a_letter++;
    if (a_letter > '9')
    a_letter = '0';
  }
}

refresh();
sleep(2);
```

- 5. 如果我们对新窗口调用刷新，什么都不会发生变化，因为我们没有更改新窗口。

```c
refresh(new_window_ptr);
sleep(2);
```

- 6. 但如果我们先触碰一下窗口再刷新它，欺骗 `curses` 认为窗口已经发生变化，下一次刷新调用将把新窗口带到前面。

```c
touchwin(new_window_ptr);
refresh(new_window_ptr);
sleep(2);
```

- 7. 接下来，我们添加另一个带框的重叠窗口。

```c
popup_window_ptr = newwin(10, 20, 8, 8);
box(popup_window_ptr, '|', '--');
mwprintw(popup_window_ptr, 5, 2, "%s", "Pop Up Window!");
wrefresh(popup_window_ptr);
sleep(2);
```

- 8. 然后在清除和删除它们之前，对新窗口和弹出窗口进行调试。

```c
touchwin(new_window_ptr);
wrefresh(new_window_ptr);
sleep(2);
clear(new_window_ptr);
wrefresh(new_window_ptr);
sleep(2);
delwin(new_window_ptr);
touchwin(popup_window_ptr);
wrefresh(popup_window_ptr);
sleep(2);
delwin(popup_window_ptr);
touchwin(stdscr);
refresh();
endwin();
exit(EXIT_SUCCESS);
}
```

# 第6章

```c
int counter;
char a_letter = '1';
initscr();

for (x_loop = 0; x_loop < COLS - 1; y_loop++) {
  for (y_loop = 0; y_loop < LINES - 1; y_loop++) {
    mvaddch(stdscr, y_loop, x_loop, a_letter);
    a_letter++;
    if (a_letter > '9') a_letter = '1';
    if (a_letter > 'Z') a_letter = 'A';
  }
}
```

- 2. 我们现在创建一个新的滚动子窗口，并且正如建议的那样，在刷新屏幕之前必须“触摸”父窗口。

```c
sub_window_ptr = subwin(stdscr, 10, 20, 10, 10);
scroll(sub_window_ptr, 1);

touchwin(stdscr);
refresh();
sleep(1);
```

- 3. 然后，我们擦除子窗口的内容，向其中打印文本并对其进行刷新。滚动文本是通过一个循环实现的。

```c
erase(sub_window_ptr);
mvprintw(sub_window_ptr, 2, 0, "%s", "This window will now scroll;");
refresh(sub_window_ptr);
sleep(1);

for (counter = 1; counter < 10; counter++) {
  mvprintw(sub_window_ptr, "%s", "This text is both wrapping and scrolling.");
  refresh(sub_window_ptr);
  sleep(1);
}
```

- 4. 完成此循环后，我们删除子窗口。然后我们刷新基础屏幕。

```c
delwin(sub_window_ptr);

touchwin(stdscr);
refresh();
sleep(1);

endwin();
exit(EXIT_SUCCESS);
```

在程序的最后尾，我们看到了图 6-6 所示的输出。

224

# 使用 curses 管理基于文本的场景

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_266_0.png)

图 6-1

## 工作原理

在安排 `sub_window_ptr` 为 `subwin` 用的结果后，我们让子窗口滚动。在子窗口被删除且基础窗口（strscr）被刷新后，屏幕上的文本保持不变。这是因为子窗口实际上是在更新 `strscr` 的字符数据。

# 数字键盘

你已经看到过 `curses` 用于处理键盘的一些功能。许多键盘至少有光标键和功能键。许多键盘还有数字键盘和其他键，如插入键（Insert）和 Home 键。

在大多数终端上，解码这些键是一个困难的问题，因为它们通常发送一个以转义字符开头的字符字符串。应用程序不仅面临区分单按 Escape 键和按下功能键触发的字符字符串的问题，还必须应对不同终端对同一逻辑键使用不同序列的情况。

幸运的是，`curses` 提供了一个用于管理功能键的优雅机制。对于每个终端，每个功能键发送的序列都存储在（通常是）`terminfo` 结构中，而头文件 `.h` 提供了一组由 `KEY_` 开头的定义，这些定义规定了逻辑键。

当光标开始时，序列与逻辑键之间的翻译是被禁用的，必须通过键盘函数开启。如果调用成功，它返回 `OK`，否则返回 `ERR`。

# 第6章

```c
#include <curses.h>

int keypad(WINDOW *window_ptr, bool keypad_on);
```

一旦通过调用 `keypad` 函数并将 `keypad_on` 设置为 `true` 启用了键盘模式，`curses` 就会接管键序列的处理，这样读取键盘现在不仅可以只返回按下的键，还可以返回逻辑键的 `KEY_` 定义之一。

使用 `keypad` 时有三个严格限制：

- 对转义序列的识别取决于时间，许多网络协议会将字符分组为数据包（导致对转义序列的识别不当），或将其分离（导致功能键序列被识别为 Escape 和单个字符）。这种行为在广域网（WAN）和其他繁忙链路上表现最差。唯一的办法是尝试让终端将你想使用的每个功能键映射到单个、唯一的字符，尽管这限制了控制字符的数量。

- 为了让 `curses` 能够区分按下 Escape 键和以 Escape 开头的键盘序列，它必须等待很短的时间。有时，在启用键盘模式后，可以察觉到处理 Escape 键存在微小的延迟。

- `curses` 无法处理非唯一的转义序列。如果你的终端有两个不同的键可以发送相同的序列，`curses` 将简单地忽略该序列，因为它不知道应该返回哪一个逻辑键。

> 在我们看来，为某些键设置转义序列同时在键盘上放置一个 Escape 键（天差地用于取消）是一个非常不幸的设计决策，但我们必须尽力接受并管理它。

# 试一试——使用数字键盘

这里有一个短程序 `keypad.c`，展示了如何使用键盘模式。当你运行此程序时，尝试按下 Escape 键，注意程序时的微小延迟，程序正在等待查看 Escape 是转义序列的开头还是单按键。

- 1. 在初始化程序和 `curses` 库后，我们将键盘模式设置为 `TRUE`。

```c
#include <curses.h>
#include <unistd.h>
#include <stdlib.h>

#define LOCAL_ESCAPE 27

int main() {
    int key;
    initscr();
    keypad(stdscr, TRUE);
```

268

# 使用 curses 管理基于文本的场景

- 2. 接下来，我们关闭回显以防止光标移动。程序等待按键，如果它不是转义序列，则打印该字符。

```c
noecho();
while ((key = getch()) != 'q') {
    if (key != LOCAL_ESCAPE) {
        printch(key);
    }
}
endwin();
exit(0);
```

229

# 第6章

# 颜色

`curses` 对色彩的支持有些特殊之处在于颜色是独立定义的。在使用 `curses` 之前，你必须检查终端是否支持颜色，然后初始化 `curses`。对于这一点，使用函数：`has_colors` 和 `start_color`。

```c
#include <curses.h>

bool has_colors(void);
int start_color(void);
```
