
来自 `syslog` 的消息是在程序中通过调用 glibc C 库程序 `syslog()` 生成的。然后 glibc 格式化消息并尝试将其写入 `/dev/log`，这是一个在 syslog 启动时打开的 Unix socket。syslog 从 `/dev/log` 读取消息，并根据 `/etc/syslog.conf`（syslog 配置文件）定义的过滤器进行处理。图 6-2 显示了整体架构和消息流。

![](img/ab18faa434b6e1e10df0a92984bf70fc_105_0.png)

图 6-2：带有 syslog的消息流

## 使用 syslog

几乎所有的 Linux 语言都有发送 syslog 消息的例程。下面的 C 库原型大多数语言的典型。

```c
void syslog(int priority, const char *format, ...);
```

优先级是日志级别、事件重要性或严重程度以及生成消息的程序类型的组合。大多数程序员在运行 syslog 例程时只指定日志级别。共有八个日志级别，重要性范围从紧急（emergency）到调试（debug）不等。这段 syslog 摘录显示了八个级别。

```c
#define LOG_EMERG 0 /* 系统不可用 */
#define LOG_ALERT 1 /* 必须立即采取行动 */
#define LOG_CRIT 2 /* 关键情况 */
#define LOG_ERR 3 /* 错误情况 */
#define LOG_WARNING 4 /* 警告情况 */
#define LOG_NOTICE 5 /* 正常但重要的情况 */
#define LOG_INFO 6 /* 信息 */
#define LOG_DEBUG 7 /* 调试级别消息 */
```

`syslog()` 例程使用 printf 风格的字符串，带有变数量的参数。格式字符串中的文本应该对事件形成清晰、无歧义的描述，格式字符串的任何参数应提供事件的更多细节。

当我们构建设备时，我们交付的内容很大一部分是文档，我们文档的大部分是所有设备日志消息的列表。（等待，这里的 OCR 文本在这里似乎变得重复/乱码了）

```c
#include <syslog.h>

main() {
    fopen("my_prog", 0, LOG_USER); //LOG_USER = 0x0008
    syslog(LOG_INFO, "abc=%d", 2); //LOG_INFO = 0x0006
}
```

如果我们查看 syslogd 从其 Unix 套接字读取消息后的后的内容，我们会看到：

<14>Aug 2 13:18:31 my_prog: abc=2

注意 `LOG_USER` (8) 和 `LOG_INFO` (6) 被合并为 `<14>`。需要一个换行符或其他终止字符，因为 `syslog()` 在将消息写入 `/dev/log` 套接字之前会添加一个空字符。如果你不包含换行符，syslogd 将在消息写入日志文件之前追加一个。

## 使用 syslog 守护进程

syslog 守护进程从 `/dev/log` Unix 套接字读取消息，并根据其设施（facility）和日志级别（log level）路由消息。syslog 消息的目的地称为动作（actions），包括文件、命名管道、系统控制台（或其他任何 TTY）、网络上的其他 syslog 系统以及用户。

syslog 的过滤器和动作定义在 `/etc/syslog.conf` 中。该配置文件通常每个目的地占一行，并列出该目的地所需的许多设施和级别。动作中的设施用逗号分隔，后面紧跟一个点，然后是日志级别。可以使用星号 `*` 来表示所有设施或级别，而指定某个日志级别意味着该级别以及所有高于该 Find级的级别。例如：

```
*.*          all log messages
mail,lpr.*   all messages from the mail and printer daemons
.*crit        all messages with a critical log level or higher
```

syslog 的常见目的地包括文件、管道、网络上的其他日志守护进程。管道通过目的地开始处的管道符号 `|` 来指定。网络目的地以 符号 `@` 开头。`syslog.conf` 的手册页（man page）对如何指定哪些设施和优先级路由到哪些动作提供了更完整的描述。`syslog.conf` 将邮件日志路由到 `/var/log/mail` 以及将关键（critical）或以上的打印打印程序和 FTP 日志路由到网络日志服务器的行如下：

