
## 磁带设备选项说明

其中`-f/dev/tape_device`指定使用的磁带设备，`-c suboptions`指定各种命令：

| 命令 | 描述 |
| :--- | :--- |
| `rewind` | 回退磁带驱动器 |
| `weof-n` | 写入文件标记 |
| `fsf-n` | 前进文件 |

列表 9.2 程序只需解析这些选项和子选项，然后列出剩余的命令参数。

### 列表 9.2 `xmt.c`—使用`getopt(3)`和`getsubopt(3)`的示例

```c
/* xmt.c */

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

extern char *suboptarg;
int getsubopt(char *optionopt, char *const tokens, char **value);

main(int argc, char **argv) { /* 返回代码 */
    int rc = 0; /* 参数索引 */
    int x; /* 整数值 */
    int n; /* 整数值 */
    char *value; /* 指向子选项值的指针 */
    int optch; /* 选项字符 */
    static char optstring[1] = "f:c";

    /* 子选项令牌表： */
    static char *tokens[] = {
        #define _SO_WEOF 0 /* 写入 n 个 EOF 标记 */
        "weof",
        #define _SO_FSF 1 /* 前进文件 */
        "fsf",
        #define _SO_BSF 2 /* 回退文件 */
        #define _SO_REWIND 3 /* 回退磁带 */
        "rewind",
        NULL
    };

    /*
     * 处理所有命令行选项：
     */
    while ((optch = getopt(argc, argv, optstring)) != -1)
        switch (optch) {
            case 'f': /* -f 设备 */
                printf("-f %s (磁带设备).\n", optarg);
                break;
            case 'c': /* -c 命令 */
                /*
                 * 处理 -c 的所有子选项：
                 */
                while (optarg != 0) {
                    switch (x = getsubopt(&optarg, tokens, &value)) {
                        case _SO_WEOF:
                            n = !value ? 1 : atoi(value);
                            printf("Write %d EOF mark%s (%s)\n",
                                n, suboptarg, value);
                            break;
                        case _SO_FSF:
                            n = !value ? 1 : atoi(value);
                            printf("Forward space %d file(s) (%s)\n",
                                n, suboptarg, value);
                            break;
                        case _SO_BSF:
                            n = !value ? 1 : atoi(value);
                            printf("Backspace %d file(s) (%s)\n",
                                n, suboptarg, value);
                            break;
                        case _SO_REWIND:
                            if (value) {
                                printf("Illegal substitution %s does not take a\n",
                                    suboptarg);
                                rc = 1; /* Flag usage error */
                            } else {
                                printf("Rewind tape (%s)\n", suboptarg);
                            }
                            break;
                        case -1:
                            printf("Illegal substitution %s%s\n",
                                suboptarg,
                                value ? "=" : "");
                            break;
                        default:
                            abort(); /* Should never happen here */
                    }
                }
                break;
            default:
                rc = 1; /* Usage error has occurred */
        }

    /*
     * Report all arguments:
     */
    for (int i = optind; i < argc; ++i) {
        printf("argv[%d] = '%s'\n", i, argv[i]);
    }

    return rc;
}
```

编译并运行此`xmt`命令会产生以下会话输出：

```bash
$ make xmt
```

从示例中你可以看到回退子进程已被处理，随后是`fsf=3`和`weof=2`，用于在带上写入两个文件结束标记。

# GNU 长选项扩展 (GNU Long Options Extension)

许多 GNU 命令（例如`gcc(1)`编译器）都支持大量的选项。除了你可以用尽这些选项的所有可能字符之外，用户也无法记住所有的选项。GNU 对此问题的解决方案是使用长选项（long options）的约定。

FreeBSD 3.4 版本包含了`gcc(1)`，允许对以下长选项进行演示：

```bash
$ gcc --version
2.7.2
$
```

长选项以两个连字符开头，后面必须紧跟一个或多个字符。为了处理长选项，必须使用 GNU 函数`getopt_long(3)`。

# The GNU `getopt_long(3)` Function

`getopt_long(3)`函数将同时处理传统的短选项和较新的 GNU 长选项。`getopt_long(3)`的概要如下：

该函数的原型与`getopt(3)`几乎相同，区别在于`longopts`和`longindex`这两个参数。参数`longindex`指向一个整数，该整数返回一个索引值。

