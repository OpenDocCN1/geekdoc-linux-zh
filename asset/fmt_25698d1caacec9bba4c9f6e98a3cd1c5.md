
`$ gcc -I/usr/include/rpm -c rpm1.c`

![](img/9d29d6681c5f42792ea5da4b12142ca2_326_0.png)

这意味着你可以根据需要将 RPM 头文件安装在其他目录，只需更改 `I` 命令行选项即可。

为了帮助调试问题，你可能想添加 `-Wall`（输出所有警告）和 `-g`（编译调试信息）选项。例如：

```bash
$ gcc -Wall -g -I/usr/include/rpm -c rpm1.c
```

## 库

主 库是 `librpm.a` 或其共享版本。为了进行任何 RPM 编程，你需要链接表 16-3 所示的库。

### 表 16-3 需要的 RPM 库
| 库 | 用途 |
| --- | --- |
| Rpm | 主 RPM 库 |
| Rpmdb | RPM 数据库库 |
| Rpmio | RPM 输入输出库 |
| Popt | 命令行选项解析库 |

如果你从你的 C 程序创建 RPM，你还需要链接 `rpmbuild` 库。要编译并链接一个简单的 RPM 程序，你需要类似下面的命令：

```bash
gcc -I/usr/include/rpm -o program program.c -lrpmbuild \
-lrpm -lrpmdb -lrpmio -lpopt
```

在某些版本的 Linux或其他操作系统上，你可能需要链接一组辅助库，如下所示：

```
gcc -I/usr/include/rpm -o program program.c -lrpmbuild \
-lrpm -lrpmdb -lrmpio -lpopt -lelf -lbz2
```

如果你在非标准目录下安装了 RPM 库，则需要使用 `-L` 选项来指定查找库的路径。例如：

```
gcc -I/usr/include/rpm -o program program.c -L/opt/lib/rpm \
-lrpmdb -lrpm -lrmpio -lpopt -lelf -lbz2
```

- `-L` 选项告诉 `cc` 编译器在 `/opt/lib/rpm` 目录以及如 `/usr/lib` 等标准位置中查找库。

从 RPM 4.2 开始，你只需要链接 RPM 库即可。如果需要，其他库将被自动引入。

## 获取你的 RPM 环境信息

第 21 节介绍了 RPM 的定制化。

```c
int rpmReadConfigFiles(const char *files, const char *target);
```

`files` 参数包含一个由冒号分隔的文件列表，这些文件组成了系统配置。`target` 参数持有目标平台。你可以为这两个参数传递 `NULL` 来使用 RPM 的默认值，这通常是现在的做法。

## 第 16 节：使用 C 语言编写 RPM

`rpmReadConfigFiles` 函数成功时返回 0，失败时返回 -1。一旦你读取了配置文件，就可以访问配置中的值，或将其打印出来。

## 打印配置

要打印配置，调用 `rpmShowRC`。

```c
int rpmShowRC(FILE* output);
```

传入一个输出文件来打印配置，例如 `stdout`。示例如：

```c
rpmShowRC( stdout );
```

`rpmShowRC` 函数始终返回 0。

为了控制 `rpmShowRC` 以及其他 RPM 库函数的某些输出，你可以通过调用 `rpmSetVerbosity` 设置日志详细程度：

```c
void rpmSetVerbosity(int level);
```

例如：

```c
rpmSetVerbosity(RPMMESS_NORMAL);
```

> 表 16-4 列出了来自 `rpmio/rpmmessages.h` 的详细程度级别，从输出最少到输出较多。

## 表 16–4 输出详细程度级别

| 级别 | 用法 |
|---|---|
| RPMESS_FATALERROR | 仅限严重错误条件及以上 |
| RPMESS_ERROR | 仅限错误条件及以上 |
| RPMESS_WARNING | 仅限警告条件及以上 |
| RPMESS_QUIET | 与 RPMESS_WARNING 相同 |
| RPMESS_NORMAL | 仅限重要消息 |
| RPMESS_VERBOSE | 详细信息消息 |
| RPMESS_DEBUG | 调试信息及以上所有内容 |

## 第三部分：编写 RPM

你可以组合成一个简单的 RPM 程序，如列表 16-1 所示。

列表 16-1：rpml.c

```c
/* 显示 rpmrc 设置。 */
#include <stdio.h>
#include <stdlib.h>
#include <rpmlib.h>
int main(int argc, char * argv[]) {
    int status = rpmReadConfigFiles((const char*) NULL,
                                   (const char*) NULL);
    if (status != 0) {
        printf("Error reading RC files.\n");
        exit(-1);
    } else {
        printf("Read OK OK\n");
    }
    rpmSetVerbosity(RPMMESS_NORMAL);
    rpmShowRC( stdout);
    exit(0);
}
```

使用如下命令编译此程序：

```
$ cc -I/usr/include/rpm -o rpm1 rpml.c -lrpm -lrpmdb -lrmio -lpopt
```

当你运行此程序时，你应该能看到屏幕上打印出的你的配置内容。

## 扩展宏的值

由于有了所有的 rc 和宏配置文件，RPM 系统有很多值，通常称为宏（macros），你可以使用它们来引用设置。使用“宏”一词是因为这些值可以不仅仅简单的字符串。你可以让一个宏引用其他宏的值，例如，基础的宏语法为：

```
%name_of_macro
```

## 第 16 节：使用 C 语言编写 RPM 305

例如：

```
%_target
```

大多数内部 RPM 宏以下划线开头。你可以使用 `rpm --eval` 命令来扩展宏：

```
$ rpm --eval %target
i386-linux
```

你也可以使用以下语法引用宏：

```
%(name_of_macro)
```

例如：

```
%(_target)
```

这种语法使得将宏与其他文本和宏组合在一起变得更加容易，因为它清晰地界定了宏名称。

第 21 节深入探讨了宏。在你的 C 程序中，代码可能需要扩展宏的值以便将数据放置在正确的目录中、确定平台架构等。

## 在你的代码中扩展宏

你可以使用 `rpmExpand` 从你的 C 程序中确定系统宏的值。

`rpmExpand` 函数可以扩展一个或多个宏的值，返回扩展后的值。你可以向 `rpmExpand` 传递变数量参数：

```c
char* rpmExpand(const char *arg);
```

相比更简单的库，popt 的主要优势在于处理复杂参数和定义别名的能力。`rpm` 命令根据上下文为 `-i` 选项提供不同的行为（安装软件包、作为查询的一部分获取软件包信息以及执行源 RPM 的安装阶段）。

列表 16-2：rpmexpand.c

```c
/* 显示 rpmrc 设置。 */
#include <stdio.h>
#include <stdlib.h>
#include <rpmlib.h>
#include <rpmmacro.h>
int main(int argc, char * argv[]) {
    int status = rpmReadConfigFiles((const char*) NULL,
                                   (const char*) NULL);
    if (status != 0) {
        printf("Error reading RC files.\n");
        exit(-1);
    }
    char *value = rpmExpand(argv[1], (const char*) NULL);
    printf("Value of macro is [%s]\n", value);
    exit(0);
}
```
