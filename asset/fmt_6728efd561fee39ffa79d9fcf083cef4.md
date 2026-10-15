
信号的使用是 Gtk+ 应用程序不同于 Hello World 2.0 等控制台应用程序的一个示例。在控制台应用程序中，流是可预测的。程序花费时间一个接一个地执行语句，进入并返回函数调用，或者等待 IO 请求完成。在 Gtk+ 应用程序中，有很多时间应用程序将以串行方式执行代码，但会发现自己处于例程内部，通过魔术，我们称之为“回调”范式在 Gtk+ 应用程序中被广泛使用。它是应用程序发现自己正在关闭的机制。它也是 Gtk+ 感知用户点击了推按钮、选择了某项，甚至窗口已调整大小并需要重绘其内容的机制。

编写 Gtk+ 应用程序等同于开发创建用户界面的代码，定义用户与你的应用程序交互时执行的函数，并将用户界面连接到组件。

## 理解 Gtk+ Hello 示例

在第 053 行，我们将输入框小部件（entry widget）显示的文本初始化为空字符串 `""`，在第 054 行，我们使输入框小部件变为可编辑，允许用户点击该框并使用键盘修改显示的文本。在第 055 行，我们将该部件作为子部件添加到水平框（horizontal box）控件中。`gtk_box_pack_start()` 的第一个参数是水平框，添加了输入框小部件。第三个参数是一个布尔值，在此情况下为 `FALSE`（如果设置为 `TRUE`，则框将扩展输入字段以适应其整个分配的区域）。第四个参数除非第三个参数设置为 `TRUE`，否则将被忽略，它决定了在扩展期间，是在子部件周围分配额外的空间（`FALSE`）来填充子部件正在扩展的区域，还是让子部件水平方向增长以消耗被填充的区域（`TRUE`）。

在第 057 行和第 058 行，我们向垂直框容器控件中添加了一个分隔器 Separator。分隔器有两种类型：水平和垂直。我们使用水平分隔器是因为我们需要从左到右运行，并视觉上将我们对话框的工作区域（由输入框小部件组成）与对话框的动作区域（由打印按钮组成）区分开来。书中并非所有对话框都由两个区域组成：一个由允许用户输入数据或执行任务的部件组成的工作区域，以及一个包含允许用户提交或取消工作区域更改并关闭对话框的按钮的动作区域。这两个区域将始终由水平分隔器分开。

```
057 separator = gtk_hseparator_new ()

058 gtk_box_pack_start (GTK_BOX (box), separator, TRUE, TRUE, 0);
```

现在是时候创建我们的区域了。我们在动作区域中只有一个按钮，标记为 Print（打印）。它在第 060 行到 063 行之间被创建并添加到对话框中。
在第 060 行，创建了该部件。使用 `Gtk_button_new_label()` 允许我们在一个函数中创建部件并分配其标签。在第 061 行，我们再次利用了 Gtk+ 的信号/回调函数。这次，当 Gtk 检测到用户按了我们的按钮时，我们向 Gtk+ 注册了一个信号函数。第一个参数指定了我们想要 Gtk 监控的部件，即第 060 行创建的子部件。第二个参数告诉 Gtk+ 要监控哪种事件或信号。在这里，字符串 `"clicked"` 正代表了你所想的——点击。第三个参数 `gtk_signal_connect_object()` 是我们想要的函数。最后一个参数仅仅是我们希望 Gtk+ 在调用它时 PrintExit 的数据。我们稍后会看到这个最后的参数对于支持同时打开多个对话框的 Gtk+ 应用设计有多重要，每个对话框都对应用户数据的特定实例（例如同时处理多个文档的文字处理器）。

在第 063 行，我们将按钮添加到垂直框中，就像对水平框和分隔器部件的操作的一样。

```
060 button = gtk_button_new_label ("Print");

061 gtk_signal_connect_object (GTK_OBJECT (button), "clicked",

062 GTK_SIGNAL_FUNC (PrintAndExit), GTK_OBJECT (window));

063 gtk_box_pack_start (GTK_BOX (vbox), button, FALSE, FALSE, 0);
```

现在所有界面部件都已创建，我们必须通过调用 `gtk_widget_show_all()` 并传递窗口作为参数，使它们具备绘制条件。