```
mail.*        /var/log/mail
lpr,ftp.crit  @loghost.myranet.com
```

回想设施是从 `syslog()` 传递到 `syslogd` 的优先级整数的一部分，你可以定义自己的设施。这让你可以在 syslog 之上建立私有的日志系统。你可以将新的设施整数和名称添加到 `syslog.h`，然后重新编译 `glibc` 和 `syslog`。然而，使用新设施显式整数可能更容易。有 24 个预定义的设施，因此选择一个大得多的数字，例如 1000。发送此设施的 INFO 日志的代码可能如下：

```
syslog((1000<<3) | LOG_INFO, "an event occurred");
```

我们展示了位移（shift）和位或（OR）操作来说正在发生什么。我们建议你使用等价的 `LOG_PRIO(facility, level)` 宏。继续这个示例，假设你有一个程序在命名管道 `/usr/local/private_pipe` 上监听你的新日志消息。你可以通过向 `syslog.conf` 中添加以下行并重启 syslog，配置 syslog 交付所有新设施的消息。

| Facility | Destination |
| :--- | :--- |
| 1000.* | /usr/local/private_pipe |

桌面开发者可能对使用 syslog 进行事件处理的想法感到畏缩。但话又回来，Linux 桌面系统通常比专用设备拥有更多的 RAM 和 CPU 资源，因此它们可以负担起 D-Bus（相对）高的磁盘、内存和 CPU 开销。我们推荐 syslog 是因为它的简单性、在几乎所有编程语言中的可用性以及较小的内存和 CPU 开销。

## syslog 的局限性、优势和替代方案

默认 syslog 守护进程有一些局限性。如之前所述，它不保存消息级别或设施（尽管你可以通过基于路由直接获取它们）。syslog 无法根据正则表达式进行路由，它只接受来自 Unix 套接字的消息，并且其动作集相当有限。某些程序员发现在设置调试和追踪机机制时，有限的级别是一个问题。优点是，syslog 被广泛接受，并且经过了彻底的调试、测试且是安全的。

`logger` 工具（我们在本章开头简要见过）让你能够绕过 syslog 有限的消息源。`logger` 将日志消息发送到 syslog，从其命令行或其标准输入的每一行获取日志消息。如果你愿意，可以指定级别、设施和前缀字符串。更多细节请参见 `logger` 页面。你还可以结合 `netcat`（一个用于读写网络连接的简单工具）和 `logger`，使用类似于下面所示的命令从单个 TCP 连接接收日志消息。

```
nc -1 -p 2250 | logger
```

`logger` 工具让你能够“监控”其他日志文件。例如，假设你想让添加到 `/usr/www/error.log` 的每一行也发送到 syslog。以下命令行执行了此操作。

```
tail -f /usr/www/error.log | logger
```

另一个值得提的辅助程序是 `klog`。由于 Linux 内核不使用 glibc，它无法使用 `syslog()` 发送内核日志。相反，内核日志通过系统调用 `k_syslog()` 或从 `/proc/kmsg` 可见的循环缓冲区可用。守护进程 `klog` 将其他源的日志消息转换为 syslog 消息。此外，`klog` 将内核中的十六进制地址转换为等效的符号名称。要从十六进制地址获取符号，`klog` 读取 `System.map` 中的内存映射。如果你在启动 `klog` 后加载或卸载内核模块，请确保使用 `-l` 命令告诉 `klog` 重新加载其符号表。

syslog 的流行替代方案包括 `minyslog`（一个可以处理大量流量的极简日志器）和 `syslog-ng`（它可以根据正则表达式过滤、重写消息，并支持 TCP 源和目的）。`evlog` 包在识别和响应日志消息方面是最好的之一。关于这些替代方案的最新信息可以通过对包名进行网络搜索找到。

### 按需日志记录