## 理解选项结构 (Understanding the option Structure)

`longopts`指针指向选项结构条目的数组。选项结构由四个成员组成：

- `name`：指向一个 C 字符串，包含长选项的名称，不包含开头的连字符。
- `has_arg`：定义为整数但用作布尔值使用。如果该选项没有参数，则必须为 0（false）；如果有参数，则为非 0（true）。
- `flag`：指向一个整数或为空。
- `val`：以不同的方式使用，取决于`flag`是如何初始化的。

# 设置选项结构 (Setting Up the option Structure)

选项结构数组中的最后一个条目必须初始化：`name`成员初始化为空指针，`has_arg`成员为 0，`val`成员为空。此条目告知`getopt_long(3)`该数组中已没有更多条目。以下是在静态结构体`long_opts[]`中定义两个长选项的示例：

```c
static struct long_opts[] = {
    { "help", 0, 0, 'h' },   /* name, has_arg, flag, val */
    { "version", 0, 0, 'v' }, /* name, has_arg, flag, val */
    { 0, 0, 0 }
};
```

# 使用空选项.flag (Using a Null option.flag)

选项结构中的`flag`和`val`成员作为一个团队工作。使用这种方法最简单的方法是通过以下步骤：

1. 将`flag`设置为空。
2. 将`val`成员设置为你想要让`getopt_long(3)`返回的值。这通常是等效短选项字母的 ASCII 字符码。

# 让长选项看起来像短选项 (Making a Long Option Look Short)

常见的做法是将`val`设置为与长选项对应的短选项。例如，如果一个命令同时支持`--help`和`-h`，那么选项`flag`将是一个空指针，而`val`将被设置为 ASCII 值 `'h'`。该结构初始化如下：

```c
static struct long_opts[] = {
    { "help", 0, 0, 'h' },   /* name, has_arg, flag, val */
    { 0, 0, 0 }
};
```

## 当 option.flag 为空时的处理 (Processing when the option.flag Is Null)

当处理长选项`--help`时，`getopt_long(3)`函数执行以下步骤：

1. `getopt_long(3)`扫描`long_opts[]`数组，使用我们称之为`x`的索引。它从`x=0`开始。
2. （此处省略部分重复逻辑描述，保持翻译逻辑一致）

# 第 10 章 转换函数

在应用程序中，数据转换的需求是始终存在的。算术运算使用`int`、`float`和`double`类型，因为它们既高效又方便。随后，必须将这些数据转换为 ASCII 字符串才能在终端上显示。数据输入也必须经过转换。

在本章，你将学习：

- `atoi(3)`、`atol(3)` 和 `atof(3)` 族
- `sscanf(3)` 函数
- `strtol(3)` 和 `strtoul(3)` 函数
- `strtod(3)` 函数

这些函数都涉及从 ASCII 到数值 C 数据类型的转换。

## 简单转换函数

这些是 C 程序员使用的是最简单的函数，因为它们不需要准备或后续转换错误测试。除了某些 Unix 平台上的`atof(3)`外，整个转换错误问题都被忽略了。因此如此，它们通常不是可用函数中的最佳选择。

在探索替代方案之前，让我们更仔细地查看这些传统函数。

### 仔细审查 `atoi(3)` 和 `atol(3)` 函数

`atoi(3)`和`atol(3)`函数具有如下用法说明：

```c
#include <stdlib.h>
int atoi(const char *nptr);
long atol(const char *nptr);
```

这些函数只需接收 C 字符串的起始地址，并将结果作为`int`或`long`数值返回。在开始转换之前，会跳过 C 库函数`isspace(3)`定义的任何空白字符。如果转换失败，`atoi(3)`和`atol(3)`函数将直接放弃并返回零。

### 使用 `atoi(3)` 函数

以下使用`atoi(3)`函数的简单示例：

```c
char buf[32];
int i;
strcpy(buf, "23");
i = atoi(buf);
```

在这个示例中，字符串 "23" 被转换为整数值 23 并赋值给变量`i`。然而，如果输入字符串包含无效输入，`i`的值将不包含有意义的结果（零）。

### 理解转换错误问题

以使用函数`atoi(3)`的情况为例。假设有一个形式为`-x n`的调试命令行选项，其中`n`是 0 到 9 之间的调试级别。在`getopt(3)`处理循环中，`x`的`optarg`值必须被转换为整数值。

