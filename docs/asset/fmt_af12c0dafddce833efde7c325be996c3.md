
17. 关闭所有终端窗口。

#### 认证目标

Linux+ 考试目标：

- 识别配置文件的用途和特点 (`3.11`)
- 编辑基本配置文件
- 管理和导航 Linux 层次结构 (`4.5`)
- 以 root 身份登录或使用 `su` 命令执行管理任务 (`4.7`)
- 管理和导航图形界面 (`4.17`)
- 识别、执行和杀死进程 (`5.7`)
- 定期监控系统日志文件中的错误、日志和异常活动 (`5.8`)

#### 复习题

+ 1. 你必须编辑哪个文件来更改计算机启动时的运行级别？
  a. `/etc/rc.d/rc`
  b. `lilo.conf` or `grub.conf`
  c. `/etc/inittab`
  d. `/etc/rc.local`

+ 2. 你想监控 `messages` 日志文件并将任何写入日志文件的额外消息也显示在屏幕上。哪个命令可以实现此功能？
  a. `head /var/log/messages`
  b. `head -f /var/log/messages`
  c. `tail /var/log/messages`
  d. `tail -f /var/log/messages`

+ 2. 哪个命令发送一条 `mail` 设施且 `info` 优先级的消息？

  a. `log mail,info This is a test`
  b. `log -p mail info This is a test`
  c. `logger -p mail.info This is a test`
  d. `logger -w mail:info This is a test`

# 实验 12.3 使用命名管道进行日志记录

#### 目标

本实验的目标是学习如何使用命名管道（named pipes）和简单脚本为系统日志记录添加功能。在 Linux 服务器上，两个或多个守护进程记录到同一设施的情况并不罕见。一个很好的例子是用于电子邮件的服务器，它运行着 SMTP 守护进程和一个 POP3 守护进程。它们都记录到 `mail` 设施，导致两个守护进程的日志消息被写入同一个日志文件中。

你无法配置 `syslog` 将这两个守护进程的日志消息写入单独的文件。但是，你可以使用命名管道和简单脚本将消息发送到单独的文件。

#### 所需材料

本实验需要以下材料：

- 访问运行 Linux 的计算机的 root 用户权限

| 预计完成时间: 30 分钟 |

#### 活动

1. 在 Gnome 或 KDE 等图形化桌面以 root 身份登录。
2. 点击桌面上的终端图标启动终端。对于 Gnome 桌面，图标是一个前面带有 Gnome 脚印标志的终端屏幕；对于 KDE 桌面，图标是一个前面带有贝壳的终端屏幕。
3. 如果你修改了 `/etc/syslog.conf`，你必须通过发送 `SIGHUP` 信号通知 `syslog` 守护进程该更改。正确还是错误？
4. 下列选项中优先级最高的是？
   a. `crit`
   b. `alert`
   c. `debug`
   d. `warning`
5. 哪条放在 `syslog.conf` 文件中的语句会将所有 `crit` 级别及以上的消息发送到所有登录用户的终端屏幕？
   a. `mail.crit /var/log/everyone`
   b. `crit.* *`
   c. `.*crit |/var/log`
   d. `.*crit *`

# 实验 12.3 使用命名管道进行日志记录

3. 创建用于记录 SMTP 和 POP3 消息的文件。输入 `touch /var/log/smtp` 并回车。输入 `touch /var/log/pop3` 并回车。输入 `ls -l /var/log` 并回车。注意这两个文件已经创建创建且长度为 0。
4. 现在你需要创建一个命名管道，用于你自己的程序过滤 `syslog` 的输出。输入 `mkfifo /var/log/mailpipe` 并回车。输入 `ls -l /var/log/mail*` 并回车。你应该能在文件列表中看到 `mailpipe` 条目。注意行的第一个字符是 `p`，它代表 `pipe`（管道）。
5. 将此行添加到 `syslog.conf` 文件中，让 `syslog` 知道输出到命名管道：`mail.* | /var/log/mailpipe`。你可以使用文本编辑器完成此操作，或者输入 `echo "mail.* | /var/log/mailpipe" >> /etc/syslog.conf` 并回车。`syslog` 不会自动检测此更改。你必须通过输入 `killall -HUP syslog` 并回车来告诉它配置文件已更改。

