
语言是双字母 ISO 语言代码，领土是双字母 ISO 国家代码。代码指定了一个字符编码集。修饰符（modifier）提供了一种区分语言、领土和字符集相同的多个区域的方法。完整区域名称示例是 `de_DE.utf-8@euro`，代表德语、UTF-8 字符编码，并使用欧元作为货币单位的区域。

正如命名格式中的括号所示，区域目录名称的各个部分可以省略。名称通常只包含语言和领土。因此，目录 `US` 是美国（英语母语）的本地目录，而 `fr_CH` 是瑞士法语区的本地目录。

`CH` 代表 *Confederatio Helvetica*，这是瑞士的拉丁语（且该名称在当地范围内是中性的）名称。瑞士拥有四种官方国家语言，是具有多个时区的国家类比示例。

当我们为程序指定要使用的区域时，我们实际上是在指定 `/usr/share/locale` 下某个子目录的名称。如果程序指定的区域与区域目录名称不完全匹配，则 C 库将按照以下顺序从指定的区域中剥离组件来寻找匹配：

1. 字符集 (codeset)
2. 规范化字符集 (normalized codeset)
3. 领土 (territory)
4. 修饰符 (modifier)

规范化字符集是字符集名称的版本，删除了非字母数字字符，所有字母转换为小写，并在生成的字符串前加上 `iso` 字符。规范化的目的是处理字符集在大小写和标点符号（例如额外的连字符）上的变体。

作为此剥离过程的示例，如果程序的区域指定为 `fr_utf-8`，但不存在该区域目录，则如果存在，将匹配 `fr_CH` 区域目录。如果 `fr_CH` 目录不存在，则将使用 `fr` 目录。在极罕见的 `fr` 目录都不存在的情况下，稍后描述的 `setlocale()` 函数将报告错误。

文件 `/usr/share/locale/locale.aliases` 定义了向程序指定区域的替代方法。详情请参阅 `locale.aliases(5)` 手册页。

每个区域子目录下有一组标准文件，规定了该区域的约定，如表 10-2 所示。注意关于此表中信息的后续几点：

- `LC_COLLATE` 定义了一组规则，描述字符集中的字符如何排序（即“字母表”顺序）。
- `LC_COLLATE` 定义了一组规则，描述字符集中的字符如何排序（即“字母表”顺序）。
- `LC_COLLATE` 定义了一组规则，描述字符集中的字符如何排序（即“字母表”顺序）。
- `LC_COLLATE` 定义了一组规则，描述字符集中的字符如何排序（即“字母表”顺序）。
- `LC_COLLATE` 定义了一组规则，描述字符集中的字符如何排序（即“字母表”顺序）。
- `LC_COLLATE` 定义了一组规则，描述字符集中的字符如何排序（即“字母表”顺序）。
- `LC_MESSAGES` 定义了。
- `LC_MESSAGES` 定义了。

### 表 10-2：区域的内容

| 字段 | 用途 |
| :--- | :--- |
| `LC_TYPE` | 字符分类 |
| `LC_COLLATE` | 排序规则 |
| `LC_MONETARY` | 货币 |
| `LC_NUMERIC` | 数值 |
| `LC_TIME` | 日期和时间 |
| `LC_MESSAGES` | 消息

注意关于此表中信息的后续几点：

- `LC_COLLATE` 定义了组规则，描述字符集排序。
- `LC_COLLATE` 定义了一组规则，描述字符集中的字符如何排序（即“字母表”顺序）。
- `LC_MESSAGES` 定义了。
- `LC_MESSAGES` 定义了。
- `LC_COLLATE` 定义了组规则，描述字符集排序。
- `LC_MESSAGES` 定义了。
- `LC_MESSAGES` 定义了。
- `LC_COLLATE` 定义了组规则，描述字符集排序。
- `LC_MESSAGES` 定义了。
- `LC_MESSAGES` 定义了。
- `LC_COLLATE` 定义了组规则，描述字符集排序。

## 指定区域

（此处未未定义区域）

`strftime()`（第 10.2.3 ），正如我们在不同的 locale 下运行程序 10-4 的 `strftime()` 结果所示：

```
LANG_de_DE /show_time | German locale
ctime() of time value is: Tue 12:23 2011
asctime() of local time is: Tue 12:23 2011
strftime() of local time is: Dienstag, 01 Februar 2011, 12:23 CET
```

下一个运行证明了 `LC_TIME` 有优先级：

```
LANG_de_DE /show_time | Italian locale
ctime() of time value is: Tue 12:24 2011
asctime() of local time is: Tue 12:24 2011
strftime() of local time is: martedi, 01 febbraio 2011, 12:24 CET
```

这次运行证明了 `LC_ALL` 有优先级：

```
LC_ALL+fr_US /show_time | French and US locales
ctime() of time value is: Tue 12:25 2011
asctime() of local time is: Tue 12:25 2011
strftime() of local time is: mardi, 01 février 2011, 12:25 CET
```

## 10.5 更新系统时钟

我们现在查看更新系统时钟的两个接口：`settime()` 和 `adj()`。应用程序很少这些接口（系统时间通常由网络协议守护进程维护），并且要求调用者具有特权（`CAP_SYS_TIME`）。

`settime()` 调用执行 `gettime()` 的逆操作（在第 10.1 节中描述）：它将系统日设置为 `tv` 结构体指定的秒和微秒。

```c
#define BSD_SOURCE

#include <sys/time.h>

int settime(const struct time *tv, const struct timezone *tz);

成功时返回 0，错误时返回 -1
```

对于 `gettime()`，`tz` 的使用已经过时，此参数应指定为 `NULL`。`tz` 字段的微秒精度并不意味着我们拥有微秒精度的系统时钟控制，粒度可能更大。虽然 `settime()` 未在 SUS3 中指定，但在其他 UNIX 实现中广泛可用。Linux 提供了 `adjtime()` 调用来设置系统时钟。`settime()` 和 `adjtime()` 的区别在于，后者允许仅以秒为精度表示新的日历时间。与 `time()` 和 `gettime()` 一样，同时存在 `adjtime()` 和 `settime()` 的历史原因是：后者更精确，由 BSD 添加。

调用 `settime()` 引起的系统时间突然变化对应用程序（例如使用时间戳的数据库、时间标记日志文件）的影响大于单调递增的系统时钟。因此，当对时间进行小更改（几秒）时，通常最好使用 `adjtime()` 函数，它会导致系统时钟逐渐调整到目标值。

```c
#define BSD_SOURCE

#include <sys/time.h>

int adjtime(struct time *delta, struct time *olddelta);

成功时返回 0，错误时返回 -1
```
