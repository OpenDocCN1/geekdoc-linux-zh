
7. 完成后，保存更改并退出编辑器。输入 `testparam` 并按**Enter**。如果发现错误，请按照步骤 3 到 7 进行修复。否则，按回车查看你的 Samba 配置。

8. 在命令提示符处，输入 `systemctl restart smbd.service` 并按**Enter** 重启 Samba 守护进程。

9. 在命令提示符处，以 root 身份输入 `smbpasswd -a root` 并按**Enter**。在提示时，提供 `LINUXrocks` 的密码。

11. 在命令提示符处，输入 `smclient //127.0.0.1/` 并按**Enter**。在提示时，提供 `LINUXrocks` 的密码。

12. 在命令提示符处，输入 `smclient //127.0.0.1/` 并按**Enter**。

13. 在命令提示符处，输入 `firewall-cmd --add-service http ; firewall-cmd --add-service --permanent` 并按回车，在系统初始化期间允许防火墙通过 HTTP 连接。

14. 在你的 Windows 或 macOS 主机上，打开浏览器并导航到位置 `http://IPaddress`（其中 `IPaddress` 是你的 Fedora Linux 虚拟机的 IP 地址）。你的网页是否？

15. 返回你的 Fedora Linux 虚拟机。在命令提示符处输入 `ls -l /var/www/index.html` 并按回车。所有者是谁？当你作为用户和组使用它们时，守护进程是什么？

16. 在命令提示符处，输入 `chmod 644 /var/www/html/index.html` 并按回车。在你的 Windows 或 macOS 主机的浏览器中，刷新页面 `http://IPaddress`（其中 `IPaddress` 是你的 Fedora Linux 虚拟机的 IP 地址）。你收到了什么？为什么？

17. 返回你的 Fedora Linux 虚拟机。在命令提示符处输入 `chgrp apache /var/www/html/index.html` 并按回车。

19. 在 Windows 主机的浏览器中，刷新页面 `http://IPaddress`（其中 `IPaddress` 是你的 Fedora Linux 虚拟机的 IP 地址）。你的页面显示正常吗？关闭 Windows 主机浏览器。

20. 返回你的 Fedora Linux 虚拟机，输入 `poweroff` 并按回车关闭虚拟机。

## 项目 13-5

**预计时间：** 30 分钟

**目标：** 配置文件共享。

**描述：** 在此项目中，你将在 Ubuntu Linux 上配置并测试 Samba 共享。

- 1. 启动你的 Ubuntu Linux 虚拟机，使用用户 `root` 和密码 `LINUXroot` 登录！

## CompTIA Linux+ 和 LPCIC-1：Linux 认证指南

2. 在命令提示符处，输入 `apt install samba smclient` 并按**Enter**。再次按**Enter** 确认 Samba 文件守护进程和 `smclient` 命令。

3. 在命令提示符处，输入 `vi /etc/samba/smb.conf` 并按**Enter**。花几分钟检查此文件的内容以编辑任何 Samba 配置选项。注意默认配置的两个共享是 `[inters]` 共享（使用 SMB 共享系统上的所有打印机）和隐藏的 `[print]` 共享（为每个打印机共享打印机，这是必要的）。

4. 向此文件添加以下行：

```
netbios name = ubuntu
```

5. 取消注释/修改向通过验证的用户共享所有主目录：

```ini
[homes]
comment = Home Directories
browse = yes
read only = no
```

6. 接下来

```ini
[etc]
comment = The etc directory
path = /etc
browseable = yes
guest ok = yes
read only = yes
```

7. 完成后，保存更改并退出编辑器。输入 `testparam` 并按**Enter**。如果发现错误，请按照步骤 3 到 7 进行修复。否则，按回车查看你的 Samba 配置。

8. 在命令提示符处，输入 `systemctl restart smbd.service` 并按**Enter** 重启 Samba 守护进程。

9. 在命令提示符处，以 root 身份输入 `smbpasswd -a root` 并按**Enter**。在提示时，提供 `LINUXrocks` 的密码。

11. 在命令提示符处，输入 `smclient //127.0.0.1/` 并按**Enter**。在提示时，提供 `LINUXrocks` 的密码。

11. 在命令提示符处，输入 `smclient //127.0.0.1/` 并按**Enter**。

## 第13章 配置网络服务与云技术

6. 在命令提示符处，输入 `grep "Group " /etc/http/conf/httpd.conf` 并按回车。

7. 在命令提示符处，输入 `apachectl configtest` 并按回车。`/etc/http/conf/httpd.conf` 文件是否存在语法错误？

8. 在命令提示符处，输入 `vi /var/www/html/index.html` 并按回车。是否有条目？以下行（当添加这些行时，vi会自动对它们进行索引以提高可读性）：

```html
<html>
<body>
<hl>My sample website</hl>
</body>
</html>
```

当您保存更改并退出 vi 编辑器时。

