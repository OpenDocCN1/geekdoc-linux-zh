
```c
// destruct.c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>

extern "C" {
    char *tempnam(const char *tmpdir, const char *prefix);
}

static char *tf_path = NULL;

/* 清理函数： */
static void mr_clean(void) {
    puts("mr_clean() started:");
    if (tf_path != NULL) {
        printf("unlinking temporary file %s\n", tf_path);
        free(tf_path);
        tf_path = NULL;
    }
    puts("mr_clean() ended.");
}

/* 主程序： */
int main(int argc, char *argv[]) {
    FILE *tmp = 0;

    /* 注册清理 */
    atexit(mr_clean);

    /* 创建临时文件名： */
    if ((tf_path = tempnam("/tmp", "tmp-")) == NULL) {
        fprintf(stderr, "%s: creating temp file.\n", strerror(errno));
        abort();
    }
    printf("Temp. file is %s\n", tf_path);

    /* 创建、打开并写入临时文件： */
    if ((tmp = fopen(tf_path, "w+")) == NULL) {
        fprintf(stderr, "%s: opening %s\n", strerror(errno), tf_path);
        abort();
    }
    fprintf(tmp, "PID %ld was here.\n", (long)getpid());

    /* 正常退出，未链接临时文件： */
    fclose(tmp);
    return 0;
}
```

### 164 高级编程

对程序的检查显示，首先通过 `atexit(3)` 注册了 `mr_clean()` 函数，位于第 49 行。54-72 行创建了临时文件、写入并将其关闭。程序在第 73 行正常退出。

退出会导致调用 `mr_clean()` 函数来释放创建的临时文件。可以通过下面的编译和运行会话所示：

```
$ make atexit
cc -c D_POSIX_SOURCE=199309L -D_POSIX_SOURCE -Wall atexit.c
ccatexit.o -oatexit
$ ./atexit
Temp. file is /tmp/tmp-D5282
mr_clean() started:
unlinking temporary file /tmp/tmp-D5282
mr_clean() ended.
$
```

程序宣布（8.6 的第 58 行）它创建了临时文件 `/tmp/tmp-D5282`，然后从 `main()` 程序默默退出（第 73 行）。这导致注册的清理函数 `mr_clean()` 被调用，随后它产生了最后三行输出，表示它已 `unlink(2)` 删除了临时文件。

你应该记住的主要可移植性问题之一是，某些平台限制注册函数的数量最多 32 个。如果你正在设计一个 C 库，这是关键的，因为你无法控制用户如何使用 `atexit(3)`。如果库的调用者已经使用了所有 32 个注册，那么你的库将无能可用。

这个问题可以通过注册一个特殊函数来回避，该函数可以调用任意数量的额外清理函数。

## 使用 C++ 析构函数

C++ 程序员有能力依赖析构函数进行清理操作。列表 8.7 展示了一个使用临时文件的 Temp 类简单示例。

# 高级 UNIX 编程

接上页

```cpp
26:    Temp &printf(const char *format,...);
27:    Temp &rewind();                      // 回置
28:    Temp &gets(char *buf, int bufs);
29:    };
30:

/////////////////////////////////////////////////////////////////////////////////
                                     // 构造函数
/////////////////////////////////////////////////////////////////////////////////
Temp::Temp() {

    /*
     * 创建临时文件路径：
     */
    if ((tf_path = tempnam("/tmp/tmp-"))) {
        throw errno;
                                      // 临时文件生成失败

    /*
     * 创建、打开并写入临时文件 =
     */
    if ((tf = fopen(tf_path,"w+"))) {
        throw errno;
                                      // 打开 tf_f 失败
    printf("Created temp file: %s", tf_path);
}

/////////////////////////////////////////////////////////////////////////////////
// 析构函数：


Temp::~Temp() {                                 // 关闭打开的文件
    fclose(tf);
    unlink(tf_path);                      // 删除临时文件
    delete tf_path;                       // 释放路径字符串

    write(1,"Temp::~Temp() called. \n",22);
}

/////////////////////////////////////////////////////////////////////////////////
// printf() 方法
//
// 允许调用者利用 printf() 的便利性向临时文件写入
/////////////////////////////////////////////////////////////////////////////////

Temp &Temp::printf(const char *format,...) {
    va_list ap;

    va_start(ap,format);
    printf(tf,format,ap);
    va_end(ap);
    return *this;
  }
```

