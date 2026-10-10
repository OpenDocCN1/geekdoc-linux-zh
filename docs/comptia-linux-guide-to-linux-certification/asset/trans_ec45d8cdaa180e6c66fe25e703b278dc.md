
## 项目 12-3

在这个动手实践中，您将使用 Ubuntu Server Linux 虚拟机上 ISP 的 DNS 服务器来测试名称解析。

- 1. 在您的 Ubuntu Server Linux 虚拟机上，使用用户名 root 和密码 LNXrocks! 登录到 tty1。
- 2. 在命令提示符处，输入 `host ftp.kernel.org` 并按 Enter。返回给 ftp.kernel.org 的 IP 地址是什么？ftp.kernel.org 是否有其他名称？
- 3. 在命令提示符处，输入 `nslookup ftp.kernel.org` 并按 Enter。您如何知道这些信息来自您 ISP 的 DNS 服务器？
- 4. 在命令提示符处，输入命令 `dig ftp.kernel.org` 并按 Enter。与 `nslookup` 和 `host` 工具相比，`dig` 提供了哪些额外信息？
- 5. 输入 `exit` 并按 Enter 注销当前 shell。

## 项目 12-4

在这个动手实践中，您将查看并配置 Fedora Linux 虚拟机上的路由表，以及查看和测试您的路由配置。

- 1. 在您的 Fedora Linux 虚拟机上，按 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用用户名 root 和密码 LNXrocks! 登录到终端。
- 2. 在命令提示符处，输入 `route` 并按 Enter。列出了哪些条目？每个条目代表什么？哪个 IPv4 地址被列为您默认网关？
- 3. 在命令提示符处，输入 `ip route add 1.0.0.0/8 via gwIP` 并按 Enter，其中 gwIP 是您默认网关的 IPv4 地址。
- 4. 在命令提示符处，输入 `route` 并按 Enter。步骤 3 中添加的路由是否可见？该路由是否会干扰发送到 1.0.0.0 网络的数据流量？请解释。
- 5. 在命令提示符处，输入 `traceroute ftp.kernel.org` 并按 Enter。将您的数据包传递到 ftp.kernel.org 计算机使用了多少台路由器？
- 6. 在命令提示符处，输入 `tracepath ftp.kernel.org` 并按 Enter。是否走了相同的路径？如果没有，请解释原因。
- 7. 在命令提示符处，输入命令 `cat /proc/sys/net/ipv4/ip_forward` 并按 Enter。您的系统是否配置为 IPv4 路由器？接下来，输入命令 `cat /proc/sys/net/ipv6/conf/all/forwarding` 并按 Enter。您的系统是否配置为 IPv6 路由器？
- 8. 输入 `exit` 并按 Enter 注销当前 shell。

## 项目 12-5

在这个动手实践中，您将在 Ubuntu Server Linux 虚拟机上安装并配置扩展 Internet 超级守护进程 (xinetd) 和 telnet 服务器守护进程。接下来，您将在 Ubuntu 主机上使用 telnet 命令，以及在 Windows 主机上使用 Putty 程序，测试对您的 Ubuntu Server Linux 虚拟机进行远程管理。最后，您将在 Fedora Linux 虚拟机上安装 telnet 服务器守护进程，并执行使用 telnet 会话进行远程管理。

- 1. 在您的 Ubuntu Server Linux 虚拟机上，使用用户名 **root** 和密码 **LNXrocks!** 登录到 tty1。
- 2. 在命令提示符处，输入 `yum install xinetd telnetd` 并按 *Enter*。
- 3. 使用文本编辑器（例如 *vi*）编辑 `/etc/xinetd.d/telnet` 文件（这将是一个新文件），并添加以下内容：

```
{
  service telnet
  {
    disable = no
    flags = REUSE
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/in.telnetd
    log_on_failure += USERID
  }
}
```

