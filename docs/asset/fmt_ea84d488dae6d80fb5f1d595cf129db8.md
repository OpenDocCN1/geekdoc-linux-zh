
你开始创建共享库时，首先生成你想要的目标代码文件。你使用`-PIC`选项编译用于共享库的源文件，该选项会生成适用于共享库的地址无关代码。以下示例创建了这样一个名为`io.o`的目标代码文件。（`-c`选项指示`gcc`仅生成目标代码文件。）

```
$ gcc -fPIC -c io.o
```

你可以使用`gcc`编译器配合`-shared`和`-Wl`选项来创建共享库。在这种情况下，编译器将把编译后的文件放入库中，而不是可执行文件。`-o`选项将指定目录的名称。你可以列出任意数量的目标代码文件。`-Wl`将选项传递给链接器，在这种情况下，是为库指定`soname`的`soname`选项。此`soname`将放置在库文件内部，稍后由`ldconfig`生成`soname`链接。以下示例使用`io.o`文件创建了一个名为`libmyio.so.1.0`的库。该库的`soname`是`libmyio.so.1`。

```
$ gcc -shared -Wl soname libmyio.so.1 -o libmyio.so.1.0
```

如果你准备好将其放入库目录，只需将其复制那里。然后运行`ldconfig`生成`dl`链接。（这在系统启动时也会自动完成。）

```
$ cp libmyio.so.1.0 /usr/lib
$ ldconfig /usr/lib
```

# 创建和使用库：静态、共享与动态 175

```c
{
  char title[20];
  float price;
  void *handle;
  void (*binput) (char*, float*);
  void (*prbook) (char*, float*);

  handle = dlopen("/usr/lib/libmyio.so",
      RTLD_LAZY);

  if(!handle) {
    fputs(perror(), stderr);
    exit(1);
  }
  binput = dlsym(handle, "bookinput");
  prbook = dlsym(handle, "printbook");

  (*binput)(title, &price);
  (*prbook)(title, price);

  dlclose(handle);
}
```

使用动态链接的程序使用`libld.so`库编译。它加载的库并不是由编译器链接的。示例创建了一个名为`bookrecrd`的程序，它可以加载`libmio.so`库并引用它的`bookinput`和`printbook`函数。注意使用`-ldl`来引用动态加载器库`libld.so`。

```
$ gcc bmain.c -o bookrecrd -ldl
```

`ld`命令显示`bookrecrd`程序使用了`libld.so`库，即动态加载器库。它没有显示`libmio.so.1.0`。

```
$ ldd bookrecrd

libld.so.1 => /lib/libld.so.1.7.14

libc.so.5 => /lib/libc.so.5.4.22
```

## 静态库：ar

你可以使用`ar`命令创建静态库而不是共享库。用`ar`创建的库名应该具有`.a`扩展。通过`ar`，你可以轻松地维护库，添加或更新文件并移除不再需要的文件。

## 使用库：静态、共享与动态 176

`ar`命令执行的操作由`ar`命令的选项决定，该选项由跟在`ar`命令后的单个字母组成。选项之间没有连字符。三个常用的选项是`r`、`x`和`t`。`r`选项指示`ar`将文件复制到库中。`x`选项提取文件，`t`选项显示库中的文件列表。归档操作的语法为关键字`ar`、选项、库文件名以及库中归档的文件列表：

```
ar option library-file list-of-object-files
```

你使用`ar`命令的选项创建一个库，如果它不存在，它将被创建。你还使用`r`选项来更新库并向其添加新文件。`r`选项代表替换（replace）。如果你正在归档一个文件且该文件的副本已在库中，它将会被替换（覆盖）。如果正在归档的文件不在库中，则它将被添加。通过使用`r`选项，你可以用新版本更新库中已存在的文件。作为创建库的示例，文件`input.o`和`print.o`被创建了`iolib.library`。

```
$ ar r iolib.a input.o print.o
```

