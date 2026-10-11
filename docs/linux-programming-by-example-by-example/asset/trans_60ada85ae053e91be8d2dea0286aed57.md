

```c
else
    status("Record added");
    break;
case KEY_F(3): /* F3 - Delete a record */
    del(kbuf);
    ret = del_rec(kbuf);
    if (ret > 0)
        status("Key not found");
    else if (ret < 0)
        status("Unknown error occurred");
    else
        status("Record deleted");
    break;
case KEY_F(4): /* F4 - Find a record */
    find(kbuf);
    memset(&value, 0, sizeof(DBT));
    ret = find_rec(kbuf, &value);
    if (ret > 0)
        status("Key not found");
    else if (ret < 0)
        status("Unknown error occurred");
    else {
        status("Record located");
        sprintf(vbuf, "%.*s",
                (int)value.size, (char *)value.data);
        show(kbuf, vbuf);
    }
    break;
case KEY_F(5): /* F5 - Get a record */
    get(kbuf);
    memset(&value, 0, sizeof(DBT));
    ret = get_rec(kbuf, &value);
    if (ret > 0)
        status("Key not found");
    else if (ret < 0)
        status("Unknown error occurred");
    else {
        status("Record located");
        sprintf(vbuf, "%.*s",
                (int)value.size, (char *)value.data);
        show(kbuf, vbuf);
    }
    break;
case KEY_F(6): /* F6 - List all records */
    if ((cnt = count_recs()) == 0) {
        status("No records in database");
        break;
    }
    /* Size a table of pointers */
    if ((keys = malloc(sizeof(DBT *) * cnt)) == NULL)
        status("Memory error");
    if ((values = malloc(sizeof(DBT *) * cnt)) == NULL)
        status("Memory error");
    /* Size each pointer in the table */
    for (i = 0; i < cnt; ++i) {
        if ((keys[i] = malloc(BUFSZ)) == NULL) {
            status("Memory error");
            break;
        }
        if ((values[i] = malloc(BUFSZ)) == NULL) {
            status("Memory error");
            break;
        }
    }
    /* Get all of the records */
    ret = list_recs(keys, values);
    if (ret == 0) {
        status("Problem with database manager");
        break;
    }
    /* Show 'em on the screen */
    for (i = 0; i < cnt; ++i) {
        sprintf(kbuf, "%.*s", (int)strlen(keys[i]), keys[i]);
        sprintf(vbuf, "%.*s", (int)strlen(values[i]), values[i]);
        list(kbuf, vbuf, i);
    }
    status("Last record displayed");
    break;
default: /* Bad keystroke, nag user */
    status("Key not defined");
    break;
} /* End switch(fkey) */

close_db(); /* Close the database */
close_scrn(); /* Close curses subsystem */
exit(EXIT_SUCCESS);
}

/*
 * Simple usage nag
 */
void usage(void)
{
    puts("USAGE: mcdui [-f database]");
    exit(EXIT_FAILURE);
}
```

`mcdui.c` 看起来应该很熟悉。其整体流程以及大量代码与 `mcddcli.c` 中的代码非常相似。这是有意为之。数据库接口的设计使得命令行客户端与交互式客户端之间唯一的实质区别在于，从数据库检索的数据必须以对 ncurses 友好的方式进行格式化。

当然，也存在一些差异。`mcdui.c` 的调用方式要简单得多。它接受一个命令行选项 `-f`，允许用户使用除默认的 `mcd.db` 之外的其他数据库。无效的参数或选项会导致显示用法消息，如下例所示：

![](img/be588b36b489136ce784030a08a1d3d4_534_0.png)

## 示例

```
$ mcdui -f some database
USAGE: mcdui [ -f database]
```

接下来的几个代码块打开数据库、启动 ncurses 子系统并绘制初始屏幕。`init_scrn` 和 `draw_scrn` 创建的初始屏幕如图 22.1 所示。

![](img/be588b36b489136ce784030a08a1d3d4_535_0.png)

所有操作都在 `while` 循环中进行。`switch` 语句处理键盘输入，调用相应的例程。有效的输入包括以下之一：

- F2—添加记录
- F3—删除记录
- F4—查找记录
- F5—获取记录
- F6—列出所有记录
- F10—退出程序

在此屏幕状态下按下其他任何键，都会在状态区域显示消息 `Key not defined`。每个操作的成功或失败都会使用 `status` 函数显示在状态行上。你可以轻松地扩展程序，以接受其他按键作为当前定义命令的别名。例如，输入 `a` 或 `A` 允许用户添加记录，而输入 `l` 或 `L` 则会列出数据库中当前所有记录。

当你按下 F2 时，首先被要求输入音乐家的名字，然后是 CD 标题。完成添加操作后的屏幕显示如图 22.2 所示。

如果该键已存在于数据库中，数据库会显示相应的错误消息。

要从数据库中删除记录，请按下 F3。删除记录后的屏幕显示如图 22.3 所示。

![](img/be588b36b489136ce784030a08a1d3d4_537_0.png)