9. 在命令提示符处，输入 `systemctl start httpd.service ; systemctl enable httpd.service` 并按回车，启动 Web 服务器并确保它在初始化时启动。

10. 在命令提示符处，输入 `curl http://127.0.0.1/` 并按回车。Apache 是否成功访问了你的网页？

11. 在命令提示符处，输入 `ab -n 1000 http://127.0.0.1/` 并按回车。Apache 响应 1000 次请求花费了多长时间？

12. 在命令提示符处，输入 `less /etc/httpd/logs/access_log` 并按回车。显示了许多页面吗？

13. 在命令提示符处，输入 `firewall-cmd --add-service http ; firewall-cmd --add-service --permanent` 并按回车，在系统初始化期间允许防火墙通过 HTTP 连接。

14. 在你的 Windows 或 macOS 主机上，打开浏览器并导航到位置 `http://IPaddress`（其中 `IPaddress` 是你的 Fedora Linux 虚拟机的 IP 地址）。你的网页是否？

15. 返回你的 Fedora Linux 虚拟机。在命令提示符处输入 `ls -l /var/www/index.html` 并按回车。所有者是谁？当你作为用户和组使用它们时，守护进程是什么？

16. 在命令提示符处，输入 `chmod 644 /var/www/html/index.html` 并按回车。在你的 Windows 或 macOS 主机的浏览器中，刷新页面 `http://IPaddress`（其中 `IPaddress` 是你的 Fedora Linux 虚拟机的 IP 地址）。你收到了什么？为什么？

17. 返回你的 Fedora Linux 虚拟机。在命令提示符处输入 `chgrp apache /var/www/html/index.html` 并按回车。

19. 在 Windows 主机的浏览器中，刷新页面 `http://IPaddress`（其中 `IPaddress` 是你的 Fedora Linux 虚拟机的 IP 地址）。你的页面显示正常吗？关闭 Windows 主机浏览器。

20. 返回你的 Fedora Linux 虚拟机，输入 `poweroff` 并按回车关闭虚拟机。

## 项目 13-5

**预计时间：** 30 分钟

**目标：** 配置 SMB 文件共享。

**描述：** 在此项目中，你将在 Ubuntu Linux 上配置并测试 Samba 共享。

- 1. 启动你的 Ubuntu Linux 虚拟机，使用用户 `root` 和密码 `LINUXroot` 登录1！

## CompTIA Linux+ 和 LPCIC-1：Linux 认证指南

2. 在命令提示符处，输入 `apt install samba smclient` 并按**Enter**。再次按**Enter** 确认 Samba 文件守护进程和 `smclient` 命令。

3. 在命令提示符处，输入 `vi /etc/samba/smb.conf` 并按**Enter**。花几分钟检查此文件的内容以编辑任何 Samba 配置选项。注意默认配置的两个共享是 `[inters]` 共享（使用 SMB 共享系统上的所有打印机）和隐藏的 `[print]` 共享（为每个打印机共享打印机，这是必要的）。

4. 向此文件添加以下行：

```
netbios name = ubuntu
```

5. 取消注释/修改向通过验证的用户共享所有主目录：

```ini
[homes]
comment = Home Directories
browseable = yes
read only = no
```

6. 接下来

```ini
[etc]
comment = The etc directory
path = /etc
browseable = yes
guest ok = yes
read only = yes
```

7. 完成后，保存更改并退出编辑器。输入 `testparam` 并按**Enter**。如果发现错误，请按照步骤 3 到 7 进行修复。否则，按回车查看你的 Samba 配置。

8. 在命令提示符处，输入 `systemctl restart smbd.service` 并按**Enter** 重启 Samba 守护进程。

9. 在命令提示符处，以 root 身份输入 `smbpasswd -a root` 并按**Enter**。在提示时，提供 `LINUXrocks` 的密码。

11. 在命令提示符处，输入 `smclient //127.0.0.1/` 并按**Enter**。在提示时，提供 `LINUXrocks` 的密码。

11. 在命令提示符处，输入 `smclient //127.0.0.1/` 并按**Enter**。

## 项目 13-6

**预计时间：** 20 分钟

**目标：** 配置 NFS 文件共享。

**描述：** 在此实验项目中，你将在 Ubuntu 上使用 NFS 导出 `/etc` 目录并从 Fedora 访问它。

