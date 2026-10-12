
```c
/* ch12-rand.c -- 使用 rand() 生成骰子点数。 */

#include <stdio.h>
#include <stdlib.h>

char *die_faces[] = {    /* ASCII 图形规则！ */
   "    .",  
   "    .",  /* 1 */
   
   "   . ",
   " . .  .",
   "    ."  /* 2 */
   
   "   .  .",
   " . .  .",
   "   .  ."  /* 3 */
   
   "   .  .",
   " . .  .",
   "   .  ."  /* 4 */
   "   .  ."
   
   " . .  .",
   "   .  ."  /* 5 */
   " . .  ."

   " * * * * *",
   "       ",    /* 6 */
   " * * * * *",
   };

/* main --- 打印 N 个不同的骰子面 */

int main(int argc, char **argv)
{
    int nfaces;
    int i, j, k;

    if (argc != 2) {
        fprintf(stderr, "usage: %s number-die-faces\n", argv[0]);
        exit(1);
    }

    nfaces = atoi(argv[1]);

    if (nfaces <= 0) {
        fprintf(stderr, "usage: %s number-die-faces\n", argv[0]);
        fprintf(stderr, "\tUse a positive number!\n");
        exit(1);
    }

    for (i = 1; i <= nfaces; i++) {
        j = rand() % 6;     /* 强制范围 0 <= j <= 5 */
        printf("+-------+\n");
        for (k = 0; k < 3; k++)
            printf("|%s\n", die_faces[(j * 3) + k]);
        printf("+-------+\n");
    }

    return 0;
}
```

该程序使用简单的 ASCII 图形来打印出类似骰子面的效果。你通过调用程序并指定要打印的骰子面数量来实现。这由第 44 行的 `atoi()` 计算得出。（通常，应避免在生产代码中使用 `atoi()`，因为它不进行错误或溢出检查，也不进行任何输入验证。）

关键行是第 53 行，它使用取模运算符 `%` 将 `rand()` 的返回值转换为 0 到 5 之间的数字。值 `j * 3` 充当 `die_faces` 数组的起始索引，用于构成每个骰子面的三个字符串。第 54 行和第 57 行打印出周围的顶部和底部行，第 55 行和第 56 行的循环打印出面本身。运行时，它会产生如下输出：

```bash
$ ch12-rand 2   # 打印两个骰子
```

![](img/766b5597246d532412fad21b1c59ccec_489_0.png)

`rand()` 接口可追溯到 V7 和 PDP-11。特别地，在许多系统上，结果仅为 16 位数字，这严重限制了可返回数字的范围。此外，其使用的算法在现代标准下被认为“较弱”。（glibc 版本的 `rand()` 没有这些问题，但编写可移植代码时需要意识到 `rand()` 不是最佳 API。）

`ch12-rand.c` 使用一种简单技术来获得特定范围内的值：`%` 运算符。该技术使用返回值的低位（就像十进制除法中，除以 10 或 100 的余数使用最低的 1 位或 2 位十进制数字）。事实证明，历史上的 `rand()` 生成器在中间和高位上产生随机值的效果优于低位。因此，如果你必须使用 `rand()`，请尽量避免使用低位。GNU/Linux 的 `rand(3)` manpage 引用了《Numerical Recipes in C》，该书推荐了此技术：

```c
j = 1+(int) (10.0*rand()/(RAND_MAX+1.0)); /* 获取 1 到 10 之间的数字 */
```

### 12.6.2 POSIX 函数：random() 和 srandom()

4.3 BSD 引入了 `random()` 及其配套函数。这些函数使用好得多的随机数生成器，返回 31 位值。它们现在是 POSIX 标准化的 XSI 扩展：

```c
#include <stdlib.h>    // XSI

long random(void);
void srandom(unsigned int seed);
char *initstate(unsigned int seed, char *state, size_t n);
char *setstate(char *state);
```

前两个函数与 `rand()` 和 `srand()` 紧密对应，可以类似地使用。然而，与产生伪随机数序列的单个种子值不同，这些函数使用种子值加上一个状态数组：一个包含计算伪随机数所需状态信息的字节数组。最后两个函数让你管理状态数组。

* `long random(void);`
  返回 0 到 2<sup>31</sup> − 1 之间的数字。（虽然 GNU/Linux 的 `random(3)` manpage 说在 0 和 `RAND_MAX` 之间，但这仅适用于 `RAND_MAX` 等于 2<sup>31</sup> − 1 的 glibc 系统。在其他系统上，`RAND_MAX` 可能更小。POSIX 明确指出范围是 0 到 2<sup>31</sup> − 1。）
* `void srandom(unsigned int seed);`
  设置种子。如果从未调用 `srandom()`，默认种子为 1。
* `char *initstate(unsigned int seed, char *state, size_t n);`
  使用生成随机数所需的信息初始化状态数组。`seed` 是要使用的种子值，类似于 `srandom()`，`n` 是状态数组中的字节数。
  `n` 应为 8、32、64、128 或 256 之一。较大的值产生更好的随机数序列。小于 8 的值会导致 `random()` 使用与 `rand()` 类似的简单随机数生成器。大于 8 且不等于列表中值的结果会被舍入到最近的合适值。
* `char *setstate(char *state);`
  将内部状态设置为 `state` 数组，该数组必须由 `initstate()` 初始化。这让你可以随意在不同的状态之间切换，提供多个随机数生成器。

如果从未调用 `initstate()` 和 `setstate()`，`random()` 使用大小为 128 的内部状态数组。

状态数组是不透明的；你用 `initstate()` 初始化它，并通过 `setstate()` 将其传递给 `random()` 函数，但除此之外你不需要查看其内部。如果你使用 `initstate()` 和 `setstate()`，则不需要再调用 `srandom()`。

因为种子包含在状态信息中。`ch12-random.c` 使用这些例程而不是 `rand()`。它还将随机数生成器用当前时间加上 PID（进程 ID）作为种子，这是一种常用的技术。
