
数组边界。（这样做时，显然 src 必须有一个终止零字节。）
以下代码片段演示了如何使用 `strxfrm()`：

```c
#define STRBUFSIZE ...
char s1[STRBUFSIZE], s2[STRBUFSIZE];      /* 原始字符串 */
char slx[STRBUFSIZE], s2x[STRBUFSIZE];    /* 转换后的副本 */
size_t len1, len2;
int cmp;
/* ... 填充 s1 和 s2 ... */
len1 = strlen(s1);
len2 = strlen(s2);

if (strxfrm(s1x, s1, len1) >= STRBUFSIZE || strxfrm(s2x, s2, len2) >= STRBUFSIZE)
    /* 太大，需恢复 */

cmp = strcmp(s1x, s2x);
if (cmp == 0)
    /* 相等 */
else if (cmp < 0)
    /* s1 < s2 */
else
    /* s1 > s2 */
```

对于一次性比较，直接使用 `strcoll()` 可能速度更快。但如果字符串需要多次比较，则使用一次 `strxfrm()` 并对转换后的值使用 `strcmp()` 会更快。

没有与 `strcmp()` 或 `strcasecmp()` 对应的具备区域设置感知能力的排序函数。

## 13.2.4 低层数值和货币格式化：`localeconv()`

正确格式化数值和货币值需要相当多的底层信息。这些信息包含在通过 `localeconv()` 函数获取的 `struct lconv` 中：

```c
#include <locale.h>                    /* ISO C */

struct lconv *localeconv(void);
```

与 `ctime()` 函数类似，此函数返回指向内部静态数据的指针。由于如果区域设置已更改，后续调用可能返回不同的值，因此您应该复制返回的数据。以下是 `struct lconv`（略微简化），直接来自 GLIBC 的 `<locale.h>`：

```c
struct lconv {
    /* 数值（非货币）信息。  */
    char *decimal_point;   /* 小数点字符。   */
    char *thousands_sep;   /* 千位分隔符。       */
    /* 每个元素是每组中的位数；
       索引较高的元素位于更左边。
       值为 CHAR_MAX 的元素表示不再进行分组。
       值为 0 的元素表示对更左边的所有组使用上一个元素。   */
    char *grouping;

    /* 货币信息。   */
    /* 前三个字符是来自 ISO 4217 的货币符号。
       第四个字符是分隔符。  第五个字符是 '\0'。  */
    char *int_curr_symbol;
    char *currency_symbol;   /* 本地货币符号。   */
    char *mon_decimal_point; /* 小数点字符。 */
    char *mon_thousands_sep; /* 千位分隔符。     */
    char *mon_grouping;      /* 类似于上面的 'grouping' 元素。 */
    char *positive_sign;     /* 正值的符号。 */
    char *negative_sign;     /* 负值的符号。 */
    char int_frac_digits;    /* 国际小数位数。 */
    char frac_digits;        /* 本地小数位数。  */
    /* 如果货币符号在正值之前为 1，在后则为 0。  */
    char p_cs_precedes;
    /* 仅当空格分隔货币符号和正值时为 1。  */
    char p_sep_by_space;
    /* 如果货币符号在负值之前为 1，在后则为 0。  */
    char n_cs_precedes;
    /* 仅当空格分隔货币符号和负值时为 1。  */
    char n_sep_by_space;
    /* 正号和负号的位置：
       0 括号包围数量和货币符号。
       1 符号字符串位于数量和货币符号之前。
       2 符号字符串位于数量和货币符号之后。
       3 符号字符串紧接在货币符号之前。
       4 符号字符串紧接在货币符号之后。  */
    char p_sign_posn;
    char n_sign_posn;
    /* 如果 int_curr_symbol 在正值之前为 1，在后则为 0。  */
    char int_p_cs_precedes;
    /* 仅当空格分隔 int_curr_symbol 和正值时为 1。  */
    char int_p_sep_by_space;
    /* 如果 int_curr_symbol 在负值之前为 1，在后则为 0。  */
    char int_n_cs_precedes;
    /* 仅当空格分隔 int_curr_symbol 和负值时为 1。  */
    char int_n_sep_by_space;
    /* 正号和负号的位置：
       0 括号包围数量和 int_curr_symbol。
       1 符号字符串位于数量和 int_curr_symbol 之前。
       2 符号字符串位于数量和 int_curr_symbol 之后。
       3 符号字符串紧接在 int_curr_symbol 之前。
       4 符号字符串紧接在 int_curr_symbol 之后。 */
    char int_p_sign_posn;
    char int_n_sign_posn;
};
```

注释相当清晰地说明了其中的原理。让我们看看 `struct lconv` 中的前几个字段：

