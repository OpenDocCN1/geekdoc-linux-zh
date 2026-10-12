
除了 `strfmon()`，POSIX（但 ISO C 不包括）还为 `printf()` 格式 `%i`、`%d`、`%u`、`%f`、`%F`、`%g` 和 `%G` 提供了一个特殊标志——单引号字符，`'`。在提供千位分隔符的区域设置中，此标志会添加该区域设置的千位分隔符。下面这个简单程序 `ch13-quoteflag.c` 演示了输出：

```c
/* ch13-quoteflag.c -- demonstrate printf's quote flag */
#include <stdio.h>
#include <locale.h>

int main(void)
{
    setlocale(LC_ALL, ""); /* Have to do this, or it won't work */
    printf("%'i\n", 1234567);
    return 0;
}
```

以下是两种不同区域设置下的结果：一种是未提供千位分隔符的，另一种是提供的：

```bash
$ LC_ALL=C ch13-quoteflag
1234567
$ LC_ALL=en_US ch13-quoteflag
1,234,567
```

传统环境，无分隔符

美国英语区域设置，有分隔符

截至今日，只有 `GNU/Linux` 和 `Solaris` 支持 `'` 标志。请务必再次检查你系统的 `printf(3)` 手册页。

### 13.2.6 示例：在 `gawk` 中格式化数值

`gawk` 实现了其自己版本的 `printf()` 和 `sprintf()` 函数。为了具备完整的区域感知能力，`gawk` 必须像 C 语言那样支持 `'` 标志。以下片段来自 `gawk` 3.1.4 中的 `builtin.c` 文件，展示了 `gawk` 如何使用 `struct lconv` 进行数值格式化：

```c
1    case 'd':
2    case 'i':
3    ...
4    tmpval = force_number(arg);
5    ...
6    uval = (uintmax_t) tmpval;
7    ...
8    ii = jj = 0;
9    do {
10   *--cp = (char) ('0' + uval % 10);
11 #ifdef HAVE_LOCALE_H
12   if (quote_flag && loc.grouping[ii] && ++jj == loc.grouping[ii]) {
13   *--cp = loc.thousands_sep[0]; /* XXX - assumption it's one char */
14   if (loc.grouping[ii+1] == 0)
15     jj = 0; /* keep using current val in loc.grouping[ii] */
16   else if (loc.grouping[ii+1] == CHAR_MAX)
17     quote_flag = FALSE;
18   else {
19     ii++;
20     jj = 0;
21   }
22 }
23 #endif
24   uval /= 10;
25 } while (uval > 0);
```

（行号相对于片段开头。）为了便于关注重要部分，代码中与讨论无关的部分已被省略。

变量 `loc`，在第 13–17 行中使用，是一个 `struct lconv`。它在 `main()` 中初始化。对我们感兴趣的是 `loc.thousands_sep`，它是千位分隔符字符，以及 `loc.grouping`，它是一个描述分隔符之间数字位数的数组。零元素意味着“对后续所有数字使用前一元素的值”，而 `CHAR_MAX` 值意味着“停止插入千位分隔符”。

介绍了这些背景之后，让我们看看代码。第 7 行设置了 `val`，这是要格式化值的无符号版本。`ii` 和 `jj` 分别记录在 `loc.grouping` 中的位置以及当前组中已转换的数字位数。¹ 当转换说明符中看到 `\'` 字符时，`quote_flag` 为真。

`do-while` 循环反向生成数字字符，从缓冲区的后端向前端填充。每个数字都在第 11 行生成。第 25 行然后除以 10，将值向右移动一位十进制数字。

第 12–24 行是我们关注的部分。这些操作仅在支持区域设置的系统上执行，如 `<locale.h>` 头文件的存在所指示的那样。符号常量 `HAVE_LOCALE_H` 在这样的系统上将为真。²

当第 13 行的条件为真时，就是时候添加一个千位分隔符字符了。这个条件可以用英语读作“如果请求了分组，并且 `loc.grouping` 中的当前位置指示了分组数量，并且当前数字计数等于该分组数量。” 如果此条件为真，第 14 行添加千位分隔符字符。注释指出了一个可能为真但日后可能会困扰维护者的假设。（“XXX”是标记危险或可疑代码的传统方式。它易于搜索，且对代码读者非常显眼。）

一旦使用了 `loc.grouping` 中的当前位置，第 15–22 行会查看下一个位置的值。如果是 `0`，则应继续使用当前位置的值。我们通过将 `jj` 重置为 `0`（第 16 行）来指定这一点。另一方面，如果下一个位置是 `CHAR_MAX`，则不应再执行分组，第 18 行通过将 `quote_flag` 设置为 `false` 完全关闭它。否则，下一个值是分组值，因此第 20 行将 `jj` 重置为 `0`，第 21 行将 `ii` 递增。

> ¹ 我们可能应该选择比仅仅 `ii` 和 `jj` 更具描述性的名称。由于使用它们的代码很短，我们缺乏想象力并不是一个大问题。
>
> ² 这是由 `Autoconf` 和 `Automake` 机制设置的。`Autoconf` 和 `Automake` 是强大的软件套件，使系统性地支持广泛范围的 `Unix` 系统成为可能。
>
> ¹ 标准中使用的技术术语是基数点（radix point），因为不同进制下的数字也可能有分数部分。然而，对于货币值，使用“小数点”这个词似乎很安全。

## 13.2.7 格式化日期和时间值：`ctime()` 与 `strftime()`

这是底层且详细的代码。然而，一旦你理解了 `struct tm` 中信息是如何呈现的，阅读这段代码就会变得很直接（编写时也很直接）。

第 6.1 节“时间和日期”，第 166 页，描述了用于获取和格式化时间及日期值的函数。如果正确调用了 `setlocale()`，`strftime()` 函数也会感知区域设置（locale）。以下简单程序 `ch13-times.c` 展示了这一点：

```c
/* ch13-times.c --- demonstrate locale-based times */

#include <stdio.h>
#include <locale.h>
#include <time.h>

int main(void)
{
    char buf[100];
    time_t now;
    struct tm *curtime;

    setlocale(LC_ALL, "");
    time(&now);
    curtime = localtime(&now);
    (void) strftime(buf, sizeof buf,
        "It is now %A, %B %d, %Y, %I:%M %p", curtime);

    printf("%s\n", buf);

    printf("ctime( ) says: %s", ctime(&now));
    exit(0);
}
```

当运行该程序时，我们会看到 `strftime()` 的结果确实随环境而异，而 `ctime()` 的结果则保持不变：

```bash
$ LC_ALL=en_US ch13-times                  Time in the United States
It is now Friday, July 11, 2003, 10:35 AM
ctime( ) says: Fri Jul 11 10:35:55 2003

$ LC_ALL=it_IT ch13-times                   Time in Italy
It is now venerdì, luglio 11, 2003, 10:36
ctime( ) says: Fri Jul 11 10:36:00 2003

$ LC_ALL=fr_FR ch13-times                   Time in France
It is now vendredi, juillet 11, 2003, 10:36
ctime( ) says: Fri Jul 11 10:36:05 2003
```

缺乏变化的原因是 `ctime()`（以及 `ctime()` 所基于的 `asctime()`）是遗留接口；它们的存在是为了支持旧代码。`strftime()` 作为较新的接口（最初是为 C89 开发的），可以自由地感知区域设置。