图 22.2：
向数据库添加新 CD 后的 *mcdui*。

![](img/be588b36b489136ce784030a08a1d3d4_537_1.png)

图 22.3：
从数据库删除 CD 后的 *mcdui*。

查找操作（通过按下 F4 触发）会在整个数据库中搜索与用户输入的键匹配的键。与 `mccli.c` 类似，它能预先知道键是否存在。图 22.4 显示了输入要搜索的键后的屏幕，图 22.5 显示了搜索成功后的屏幕。`mcdui` 使用 `show` 函数显示其找到的记录。图 22.6 说明了搜索失败时的屏幕状态。

![](img/be588b36b489136ce784030a08a1d3d4_538_0.png)

图 22.4：
输入要搜索的键后的 mcdui。

![](img/be588b36b489136ce784030a08a1d3d4_539_0.png)

图 22.5：
显示成功搜索结果的 mcdui。

![](img/be588b36b489136ce784030a08a1d3d4_539_1.png)

图 22.6：
搜索失败后 mcdui 的状态。

正如在讨论 `mccli` 时提到的，获取（get）操作是查找特定的键，而不是在整个数据库中搜索匹配项。从用户的角度来看，产生的屏幕显示是完全相同的。

列出数据库中所有记录的代码是 `mcdui.c` 中最有趣的代码。再次，它在交互式应用程序中的功能与命令行客户端中的对应功能几乎相同。它首先获取数据库中记录的数量。如果数量为零，程序会在状态行上写入相应消息。否则，`mcdui.c` 首先调整指向键和值的指针表的大小，然后调整两个表中每个指针的大小。

> **提示**
> 同样，一种有价值的改进是动态调整每个表元素的大小，而不是静态调整它们的大小。

`list_recs` 调用填充 `keys` 和 `values` 表。下一个代码块使用 `list` 辅助例程将数据库中的所有 CD 显示在屏幕上。图 22.7 显示了 `list` 更新状态行以指示已显示最后一条记录后的屏幕状态。

![](img/be588b36b489136ce784030a08a1d3d4_541_0.png)

列出 CD 数据库中的所有记录。

`mcdui.c` 的 `list` 操作在列出数据库中的所有 CD 方面做得不错。如果你想增强其功能，请修改它以允许在列表中前后滚动。

## 接下来是什么？

接下来是什么？当然是合上书，成为一名著名的 Linux 程序员！严肃地说，你在本书中已经涵盖了大量材料，并为进一步的编程打下了坚实的基础。剩下的只是编写许多使用你所学知识的程序。除了通过实践，并没有其他途径能成为熟练的 Linux 黑客。虽然书籍可以向你展示基本原理和惯用法，但经验才是最好的老师。去编程吧！

# 第六部分—附录

- A **额外资源**
- B **额外的编程工具**

# A—额外资源

## 参考书目注释

*Advanced Programming in the UNIX Environment*（UNIX 环境高级编程），W. Richard Stevens（Addison-Wesley，1993），ISBN 0-201-56317。这是 UNIX 编程的经典著作。虽然它不专门针对 Linux（事实上，它甚至从未提及 Linux），但它完全涵盖了关于 POSIX 合规性的所有问题。由于 Linux 是 UNIX 的克隆，其中提到的大多数技术也适用于 Linux。Stevens 目前正在修订 APUE（它的常规名称）。

*The Art of Computer Programming, Volume 1: Fundamental Algorithms*（计算机程序设计艺术，第 1 卷：基本算法），第 3 版，Donald Knuth（Addison-Wesley，1997），ISBN 0-201-89683-4。

*The Art of Computer Programming, Volume 2: Seminumerical Algorithms*（计算机程序设计艺术，第 2 卷：半数值算法），第 3 版，Donald Knuth（Addison-Wesley，1998），ISBN 0-201-89684-2。

*The Art of Computer Programming, Volume 3: Sorting and Searching*（计算机程序设计艺术，第 3 卷：排序与搜索），第 3 版，Donald Knuth（Addison-Wesley，1998），ISBN 0-201-89685-0。这三卷是软件开发领域的经典著作。它们与工具和语言无关，但其中蕴含的 30 年编程的精华知识以及数千种算法非常值得投入（三卷套装的价格超过 125.00 美元）。

*Beginning Linux Programming*（Linux 编程入门），Neil Matthewes 和 Rick Stones（Wrox Press，1996）。这本书虽然现在已经过时，但涵盖了基本的 Linux/UNIX 编程技术。然而，它的标题有些误导，因为它也涵盖了 UNIX 编程。

*The C Answer Book: Solutions to Exercises in the C Programming Language*（C 语言参考答案：C 语言程序设计习题解答），第 2 版，Clovis L. Tondo，Scott E. Gimpel（Prentice Hall，1989），ISBN 0-13-109653-2。这本书包含了 Kernighan 和 Ritchie 在其著作 *The C Programming Language*（C 编程语言）中提出的每个练习的解答。不幸的是，这些解答假设读者已经掌握了尚未介绍的语言特性。