# 第 8 章 • 临时文件与进程清理 167

```cpp
   /////////////////////////////////////////////////////////////////////////////////
   // 回置临时文件：
   /////////////////////////////////////////////////////////////////////////////////

   Temp &
   Temp::rewind() {
       rewind(tf);      // 回置临时文件
       return *this;
   }

   /////////////////////////////////////////////////////////////////////////////////
   // 从临时文件中回读一行文本：
   /////////////////////////////////////////////////////////////////////////////////

   Temp &
   Temp::gets(char *buf, int bufsiz) {
      int e;
      if (!fgets(buf, bufsiz, tf)) {
          if (feof(tf))         // 是否 EOF？
              throw EOF;            // 表示 EOF
          e = errno;
          clearerr(tf);
          throw e;                // 抛出错误
      }
  }
  return *this;
 }

  /////////////////////////////////////////////////////////////////////////////////
  // 主程序：
  /////////////////////////////////////////////////////////////////////////////////

  int main(int argc, char *argv[]) {
     Temp tf;                  // 创建临时文件
     char buf[256];

     (void)argc;
     (void)argv;

     // 宣布程序开始：
     printf("PID %ld started:\n", (long)getpid());

     // 向临时文件写入一行文本：
     tf.printf("PID %ld was here.\n", (long)getpid());

     tf.rewind();              // 回置临时文件
```

# 168 高级 UNIX 编程

接上页

```cpp
    // 现在从临时文件中回读那行文本
    {
        try {
            tf.gets(buf,sizeof(buf));
        } catch (int e) {
            fprintf(stderr,"%s\n",strerror(errno));
            exit(1);
        }
    }
    printf("Read back: %s\n",buf);
    puts("Now exiting.");
    return 0;
```

// destruct.cc 结束

列表 8 中的程序在第 20–29 行定义了 Temp 类。`Temp::printf()` 方法允许调用者格式化一行文本并写入临时文件。`Temp::rewind()` 方法回置临时文件，而 `Temp::gets()` 方法允许调用者从临时文件中检索一行内容。

构造函数实现在第 36–51 行。注意第 41 行中对 `tempnam(3)` 的调用，以及第 47 行中对 `open(3)` 的调用用于创建并打开文件。路径存储在私有成员 `tf_path` 中，打开的文件保存在私有成员 `tf` 中（在第 21 和 22 行声明）。

当 Temp 对象被销毁时，会调用在第 57–63 行实现的析构函数。析构函数关闭临时文件，删除路径，然后释放路径字符串（第 58–60 行）。

`main()` 程序在第 119 行构造了一个 Temp 实例（对象命名为 `tf`）。当 `main()` 程序在第 145 行退出（返回语句）时，该对象会被销毁。第 129–142 行演示了对象的某些方法：向临时文件写入了一行，对文件进行了回置，并回读了一行文本。

编译并运行此程序应该得到类似以下的结果：

```
$ make destruct
cc -c -D_POSIX_SOURCE -Wall destruct.cc
cc destruct.o -o destruct -lstdc++
$ ./destruct
PID 1234 started:
Created temp file: /tmp/tmp-XXXXXX
Read back: PID 1234 was here.
```

Temp exiting called.

# 第 8 章 • 临时文件与进程清理 169

许多 UNIX 工具都使用临时文件。本章将介绍如何创建、使用和清理这些文件。你现在将了解如何管理临时文件，例如：

`tempnam(3)` 生成临时文件路径；`open(3)` 打开文件；`fclose(3)` 关闭文件；`unlink(3)` 删除文件；`rewind(3)` 回置文件指针；`printf(3)` 和 `gets(3)` 用于文件的读写。

# 使用 exit() 避免清理

在 UNIX 程序中，有时需要通过 `exit()` 终止程序而不执行某些清理操作。这在发生错误时是必要的。使用 `exit()` 方法如下：

```c
#include <unistd.h>

void exit(int status);
```

## 总结

本章结束了对临时文件的介绍。你现在已经掌握了管理临时文件的知识，例如使用 `exit()` 避免清理。下一章将检查非常重要的 `getopt(3)` 函数。该函数使你的应用程序能够轻松解析命令行选项。

