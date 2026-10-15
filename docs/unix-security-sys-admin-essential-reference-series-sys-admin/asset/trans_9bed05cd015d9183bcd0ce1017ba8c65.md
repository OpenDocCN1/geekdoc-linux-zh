

这些脚本有多种用途。例如，LOGIN_SCRIPT 可用于向用户显示系统消息，而 LOGOUT_SCRIPT 可用于在注销时清理临时和 scratch 目录。当 rma 启动子 shell 时，这些脚本不会被调用。因此，例如在工作站上打开和关闭窗口不会导致登录或注销脚本被执行。

## 限制和关注点

rma 在限制控制台登录、telnet、rlogin 和 rsns 方面做得很好。不幸的是，rma 没有提供限制 ftp 访问的功能。ftp 守护进程从不尝试执行用户的登录 shell。与 ftp 相反，su 会执行被 su 的用户的 shell。因此，su 一个被禁止访问某台机器的账户会产生访问违规。rma 代码包含一个用于处理 SunOS su 程序的一个奇特之处的部分。SunOS 上的 su 不会将 argv[0] 重置为正在执行的 shell 的名称，因此在 Login() 函数中执行了特殊检查。如果 su 是调用程序，则 shell 的名称从 SHELL 环境变量中提取。

## 结论

rma 看起来像是一个安全工具，但它仅用于强制执行访问策略。聪明的用户可能能够绕过 rma 的功能。这个问题在我使用的 rma 的任何变体中都没有出现。这些包括在运行 SunOS v4.1.x 和 Solaris v2.x 的工作站和服务器上运行的版本。本章讨论的 rma 版本已在 SunOS v4.1.4 和 Solaris v2.5 下测试过。虽然我没有全部测试过，但 rma 应该可以在几乎任何具有 ANSI C 编译器的 UNIX 变体上编译，只需做极少的修改。

就是在那时我写了 logit（清单 7.1）。logit 是一个简单的 shell 脚本，它通过夜间重命名当天的日志文件来为任何系统记账或日志文件“加龄”，以添加扩展名（例如，syslog 将变为 syslog.1）。同时，之前已加龄文件的扩展名会被递增（例如，syslog.1 变为 syslog.2，syslog.2 变为 syslog.3，等等）。

日志文件在成为 n 天后将被清除。因此，变量 LOGFILE 中指定的任何文件将被加龄至 OLD，然后从系统中删除。我保留日志文件一周（图 7.1）。每个加龄文件都以 .n 扩展名命名，显示其当前年龄。syslog.6 是最旧的 syslog 文件，将被下一次清除。

## 清单 7.1 logit shell 脚本可对任何系统记账或日志文件进行加龄。

```
#!/bin/sh
#
# Move today's system log files to yesterday's,
# and yesterday's to the day before's, etc.
# Then, mail the contents of yesterday's.

for LOGFILE in /usr/adm/isdn.log /usr/adm/syslog
do
    OLD=6 # Logs older than current.
    while [ $OLD -gt 1 ]
    do
        NEW=`expr $OLD - 1`
        mv $LOGFILE.$NEW $LOGFILE.$OLD
        OLD=$NEW
    done
    mv $LOGFILE $LOGFILE.$OLD 2> /dev/null
    touch $LOGFILE 2> /dev/null
done

kill -HUP `cat /etc/syslog.pid` # Restart syslog.d

nohup /usr/bin/mailx -s "SYSLOG Status" root </usr/adm/syslog.1 &
nohup grep "Security Error" /usr/adm/isdn.log.1 \
| /usr/bin/mailx -s "ISDN Status" root &
```

没有扩展名的 syslog 文件是系统当前正在使用的文件。加龄后，logit 使用 kill 强制 syslogd 重新读取其配置文件。在当前文件被加龄后这是必要的：如果不执行 kill，消息将发送到 syslog.1 而不是 syslog。我通过 cron 每晚触发 logit。

对 syslog 文件进行加龄并每晚清除最旧的文件可确保 syslog 不会增长到无限大。不幸的是，它并不能保证我会记得查看日志或在其中找到正确的信息。为了帮助

## 图 7.1 一个示例文件列表显示了 logit 生成的当前和加龄的 syslog 文件。

```
-rw-r--r-- 1 root sys 39 Aug 21 03:05 syslog
-rw-r--r-- 1 root sys 45 Aug 20 03:05 syslog.1
-rw-r--r-- 1 root sys 2850 Aug 19 03:05 syslog.2
-rw-r--r-- 1 root sys 8735 Aug 18 03:05 syslog.3
-rw-r--r-- 1 root sys 39 Aug 17 15:38 syslog.4
-rw-r--r-- 1 root sys 541 Aug 16 03:05 syslog.5
-rw-r--r-- 1 root sys 1502 Aug 15 03:05 syslog.6
```

## 清单 7.2 一个示例 syslog.conf 文件显示了记账和日志消息的优先级和路由。

```
# syslogd configuration file.
#
# facility[...].severity    Destination
#
mail.debug                /usr/spool/mqueue/syslog
local0.debug              /usr/adm/isdn.log
*.info;local0.mail.none   /usr/adm/syslog
*.alert                   /dev/console
*.alert                   root
*.emerg                   *
```
