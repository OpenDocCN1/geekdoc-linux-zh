
此防火墙规则将允许来自内部客户端的远程服务器端口514（syslog端口）的UDP包。更多信息请参见第7章“防火墙”。

最后，在本地服务器上编辑 `syslog.conf` 文件（`vi /etc/syslog.conf`），在该文件末尾添加：

`authpriv.*,mail:daemon.info`

其中 `mail` 是远程服务器的主机名。现在，如果有人黑入你的机器并删除了系统日志，你有一个所有内容的副本。你应该据此追踪他们的来源并进行处理。

现在重启 syslog 守护进程以更改生效：

```
[root@deep ~]# /etc/rc.init.d/syslog restart
```

作为远程服务器，我们必须在本地主机的防火墙文件中添加或验证以下行：

```
ipchains -A output -s EXTERNAL_INTERFACE -p udp \
-s $SYSLOG.SERVER
-d $SYSLOG.SERVER 514 -j ACCEPT
```

在防火墙文件中 `EXTERNAL_INTERFACE="eth0"`。

在防火墙文件中 `IPADDR="28.164.168.1"`。

在防火墙文件中 `SYSLOG_SERVER="mail.openapi.com"`。

现在重启防火墙以更改生效：

```
[root@deep ~]# /etc/rc.init.d/firewall restart
```

## Linux通用安全 | 第3章

此防火墙规则将允许本地服务器发往远程 syslog 服务器端口514（syslog端口）的UDP包。更多信息请参见第7章“防火墙”。

注意：永远不要使用网关服务器作为控制所有 syslog 消息的主机；这是一个非常糟糕的想法。更多选项和策略请参见 `syslog(8)`、`syslog(2)` 和 `syslog.conf(5)`。

## 修改 "etc/rc.d/init.d/" 目录下文件的权限

修复启动和停止所有需要在启动时运行的进程的脚本权限。

```
## chmod -R 700 /etc/rc.d/init.d/
```

这意味着只允许 root 读取、写入和执行该目录下的脚本。我认为普通用户不需要知道这些脚本的内容。

注意：如果你安装或更新了使用 "etc/rc.d/init.d/" 目录下系统 V 脚本的程序，不要忘记再次更改或验证该脚本文件的权限。

## /etc/rc.d/rc.local 文件

默认情况下，当你登录 Linux 机器时，它会告诉你 Linux 发行版名称、版本和服务器名称。这暴露了太多信息。我们更倾向于只给用户显示“Login:”。

### 第一步

要执行此操作，编辑 `etc/rc.d/rc.local` 文件，并在如下所示的行前放置 `"#"`：

```
## 这将在每次启动时覆盖 /etc/rc.local。因此，如果你想在此处对 /issue 进行任何更改，在重启时将丢失它们。
#echo "#" > /etc/issue
#echo "SR" >> /etc/issue
#echo "Kernel $(uname -r) on Sa $(uname -m)" >> /etc/issue
#-cp -f /etc/issue /etc/issue.net
#echo >> /etc/issue
```

### 第二步

然后删除 `"/etc"` 目录下的 `"issue.net"` 和 `"issue"` 文件：

```
## rm -f /etc/issue
## rm -f /etc/issue.net
```

注意：`issue.net` 文件是用户通过网络（如 telnet、SSH）连接机器时看到的登录 banner。你会在 `etc` 目录下找到它，还有一个名为 `issue` 的类似文件，它是显示给本地用户的登录 banner。它仅仅是一个文本文件，可以根据自己的喜好进行自定义。请注意，如上述，如果你更改或删除了它，还需要修改 `etc/rc.d/rc.local` shell 脚本，该脚本每次系统启动时都会重新创建 `issue` 和 `issue.net` 文件。

## root 权限程序的位位信息

如果一个 root 程序被设置为 SUID，则普通用户就可以运行该程序。你计算机上所有模式位中出现 's' 位的程序和文件，都启用了 SUID `-rws-xr-x` 或 SGID `-r-xr-sr-x` 位。这些程序赋予了执行用户特殊的特权，重要的是要从那些绝对不需要此类权限的 root 拥有程序中移除 's' 位。这可以通过执行命令 `chmod a-s` 并将 SUID/SGID 文件的名称作为参数来实现。

此类程序包括但不限于：

- 你从不使用的程序。
- 你不希望任何非 root 用户运行的程序。
- 你偶尔使用的程序，且不介意必须通过 `su(1)` 切换到 root 来运行。

我们在我们个人可能会禁用的每个程序旁边标记了星号 `*`，并认为它们对于我们服务器的日常工作并非绝对必需。请记住，你的系统需要一些 root 程序才能正常工作，因此请谨慎操作。

要找到所有 root 拥有程序中带有 's' 位的程序，请使用命令：

```
root@deep# find -type f -perm -04000 -o -perm -02000 -exec ls \
```

| | | size | day | time | path |
| --- | --- | --- | --- | --- | --- |
| *rws-xr-x | root | 35168 | 22 | 23:35 | /usr/bin/chage |
| *rws-xr-x | root | 36756 | 22 | 23:35 | /usr/bin/gpasswd |
| *rws-xr-x | tty | root | 6788 | 6 | 18:17 | /usr/bin/wall |
| *rws-xr-x | man | 33162 | 16 | 16:35 | /usr/bin/cron |
| *rws-xr-x | root | 34858 | 13 | 20:26 | /usr/bin/man |
| -r-s-xr-x | root | 22312 | 25 | 11:52 | /usr/bin/passwd |
| *rws-xr-x | root | 518140 | 30 | 23:12 | /usr/bin/sudoperl |
| *rws-xr-x | root | 2454 | 20 | 10:39 | /usr/bin/locate |
| *rws-xr-x | root | 14024 | 25 | 01:01 | /usr/bin/chfn |
| *rws-xr-x | root | 13768 | 29 | 01:01 | /usr/bin/chsh |
| *rwx-xr-x | tty | root | 5576 | 9 | 01:01 | /usr/bin/newgrp |
| *rwx-xr-x | root | 8329 | 9 | 01:01 | /usr/bin/write |
| *rws-xr-x | root | 21816 | 10 | 16:03 | /usr/bin/systemctl |
| *rws-xr-x | root | 5896 | 29 | 23:59 | /usr/bin/netstat |
| *rws-xr-x | tty | root | 6096 | 32 | 20:11 | /usr/bin/tmp |
| *rws-xr-x | root | 14104 | 14 | 17:22 | /bin |
| *rws-xr-x | root | 53620 | 13 | 20:26 | /bin/mount |
| *rws-xr-x | root | 26700 | 23 | 20:26 | /bin/umount |
| *rws-xr-x | root | 3860 | 29 | 21:59 | /bin/ping |
| *rws-xr-x | root | 2029 | 21 | 20:48 | /sbin/passwd_chkwd |

要禁用上述 suid 程序，请使用以下命令：

```
root@deep# chmod a-s /usr/bin/chage
root@deep# chmod a-s /usr/bin/gpasswd
root@deep# chmod a-s /usr/bin/wall
root@deep# chmod a-s /usr/bin/chfn
root@deep# chmod a-s /usr/bin/chsh
root@deep# chmod a-s /usr/bin/newgrp
root@deep# chmod a-s /usr/bin/write
root@deep# chmod a-s /usr/bin/systemctl
root@deep# chmod a-s /usr/bin/traceroute
root@deep# chmod a-s /bin/mount
```