# 第二部分

# 库函数

- 9 UNIX 命令行处理
- 10 转换函数
- 11 UNIX 日期时间设施
- 12 用户 ID、密码与组管理
- 13 静态与共享库
- 14 数据库库例程

# 第 9 章

# UNIX 命令行处理

任何在 shell 提示符下使用 UNIX 一段时间的人都会无意中熟悉各种命令。例如，最常用的命令——`ls(1)`, `mv(1)`, `cp(1)`, `rm(1)` 和 `ln(1)`——都遵循通用命令行规范。

这种一致性源于 UNIX 开发者采用的规范以及一种便于遵循的库机制。在本章中，你将学习：

- UNIX 命令行规范
- 使用 `getopt(3)` 解析行
- 使用 `getsubopt(3)` 解析子选项
- 使用 GNU 的 `getopt_long(3)` 解析行

### 命令行规范

UNIX 命令使用的通用格式如下：

```
$ command_name [-options] [arg1] [arg2] [argn]
```

方括号表示项目是可选的。选项紧跟在后面并以连字符开头。每个选项由单个字符组成——通常是字母，也可以是数字或其他字符。使用时，参数位于选项之后。有效参数的数量由调用的命令决定。

# 使用多个选项

命令行可以使用多个选项。使用多个选项的示例：

```bash
$ ls -1 -u b*
```

该示例使用了选项 `-1` 和 `-u`。在这种情况下，命令行参数是一个通配符文件名。

# 组合多个选项

选项可以组合在一个连字符后面后面。之前的命令在功能上等同于以下命令：

```
$ ls -lu b *
```

此 `ls(1)` 命令演示了选项字符可以在初始连字符字符之后进行组合。

# 使用带参数的选项

某些选项接受除已显示的命令行参数以外的其他参数。查看以下 `tar(1)` 命令：

```
$ tar -cvf project.tar project
```

在这个 FreeBSD 示例中，选项被组合为 `-cvf`。然而，`tar(1)` 的 `-f` 选项必须紧跟一个文件名，这里是 `project.tar`。命令行末尾是命令行参数 `project`，它是要归档的目录名称。该命令也可以写成：

```
$ tar -cv -fproject.tar project
```

在此例中，参数紧紧跟在选项名之后。接受参数的选项，其参数值可以紧跟在选项字母后面，也可以像普通参数一样在命令行中指定。

# 识别选项或参数

你可能会好奇如何知道在选项字母后面的是选项参数还是更多选项。这无法通过命令行的外观来确定。这种行为是由选项本身定义的，它是在程序内部声明的。

# 看起来像选项的参数

你可能遇到过这样的情况：你想指定一个以连字符开头的参数，但你的命令报错说使用了不恰的选项。例如，如果使用 `grep(1)` 在源程序搜索字符串 `--help`，你可能会在 FreeBSD 上遇到以下情况：

```
$ grep -help tempnam.c
grep: illegal option ...
usage grep [-AB] <name> [-CEGLVXHPRSZAbchilnsqvwxy]
  [-e expr] [-f file] [... ]
```

```
$
```

这个 `grep(1)` 命令的问题在于命令对如何处理 `--help` 感到困惑。以下技术了如何避免这个小问题：

```
$ grep --help tempnam.c
$
```

示例显示 `grep(1)` 能够理解命令行上的 `--`（双连字符）表示没有进一步的选项。这允许 `grep(1)` 识别出 `--help` 是要为文件 `tempnam.c` 搜索的文本。

# getopt(3) 函数

帮助 UNIX 命令语法保持一致的方法是，大多数命令都使用了库函数 `getopt(3)`。它的原型如下：

```c
#include <unistd.h>
```

`getopt(3)` 返回解析出的选项字母。或者，当到达选项末尾时返回 `-1`。当遇到未识别的选项字符时，值为 `?`。如果参数 `optstring` 以冒号开头，那么当一个期望参数的选项没有参数时，则返回 `:`。

# getopt(3) 外部值

在使用 `getopt(3)` 之前，你需要了解它是如何使用外部值的。这些变量中最重要的两个是 `optarg` 和 `optind`。

# optarg 变量
