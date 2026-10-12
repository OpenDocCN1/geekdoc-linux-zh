
`char *b;`

};

每当你遇到 `struct teststruct` 时，你就知道它实际上是两个紧相邻的单词，第一个是整数，第二个是指向字符或一组字符的指针。你永远不会看到结构作为参数传递给函数。相反，你通常看到指向结构的指针作为参数传递。这是因为将结构传递给函数是非常复杂的，因为它们会占用很多存储位置。

## typedef

`typedef` 基本上允许你重命名类型。例如，我可以在 C 程序中执行 `typedef int myowntype;`，每当我输入 `myowntype` 时，就好像输入了 `int` 一样。这可能会让人很困恼，因为你必须查找函数原型中所有的 `typedef` 和 `struct` 到底意味着什么。然而，`typedef` 对于给类型赋予更有意义且具描述性的名称非常有用。

**兼容性注意：** 列出的尺寸适用于 intel 兼容 (`x86`) 机器。其他机器具有不同的尺寸。此外，即使将短于字长的参数传递给函数，它们也会作为 `long` 在栈上进行传递。

那里是阅读函数文档的地方。现在，让我们回到如何查找库的问题。你大多数的系统库位于 `/usr/lib` 或 `/lib`。如果你想查看它们定义了哪些符号，只需运行 `objdump -R FILENAME`，`FILENAME` 是库的完整路径。不过输出对于寻找你可能需要的接口并没有太大帮助。通常，你需要在开始时就知道你需要哪个库，然后只需阅读文档。大多数库的函数都有手册或手页（man pages）。互联网是库文档的最佳来源。GNU 项目的大多数库也有它们的 info 页，这些页面比手页更详细。

# 第 8 章与代码库共享函数

## 有用函数

你可能需要注意的几个 c 库有用函数包括：

- `size_t strlen (const char *s)` 计算空终止字符串的大小。
- `int strcmp (const char *s1, const char *s2)` 按照字母顺序比较两个字符串。
- `char * strdup (const char *s)` 接收字符串的指针，在新位置创建一个新副本，并返回新位置。
- `FILE fopen (const char *filename, const char *opentype)` 打开一个受管理的缓冲文件（比直接使用文件描述符更容易读写）。 23
- `int fclose (FILE *stream)` 关闭用 `fopen` 打开的文件。
- `char * gets (const char *s, int count, FILE *stream)` 将一行字符获取到字符串 `s` 中。
- `int fputs (const char *s, FILE *stream)` 将字符串写入给定的打开文件。
- `int sprintf (FILE *stream, const char *template, ...)` 就像 `printf`，但它使用打开的文件而不是默认使用标准输出。

你可以通过访问 `http://www.gnu.org/software/libc/manual/` 找到此库的完整手册。

- 2. `stdin`, `stdout`, `stderr`（全小写）可以在这些程序中使用。
- 3. `FILE` 是一个 `struct`。

## 构建共享库

假设我们想取第 6 章的所有代码并将其构建成库。我们要做的第一件事是将它们汇编如下：

```
as write-record.s -o write-record
as-record.o
```

现在，我们不是将它们链接到程序中，而是将它们链接到一个共享库中。这改变了我们的命令：

```
ld -shared write-record.o
```

这把两个文件链接到名为 `librecord.so` 的共享库中。如果我们需要更新函数，只需更新这一个即可。要链接此库，我们将执行操作：

```
as write-record.s -o write-record
ld -L .dynamic-linker /lib/linux.so.2 \
-o write-records -lrecord write-record.o
```

在该命令中，`-L` 告诉链接器在当前目录查找库（它通常搜索 `/lib`、`/usr/lib` 和其他几个）。正如我们所看到的，选项 `-dynamic-linker /lib/linux.so.2` 指定了动态链接器。选项 `-lrecord` 告诉链接器搜索文件 `librecord.so`。

现在 `write-records` 程序构建了，但它将无法运行。如果我们尝试运行，将得到类似下面的错误：

```
/write-records: error while loading shared libraries:
librecord.so: cannot open shared object file: No file or directory
```

这是因为默认情况下，动态链接器搜索 `/lib`、`/usr/lib` 以及 `/etc/ld.conf` 中列出的任何目录来查找库。为了运行该程序，你需要将库移动到这些目录之一一个，或者执行以下命令：

```
LD_LIBRARY_PATH=
export LD_LIBRARY_PATH
```

或者，如果那给你带来错误，请执行此操作：

```
setenv LD_LIBRARY_PATH .
```