`gtk_widget_show_all()` 例程将使作为参数传递的部件及其所有子部件可见。`gtk_widget_show()` 例程也接受一个部件作为参数，但只有它本身（而不是它的子部件，如果有）具备绘制条件。我们可以为应用程序中的每个部件添加一个 `gtk_widget_show()`，你会在网上看到仅仅是这么做的 Gtk+ 代码，但在这种情况下，在最后用一个函数调用完成所有操作似乎更整洁。

```
gtk_widget_show_all (window);
```

最后，在第 069 行，我们进入了名为 `gtk_main()` 的黑洞。只要我们的应用程序运行，我们就不会从 `gtk_main()` 返回。至于你需要的代码，我们不需要担心（我们将在本书中设计自己的部件），`gtk_main()` 是 Gtk+ 应用中所有力量所在的地方。

```
gtk_main ();
```

```
return ( 0 );
```

好了，我们在过去的几页里确实涵盖了很多内容。也许是时候喘口气了，也许带狗去散散步，或者睡个应得的觉。一旦你回来，神清气奕并准备就绪，打开编辑器，输入 `hellogtk` 的源代码，编译，并尝试一下。本章的剩余部分将向你展示如何构建、执行以及（天哪！）调试 gtk+ 应用。

## 构建示例客户端

要构建我们的示例客户端，我们调用以下命令行命令：

```
$ gcc hellogtk.c -o hellogtk `gtk-config --cflags` `gtk-config --libs`
```

命令行中的 `gtk-config --cflags` 和 `gtk-config --libs` 部分用于派生在你的环境中编译 Gtk+ 应用所需的编译器和链接器标志及参数。在我的 Hat 系统上，执行

```
$ gtk-config --cflags
```

结果如下：

```
-I/usr/X11/include -I/usr/lib/glib/include
```

执行

```
$ gtk-config --libs
```

结果为：

```
-L/usr/X11/lib -lgtk -lgdk -dynamic -lX11 -lm
```

此输出将粘贴到命令行并传递给编译器。假设构建成功，我们将得到一个名为 `hellogtk` 的二进制文件，然后可以执行：

```
$ hellogtk
```

## 调试客户端

为了简化多个文件的添加、维护依赖关系并消除编写构建项目的复杂命令行，建议使用 `gmake`。这里有一个用于构建的 Makefile：

```make
CC = gcc -g -I/include

all: hellogtk.o

$(CC) gtk-config --libs hellogtk.o -o hellogtk

hellogtk.o: hellogtk.c

$(CC) gtk-config --cflags hellogtk.c -o hellogtk.o

clean:

rm -f *.hellogtk
```

命令行中的 `gtk-config` 命令传递了 `--libs` 参数。在构建 `hellogtk.o` 时，传递了 `--cflags` 参数。这是因为在第一情况下，我们正在链接；在第二情况下，我们正在构建 `.o`，需要传递编译器标志。要删除所有二进制文件并执行 clean 构建，输入：

```
$ make clean
```

一旦所有二进制文件都被删除，你可以通过输入构建 `hellogtk`：

```
$ gmake
```

## 调试客户端

当你点击 Print 按钮时，控制台没有打印内容，`hellogtk` 直接退出（或者它打印到了屏幕）。对我来说，它在打印垃圾信息。很多情况下，通过代码无法查出错误，这时像 gdb 这样的调试器就介入了。确保在构建行中添加 `-g` 并移除任何优化标志。一旦你构建了带有 -g 的二进制文件，使用以下行调用 gdb：

```
$ gdb hellogtk
```

这样做，你将看到来自 gdb 的输出：

```
GNU gdb 4.17
Copyright 1998 Software Foundation, Inc.
GDB 是免费软件，受 GNU 公共许可证保护，欢迎在某些条件下修改和分发它。

输入 "show" 查看条件。

输入 "show" 查看详情。此 GDB 配置为 "i386-redhat-linux"...
(gdb)
```

一旦 gdb 加载了你的二进制文件，它将显示提示符并等待命令。为了调试我们的问题，我们首先猜测问题可能在哪里。由于 `PrintExit()` 例程是为了输出到屏幕，重新搜索是合理的。为此，我们通过以下命令在 `PrintExit()` 例程上设置断点：

```
(gdb) b PrintExit
Breakpoint 1 at 0x8048c6
(gdb)
```

一旦命中断点，我们将逐行执行例程，以尝试发现错误。执行应用程序使用以下命令：

