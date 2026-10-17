
### 日志设施

| 常量 | 说明 |
| :--- | :--- |
| `LOG_LOCAL[@-7]` | 留供本地/站点使用 |
| `LOG_LPR` | 打印机子系统 |
| `LOG_MAIL` | 邮件子系统 |
| `LOG_NEWS` | 新闻子系统 |
| `LOG_SYSLOG` | `syslog` 生成的内部消息 |
| `LOG_USER` | (默认) 普通用户级消息 |
| `LOG_UUCP` | `uucp` 子系统 |

在大多数情况下，使用默认值 `LOG_USER` 作为设施值是最好的。当然，除非你正在编写邮件程序或新客户端。如果你所在地的系统管理员设置了本地级别 `LOG_LOCAL[@-7]`，如果适用，你可以使用其中之一。选择正确的级别稍微复杂一点。通常，使用 `LOG_ERR` 和 `LOG_INFO` 之间的任意级别，但如果你发送了 `LOG_ERR` 消息，它通常会显示给所有用户和系统控制台，并很可能向机器管理员发送页面——希望其含义是：为消息内容选择合适的级别。我对用户级程序的建议是：错误使用 `LOG_ERR`，普通无聊的日志消息使用 `LOG_INFO`。

### 处理错误

综上所述，假设你在打开文件时遇到错误。你的 `syslog()` 可能像这样：

```c
syslog(LOG_ERR, LOG_USER, "unable to open file %s %%m\n", fname);
```

其中文件名是你尝试打开失败的文件。这在 `/var/log/messages` 中调用了以下消息：

```
Mar 26 19:36:25 hoser syslog: unable to open file foo
*** No such file or directory
```

`%m` 格式说明符附加了字符串 "No such file or directory"，就像调用了 `strerror(errno)`。因为 `LOG_USER` 是默认设施，之前的代码段可以写成：

```c
syslog(LOG_ERR, "unable to open file %s %%m\n", fname);
```

同样，如果你只是想随写一条非关键的日志条目，尝试：

```c
syslog(LOG_INFO, "this is a normal message\n");
```

它写入 `/var/log/messages` 的消息：

```
Mar 26 19:29:03 hoser syslog: this is a normal message
```

之前的示例存在问题之一是，生成的日志消息不够独特，无法定位一个容易增长到七八兆字节的日志文件。`openlog()` 出现救了：

```c
void openlog(const char *ident, int option, int facility);
```

`facility` 是表 13.2 中的值之一。`ident` 指定了要附加到日志消息前的字符串。`option` 是表 13.3 中列出的一个或多个选项的按位或。

### 表 13.3 `openlog()` 选项

| 选项 | 说明 |
| :--- | :--- |
| `LOG_PID` | 在每条消息中包含 PID |
| `LOG_CONS` | 如果未记录，则将消息写入控制台 |
| `LOG_NDELAY` | 立即打开连接（默认等待到第一次调用 `syslog()`） |
| `LOG_PERROR` | 将消息打印到 `stderr` |

第 13 章 系统编程 第二部分
