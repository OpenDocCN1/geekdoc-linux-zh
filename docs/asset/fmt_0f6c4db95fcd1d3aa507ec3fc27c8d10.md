
如表 5.1 所示的变量定义在所有邮件器中都是可用的。请参阅附录 A 中的“OSTYPE”部分以获取这些变量的完整列表。

注意：附录 A 在 `OSTYPE` 文件的讨论中列出了这些变量，因为邮件器和路径信息应该存储在该处。然而，大多数 Sendmail 管理员并不想自己去创建 `OSTYPE` 文件。大多数管理员会直接将此类命令添加到宏配置文件中。

列表 5.2 显示的 `linux.m4` `OSTYPE` 文件调整了 `PROCMAIL_MAIL_PATH` 的邮件器路径。这是 `generic-linux.mc` 配置唯一涉及的邮件器设置，它表明邮件器设置需要更改是多么罕见。

对 `generic-linux.mc` 的分析显示了几个问题。我们发现了 `m4` 源文件之间的相互关系，并学习了几种不同配置命令的作用和语法。此外，我们发现由 Sendmail 8.11 源码分发提供的 `generic-linux.cf` 文件在示例 Linux 系统上运行良好；Sendmail 需要的各种文件都以正确的名称放在正确的目录下。

接下来，我们分析在 Red Hat 系统上作为 RPM 包一部分安装的 Sendmail 配置。该配置从开始一直运行良好。分析 Red Hat 配置不是为了调试问题，而是为了了解供应商提供的配置，并看看我们可以做什么来改进它。

## Red Hat 配置

在第 3 章“运行 Sendmail”中，使用 `rpm` 命令在示例 Red Hat 系统上安装了 Sendmail 8.11。通过这种方式安装了三个 RPM 包：文档、配置文件和 Sendmail 程序。在本节检查的 Sendmail 配置文件是作为 `sendmail-cf-8.11.0-1.i386.rpm` 部分安装的文件。

RPM 包在 `/usr/lib/sendmail-cf` 中创建了一个目录结构，与 Sendmail 源码分发中的 `cf` 目录结构非常相似。对 `/usr/lib/sendmail-cf` 执行 `ls` 显示以下目录：

```
[craig]$ ls /usr/lib/sendmail-cf

README cf domain feature hack m4 mailer ostype siteconfig
```

该目录包含了我们在第 4 章看到的相同的 `cf`, `m4`, `ostype`, `feature`, `mailer` 和 `domain` 子目录，它们执行相同的功能。Red Hat 配置的宏控制文件位于 `/usr/lib/sendmail-cf/cf/` 目录下。它很容易找到。在通用文件中，有一个简单命名为 `redhat.mc` 的文件。这就是我们要找的文件。切换到 `/usr/lib/sendmail-cf/cf` 并 `cat` 该文件。

```
[craig]$ cat /usr/lib/sendmail-cf/cf

[craig]$ cat redhat.mc
```

```
dnl 这是一个用于生成
dnl /etc/sendmail.cf 文件的宏配置文件。如果你修改了该文件，你必须
dnl 通过 m4 预处理器运行此宏配置来
dnl 重新生成 /etc/sendmail.cf：
```

```
dnl m4 /etc/sendmail.mc > /etc/sendmail.cf
```

`dnl` 你需要拥有 `sendmail`