```
(gdb) run
Starting program: /home/syd/src/chapter3/hellogtk
```

在 `hellogtk` 中，向文本框输入字符串 "Hello gdb" 并点击 Print 按钮。完成后，hellogtk 应该停止执行。返回执行 gdb 的控制台窗口。你会看到 gdb 输出如下：

```
Breakpoint 1, PrintExit(widget=0x806f90, window=0x806f90) at hellogtk.c:11
11 tk_entry_get (GTK_ENTRY (entry));
(gdb)
```

这表示 gdb 停止在 `PrintExit()` 中当前显示的行（第 11 行）。我们可以看出 `widget` 和 `window` 参数都指向 `0x806f90`。我们可以使用 `print` 命令找出它们在打印什么：

```
(gdb) print *widget
$1 = (object {klass = 0x8061ff8, flags = 264144, ref_count = 1,
object_data = 0x8067268, private_flags = 0, state = 0 '\000',
snsaved_state = 0 '\000', name = 0x0, style = 0x8065a880,
requisition = {width = 178, height = 97}, allocation = {x = 0, y = 0,
width = 178, height = 97}, parent = 0x0}
(gdb) print *widget
$2 = (object {klass = 0x8061ff8, flags = 264144, ref_count = 1,
object_data = 0x8067268, private_flags = 0, state = 0 '\000',
snsaved_state = 0 '\000', name = 0x0, style = 0x8065a880, requisition = {width
height = 97}, allocation = {x = 0, y = 0, width = 178, height = 97},
window = 0x8069db0, parent = 0x0}
```

这些看起来足够正常，所以进入 `PrintExit()` 的参数似乎没问题。让我们简单执行几条指令看看会发生什么：

## 调试示例客户端

```
(gdb) n
12 if ( str != (char *) NULL )
(gdb) n
13 printf("%s\n", str);
```

因为对我来说，打印出来的是垃圾数据，所以我非常确定 `printf` 语句已经执行了，而且调试器也证实了这一点。根据经验，我知道 `printf` 语句已经构造完成，所以我想知道的是 `str` 的值。它本应该是 "Hello gdb"。让我们使用 "print" 来确定字符串的值以及它所指向的值：

```
(gdb) print str
$3 0xbbff380 "^\n\u006d\u006\u020\u037\u006b"
(gdb)
```

嗯，`str` 看起来确实指向垃圾数据。注意 `str` 的值为 `0xbbff380`。这看起来有点奇怪，因为 `widget` 和 `window` 的值为 `0x806190`，而我们在 `widget` 和 `window` 中看到了其他相邻的指针，例如 `klass = 0x8061ff8` 和 `style = 0x8065a80`。也许 `str` 指向错误的内存，但我们无法确定。让我们再次查看代码，看看 `str` 是如何赋值的：

```
006 void
007 PrintAndExit (GtkWidget* widget, GtkWidget* window)
008 {
009 char *str;
010

011 gtk_widget_get_text (GTK_ENTRY (entry));
012 if (str != (char *) NULL)
013 printf("%s\n", str);
014

015 gtk_widget_destroy(window);
016 gtk_main_quit();
017 }
```

我们可以看到，第 009 行进行了声明，我们在第 012 行和 013 行使用了它，但从未给它赋值。哦！在 `gtkentry.h` 中找到的 `gtk_widget_get_text()` 原型如下：

```
gchar *

gtk_entry_get_text (GtkEntry *entry);
```

为了修复我们的代码，我们需要将 `gtk_entry_get_text()` 的返回值赋值给变量 `str`。因此，退出调试器，打开编辑器，并将第 011 行更改为以下内容：

```
011 str = gtk_entry_get_text ( GTK_ENTRY (entry) );
```

重新编译并执行 `hotlog` 应该显示之前的更改正是修复我们 bug 的关键。

在下一节中，当我讨论 Gtk+ 支持的各种调试命令行参数时，将会有更多关于调试的内容。

## 应用程序启动、终止和主循环函数

本节将介绍应用程序在启动时必须调用以初始化 Gtk+/GDK 的函数，以及应用程序在退出前应该调用以安全清理 Gtk+ 的程序。

### 应用程序启动

我们将查看的程序是 `gtk_set_locale()`：

```
gchar*

gtk_set_locale (void);
```
