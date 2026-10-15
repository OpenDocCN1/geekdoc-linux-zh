
`new_field` 调用创建一个具有 `height` 行和 `width` 列的新字段。此调用将左上角放置在 (y,x) 坐标 (`toprow`, `leftcol`)。如果字段的任何行应被隐藏，请在 `offscreen` 中传入该数字。`nbufers` 是要与字段关联的额外缓冲区数量。`new_field` 返回指向新字段的指针，如果发生错误则返回 NULL。`free_field` 解除分配与 `field` 相关的资源。成功时返回 `E_OK`，失败时返回 `E_SYSTEM_ERROR` 或 `E_BAD_ARGUMENT`。

`new_form` 创建新表单，将 `fields` 中的字段与其关联并返回指向新表单的指针（如果发生错误则返回 NULL）。同样，`free_form` 释放分配给 `form` 的资源并将其与字段分离。如果 `free_form` 成功，它返回 `E_OK`。发生错误时，它返回 `E_SYSTEM_ERROR`、`E_BAD_ARGUMENT` 或 `E_POSTED`。

`post_form` 在强制 `refresh` 或类似调用后，在其窗口上显示 `form`，而 `unpost_form` 从窗口中擦除表单。`unpost_form` 成功时返回 `E_OK`。如果发生错误，它将返回 `E_SYSTEM_ERROR`、`E_BAD_ARGUMENT`、`E_BAD_STATE`、`E_NO_ROOM`、`E_NOT_POSTED` 或 `E_NOT_CONNECTED` 之一。

`set_field_buffer` 将与 `field` 关联的、由 `buf` 指示的缓冲区设置为字符串 `value`。这些缓冲区由传递给 `new_field` 的 `nbufers` 参数创建。缓冲区 0 是菜单库操纵的那个。其他所有缓冲区都必须由程序员管理。可以通过 `set_field_opts` 设置各种行为选项。字段的所有选项默认都是开启的，因此 `opts` 包含要禁用的选项。表 12.3 列出了可用的选项。

| **选项** | **描述** |
| :--- | :--- |
| `O_VISIBLE` | 显示该字段。 |
| `O_ACTIVE` | 该字段在处理过程中将被访问。不可见的字段不能被访问。 |
| `O_PUBLIC` | 在数据输入期间显示字段内容。 |
| `O_EDIT` | 该字段可被编辑。 |
| `O_WRAP` | 不适合一行显示的单词换行到下一行。 |
| `O_BLANK` | 当在第一个位置输入字符时，该字段将被清空。 |
| `O_AUTOSKIP` | 当一个字段填满时，自动跳过到下一个字段。 |
| `O_NULLOK` | 允许空白字段。 |
| `O_STATIC` | 字段缓冲区固定为字段的原始大小。 |
| `O_PASSOK` | 只有当该字段被修改时才进行验证。 |

`set_field_userptr` 将通过 `userptr` 传递的应用数据关联到 `field`。由于 `userptr` 是一个 void 指针，它可以指向任何类型的指针。要检索此数据，请使用 `field_userptr` 调用，它返回指向 `field` 的指针。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_311_0.png)

以下示例展示了这些调用的大部分用法：

```c
/*
 * useform.c - Simple form usage demo
 */
#include <curses.h>
#include <form.h>
#include <stdlib.h>
#include <ctype.h>     /* for isprint() */
#include "utilfns.h"

int main(void)
{
    FORM *form;
    FIELD *fields[5];
    int ch, i = 0;

    /* start curses */
    app_init();
    cbreak();
    keypad(stdscr, TRUE);

    /* create the form fields */
    fields[0] = new_field(1, 12, 1, 1, 0, 0);
    set_field_buffer(fields[0], 0, "First Name: ");
    set_field_opts(fields[0], field_opts(fields[0]) & ~O_ACTIVE);

    fields[1] = new_field(1, 20, 1, 14, 0, 0);
}
```

```cpp
set_field_userptr(fields[1], NULL);

fields[2] = new_field(1, 12, 2, 1, 0, 0);
set_field_buffer(fields[2], 0, "Last Name : ");
set_field_opts(fields[2], field_opts(fields[2]) & ~O_ACTIVE);

fields[3] = new_field(1, 20, 2, 14, 0, 0);
set_field_userptr(fields[3], NULL);

fields[4] = NULL;

/* create and post the form */
form = new_form(fields);
post_form(form);
refresh();

/* start the command loop */
form_driver(form, REQ_OVL_MODE);
while(toupper(ch = getch()) != KEY_F(10)) {
    if(ch == KEY_UP || ch == KEY_PPAGE)
        form_driver(form, REQ_PREV_FIELD);
    else if(ch == '\n' || ch == KEY_DOWN || ch == KEY_NPAGE)
        form_driver(form, REQ_NEXT_FIELD);
    else if(ch == KEY_BACKSPACE)
        form_driver(form, REQ_DEL_PREV);
    else if(isprint(ch))
        form_driver(form, ch);
    else
        form_driver(form, E_UNKNOWN_COMMAND);
}

unpost_form(form);
free_form(form);
for(i = 0; i < 5; i++)
    free_field(fields[i]);

keypad(stdscr, FALSE);
nocbreak();

app_exit();
exit(EXIT_FAILURE);
}
```

在学习代码中的具体内容之前，请先查看图 12.7，该图展示了该程序的运行效果。不过，如果你编译并运行该程序，会对它的工作原理有更直观的感受。使用下箭头键或 Page Down 键移动到下一个字段，使用上箭头键或 Page Up 键移动到上一个字段，按 F10 键退出。要填写字段，只需输入内容并按 Enter 键即可。

![](img/be588b36b489136ce784030a08a1d3d4_313_0.png)

### 输出

![](img/be588b36b489136ce784030a08a1d3d4_313_1.png)

图 12.7：使用 ncurses 表单库构建的数据输入屏幕。

ncurses 的初始化包括设置 `cbreak` 模式，以便内核允许大部分击键操作直接传递给应用程序而不经过处理。下一个代码块创建了五个字段、两个标签和两个文本输入字段，以及一个 `NULL` 字段来终止字段向量。`fields` 向量是 `post_form` 的参数，该函数创建表单并在调用 `refresh` 后将其显示在屏幕上。

在进入处理所有用户输入的 `while` 循环之前，`form_driver` 为输入字符设置了覆盖模式。除非用户按下 F10，否则应用程序会处理所有输入。按下上箭头键或 Page Up 键（解释为 `KEY_UP` 或 `KEY_PPAGE`）将映射为移动到上一个字段的请求（`REQ_PREV_FIELD`）。类似地，下箭头键和 Page Down 键映射为 `REQ_NEXT_FIELD` 事件请求。该程序还通过将其映射到 `REQ_DEL_PREV` 启用了退格键，该键用于删除前一个字符。按下 F10 时，程序会进行清理并终止。

## 下一步是什么？

在本章中，你完成了对 ncurses 一些高级功能的入门介绍。下一章，“音频 API：OSS/Free”，将继续带你了解 Linux 编程接口的其余部分。

# 13— 音频 API：OSS/Free