- 1. 在你的 Ubuntu Linux 机器上，使用用户 `root` 和密码 `LINUXroot` 登录！
- 2. 在命令提示符处，输入 `apt install nfs-server` 并按回车。再次按回车安装 NFS。
- 3. 在命令提示符处，输入 `vi /etc/exports` 并按回车。添加一行：`/etc (rw)` 完成后，保存更改并退出编辑器。
- 4. 在命令提示符处，输入 `exports -a` 并按回车。接下来，输入 `systemctl restart nfs-kernel-server.service` 并按回车退出 shell。
- 5. 输入 `exit` 并按回车退出 shell。
- 6. 启动你的 Linux 虚拟机。在 Linux 加载后，通过 Ctrl+Alt+5 切换到终端 `tty5`，使用用户 `root` 和密码 `LINUXrocks` 登录终端。
- 7. 在命令提示符处，输入 `mount -t nfs IPAddress:/etc /mnt`（其中 `IPAddress` 是你的 Ubuntu 虚拟机的 IP）并按回车。
- 8. 在命令提示符处，输入 `df -HT` 并按回车。挂载目录是什么？
- 9. 在命令提示符处，输入 `ls -F /mnt` 并按回车。你观察到了什么？在命令提示符处输入 `cat /mnt/issue` 并按回车。该 `issue` 文件来自你的 Ubuntu 服务器虚拟机吗？
- 10. 在命令提示符处，输入 `umount /mnt` 并按回车卸载文件系统。

## 项目 13-7

**预计时间：** 40 分钟

**目标：** 配置 FTP 文件服务。

**描述：** 在此实验项目中，你将在 Ubuntu Linux 上安装并配置安全 FTP 守护进程，并使用 FTP 和 SFTP 传输文件。

- 1. 在你的 Ubuntu Linux 机器上，使用用户 `root` 和密码 `LINUXrocks` 登录。
- 2. 在命令提示符处，输入 `apt install vsftpd` 并按回车安装 `vsftpd`。
- 3. 在命令提示符处，输入 `cp /etc/hosts -user/file1 ; cp /etc/hosts /srv/ftp/file3` 并按回车，在你的主目录 `file1` 中创建 `/etc/hosts` 的两个副本，同时在 `/srv/ftp` 目录中创建一个 `/etc/hosts` 的副本。
- 4. 在命令提示符处，输入 `vi /etc/vsftpd.conf` 并按回车。花几分钟阅读此文件的内容并编辑每个选项。

## CompTIA Linux+ 与 LPIC-1：Linux 认证指南

`write_enable=YES`, 将 `anonymous_enable` 行修改为 `read anonymous_enable=YES`，保存更改并退出编辑器。

- 5. 在命令提示符下，输入 `systemctl restart vsftpd.service` 并按回车以重启 `vsftpd`。
- 6. 在命令提示符下，输入 `ftp localhost` 并按回车。以用户 `user1` 登录，密码为 `LINUXrocks!`。
- 7. 在 `ftp` 提示符下，输入 `dir` 并按回车列出 `/home/user1` 目录的内容。
- 8. 在 `ftp` 提示符下，输入 `lcd /etc` 并按回车将 FTP 客户端的当前工作目录更改为 `/etc`。
- 9. 在 `ftp` 提示符下，输入 `put issue` 并按回车将文件到远程 FTP 服务器。
- 10. 在 `ftp` 提示符下，输入 `dir` 并按回车列出 `/home/user1` 目录的内容。`issue` 文件是否成功上传？
- 11. 在 `ftp` 提示符下，输入 `lcd /` 并按回车将 FTP 客户端的当前工作目录更改为 `/`。
- 12. 在 `ftp` 提示符下，输入 `get issue` 并按回车将 `issue` 文件下载到本地电脑的目录。
- 13. 在 `ftp` 提示符下，输入 `mget file*` 并按回车。按 `a` 将所有匹配 `file*` 的文件下载到本地电脑。
- 14. 在 `ftp` 提示符下，输入 `help` 并按回车列出 FTP 客户端程序中可用命令。
- 15. 在 `ftp` 提示符下，输入 `bye` 并按回车退出 FTP 客户端。
- 16. 在命令提示符下，输入 `ls /` 并按回车列出 `/` 目录。`file1` 和 `file2` 是否成功下载到 `/` 目录？
- 17. 在命令提示符下，输入 `ftp localhost` 并按回车。以匿名身份登录（实际密码对匿名用户不重要；你可以使用任何密码）。
- 18. 在 `ftp` 提示符下，输入 `lcd /` 并按回车将 FTP 客户端的当前工作目录更改为 `/`。
- 19. 在 `ftp` 提示符下，输入 `get file3` 并按回车将 `hosts` 文件下载到本地电脑的目录。
- 20. 在 `ftp` 提示符下，输入 `bye` 并按回车退出 FTP 客户端。
- 22. 在命令提示符下，输入 `ls /` 并按回车。`file3` 是否成功下载到 `/` 目录？
- 23. 在命令提示符下，输入 `ftp localhost` 并按回车。在提示时以 `root` 用户身份登录，密码为 `LINUXrocks`。你能够成功登录了吗？在 `ftp>` 提示符下，输入 `bye` 并按回车退出 FTP 客户端。
- 24. 在命令提示符下，输入 `vi /etc/ftpsusers` 并按回车。删除以下行：

```
root
```
