
### 项目 12-4

在本次实操项目中，你将查看并配置计算机的路由表并测试你的路由配置。

1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，并使用用户名 `root` 和密码 `secret` 登录终端。
2. 在命令提示符下，输入 `route` 并按回车。列出了哪些条目？每个条目代表什么？列出的默认网关 IPv4 地址是什么？
3. 在命令提示符下，输入 `ip route add 1.0.0.0/8 via gwIP`，其中 `gwIP` 是你默认网关的 IPv4 地址。
4. 在命令提示符下，输入 `route` 并按回车。步骤 3 中添加的路由可见吗？此路由会干扰发送到 1.0.0.0 网络的流量吗？请解释。
5. 在命令提示符下，输入 `traceroute ftp.kernel.org` 并按回车。使用了多少路由器来将你的数据包传递到 `ftp.kernel.org` 计算机？
6. 在命令提示符下，输入命令 `cat /proc/sys/net/ipv4/ip_forward` 并按回车。你的系统是否配置为 IPv4 路由器？接下来，输入命令 `cat /proc/sys/net/ipv6/all/forwarding` 并按回车。你的系统是否配置为 IPv6 路由器？作为路由器最少需要多少网络接口？
7. 输入 `exit` 并按回车退出你的 shell。

### 项目 12-5

在本次实操项目中，你将安装并配置 Internet Super Daemon（超级守护）以及 telnet 和 r 守护进程。接下来，你将使用 telnet 和 r 命令对你的本地计算机进行远程管理。

1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，并使用用户名 `root` 和密码 `secret` 登录终端。
2. 在命令提示符下，输入 `telnet localhost` 并按回车。你收到了什么错误？为什么？
3. 在命令提示符下，输入 `yum install xinetd-telnet-server rsh-server` 并按回车。在提示确认下载时输入 `y` 并按回车。
4. 使用 `vi` 等文本编辑器编辑 `/etc/xinetd.d/telnet` 文件，将如下行改为：

```
disable = yes
```

变为

```
disable = no
```

完成后，保存更改并退出编辑器。对 `/etc/xinetd.d/login` 和 `/etc/xinetd.d/rsh` 文件重复此步骤。
5. 在命令提示符下，输入 `service xinetd start` 并按回车启动 Internet Super Daemon。接下来，输入 `chconfig --level 5 xinetd` 以确保 Internet Super Daemon 在运行级别 5 下启动。
6. 在命令提示符下，输入 `telnet localhost` 并按回车。你成功了吗？接下来，在提示时使用用户名 `root` 和密码 `secret` 登录系统。你成功了吗？你收到了什么错误信息？等待一分钟让 `telnet` 工具关闭。
7. 在命令提示符下，输入 `rm -f /etc/xinetd/security` 并按回车。
8. 在命令提示符下，输入 `telnet localhost` 并按回车。接下来，在提示时使用用户名 `root` 和密码 `secret` 登录系统。你成功了吗？为什么？

## 第 12 章 网络配置

### 销售

9. 在命令提示符下，输入 `date` 并按回车。接下来，输入 `who`。根据这些命令，你知道你所在的哪里吗？
10. 输入 `exit` 并按回车退出 shell。你退出了哪个 shell？接下来，输入 `who`。你如何知道 `telnet` 会话已关闭？
11. 在命令提示符下，输入 `echo >> .hosts`。这条命令做了什么？
12. 在命令提示符下，输入 `login` 并按回车。你登录了系统吗？
13. 在命令提示符下，输入 `who` 并按回车。你使用的是哪个终端？
14. 输入 `exit` 并按回车退出。
15. 在命令提示符下，输入 `rsh localhost` 并按回车。在本地运行。
