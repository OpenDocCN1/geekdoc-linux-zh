
3.  在命令提示符下，键入 `systemctl enable sshd.service; systemctl start sshd.service` 并按 **Enter**（回车键），以启动 SSH 守护进程并确保其在系统启动时自动启动。

4.  在命令提示符下，键入 `ssh root@localhost` 并按 **Enter**。当提示连接到远程系统时，键入 **yes**（是）并按 **Enter**。接下来，输入 root 用户的密码 LNXrocks! 并按 **Enter**。

5.  在命令提示符下，键入 `who` 并按 **Enter**。你是否位于伪终端（pseudoterminal）上？键入 `exit` 并按 **Enter** 以注销你的远程 shell。

6.  按 **Ctrl+Alt+F1** 切换到图形终端，并使用用户名 `user1` 和密码 LNXrocks! 登录到 GNOME 桌面。接下来，打开命令行终端（Activities [活动]、Show Applications [显示应用程序]、Utilities [实用工具]、Terminal [终端]）。

7.  在命令提示符下，键入 `ssh -X root@localhost` 并按 **Enter**。当提示连接到远程系统时，键入 **yes** 并按 **Enter**。当被要求时，输入 root 用户的密码 LNXrocks! 并按 **Enter**。

8.  在命令提示符下，键入 `system-config-abrt` 并按 **Enter**。请注意，此命令会在图形窗口中启动远程问题报告实用程序。关闭问题报告实用程序，键入 `exit` 并按 **Enter** 以关闭你的远程 shell。完成后，注销 GNOME 桌面。

9.  按 **Ctrl+Alt+F2** 切换回 tty2，并键入 `ssh user1@IP`，其中 *IP* 是你 Ubuntu Server Linux 虚拟机的 IP 地址。当提示连接到远程系统时，键入 **yes** 并按 **Enter**。当被要求时，输入 root 用户密码 LNXrocks!。为什么 Ubuntu Server 中默认启动 SSH 守护进程？

10. 在命令提示符下，键入 `su - root` 并按 **Enter**。当被要求时，输入 root 用户密码 LNXrocks! 以获取 root shell。

11. 在命令提示符下，键入 `vi /etc/ssh/sshd_config` 并按 **Enter**。修改 **PermitRootLogin** without-password 行，使其读取为 **PermitRootLogin yes**，保存你的更改并退出 vi 编辑器。

12. 在命令提示符下，键入 `service ssh reload` 并按 **Enter**，以强制 SSH 守护进程重新加载其配置文件。

13. 键入 `exit` 并按 **Enter** 以注销你的远程 shell。

14. 在命令提示符下，键入 `ssh user1@IP`，其中 *IP* 是你 Ubuntu Server Linux 虚拟机的 IP 地址，并在被要求时输入 root 用户密码 LNXrocks!。接下来，键入 `exit` 并按 **Enter** 以注销你的远程 shell。

15. 当被要求时，输入 root 用户密码 LNXrocks!。在命令提示符下，键入 `ssh root@IP cat /etc/issue > /root/partner_issue` 并按 **Enter**，其中 *IP* 是你伙伴计算机的 IP 地址。接下来，输入 root 用户的密码 LNXrocks! 并按 **Enter**。

16. 在命令提示符下，键入 `cat partner_issue` 并按 **Enter**。你伙伴的 issue 文件是否成功传输？

17. 在命令提示符下，键入 `less /etc/ssh/sshd_config` 并按 **Enter**。检查可用的 SSH 客户端选项。注意在注释掉的 Ciphers 行中支持的加密算法。完成后按 **q**。

18. 在命令提示符下，键入 `less /etc/ssh/sshd_config` 并按 **Enter**。检查可用的 SSH 守护进程选项。如果默认不允许 root 连接到 SSH 守护进程，哪一行代码可以允许？完成后按 **q**。

19. 在命令提示符下，键入 `cat /root/.ssh/known_hosts` 并按 **Enter**。这个文件中列出了哪两个主机，为什么？

20. 键入 `exit` 并按 **Enter** 以注销你的 shell。

21. 在你的 Windows 宿主机上，双击桌面上的 putty.exe 文件。注意默认连接类型为 SSH，在 Host Name (or IP address) [主机名（或 IP 地址）] 框中输入你 Fedora Linux 虚拟机的 IP 地址，并点击 **Open**（打开）。使用用户名 root 和密码 LNXrocks! 登录到你的 Fedora Linux 虚拟机。完成后，键入 `exit` 并按 **Enter** 以注销你的远程 shell。

22. 在你的 Windows 宿主机上，双击桌面上的 putty.exe 文件。注意默认连接类型为 SSH，在 Host Name (or IP address) 框中输入你 Ubuntu Server Linux 虚拟机的 IP 地址，并点击 **Open**。使用用户名 root 和密码 LNXrocks! 登录到你的 Ubuntu Server Linux 机器。完成后，键入 `exit` 并按 **Enter** 以注销你的远程 shell。

