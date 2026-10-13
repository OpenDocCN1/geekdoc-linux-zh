
或者使用我们在第 15 章“自动化任务”中讨论过的任何方法。

# 介绍 Postfix

长期以来，`Sendmail` 一直是事实上的事实邮件传输代理（MTA）。曾一度，它是全球 90% 邮件流量背后的力量，尽管它现在已很大程度上被更有价值的程序所取代。

目前流行的程序之一是 `Postfix`，它由 `Wietse Verma` 开发并由其专门维护。`Postfix` 被设计为 `Sendmail` 的无缝替代品，允许系统管理员在字面上替换 `Sendmail` 而不会对系统产生任何不利影响。

`Postfix` 从底层开始设计就是为了保持与 `Sendmail` 的兼容性，但以更高效的方式运行。`Sendmail` 在处理大量邮件或大量客户端时，众周知地非常消耗系统资源。一个常见的问题是处理一切，这使得 `Sendmail` 变成了一个某种单体结构。另一方面，`Postfix` 通过各个独立的模块协同工作，仅使用需要的模块

# 进切换

`Postfix` 易于安装和配置。要做的第一件事是对你可能想要保留的所有 `Sendmail` 信息进行备份，以防万一。完成此后，你需要使用 `yum` 移除 `Sendmail` 并安装 `Postfix`。

成功安装 `Postfix` 后，你可以开始配置它。所有的脚本都位于 `/etc/postfix` 中，包括：

- `install.cf`—`Postfix` 安装时生成的脚本。此文件列出了 `Postfix` 使用的路径位置，在处理 `main.cf` 文件时会有很大帮助。
- `main.cf`—`Postfix` 的主配置脚本。在脚本开头的注释中，建议你任何时候只更改几个选项。考虑到有超过 300 种可能性，这是一个明智的建议！
- `master.cf`—`Postfix` 的节流控制。此脚本允许你更改直接影响其运行速度的 `Postfix` 设置。除非你有理由调整它，否则请让它保持。。我：当你需要更改更改时我会知道的。
- `postfix-script`—`Postfix` 作为封装器使用的脚本。你不能直接执行；相反，它由 `Postfix` 自身调用。

你可以保留原始的 `Sendmail` 别名供 `Postfix` 使用，因为这不会产生太大差异。

# 配置 Fetchmail

在你安装 `Fetchmail` 后，你必须在家目录下创建 `.fetchmailrc`，它为 `Fetchmail` 程序提供配置。你可以使用任何文本编辑器创建并编辑 `.fetchmailrc` 文件。接下来的章节将介绍创建和编辑文件的手动方法。涵盖了基础 `Fetchmail` 安装和运行所需的。

# 第 25 章 处理电子邮件

```
set daemon 600

set postmaster foobar

set logfile ./.fetchmail.log
```