- 4. 在命令提示符处，输入 `service xinetd restart` 并按 *Enter* 以重启扩展 Internet 超级守护进程。
- 5. 在命令提示符处，输入 `telnet localhost` 并按 *Enter*。当提示时，提供用户名 **user1** 和密码 **LNXrocks!**。
- 6. 接下来，在命令提示符处输入 **who** 并按 *Enter*。您是否通过本地连接使用伪终端？
- 7. 输入 `exit` 并按 *Enter* 注销您的远程 shell。
- 8. 在命令提示符处，输入 `telnet localhost` 并按 *Enter*。当提示时，提供用户名 **root**。您收到了什么错误？
- 9. 在命令提示符处，输入 `mv /etc/security /etc/security.backup` 并按 *Enter*。
- 10. 在命令提示符处，输入 `telnet localhost` 并按 *Enter*。当提示时，提供用户名 **root** 和密码 **LNXrocks!**。
- 11. 输入 `exit` 并按 *Enter* 注销您的远程 shell。
- 12. 在您的 Windows 主机上，使用 Web 浏览器从 [www.chiark.greenend.org.uk/sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/sgtatham/putty/download.html) 下载 putty.exe 程序，并将可执行文件保存到您的 Windows 桌面上。
- 13. 双击您 Windows 桌面上的 putty.exe 文件。默认连接类型是什么？选择 **Telnet** 作为连接类型，在 Host Name (or IP address) 框中输入您的 Ubuntu Server Linux 虚拟机的 IP 地址，并单击 **Open**。使用用户名 **root** 和密码 **LNXrocks!** 登录到您的 Ubuntu Server Linux 虚拟机。接下来，在命令提示符处输入 **who** 并按 *Enter*。您的伪终端会话旁边的括号中列出了什么以及为什么？
- 14. 输入 **exit** 并按 **Enter** 注销您的远程 shell（这将关闭 PuTTY 程序）。最后，输入 **exit** 并按 **Enter** 注销您的本地 shell。
- 15. 在您的 Fedora Linux 虚拟机上，按 **Ctrl+Alt+F2** 切换到命令行终端 (tty2)，并使用用户名 **root** 和密码 **LNXrocks!** 登录到终端。
- 16. 在命令提示符处，输入 `telnet IP`，其中 `IP` 是您的 Ubuntu Server Linux 虚拟机的 IP 地址，并按 **Enter**。当提示时，提供用户名 **root** 和密码 **LNXrocks!**。
- 17. 在命令提示符处，输入 `who` 并按 **Enter**。您的伪终端会话旁边的括号中列出了什么以及为什么？输入 **exit** 并按 **Enter** 注销您的远程 shell。
- 18. 在命令提示符处，输入 `yum install telnet-server telnet` 并按 **Enter**，在您的 Fedora Linux 虚拟机上安装 telnet 守护程序和 `telnet` 命令。在提示完成安装时按 `y`。
- 19. 在命令提示符处，输入 `systemctl start telnet.socket` 并按 **Enter** 以启动 telnet 守护程序。
- 20. 在命令提示符处，输入 `mv /etc/security/ /etc/security.backup` 并按 **Enter**。
- 21. 在命令提示符处，输入 `telnet localhost` 并按 **Enter**。当提示时，提供用户名 **root** 和密码 **LNXrocks!**。为什么 root 登录成功？输入 **exit** 并按 **Enter** 注销您的远程 shell。
- 22. 在命令提示符处，输入 `firewall-cmd --add-service telnet` 并按 **Enter**，在您的 Fedora Linux 虚拟机上为 telnet 添加防火墙例外。我们在第 14 章中讨论防火墙。
- 23. 接下来，输入 **exit** 并按 **Enter** 注销您的 shell。
- 24. 在您的 Windows 主机上，双击桌面上的 putty.exe 文件。选择 **Telnet** 作为连接类型，在 **Host Name (or IP address)** 框中输入您的 Fedora Linux 虚拟机的 IP 地址，并单击 **Open**。使用用户名 **root** 和密码 **LNXrocks!** 登录到您的 Fedora Linux 虚拟机。
- 25. 接下来，在命令提示符处输入 `who` 并按 **Enter**。您的伪终端会话旁边的括号中列出了什么以及为什么？输入 **exit** 并按 **Enter** 注销您的远程 shell（这将关闭 PuTTY 程序）。

## 项目 12-6

在这个动手实践中，您将在 Ubuntu Server Linux 和 Fedora Linux 虚拟机上配置 SSH。此外，您还将使用 SSH 对您的 Ubuntu Server Linux 和 Fedora Linux 虚拟机执行远程管理。

- 1. 在您的 Fedora Linux 虚拟机上，按 **Ctrl+Alt+F2** 切换到命令行终端 (tty2)，并使用用户名 **root** 和密码 **LNXrocks!** 登录到终端。
- 2. 在命令提示符处，输入 `ps -ef | grep sshd` 并按 **Enter**。SSH 守护程序是否默认启动？
