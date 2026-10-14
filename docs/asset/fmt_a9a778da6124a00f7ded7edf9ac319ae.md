
下一行如果本地系统名为 `loghost`，则将来自 `mail` 设施的所有 `debug` 消息重定向到 `/var/log/syslog`；否则将它们重定向到 `/etc/hosts`、DNS 或 NIS 中定义的 `loghost` 机器。

> 系统在 `/etc/hosts` 文件中被广泛定义为 `loghost`。例如

```
#/etc/hosts

127.0.0.1 localhost

149.46.23.16 lpserver loghost
```

```
mail.debug ifdef('LOGHOST', /var/log/syslog, @loghost)

#
```

下一组行将来自 `user` 设施的消息重定向到控制台、文件 `/var/adm/messages`，并且仅在本地系统名为 `loghost` 时才重定向到用户的 `root` 和 `operator`。

```
# 非 loghost 机器将使用以下行来使 "user"
# 日志消息记录在本地。
```

```
ifdef('LOGHOST', '
user.err /dev/console
user.err /var/adm/messages
user.alert 'root, operator'
user.emerg *
```

后续条目将被写入 `/var/adm/messages`。

`5`月`15`日 `16:21:49` `alpha` `pete`: 这是下次测试。

+   4. 要停止测试 `syslog`，请在调试模式运行 `syslog` 的窗口中按 `^C`。`syslog` 将显示以下消息：
5. `^Csyslog: going down on signal 2`
6. `syslog: going down on signal 2`
8. #
9.

使用命令 `/usr/syslogd` 在普通模式下重启 `syslogd`。

注意

`syslogd` 应该仅在交互时以调试模式运行。如果系统系统启动脚本（通常为 `/etc/rc.d/S74 syslog`）以调试模式运行 `syslog`，系统将会挂起。

# loginlog

连续失败五次后的未登录尝试将记录在文件 `/var/adm/loginlog` 中，前提是该文件 `/var/adm/loginlog` 存在，且所有者为 `root`，所属组为 `sys`，并且仅对 `root` 具有读写权限。请按照以下步骤创建并配置 `/var/adm/loginlog` 文件以记录未登录尝试：

+   1. 以 `root` 身份登录（或 `su`）。
2. 输入命令 `touch /var/adm/loginlog`。
3. 输入命令 `chown root /var/adm/loginlog`。
4. 输入命令 `chgrp sys /var/adm/loginlog`。
5. 输入命令 `chmod 600 /var/adm/loginlog`。

以下是写入 `/var/adm/loginlog` 的一个示例条目：

```
adm:dev/pts/9 Tue May 5 21:07:49 1998
```

该条目表示用户尝试在 5 月 5 日 9:07 端口 `/dev/pts/9` 上以 `adm` 身份登录。

## syslog

`syslog` 文件 `/var/adm/syslog` 是一个日志文件，包含了所有对 `su` 命令的尝试（无论成功与）。每当执行 `su` 命令时，都会向 `syslog` 文件中添加一个条目。`syslog` 文件的示例所示：

```
SU 02/03 22:47 + tty root-daemon
SU 02/07 15:41 + pts/8 pete-root
SU 02/07 15:45 + console root-daemon
SU 02/13 21:43 + pts/5 pete-root
SU 02/13 22:18 + pts/5 pete-root
SU 02/15 20:03 + console root-daemon
SU 02/15 20:06 + pts/3 pete-root
SU 02/15 20:10 + tty root-daemon
SU 02/23 20:51 + pts/6 pete-root
SU 02/23 21:14 + console root-daemon
```
`syslog` 中的字段为：日期、时间、成功或失败、端口、执行命令的用户。在前面的示例中，所有尝试都是成功的，尝试 `su root` 的尝试除外。

## last

`last` 命令按时间顺序显示登录/注销和启动信息。`last` 读取二进制文件 `/var/adm/wtmp`，该文件每当用户登录或系统重启时都会被写入。示例命令输出如下：

```
pete console :0 Wed Apr 1 20:52 still
logged in console :0 Wed Apr 1 20:40 - 20:51
pete console :0 (00:10) pete console :0 Mon Feb 23 23:31 - 20:39
(23:08) reboot system boot :0 Mon Feb 23 23:13
pete console :0 (01:07) Sun Feb 15 20:03 - 21:11
reboot system boot :0 Sun Feb 15 20:02
pete console :0 (03:55) Sat Feb 7 16:05 - 20:00
reboot system boot :0 Sat Feb 7 15:44
pete console :0 (16:51) Tue Feb 3 22:50 - 15:42
root console :0 (01:46) pete console :0 Tue Feb 3 21:04 - 22:50
pete console :0 (00:04) pete console :0 Tue Feb 3 20:59 - 20:13
root console :0 (00:06) pete console :0 Tue Feb 3 20:52 - 20:59
pete console :0 (00:13) root console :0 Tue Feb 3 20:35 - 20:38
(00:02) pete console :0 Tue Feb 3 20:19 - 20:35
(00:15) pete console :0 Tue Feb 3 20:18 - 20:19
(00:00) pete console :0 Tue Feb 3 20:18 - 20:18
(00:05) root console :0 Tue Feb 3 20:12 - 20:18
reboot system boot :0 Tue Feb 3 20:13
reboot system boot :0 Tue Feb 3 20:11
reboot system boot :0 Tue Feb 3 20:56
root console :0 (00:00) Fri Jan 30 09:11 - 09:12
reboot system boot :0 Jan 28 11:26
root console :0 (20:25) Fri Jan 23 15:00 - 11:25
reboot system boot Thu Jan 22 15:14
```
