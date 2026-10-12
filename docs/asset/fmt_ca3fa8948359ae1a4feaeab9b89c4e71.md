
`fprintf(stderr, _("%s: cannot read pipe: %s\n"), argv[0], strerror(errno));`

这种方式更好：

```c
if (an error occurred) {    /* 错误 */
    fprintf(stderr, _("%s: cannot read %s: %s\n"),
           input_type == INPUT_FILE ? _("file") : _("pipe"),
           strerror(errno));
}
```

正如刚才所示，包含一条注释说明特意使用了多个消息是一个好主意——这可以使消息变得更容易翻译。

## 13.3.8 创建翻译

一旦你的程序完成了国际化，就有必要准备翻译。这是通过几个 shell 级工具完成的。我们从 `ch06-echodate.c`（见第 6.1.4 节“将拆分的时间转换为 time_t”，第 176 页）的国际化版本开始：

```c
/* ch13-echodate.c --- 演示翻译 */
#include <stdio.h>
#include <time.h>
#include <locale.h>

#define ENABLE_NLS 1

#include <gettext.h>

#define __(msid) gettext(msid)

#define N_(msid) msid

int main(void)
{
    struct tm tm {
        time_t then;
    };

    setlocale(LC_ALL, "*");
    bindtextdomain("echodate", ".");
    textdomain("echodate");

    printf("%s", "Enter a Date/time as YYYY/MM/DD HH:MM:SS : %s");
    scanf("%d/%d/%d %d:%d:%d",
          &tm.tm_year, &tm.tm_mon, &tm.tm_mday,
          &tm.tm_hour, &tm.tm_min, &tm.tm_sec);

    /* 为了简见，省略了对值的检查 */

    tm.tm_year += 1900;
    tm.tm_mon -= 1;
    tm.tm_isdst = -1; /* 不知道夏时时间 */

    then = mktime(&tm);

    printf("Got: %s", ctime(&then));
    exit(0);
}
```

我们特意使用了 `"gettext.h"` 而不是 `<gettext.h>`。如果我们的应用程序发布时带有 `gettext` 库的私有副本，那么 `"gettext.h"` 将找到它，从而避免使用系统的副本。另一方面，如果只有系统的副本，那么在没有本地副本的情况下，它会被找到。必须承认，由于 `Solaris` 系统也有一个 `gettext` 库，但其功能不如 `GNU` 版本丰富，情况变得复杂。

继续创建翻译，第一步是提取可翻译的字符串。这是通过 `gettext` 程序完成的：

```bash
$ gettext --keyword --keyword=N_\n --default-domain=echodate ch13-echodate.c
```

`--keyword` 选项告诉 `gettext` 去寻找 `_()` 和 `N_()` 宏。它已经知道从 `gettext()` 及其变体中提取字符串。

`gettext` 的输出称为 `gettext` 的输出。

此外，简单的格式化字符串如 `"%d %d\n"` 不需要翻译，调试信息也不需要。

## 13.3 程序消息的动态翻译

8. 使用代表完整句子的多个字符串而不是使用 `%s` 和 `?` 进行单词替换，为你的翻译人员提供便利：例如：

```c
if (an error occurred) {    /* 正确 */
    /* 使用多个字符串使翻译更简单。 */
    if (input_type == INPUT_FILE)
        fprintf(stderr, _("%s: cannot read file: %s\n"),
               argv[0], strerror(errno));
    else
        fprintf(stderr, _("%s: cannot read pipe: %s\n"),
               argv[0], strerror(errno));
}
```

这种方式更好：

```c
if (an error occurred) {    /* 错误 */
    fprintf(stderr, _("%s: cannot read %s: %s\n"),
           input_type == INPUT_FILE ? _("file") : _("pipe"),
           strerror(errno));
}
```

正如刚才所示，包含一条注释说明特意使用了多个消息是一个好主意——这可以使消息变得更容易翻译。

## 13.3.8 创建翻译

一旦你的程序完成了国际化，就有必要准备翻译。这是通过几个 shell 级工具完成的。我们从国际化版本的 `ch06-echodate.c` 开始：

```bash
$ gettext --keyword --keyword=N_\n --default-domain=echodate ch13-echodate.c
```
