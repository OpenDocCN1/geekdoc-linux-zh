
# 第 2 章

编译并运行该应用程序，你应该会在你的终端窗口中看到以下内容：

```
In order traversal coming up

+ - Person: Heather Preferred User Interface : KDE and GNOME in Enlightenment
- Person: John Preferred User Interface : Windows
- Person: Louay Preferred User Interface : Jedi mind control
- Person: Peter Preferred User Interface : GNOME in Windowaker

Pre order traversal now

+ - Person: John Preferred User Interface : Windows
- Person: Heather Preferred User Interface : KDE and GNOME in Enlightenment
- Person: Peter Preferred User Interface : GNOME in Windowaker
- Person: Louay Preferred User Interface : Jedi mind control

Finally, post order traversal

+ - Person: Heather Preferred User Interface : KDE and GNOME in Enlightenment
- Person: Louay Preferred User Interface : Jedi mind control
- Person: Peter Preferred User Interface : GNOME in Windowaker
- Person: John Preferred User Interface : Windows
```

## 扩展数据类型

正如你现在看到的，它们也相当容易使用。为了确保一切都记住了，请看 `tree.c`，这是一个演示 `g_tree` 函数的简单应用程序：

```c
/**
* tree.c
* 一个展示如何在 GLib 中使用树的小型示例
 */
```

## 字符串

由于你最初创建树时指定的比较函数所确定的顺序，`G_IN_ORDER` 可能是最容易解释的。它按照你最初创建树时指定的比较函数所确定的顺序遍历树中的项。

不过，`G_POST_ORDER` 和 `G_PRE_ORDER` 类型最好通过图表来演示。在下面的图中，框中的数字表示了你遍历同一棵树的顺序：

![](img/aa3546013f120531cd191b770d85869c_71_0.png)

## GLib

最后，当你用完树后，不要忘记释放它使用的内存。这是通过调用 `g_tree_destroy` 实现的。

```c
void g_tree_destroy ( GTree * tree );
```

树是管理有序数据列表的一种非常有效的方法，并且提供了一种快速获取这些数据的方法。谢天，正如你现在看到的，它们也相当容易使用。为了确保一切都记住了，请看 `tree.c`，这是一个演示 `g_tree` 函数的简单应用程序：

```c
/**
* tree.c
* 一个展示如何在 GLib 中使用树的小型示例
 */
```

## 附加和前字符串

对于 `GString`，可以很容易地在现有字符串的末尾或开头添加更多文本。有两个函数也恰好发生这种情况，`g_string_append` 和 `g_string_prepend`。它们都以相同的方式工作。它们都期望接收指向 `GString` 的指针以及指向以 `NULL` 结尾字符数组的指针。GLib 在需要时为 `GString` 重新分配内存，并构建下一个 `GString`。最后，会返回指向新 `GString` 的指针。

## 创建和销毁 GString

要销毁 `GString` 并释放它占用的内存，GLib 提供了 `g_string_free` 函数。它接受两个参数（出乎意料，你可能认为它只需要一个）。第一个是布尔值，指示你是否要释放字符数据占用的内存。将此参数设置为 `TRUE` 以移除字符数据，设置为 `FALSE` 以移除 `GString` 结构。不过要小心；去释放静态字符串占用的内存不是好主意，因为 C 会自动完成这项工作。

这种工作方式的原因是 GLib 允许你释放结构占用的内存，但保留 `GString` 结构中可以通过 `str` 成员访问的字符串。

## 分配字符串

一旦你创建了 `GString`，就可以通过 `g_string_assign` 函数向其分配文本。它接受两个参数，第一个是你要赋值的 `GString`，第二个是你要赋值的文本的普通 `char` 指针。该函数返回分配后的 `GString` 指针。这是重要的。记住，通过分配大于 `GString` 能够容纳的文本，在这种情况下 `g_string_assign` 将不得不重新分配内存来容纳 `GString`。确保你捕获了返回值。如果函数失败，你将得到 `NULL` 指针。

## 调整大小的 GString

你也可以通过 `g_string_sized_new` 函数来实现这一点。在这种情况下，你需要传递一个定义的大小，GLib 会根据此大小分配内存，并返回一个准备好使用的 `GString` 指针。例如：

```c
GString * MyName;
Name = g_string_new ( "Peter" );
```

一旦你创建了 `GString`，由于已知大小，就可以通过 `g_string_sized_new` 函数来创建它。在这种情况下，你需要传递一个定义的大小，GLib 会根据此大小分配内存，并返回一个准备好使用的 `GString` 指针。例如：

```c
MyName = g_string_sized_new ( 1000 );
```

对于 `GString`，你可以通过 `g_string_assign` 函数向其分配文本。它接受两个参数，第一个是你要赋值的 `GString`，第二个是你要赋值的文本的普通 `char` 指针。该函数返回分配后的 `GString` 指针。这是重要的。记住，通过分配大于 `GString` 能够容纳的文本，在这种情况下 `g_string_assign` 将不得不重新分配内存来容纳 `GString`。确保你捕获了返回值。如果函数失败，你将得到 `NULL` 指针。