## 项目 12-7

在这个动手项目中，你将配置你 Fedora Linux 虚拟机上的 VNC 服务器，并从你的 Windows 宿主机远程连接到它。

1.  在你的 Fedora Linux 虚拟机上，按 **Ctrl+Alt+F2** 切换到命令行终端（tty2），并使用用户名 root 和密码 LNXrocks! 登录到终端。

2.  在命令提示符下，键入 `yum install tigervnc-server` 并按 **Enter**。当提示时按 **y** 以完成 tiger VNC 服务器的安装。

3.  在命令提示符下，键入 `cp /lib/systemd/system/vncserver@8.service /lib/systemd/system/vncserver@3.service` 并按 **Enter**，以创建显示屏号 3 的 VNC 配置。

4.  在命令提示符下，键入 `vi /lib/systemd/system/vncserver@3.service` 并按 **Enter**。将所有的 **<USER>** 更改为 user1。保存你的更改，完成后退出 vi 编辑器。

5.  在命令提示符下，键入 `systemctl daemon-reload` 并按 **Enter**，以强制所有守护进程重新读取它们的配置文件。

6.  在命令提示符下，键入 `su - user1` 并按 **Enter**，以将你的 shell 切换到 user1。接下来，键入 `vncpasswd` 并按 **Enter** 以设置 VNC 密码。当提示时（两次）输入密码 LNXrocks!。

7.  在命令提示符下，键入 `exit` 并按 **Enter** 以返回到你的 root shell。

8.  在命令提示符下，键入 `systemctl enable vncserver@3.service; systemctl start vncserver@3.service` 并按 **Enter**，以启动 VNC 守护进程并确保其在系统启动时自动启动。

9.  在命令提示符下，键入 `firewall-cmd --permanent --zone=public --add-service vnc-server` 并按 **Enter**，以为 VNC 服务器添加永久防火墙例外规则。

10. 在命令提示符下，键入 `reboot` 并按 **Enter** 以重启你的 Fedora Linux 虚拟机。

11. 在你的 Windows 宿主机上，打开 Web 浏览器，从 `https://www.realvnc.com/download/viewer/` 下载 `RealVNC Viewer for Windows EXE` 程序。安装完成后安装该程序，并在安装后打开该程序。

12. 在 VNC Viewer 程序中，在 VNC Server 对话框中输入 `IP:5903`，其中 `IP` 是你 Fedora Linux 虚拟机的 IP 地址，并点击 **Connect**（连接）。当提示时，输入 VNC 密码 `LNXrocks!`。探索你的 user1 桌面，完成后关闭 VNC Viewer 窗口。

## 探索练习

1.  假设你的公司使用 A 类网络 `100.0.0.0/8`，你需要配置什么子网掩码才能将网络分割 11 次以匹配公司的 11 个部门？每个网络可以有多少台主机？你可以分配给不同部门的前五个地址范围是什么？

2.  在项目 12-6 中，你使用以下方法将文件从远程系统传输到你的本地计算机：

    ```bash
    ssh remotecomputer cat remotefile > localfile
    ```

    利用你对重定向的知识，简要描述此命令如何实现此传输。此命令能否用于传输二进制文件？请解释。

3.  使用互联网、书籍或其他资源，查找如何在 DNS 服务器上注册 `FQDN` 以供互联网使用。描述相关步骤和费用。另外，找出三个如果你愿意注册就可以免费注册的域名。

4.  使用互联网、书籍或其他资源，研究 `DNS` 的历史。它是在何时何地开始的？`DNS` 有不同的版本吗？如果有，它们的区别是什么？

5.  在传统 UNIX 和 Linux 系统中，远程命令（`rlogin`、`rsh` 和 `rcp`）用于在远程系统上执行命令、获取远程 shell 以及在系统之间复制文件。这些命令通常被称为 `r` 命令，它们允许在没有密码的情况下访问远程计算机，前提是该远程计算机拥有受信任的访问权限——也就是说，通过 `/etc/hosts.equiv` 文件或 `~/.rhosts` 文件中的条目允许这样做。虽然现代 Linux 发行版的安全子系统不允许使用 `r` 命令进行受信任的访问，但你仍然可以安装这些 `r` 命令并使用它们（前提是你提供密码）。使用互联网研究 `r` 命令的使用以及你需要托管这些命令的包。接下来，在你的 Ubuntu Server Linux 虚拟机上安装这些包，检查 `/etc/inetd.conf` 文件（用于启动相关服务），并使用 `r` 命令在你的本地 Ubuntu Server Linux 虚拟机上执行远程管理。