一旦你创建了库文件并想在程序中使用它，你首先需要使用`ranlib`命令对其进行准备，以便链接器使用。`ranlib`会组织库文件，以便链接器能够对其进行有效搜索。

```
$ ranlib iolib.a
```

该库现在可以供编译器使用了。

```
$ gcc main.c iolib.a -o bookrec
```

如果你想从库中移除函数，你需要移除它们所在的文件。带有`d`选项的`ar`命令将从库中删除一个文件。

```
$ ar d iolib.a input.o
```

| 选项 | 功能 |
| --- | --- |
| `r` | 创建库文件或在库中添加和更新文件。 |
| `d` | 从库中删除文件。 |
| `x` | 从库中提取文件。 |
| `t` | 生成库中所有文件的列表。 |

## 开发库

如果你从`ftp`站点下载源代码形式的软件，然后在你的`Linux`系统上编译它们，那么你可能需要一些特殊的库。这对于基于`X-Window`的程序来说尤为如此，它们使用特殊的库。`Xview`程序使用它们自己的特殊库。其他软件可能使用专门的图形库，如`QT`库或`xforms`。大多数库包含在你的`OpenLinux`光刻ROM中，但它们不会随标准安装一起安装。你可能需要从`Linux` `ftp`或`Web`站点下载其他库，如`QT`。标准的`Linux`库通常位于`/usr/lib`目录，其中`X-Window`库通常位于`/usr/X11R6/lib`目录，而`OpenLook`库则位于`/usr/opwin/lib`目录。下表列出了一些常用的库：

| 库名 | 描述 |
| --- | --- |
| `libc.so` | C 编程语言的标准库。 |
| `lib++.so` | `gcc` 编译器支持的 C++ 类库。 |
| `objc.so` | Objective-C 库。编译 Objective-C 程序所需。 |
| `libm.so.5` | 数学库。 |
| `libdb.so.2` | 用于 C 语言的 BSD 数据库库。 |
| `libelf.so` | 操作 ELF 对象的库。 |
| `libgdm.so` | gnu 版本的 dbm 库。 |
| `libgpm.so` | ncurses 库。 |
| `libcurses.so` | 终端库。 |
| `libtiff.so` | TIFF 库。 |
| `libdl.so` | 动态加载器库。 |
| `libforms.so` | 表单库。 |
| `libct.so` | TCL 库。 |
| `libtk.so` | TK 库。 |
| `libqt.so` | QT 库。 |
| `libx11.so` | X-Window 库。 |
| `libX.so` | X 库。 |
| `libXaw.so` | Athena 库。 |
| `libXpm.so` | Pixmap 。 |
| `libICE.so` | ICE 库。 |
| `libXview.so` | Xview 库。 |

## gdb 调试器 179

如果程序出现错误，`gdb`会在错误处停止。然后可以使用`gdb`检查发生了什么。你可以使用的不同`gdb`命令列如下表所示并在本节中描述。许多命令与`sdb`中使用的具有可比性。

| 命令 | 单字母等效命令 | 功能 |
| --- | --- | --- |
| `run` | `r` | 运行程序。 |
| `quit` | `q` | 退出 `gdb`。 |

## 显示变量和参数

如果程序出现错误，`gdb`会在错误处停止。然后可以使用`gdb`命令检查发生了什么。你可以使用的不同`gdb`命令列如下表所示。

| 命令 | 单字母等效命令 | 功能 |
| --- | --- | --- |
| `print variable` | `p variable` | 显示变量的内容。 |
| `print &variable` | `p &variable` | 显示变量的地址。 |
| `set variable = value` | | 在 `gdb` 会话中为变量赋值。 |
| `where` | | 显示堆栈跟踪，显示函数调用序列以及函数名及其参数。 |
| `info locals` | | 显示局部变量和参数。 |
| `list line-number` | `l line-number` | 显示指定行号开始的代码。 |

## 180 gdb 符号调试器

| 命令 | 等效写法 | 功能 |
|---|---|---|
