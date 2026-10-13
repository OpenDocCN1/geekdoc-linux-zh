
`priority` 是级别（level）和设施（facility）的位或组合，级别指示消息的严重程度，设施则告诉 `syslog` 谁发送了消息以及如何响应。它格式化消息以写入日志以及任何指定的类似于 `printf()` 的格式。特殊指定符 `%m` 将被 `str-error()` 分配给 `errno` 的错误消息替换，或者如果已经调用过 `strerror(errno)`。表 13.1 按降序列出了层级的可能值。

### 表 13.1 syslog 日志级别

| 级别 | 严重程度 |
| --- | --- |
| LOG_EMERG | 系统不可用 |
| LOG_ALERT | 需要立即采取行动 |
| LOG_CRIT | 严重错误，例如硬件 |
| LOG_ERR | 错误情况 |
| LOG_WARNING | 警告情况 |
| LOG_NOTICE | 正常但重要的消息 |
| LOG_INFO | 纯信息性消息 |
| LOG_DEBUG | 调试或跟踪输出 |

表 13.2 列出了设施的可能值。

### 表 13.2 syslog 设施名称

| 设施 | 描述 |
| --- | --- |
| LOG_AUTHPRIV | 安全与授权 |
| LOG_CRON | 计时守护进程 (cron) |
| LOG_DAEMON | 其他系统守护进程 |
| LOG_KERN | 内核消息 |
| LOG_LOCAL | 留作本地使用 |
| LOG_PRINTER | 打印机设施 |
| LOG_MAIL | 邮件设施 |
| LOG_NEWS | 新闻设施 |
| LOG_SYSLOG | 内部消息 |
| LOG_USER | 普通用户 |
| LOG_UUCP | UUCP 设施 |

### 表 13.3 openlog() 选项

| 选项 | 描述 |
| --- | --- |
| LOG_PID | 在每条消息中包含 PID |
| LOG_CONS | 如果无法记录，则将消息写入到控制台 |
| LOG_NDELAY | 立即打开连接（默认直到第一次调用 syslog() 时） |
| LOG_ERROR | 除日志外，还将消息打印到 stderr |

## 系统编程

第二部分

文件描述符 `openlog()` 已打开。为了说明 `openlog()` 的用法，请考虑以下两个代码段：

```
openlog("my_program", LOG_PID, LOG_USER);
syslog(LOG_NOTICE, "Pay attention to me!\n");
```

此片段产生了：

```
Mar 26 20:11:58 hoser my_program[1354]: Pay attention to me
in /var/log/messages, while the next one
```

```
openlog("your_program", LOG_PID, LOG_USER);
syslog(LOG_INFO, "No, ignore other program!\n")
```

生成了如下：

```
Mar 26 20:14:28 hoser your_program[1363]: No, ignore that other program
```

注意缩进字符串和 PID 如何替换了第一个。这非常清晰地显示了哪个程序拥有日志消息。实际上，`openlog()` 为你程序后续所有的 `syslog()` 调用设置了默认设施（facility）。正如你可能猜到的，一组类似的设置函数 `setlogmask()` 设置了默认优先级：

```
int setlogmask(int priority);
```

在此上下文中，`priority` 参数可以是单一优先级或一个包含性的优先级范围。

调用 `setlogmask()` 为优先级设置一个默认掩码；`syslog()` 会拒绝任何优先级未在掩码中设置的消息。`<syslog.h>` 还定义了两个设置掩码的辅助宏：

```
int LOG_MASK(int priority)
```

以及

```
LOG_UPTO(int priority)
```

`LOG_MASK()` 创建一个仅包含一个优先级的掩码，即作为参数传递的优先级。另一方面，`LOG_UPTO()` 创建一个优先级范围的掩码。例如，`LOG_UPTO(LOG_NOTICE)` 创建了一个包含从 `LOG_EMERG` 到 `LOG_NOTICE` 任何级别任何消息的掩码。级别为 `LOG_INFO` 或 `LOG_DEBUG` 的消息将无法通过。看列表 13.8。

### 列表 13.8 mask_log.c

```
1 /*
2 * Listing 13.8
3 * mask_log.c - demonstrate openlog() and family
```

### 错误处理

第13章

```
/* /
#include <syslog.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main(void)
{
    int ret;

    openlog("mask_log", LOG_PID, LOG_USER);
    syslog(LOG_INFO, "This message courtesy of UID %%d\n",
           getpid());
    syslog(LOG_NOTICE, "Hopefully, you will see this\n");

    /* 不想看到 DEBUG 和 INFO 消息 */
    ret = setlogmask(LOG_UPTO(LOG_NOTICE));
    syslog(LOG_INFO, "You should not be seeing this\n");
    syslog(LOG_DEBUG, "I hope you do not see this\n");
    syslog(LOG_NOTICE, "This should still appear\n");

    closelog();
    exit(SUCCESS);
}
```

编译并执行后，`/var/log/messages` 显示：

Mar 26 22:42:06 hoser_mask_log[17218]: This message courtesy of UID #100

Mar 26 22:42:06 hoser_mask_log[17218]: Hopefully, you will see this

Mar 26 22:42:06 hoser_mask_log[17218]: This should still appear

成功！在我们更改优先级掩码后，带有 `LOG_INFO` 和 `LOG_DEBUG` 的消息没有通过，但优先级更高的消息（如 `LOG_NOTICE`）通过了。

> 注意

跟踪 `/var/log/messages` 的简单方法是打开单独的 xterm 并使用 `tail -f /var/log/messages` 跟踪该文件。每当新消息写入日志时，它就会出现在你的屏幕上。

### 用户程序

对于 shell 程序员们，你们没有被忘记。存在一个用户程序 `logger(1)`，它为 syslog 设施提供了 shell 接口。如所述，`logger` 是 syslog 的 shell 和命令行接口。它的完整语法是：

```
logger [-is] [-f file] [-p pri] [-t tag] [message ... ]
```

`-i` 选项告诉 logger 将 PID 添加到日志消息中。使用 `-t` 获取调用 logger 的脚本名称并加入到日志消息中。列表 13.9 展示了你可能如何在 shell 脚本中使用 `logger`：

### 列表 13.9 logger.sh

```
#!/bin/sh
# Listing 13.9
# logger.sh Demonstrate logger(1) interface to syslog
# ################################################
```

```
echo "type the log message and press ENTER"
read _msg
logger -i -t logger.sh $_msg
```

不要费心理解这些语法，它将在第 34 章“使用 GNU bash 进行 Shell 编程”中介绍。在提示日志消息后，脚本读取该日志消息并调用 `logger` 将其插入日志文件。一个示例运行可能如下：