```c
MyName = g_string_assign ( MyName, "Pete Da Money-Wright" );
```

这实际上展示了我刚才提到的点。在这种情况下，新字符串比我们在第一个示例中创建的原始字符串大得多。GLib 几乎不得不重新分配 `GString` 的内存，导致原来的 `MyName` 指针失效。如果没有对返回值的赋值，我们将没有方法获取新字符串。

# 第 2 章

```c
GString * MyName;
MyName = g_string_new ( "Pete " );
MyName = g_string_append ( MyName,"Wright" );
MyName = g_string_prepend ( MyName,"Mr. " ) ;
```

在这个示例中，`GString` 变成了 "Mr. Pete Wright"。你也可以通过 `GString` 结构体的 `str` 成员获取该数据。

```c
g_print ( MyName->str );
```

当然，如果字符串本身包含 `%` 字符，上面的代码可能会出现问题，因为 `g_print` 会将其解释为并预期有更多数据传入。

## 在字符串之间相互插入字符串

除了在现有 `GString` 的开头和结尾粘贴新文本之外，GLib 还提供了 `g_string_insert` 函数，用于在现有字符串的任何位置插入新字符串。只需传递指向要修改的 `GString` 指针、想要插入的位置，最后传递指向要插入的字符数组字符串的指针即可。例如：

```c
GString * MyName;
MyName = g_string_new ( "Beginning GNOME" );
MyName = g_string_insert ( MyName, 10,"GTK+" ) ;
```

最初，这里使用 `GString` 用来存储文本 "Beginning GNOME"。插入后，它变成了 "Beginning GTK+/GNOME"。

## 其他函数

我不会再过多讨论 `GString` 了，但值得提到的是，还有几个函数在不时可以派上用场。要更改字符串中字母的大小写，可以使用 `g_string_upcase` 和 `g_string_down` 函数。对于其他 `GString` 函数，这两个函数期望接收一个 `GString` 指针（即需要更改大小写的字符串），并返回一个指向新更改后的 `GString` 的指针。

你还可以使用 `g_string_erase` 函数清除 `GString` 中的文本。传递指向 `GString` 的指针，以及要从哪个起始位置开始清除，以及要清除的字符数量。例如：

```c
MyName = g_string_erase ( MyName, 0, 4 );
```

...从 `MyName` 指向的 `GString` 所引用的文本开头删除前四个字符。

## 字符串实用函数

除了 `GString` 的功能外，GLib 还包含了许多与传统字符数组配合工作的实用字符串处理函数。它们的设计并不是为了替换 `string.h` 以及大多数编译器自带库中已有的函数。相反，它们是为了进行补充。

## 仅用于复制字符串而设计的函数：strdup 和 strndup

`strdup` 函数是最常用的。它接收一个 `gchar` 指针并返回一个指向新复制字符串的 `gchar` 指针。在使用完返回的字符串后，确保你释放了它，这是重要的。在复制字符串的过程中，GLib 显然需要分配内存来存放新副本，在使用完新字符串后，由你负责释放内存。如果不这样做，就会发生内存泄漏。

```c
gchar *Me() = "Pete";
gchar * MiniMe;
```

```c
MiniMe = strdup ( Me );
```

另一方面，`strndup` 允许你复制字符串的一部分，特别是第一部分。它接受两个参数：指向要复制字符串的 `gchar` 指针，以及一个包含你想从开始复制的字符数量的 `int`。

```c
gchar Book[] = "Beginning GTK+/GNOME";
gchar * SmallerBook;
```

```c
SmallerBook = strdup ( Book, 13 );
```

与之前一样，它返回一个指向新字符串的指针，你在使用完后需要释放它。

我一直在强调释放这些返回字符串的必要性，这是一个贯穿在后续许多字符串实用函数中的共同主题。在使用完后，如何释放返回的字符串内存呢？这只需要调用 `g_free` 并传递字符串指针即可。

## 比较字符串

标准字符串库已经包含一个函数来比较两个字符串以判断它们是否相等，并使用字典序对它们进行比较（例如 Peter 比 Petra 大还是小？）。GLib 实用函数包含了两个可以轻松对两个字符串、甚至是字符串的一部分进行不区分大小写比较的函数。

这些函数是 `g_strcmp` 和 `g_strcasecmp`。它们仅接收两个 `gchar` 指针，并比较它们指向的字符串，忽略任何大小写差异。后者接收一个额外的参数，用于指定从字符串开始要比较的字符数量。这两个函数都返回一个 `int`：如果第一个字符串匹配则返回 0；如果第一个字符串在第二个字符串之前（按字母顺序），则小于 0；如果第一个字符串在第二个字符串之后，则大于 0。

## 分割字符串

在某些情况下，有必要将字符串分割成小片段，一个例子就是我们之前的示例程序，其中路径被拆解为它的组成目录。GLib 提供了 `g_strsplit`，它会根据某些分隔符分割字符串。例如，如果你想找出名字的每个部分，整个字符串的常用分隔符是空格字符（因为大多数人用空格分隔名、中间名和姓）。

要使用 `g_strsplit`，只需传递你想要分割的字符串指针即可。

