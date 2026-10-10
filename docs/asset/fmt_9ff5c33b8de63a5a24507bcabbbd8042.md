
`$(CC)` `--gtk-config --libs hellogtk+.o -o hellogtk+`

`hellogtk+.o: hellogtk+.c`

`$(CC)` `--gtk-config --cflags -c hellogtk+.c -o hellogtk+.o`

```
```

`clean:`

`rm -f *.hellogtk`

```
```

在命令行中对应 `hellogtk+` 依赖项时使用的 `Gtk-config` 命令传递了 `--libs` 参数。在编译 `hellogtk+.o` 时，它传递了 `--cflags` 参数。这是因为在第一种情况下，我们正在进行链接，所以我们只需要传递链接器文件。在第二种情况下，我们正在构建 `.o` 文件，在这种情况下我们需要传递编译器标志。
要删除二进制文件并进行清理构建，请输入以下：

```
$ make clean
```

一旦所有二进制文件都被删除，你可以通过输入以下命令来编译 `hellogtk+`：
`$ gmake`

### 调试示例客户端

你可能已经注意到，点击 `Print`（打印）按钮后，控制台没有打印任何内容，且 `hellogtk+` 在什么都没做的情况下退出了（或在屏幕上打印垃圾信息，甚至崩溃）。对于我来说，它是在打印垃圾信息。
你可能仅仅通过检查代码就能找出导致此 bug 的原因。然而，通常情况是通过代码检查无法发现 bug。这时像 `gdb` 这样的调试器派上用场了。在构建行中添加 `-g` 标志并移除任何优化标志，就像在之前 `Makefile` 中的 `CC` 宏中所做的那样。一旦你使用 `-g` 完成编译并获得了调试二进制文件，使用以下命令行调用 `gdb`：

```
$ gdb hellogtk+
```

这样做后，你会看到来自 `gdb` 的输出：

```
GNU gdb 4.17
Copyright 1998 Free Software Foundation, Inc.
GDB 是一个免费软件，受 GNU 通用公共许可证保护，欢迎在某些条件下修改它/或分发它的副本。
输入 "show copying" 查看具体条件。

GDB 不提供任何保证。输入 "show warranty" 查看详情。此 GDB 被配置为 "i386-redhat-linux"...（未找到调试符号）...
(gdb)
```

一旦加载了你的二进制文件，它将显示一个提示符并等待命令。为了调试我们的问题，我们首先对问题可能出现的地方进行猜测。由于 `PrintAndWait()` 程序负责将输出打印到屏幕上，从这里开始搜索是合理的。为了做到这一点，我们将输入以下命令在 `PrintAndWait()` 程序上设置一个断点：

```
(gdb) b PrintAndWait
Breakpoint 1 at 0x8048c06
(gdb)
```

一旦命中断点，我们将逐行单步执行该程序，试图发现哪里出了问题。
要开始执行，请使用以下命令之一：

```
(gdb) run
Starting: /home/syd/db/src/chapter3/hellogtk+
```

一旦运行了 `hellogtk+`，在文本框中输入 "Hello gdb" 并点击 `Print` 按钮。完成此操作后，`hellogtk+` 应该停止执行。回到执行 `gdb` 的控制窗口。你应该看到以下打印内容：

```
Breakpoint 1, PrintAndWait (widget=0x8061f90, window=0x8061f90) at hellogtk+::c:11
11 gtk_entry_get ( GTK_ENTRY (entry) );
(gdb)
```

这表明 `gdb` 停止在 `PrintAndWait()` 中当前显示的行（第 11 行）。我们可以看到 `widget` 和 `window` 参数都指向 `0x8061f90`。现在我们可以使用 `print` 命令打印出它们的内容：

```
(gdb) print *widget
$1 = (object (klass = 0x8061ff8, flags = 264144, ref_count = 1,
object_data = 0x8067268, private_flags = 0, state = 0 '\u000',
saved_state = 0 '\u000', name = 0x, style = 0x8065a80,
requisition = {width = 178, height = 97}, allocation = {x = 0, y = 0,
width = 178, height = 97}, parent = 0x0}
print *window
$2 = (object (klass = 0x8061ff8, flags = 264144, ref_count = 1,
object_data = 0x8067268, private_flags = 0, state = 0 '\u000',
saved_state = 0 '\u000', name = 0x, style = 0x8065a80,
requisition = {width = 178, height = 97}, allocation = {x = 0, y = 0,
width = 178, height = 97}, parent = 0x0}
```

这表示 `gdb` 停止在 `PrintAndWait()` 的当前显示这一行（第 11 行）。我们可以看到 `widget` 和 `window` 参数都指向 `0x8061f90`。

### 应用启动、终止和主循环函数

本节将介绍在应用程序启动时初始化 `Gtk+/GDK` 的函数，以及在应用程序退出前清理 `Gtk+` 的程序。

#### 应用启动

我们首先查看的程序是 `set_locale()`：

```
gchar* tk_set_locale (void)
```

`gtk_set_locale` 必须在 `gtk_init` 之前调用（如果应用程序决定调用的话）。`gtk_set_locale` 是一个包装器，它调用 `gdk_set_locale()`，后者调用 `locale(LC_ALL,"")`，读取由 `LANG` 环境变量定义的本地化数据库。有关应用程序国际化的详情，请参考 `locale(1)` 和 `locale(7)` 页面。如果不调用 `gtk_set_locale`，locale 将是可移植的 "C"。

除了 `setlocale()`，还调用了两个 `Xlib` 库：`XXsupport_locale()` 和 `XSetLocaleModifiers()`。如果 `XXsupport_locale()` 失败，则应用程序不支持 `LANG` 环境变量定义的 locale，并退回到 "C" locale。`XSetLocaleModifiers()` 读取 `XMODIFIERS` 环境变量，它由一系列 "category=value" 组成。作为 `im` 被 `setlocale` 定义的标准类别是 "im"，用于指定用于国际化文本输入的输入方法。更多信息请参见 `XSetLocaleModifiers()`。

`tk_set_locale()` 在 `setlocale()`, `XXsupport_locale()` 或 `XSetLocaleModifiers()` 失败时产生产生或多个警告。无论成功与否，都会返回当前字符串。为了确保用户的 locale 选择得到尊重，你应该将返回的字符串与 `LANG` 环境变量进行比较，如果不匹配则退出，如下所示：

```
gchar *envlang, *lang;
envlang = getenv("LANG" );
lang = gtk_set_locale();
```

```
if ( envlang != (char *) NULL && strcmp(lang, envlang ) ) {
	fprintf(stderr, "Unable to set locale to %s\n", envlang);
	exit( 1 );
}
```

为了修复这个问题，我们需要将 `gtk_entry_text()` 的返回值赋值给变量。退出调试器，查看第 11 行：

```
11     str = gtk_entry_text (GTK_ENTRY (entry));
```