> 注意，当你在 `syslog.conf` 文件中指定命名管道时，必须在日志文件路径和名称前加上一个竖线 (`|`)。
6. `Syslog` 现在将 `mail` 消息记录到命名管道。然而，没有程序在监听该管道。你需要构建一个程序来接收管道中的消息，判断它们是来自 SMTP 还是 POP3 守护进程，并将消息发送到相应的文件。将以下 shell 脚本输入到名为 `mailscript` 的文件中，并将其放在 `/usr/local/bin` 目录下。接下来的几步展示了如何使用 `vi` 编辑器进行操作。

```
while [ true ];

do

read </var/log/mailpipe

if echo $REPLY | grep "pop3" > /dev/null

then

echo $REPLY > /var/log/pop3

else

echo $REPLY > /var/log/smtp

fi

done
```

> 注意此程序非常简单，如果你想在真实服务器上使用，可能需要进行完善。你可以使用任何语言（如 Perl 或 C）编写你的程序。
7. 输入 `vi /usr/local/bin/mailscript` 并回车。按 `i`。现在输入步骤 6 所示的程序。完成后，按 `Esc` 键。输入 `:wq` 并回车。
10. 按照第 2 步的操作启动两个终端，并调整它们的大小和位置，使其看起来与上一个练习中的图 12-1 相似。将你用于本次练习第 1 到第 9 步的窗口放在顶部。将其称为第一个窗口。
11. 选择第二个窗口。输入 `tail -f /var/log/smtp` 并回车。
12. 选择第三个窗口。输入 `tail -f /var/log/pop3` 并回车。
13. 选择第一个窗口。输入 `logger -p mail.info "This is a message from the pop3 daemon"` 并回车。消息出现在第三个窗口中。消息被写入了 `/var/log/pop3`。
14. 选择第二个窗口。输入 `logger -p mail.info "This is a message from the smtp daemon"` 并回车。消息出现在第二个窗口中。消息被写入了 `/var/log/smtp`。
15. 关闭所有终端窗口。

#### 目标

Linux 考试目标：
- 编辑基本文件 (`3.2`)
- 使用 `chmod`, `chown` 和 `chgrp` 识别并更改文件权限、模式和类型 (`4.4`)
- 管理并导航 Linux 层次结构 (`4.5`)
- 以 root 身份执行管理任务 (`4.7`)
- 使用 shell (`10`)
- 创建、编辑 (`16`)
- 使用图形界面 (`17`)
- 使用 shell (`18`)
- 识别、杀死 (`5`)
- 监控文件 (`8`)

## 实验 12.4 查找链接与所有者

#### 复习题

1. 哪个命令创建命名管道？
   a. `mnode`
   b. `mkfifo`
   c. `touch`
   d. `mkfs`
2. 使用 `ls -l` 查看，第一个字符是：
   a. `1`
   b. `n`
   c. `p`
   d. `s`
3. 在 `syslog.conf` 中的哪条语句是正确的？
   a. `mail.crit`
   b. `/var/log`
   c. `/var/log`
   d. `info`
4. `syslog` 不会自动检测此更改。正确还是错误？
5. 下列哪个在后台运行？
   a. `logscript`
   b. `background`
   c. `&`
   d. `|`

## 实验 12.4 查找断链和无所有者的文件

8. 输入 `exit` 并按 `Enter`。你不再是以 Betty 的身份登录：你现在是以 root 的身份登录的。

9. 现在删除用户 Betty。输入 `userdel bety` 并按 `Enter`。

10. 输入 `ls -l` 并按 `Enter`。你正在查看 Betty 主目录下的所有文件。注意，用户所有者现在是一个数字（例如 502），而不是 Betty。组所有者也是一个数字。这是因为每个文件的所有者都是以数字 ID（UID）的形式存储在目录中的。当你删除用户时，`ls` 程序会打印 UID 而不是账户名。该文件不再拥有所有者。以下是一个没有所有者的账户的 `ls` 输出的示例：

```
total 0

-rw-rw---- 1 502 502 0 Oct 22 09:48 file1

-rw-rw---- 1 502 502 0 Oct 22 09:48 file2
```