- **`decimal_point`**：要使用的小数点字符。在美国和其他英语国家，它是一个句点，但许多国家使用逗号。
- **`thousands_sep`**：用于分隔值中每 3 位数字的字符。
- **`grouping`**：单字节整数值数组。每个元素表示分组多少位数字。正如注释所述，`CHAR_MAX` 表示不应再进行分组，0 表示重用最后一个元素。（我们将在本章后面的示例代码中展示。）
- **`int_curr_symbol`**：这是本地货币的国际符号。例如，美元的 `'USD'`。
- **`currency_symbol`**：这是本地货币的本地符号。例如，美元的 `$`。
- **`mon_decimal_point`、`mon_thousands_sep`、`mon_grouping`**：这些对应于前面的字段，提供相同的信息，但针对的是货币金额。

其余的大多数值对日常编程没有太大用处。以下程序 `ch13-lconv.c` 打印了这些值中的一些，以让您了解可以获取什么样的信息：

```c
/* ch13-lconv.c --- 显示 struct lconv 的一些组件 */
#include <stdio.h>
#include <limits.h>
#include <locale.h>

int main(void)
{
    struct lconv l;
    int i;

    setlocale(LC_ALL, "");
    l = *localeconv();

    printf("*decimal_point = [%s]\n", l.decimal_point);
    printf("*thousands_sep = [%s]\n", l.thousands_sep);

    for (i = 0; l.grouping[i] != 0 && l.grouping[i] != CHAR_MAX; i++)
        printf("*grouping[%d] = [%d]\n", i, l.grouping[i]);

    printf("*int_curr_symbol = [%s]\n", l.int_curr_symbol);
    printf("*currency_symbol = [%s]\n", l.currency_symbol);
    printf("*mon_decimal_point = [%s]\n", l.mon_decimal_point);
    printf("*mon_thousands_sep = [%s]\n", l.mon_thousands_sep);
    printf("*positive_sign = [%s]\n", l.positive_sign);
    printf("*negative_sign = [%s]\n", l.negative_sign);
}
```

当使用不同的区域设置运行时，不出所料，我们得到了不同的结果：

```bash
$ LC_ALL=en_US ch13-lconv                # 美国的结果
decimal_point = [.]
thousands_sep = [,]
grouping[0] = [3]
grouping[1] = [3]
int_curr_symbol = [USD ]
currency_symbol = [$]
mon_decimal_point = [.]
mon_thousands_sep = [,]
positive_sign = []
negative_sign = [-]
```

```bash
$ LC_ALL=it_IT ch13-lconv                # 意大利的结果
decimal_point = [.]
thousands_sep = []
int_curr_symbol = []
currency_symbol = []
mon_decimal_point = []
mon_thousands_sep = []
positive_sign = []
negative_sign = []
```

请注意，在 `en_US` 区域设置中，`int_curr_symbol` 的值包含一个尾随空格字符，它起到将符号与随后的货币值分隔开的作用。

### 13.2.5 高层数值和货币格式化：`strfmon()` 和 `printf()`

在查看了 `struct lconv` 中的所有字段后，您可能会想知道，“我真的必须弄清楚如何使用所有这些信息才能格式化货币值吗？” 幸运的是，答案是否定的。³ `strfmon()` 函数为您完成了所有工作：

```c
#include <monetary.h>            /* POSIX */

size_t strfmon(char *s, size_t max, const char *format, ...);
```

此例程很像 `strftime()`（参见第 6.1.3.2 节，“复杂时间格式化：`strftime()`”，第 171 页），使用 `format` 将字面字符和格式化数值复制到 `s` 中，最多放置 `max` 个字符。以下简单的程序 `ch13-strfmon.c` 演示了 `strfmon()` 的工作原理：

```c
/* ch13-strfmon.c --- 演示 strfmon() */

#include <stdio.h>
#include <locale.h>
#include <monetary.h>

int main(void)
{
    char buf[BUFSIZ];
    double val = 1234.567;

    setlocale(LC_ALL, "");
    strfmon(buf, sizeof buf, "You owe me %n (%i)\n", val, val);
    fputs(buf, stdout);
    return 0;
}
```

当在两个不同的区域设置中运行时，它产生以下输出：

```bash
$ LC_ALL=en_US ch13-strfmon                  # 在美国
You owe me $1,234.57 (USD 1,234.57)
$ LC_ALL=it_IT ch13-strfmon                  # 在意大利
You owe me EUR 1.235 (EUR 1.235)
```

3 我们和您一样高兴，因为我们不必提供使用这个嗯、功能齐全的 `struct` 的示例代码。