```c
switch (optch) {
  case 'x':
    cmopt_x = atoi(optarg); /* 获取调试级别 */
    break;
}
```

假设用户在命令行上提供了选项`-x`，但他们并不知道为什么。在这种情况下，`atoi(3)`函数会轻率地返回值 0，因为它无法将无效字符串转换为整数数值。程序将不会察觉到应该设置调试级别，因为转换值是 0（由于转换错误）。因此，程序将在没有任何调试级别的情况下运行。这导致程序对用户不友好。

### 转换乱码数据

当用户因为键盘打字笨拙而提供`-x 5loops`作为调试选项时，也会出现类似的问题。程序会乐意地接受`atoi(3)`能够成功转换的值 5。字符串的剩余部分 "loops" 被忽略了。

`atoi(3)`、`atol(3)` 和 `atof(3)` 函数都缺乏错误信息。需要更好的指示来判断转换何时成功或失败。

### 知道转换在何处结束

`atoi(3)`族函数的另一个限制是调用者没有关于转换从输入字符串何处结束的信息。如果需要编写一个函数从日期字符串中提取月、日、年，使用`atoi(3)`函数将面临挑战。考虑可能从终端作为输入的日期字符串的以下变化：

- `01/01/2000`
- `1/2/2000`
- `12/1/2000`
- `1 / 9/2000`
- `1 / 31 / 2000`
- `6-31-2000`

`atoi(3)`函数只能帮助提取月份（假设格式为 月/日/年）。提取月份后，你还会剩下这些问题：跳过了多少空格？有多少个数字？是否有尾随空格？因为`atoi(3)`没有获取到扫描信息，你的代码不知道从哪里开始提取后续的天或年字段。

### `atof(3)` 函数

`atof(3)`函数与`atoi(3)`函数非常相似，区别在于它将字符串值转换为浮点值。`atof(3)`的用法说明如下：

```c
#include <stdlib.h>
double atof(const char *nptr);
```

它的用法同样简单。这是一个示例：

```c
char buf[32];
double f;
strcpy(buf, "-467.01E+02");
f = atof(buf);
```

示例显示了领先空白、一个符号字符、一个小数和一个带符号的指数。`atof(3)`函数跳过领先空白，并将剩余字符转换为`double` C 值，并赋值给变量`f`。

再次，这种调用的简单性诱导了许多 C 程序员使用这种转换形式。然而，`atoi(3)`和`atof(3)`存在的问题也适用于`atof`。大多数 UNIX 平台将`atof(3)`函数实现为对`strtod`的调用：

```c
strtod(nptr, &NULL);
```

`strtod`函数返回特殊值`HUGE_VAL`、`-HUGE_VAL`和 0（零），并带有外部变量`errno`（见“测试错误”章节）。由于`atof(3)`的实现可能总是基于`strtod`，你应该使用`strtod`来测试错误。

### 使用 `sscanf(3)` 进行转换

`sscanf(3)`函数就像是输入和转换的“瑞士军刀”。虽然这种机制不是所有转换的完美解决方案，但它仍然具有使用的简单性并提供了一些错误检测。

### 将 `sscanf(3)` 应用于转换

列表 10.1 显示了一个从字符串提取月、日、年的程序。输入数据被变得尽可能混乱，带有大量空白。

**列表 10.1 `sscanf.c` — 提取字段**

```c
/* sscanf.c */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, char *argv[]) {
    int x;
    char *datestr; /* 日期字符串 */
    int nf; /* 转换的字段数量 */
    int mm, day, yyyy; /* 月、日、年 */
    static char *sdate[] = {
        "1 / 2 / 2000 ",
        "03 9-2001,etc."
    };
    
    for (x = 0; x < 2; x++) {
        datestr = sdate[x]; /* 解析此日期 */
        nf = sscanf(datestr, "%d/%d/%d", &mm, &day, &yyyy);
        printf("Extracting %s\n", datestr);
        
        if (nf >= 3) {
            printf("Remainder '%s'\n", datestr + strlen(datestr) - 8); // 示意性代码，实际需根据解析位置调整
        }
    }
    
    printf("%02d/%02d/%04d nf=%d\n", mm, day, yyyy, nf);
    return 0;
}
```
