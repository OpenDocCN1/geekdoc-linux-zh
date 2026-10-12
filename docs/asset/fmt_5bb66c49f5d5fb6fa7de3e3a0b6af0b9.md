
| 函数 | 描述 | 本地化依赖 |
| :--- | :--- | :--- |
| `iswalnum` | 分类宽字符 | 所有；`wctype` 允许针对本地化的实现的类 |
| `isnum` | 分类宽字符 | 所有 |

| 函数 | 描述 | 本地化依赖 |
| :--- | :--- | :--- |
| `towlower`, `touupper` | 将宽字符转换为指定的类 | 所有 |
| `tolower`, `toupper` | 将字符转换为小写或大写 | 所有 |

| 函数 | 描述 | 本地化依赖 |
| :--- | :--- | :--- |
| `wcs` | 拷贝宽字符字符串 | 无 |
| `ccs` | 拷贝宽字符字符串 | 无 |

| 函数 | 描述 | 本地化依赖 |
| :--- | :--- | :--- |
| `wcs` | 在宽字符字符串中搜索宽字符 | 无 |
| `str` | 在字符串中搜索字符 | 无 |

| 函数 | 描述 | 本地化依赖 |
| :--- | :--- | :--- |
| `strcoll`, `strxfrm` | 比较（宽字符）字符串或对其进行“编译”以供重复比较 | 排序规则 |

| 函数 | 描述 | 本地化依赖 |
| :--- | :--- | :--- |
| `regcomp`, `reexec`, `regorror`, `regfree` | 正则表达式搜索 | 可能会添加字符类；比较可能是本地化特定的 |

# 国际化

## 类别 - 区域设置操作

| 函数 | 描述 | 区域依赖性 |
| --- | --- | --- |
| `setlocale`, `localeconv`, `nl_langinfo` | 设置和获取区域信息 | |

## 类别 - 消息目录

| 函数 | 描述 | 区域依赖性 |
| --- | --- | --- |
| `gettext`, `dgetext`, `dcgettext`, `textdomain`, `bindtextdomain`, `catgets`, `catopen`, `catclose` | 处理特定于区域的消息 | |

将程序适配以使用当前区域（`locale`）的基本步骤非常简单：

- 1. 为每个需要设置的区域类别调用 `setlocale` 函数（你可以想象，一份关于美国经济的法语报告将使用法语的语言和日期惯例，但美国金融数据的表格将按照美国货币格式输出）。
- 2. 使用 `gettext` 对消息进行本地化。
- 3. 使用遵循区域设置的函数来格式化输出。

但彻底执行这一过程需要自律。这里有一个使用了上述描述的若干技术的程序，它并不完美。在默认配置下，该程序期望消息目录名为 `Plip_hello.mo` 并安装在当前目录下的：

```
/.($LOCALE1, $LOCALE2,...)/LC_MESSAGES/PLIP_hello.mo
```

其中 `$LOCALE1` 是一个区域名称，如 `ja_JP.eUCJP`（通常的日语区域）。若要在系统的通常位置查找目录，请保持 `GETTEXT_DATA_ROOT` 未定义。在符合 FHS 标准的 Linux 系统上，等同于：

```
#define GETTEXT_DATA_ROOT "usr/share/locale"
```

意味着目录安装在：

```
/usr/share/locale/($LOCALE1, $LOCALE2,...)/LC_MESSAGES/PLIP_hello.mo
```

另一个定义 `#define` 是 `USE_YESNO_STR`，如果定义（默认值），将获取该区域的 POSIX 定义是/否字符串。GNU libc 提供的区域中很少定义这些字符串，因此应该避免使用（它是为了“教学目的”设置的默认值）。

# 第 28 章

在这些定义之后是标准包含文件：

