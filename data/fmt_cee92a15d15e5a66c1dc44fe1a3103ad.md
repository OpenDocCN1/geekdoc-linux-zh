
```
printf("No, x is not equal to 10 or 20\n");

if (x > 10) {

    printf("Yes, x is more than 10\n");

}

while (x > 0) {

    printf("x is %d\n", x);

    x = x - 1;

}

for (x = 0; x < 10; x++) {

    printf("x is %d\n", x);

}

switch (x) {

    case 9:

    printf("x is nine\n");

    break;

    case 10:

    printf("x is ten\n");

    break;

    case 11:

    printf("x is eleven\n");

    break;

    default:

    printf("x is huh?\n");

    break;

}

return 0;
```

很容易看出，这些语句是执行的，尽管它们与 shell 脚本大不相同。C 代码工作在花括号括的语句块中，就像 shell 脚本中的 `do` 和 `done` 一样。

注意，在许多其他编程语言中，当我们想给一个变量加 1 时，必须写成类似 `x = x + 1`。在 C 中，使用了缩写 `x++`，意味着将变量加 1。

`for` 循环在 `(...)` 之间接受三个语句：一个起始语句、一个比较语句，以及一个在每次完成语句块执行后执行的语句。`for` 之后的语句块会重复执行，直到比较结果为假为止。

`switch` 语句类似于 shell 脚本中的 `case`。`switch` 考虑其 `(...)` 内部的参数并决定跳转到哪一行。在这个示例中，它显然将执行 `printf("x is ten\n");`，因为当上一个 `for` 循环执行时 `x` 是 10。`break` 标记意味着我们已经完成了 `switch` 语句，执行应该从第 46 行继续。

## 22. C 语言入门介绍
## 22.1. C 基础

注意在 C 语言中，比较使用的是 `==` 而不是 `=`。符号 `=` 意味着给变量赋值，而 `==` 是一个相等性判断运算符。

### 22.1.5 字符串、数组和内存分配

你可以通过以下方式定义数字列表：

```c
int y[10];
```

这个列表被称为数组：

```c
#include <stdlib.h>

#include <stdio.h>

int main(int argc, char *argv[]) {

    int x;

    int y[10];

    for (x = 0; x < 10; x++) {

        y[x] = x * 2;

    }

    for (x = 0; x < 10; x++) {

        printf("item %d is %d\n", x, y[x]);

    }

    return 0;

}
```

如果数组的类型是字符，那么它被称为字符串：

```c
#include <stdlib.h>

#include <stdio.h>

int main(int argc, char *argv[]) {

    int x;

    char y[11];

    for (x = 0; x < 10; x++) {

        y[x] = 65 + x * 2;

    }

    for (x = 0; x < 10; x++) {

        printf("item %d is %d\n", x, y[x]);

    }

    y[10] = 0;

    printf("string is %s\n", y);

    return 0;

}
```

注意，字符串是空字符终止的。这意味着最后一个字符是零。代码 `y[10] = 0` 将数组中的第 11 个项目设置为零。这也意味着字符串需要比你认为的要长一个字符。

（注意，数组中的第一个项目是 `y[0]`，而不是 `y[1]`，这与其他编程语言不同。）

在之前的示例中，`char y[11]` 这一行代码为字符串预留了 11 个字节。但如果你想要一个 100,000 字节的字符串呢？C 允许你向内核请求内存。任何非平凡的程序都会为自己分配内存，并且没有其他方法可以为程序获取大块内存内存来使用：

```c
#include <stdlib.h>

#include <stdio.h>

int main (int argc, char *argv[]) {

    int x;

    char *y;

    y = malloc(11);

    printf("%d\n", y);

    for (x = 0; x < 10; x++) {

        y[x] = 65 + x * 2;

    }

    y[10] = 0;

    printf("string is %s\n", y);

    free(y);

    return 0;

}
```

声明 `char *y` 意味着声明一个名为 `y` 的变量（数字），它指向一个内存位置。在此语文中，`*`（星号）意味着指针。例如，如果你有一台可能有 256 兆字节 RAM + 交换内存的机器，那么你可能拥有这样一个范围。`y` 的数值值也会通过 `printf("%d\n", y)` 打印出来，但这对程序员来说是有意义的。当你用完内存后，必须通过 `free` 将其归给操作系统。不释放内存的程序会导致内存泄漏。

## 22. C 语言简单简介
## 22.1. C 基础

`fgets` 命令从文件中获取一个字符。它从文件中检索连续的字节，直到到达文件末尾，此时它返回 -1。`break` 语句表示立即终止 `for` 循环，随后执行将从第 21 行开始继续。`break` 语句也可以出现在 `while` 循环中。

你会发现 `for` 语句是空的。这是合法的 C 代码，并意味着无限循环。

其他文件函数还有 `fread`、`fwrite`、`fputs`、`printf` 和 `fseek`。参见 `fwrite(3)`、`fputc(3)`、`fprintf(3)` 和 `fseek(3)`。

### 22.1.8 在 C 程序中读取命令行参数

到为止，你可能在想 `(int argc, char *argv[])` 是干什么用的。这些是 shell 传递给程序的命令行参数。`argc` 是命令行参数的总数，`argv` 是一个包含每个参数字符串的数组。我们像这样输出它们：

```c
#include <stdlib.h>

#include <stdio.h>

#include <string.h>

int main(int argc, char *argv[]) {

    int i;

    for (i = 0; i < argc; i++) {

        printf("argument %d is %s\n", i, argv[i]);

    }

    return 0;

}
```

### 22.1.9 一个更复杂的示例

这里我们将这些内容整合到一个程序中，该程序读取许多文件并作为单词输出。这里你将遇到一些新符号：`!=` 是 `==` 取反，用于测试不等于；`realloc` 重新分配内存——它调整旧内存块的大小，以确保内存块中的任何字节都被保留；`\n`、`\t` 分别表示换行字符 10 和制表符 9（参见 `ascii(7)`）。

```c
#include <stdlib.h>

#include <stdio.h>

#include <string.h>

void word_dump(char *filename) {

    int length_of_word;
```
