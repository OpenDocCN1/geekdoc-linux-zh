
# 第 2 章 • 参数、选项与环境

并且在其他情况下不存在。在缺失的情况下，`GNU getopt()` 返回选项字母并将 `optarg` 设置为 `NULL`。例如，给定的输入是——

```c
while ((c = getopt(argc, argv, "ab:")) != -1)
```

`-bYANKEES`，返回值为 `'b'`，`optarg` 指向 `"YANKEES"`；对于 `-b` 或 `- YYANKEES`，返回值仍然是 `'b'`，但 `optarg` 被设置为 `NULL`。在后一种情况下，`"YANKEES"` 是一个独立的命令行参数。

## 2.3 选项解析：`getopt()` 和 `getopt_long()`

### 2.3.3 长选项

`getopt_long()` 函数处理上述描述形式的长选项的解析。另一个例程 `getopt_long_only()` 的工作原理相同，但它用于所有选项均为长选项且以单字符 `-` 字符开头的程序。否则，两者的作用都与 `GNU getopt()` 函数一样。为了简洁起见，每当我们说“`getopt_long()`”，就等同于在说“`getopt_long()` 和 `getopt_long_only()`”。以下是来自 `GNU/Linux` `getopt(3)` 手册的声明：

```c
#include <getopt.h>

int getopt_long(int argc, char *const argv[],
             const char *optstring,
             const struct option *longopts, int *longindex);

int getopt_long_only(int argc, char *const argv[],
             const char *optstring,
             const struct option *longopts, int *longindex);
```

前三个参数与 `getopt()` 相同。下一个参数是一个指向 `struct option` 数组的指针，我们称之为长选项表，稍后会进行描述。`longindex` 参数如果没有设置为 `NULL`，则指向一个变量，该变量将被填充为找到的长选项在长选项表中的索引。这对于错误诊断等非常有用。

#### 2.3.3.1 长选项表

长选项通过 `struct option` 结构体数组描述。`struct option` 在 `<getopt.h>` 中声明；它看起来如下：

```c
struct option {
  const char *name;
  int has_arg;
  int *flag;
  int val;
}
```

结构体中的元素如下：

*   `const char *name`
    这是选项的名称，不带任何前导横线，例如 `"help"` 或 `"verbose"`。

*   `has_arg`
    这描述了长选项是否带有参数，如果是，是什么种类型的参数。该值必须是表 2.1 中所示的数值之一。
    符号常量是表中给定数值值的宏。虽然数值值可以工作，但符号常量的可读性高得多，在您编写的任何代码中，都应该使用它们代替相应的数字。

*   `flag`
    如果此指针为 `NULL`，则 `getopt_long()` 返回结构体中 `val` 字段的值。如果它不是 `NULL`，则它指向的变量将被填充为 `val` 中的值，且 `getopt_long()` 返回 `0`。如果 `flag` 不是 `NULL` 但从未见过该长选项，则所指向的变量不会改变。

*   `val`