```c
/* locale.c
演示区域设置支持和 gettext 的使用

#define GETTEXT_DATA_ROOT getcwd(NULL,0)
#define USE_YESNO_STR

/* 获取所需的设施 ... / */
#include <locale.h>      /* 用于 setlocale(3) 及其函数 */
#include <langinfo.h>    /* 用于 nl_langinfo(0) 及其函数 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <syslog.h>
#include <unistd.h>

/* ... */
```

现在设置 gettext 设施。下划线宏在 gettext 应用中是惯用写法，以减少视觉影响（并避免增加过多行长度），但在头文件中并未定义。`N_` 用于创建静态数据初始化器。（参见示例下函数使用的定义。）

```c
#include <libintl.h>
#define (String) gettext (String)
#define N_(String) String

/* * 下定义的函数原型 * */
void usage(char);
void do_date();
void do_hello();
```

```c
/* 全局变量是糟糕的，但我很懒 * */
char *default_locale;
```

这里是设置区域的驱动程序：

```c
int main (int argc, char *argv[]) {

#ifdef GETTEXT_DATA_ROOT
const char *gettext_data_root = GETTEXT_DATA_ROOT;
#endif
```

根据环境初始化区域设置。语义请参见 `setlocale(3)`。这是一个相当昂贵的操作，因为涉及为那些行为随区域设置而改变的函数设置表格和回调。

参见某些上下文中 `LC_ALL` 的文档。问题是程序可能不需要控制所有的区域功能，而这会覆盖用户对此类无关类别的环境设置。在文本编辑器等多语言应用程序中可能会导致困惑，用户通常希望适当设置 `LC_COLLATE` 和 `LC_CTYPE` 以对第二语言缓冲区进行排序和搜索，但以原始格式显示时间戳和数值数据。

在解析命令行之前先设置区域，以便为用法说明提供消息翻译。注意，如果区域设置失败，`gettext` 将无法翻译消息。因此，在确定区域设置成功之前，我们不必费力标记 `gettext` 字符串。

```c
default_locale = setlocale(LC_ALL, "*");

if (!default_locale) {
    fprintf(stderr,
        /* libc 在此处也会打印一条错误消息 */
        "%s: 哎! 无法设置默认区域，换个系统吧!\n", argv[0]);
    /* 通常会勉强运行，但在示例中这是致命的 */
    exit(EXIT_FAILURE);
}
```

现在我们通过绑定默认目录初始化 `gettext`。此初始化也应该在解析命令行之前完成。目录通常为 `GETTEXT_DATA_ROOT/$LOCALE/LC_CATEGORY/$TEXT_DOMAIN.mo`，其中 `GETTEXT_DATA_ROOT` 在 Linux 上是 `/share/locale`，`$LOCALE` 根据上述区域计算，`LC_CATEGORY = LC_MAGES`（异常参见 `gettext` 文档），`$TEXT_DOMAIN` 通过调用 `textdomain` 为 `PLIP_hello`。注意库尚未初始化，因为程序是为了消息准备的。

> 译者注意：此消息应翻译为

如果你没有预期看到这种语言，请检查你的 `LANGUAGE`、`LANG`、`LC_MAGES` 和 `LC_ALL` 变量。如果它们设置正确，那么你的语言消息目录放置错误了。

> puts ('希望你对默认的 POSIX 区域满意，因为你得到的只有这个！');

puts ('成功初始化国际化。');

现在检查参数并调用请求的函数：

```c
if (argc == 2 || argv[1][1] != '\0') {
    usage (argv[0]);
    exit (EXIT_FAILURE);
}

switch (argv[1][0]) {
  case '1':
    do_date ();
    break;
  case '2':
    do_hello ();
    break;
  default:
    usage (argv[0]);
    exit (EXIT_FAILURE);
}
```

```c
putchar('\n');
exit (EXIT_SUCCESS);
```

本地化的打印日期和时间函数。`%c` 和 `%Z` 转换说明符请求根据区域自身的格式转换时间和日期。

打印“hello”的函数：