# 第 2 章

## 创建和销毁计时器

创建计时器非常简单。只需调用 `g_timer_new` 即可。它不接受参数，并返回一个指向 `GTimer` 对象的指针。它分配了一块内存来存储计时器的结构和其他内部内容，因此在程序退出之前，你必须务要记住销毁计时器。这可以避免浪费内存。

你可以通过调用 `g_timer_destroy` 来销毁计时器。它接受一个参数，当然是 `g_timer_new` 传递给你的 `GTimer` 指针。

```c
GTimer * MyTimer;
MyTimer = g_timer_new ();
/**
* 你的代码写在这里
 */
g_timer_destroy ( MyTimer );
```

## 启动、停止和重置计时器

用于启动、停止和重置计时器的三个函数的工作方式完全相同。它们都接受一个参数，即从 `g_timer_new` 返回的 `GTimer` 指针，仅此而已。它们没有返回值。

## 检查计时器

为了检查计时器的值（即当前已过去的时间，记住秒表类比），我们需要调用 `g_timer_elapsed`。这个函数实际上非常通用，如果你需要，它可以为你提供 1/1000 秒为单位的已通过时间分辨率。

`g_timer_elapsed` 函数返回一个 `double` 类型，即以秒为单位的已通过时间。语句中重要的部分是返回的时间是一个 `double` 类型。这意味着如果自计时器启动以来已经经过了 1.5 秒，你将得到的结果是 1.5，而不是 1 或 2。

它实际上接受两个参数。第一个是现在通用的 `GTimer` 指针。第二个是指向 `glong`（`GLib` 的无符号整数）的指针。如果你传递一个有效指针作为此参数（而不是 `NULL` 值），那么所指指针的变量值将被设置为已通过时间的毫秒部分。例如，假设已通过的时间为 1.5 秒。通过将一个指向 `glong` 的指针作为调用的第二个参数，你可以检查 `gtimer` 的值并发现它被设置为 512。这意味着实际通过的时间是 1.512 秒。

## 灵异的计时器

是时候玩玩代码了，在本章中，我们将以此增加一些乐趣。你是否看过那类电影，英雄盯着电脑屏幕，灵异地看到一个鬼魂在输入它完全想要的内容？通过使用一点小的随机数来创建延迟，我们实际上可以一个字母字母打印出一个字符串。每个字母出现之间的延迟是 0 到 1 秒之间的随机值，结果是字母出现在屏幕上的样子就像它们正在被输入一样。后者当然通过明智使用计时器来实现。

复制这段代码，并在尽早机会运行在最近的实习生电脑上。根据该计算机用户到底有多没经验，不要忘记准备好隐藏摄像机来记录下这令人“惊悚”的日志。将其保存为 `spooky.c`：

```c
/**
 * spooky.c
 * 以灵异方式打印用户信息的程序。
 */

#include <glib.h>
#include <time.h>
#include <stdlib.h>

void SpookyDump ( gchar * sText )
{
	gdouble dTime;
	gint nIndex;
	Gtimer * DumpTimer;
	gint Delay;

	dumpTimer = g_timer_new ( );
	dTime = g_timer_elapsed ( DumpTimer, NULL );

	for ( nIndex = 0; nIndex < strlen ( sText ); nIndex ++)
	{
		delay = rand ( % 3);
		/* 下面的循环只是停在那儿等待。我知道在多任务环境中
		* 这样做不是什么好事，在现实世界中有更优雅的方法
		* 来实现这一点。它在这里仅仅是为了
		* 计时器。

		while ( ( ( g_timer_elapsed ( DumpTimer, NULL ) - dTime ) * 10 ) < Delay );
		g_print ( "%s\n", sText[nIndex] );
		dTime = g_timer_elapsed ( DumpTimer, NULL );
	}
}
```

```c
g_timer_stop ( DumpTimer );
g_timer_destroy ( DumpTimer );
}
gint main ( gint argc, gchar * argv[])
{
	gchar * OutputString;

	g_print ( "* ALERT - TERMINAL ACCOUNT HAS BEEN COMPROMISED ***\n\n" );

	OutputString = g_strjoin ( " ",
"Initiating user scan\n",
"User is t:\", g_get_real_name (),
"aka," g_get_user_name (), "\n",
"Files stored at:", g_get_home_dir (), "\n",
"Commencing password decrypt.........\n\n", NULL );
	SpookyDump ( OutputString );
	g_free ( OutputString );
	g_print ( "Just kidding! (hehe)\n" );

	return 0;
}
```

计时器代码都在 `SpookyDump` 函数中。这所有代码所做的只是创建一个计时器，并逐个字符遍历传递的字符串。在打印字符之前，程序会暂停一段很短的随机时间，以创建出输入的效果。完全没问题。你实际上可以通过添加一个随机错误元素，并在继续之前删除错误来让程序更智能。你还可以更改代码。

## 总结

在本章中，我们涵盖了许多内容，我认为你会同意 GLib 确实是一个非常有用的库。我们学习了：

- GLib 提供了什么

- GLib 如何处理字符串

- GLib 在内存管理方面可以做什么

- GLib 如何支持多线程
