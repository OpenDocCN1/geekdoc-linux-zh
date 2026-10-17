
## 复习题

+ 1. 哪种类型的 netfilter/iptables 链针对指向本地计算机的流量？
   a. INPUT
   b. ROUTE
   c. FORWARD
   d. OUTPUT

+ 2. 路由器必须在多个网络上拥有网络接口才能在网络之间传输信息。对或错？

+ 3. 与网络服务相关的守护进程监听与特定 ________ 相关的网络流量。
   a. 站
   b. 端口
   c. TCP/IP 地址
   d. 分配号

+ 4. 下列哪个端口号与 telnet 相关？
   a. 20
   b. 137
   c. 49
   d. 23

+ 5. 文档根目录包含 Samba 守护进程共享的文件。对或错？

+ 6. 在计算机被用作路由器之前，必须提供什么配置信息？
   a. 路由表
   b. 子网掩码
   c. 默认网关
   d. 默认路由器

+ 7. 下列哪些是常用端口？（选择所有适用项）。
   a. 1020
   b. 50
   c. 2048

+ 8. 为了成为 DNS 服务器，必须做什么？（选择所有适用项）。
   a. 创建区域文件。
   b. 为 DNS 查找创建资源记录。
   c. 创建 NIS 映射。
   d. 运行名称守护进程 `named`。

+ 9. 下列哪个 Linux 入侵检测系统可以检测端口扫描？（选择所有适用项）。
   a. ICU
   b. PortSentry
   c. tripwire
   d. Snort

+ 10. 哪两个命令可以修改 Linux 计算机上的路由表？（选择两个答案）。
    a. `route`
    b. `ipconfig`
    c. `ip`
    d. `traceroute`

+ 11. 哪个文件包含 Red Hat Fedora Core 2 上 Samba 守护进程的配置信息？
    a. `/etc/samba/samba.cfg`
    b. `/etc/samba.conf`
    c. `/etc/samba/smb/smb.conf`
    d. `/etc/samba/smb.conf`

## 复习题 685

+ 12. 下列哪个端口号与 DNS 相关？
    a. 29
    b. 21
    c. 53
    d. 111

+ 13. 哪个文件包含关于 `sudo` 命令使用的用户、计算机和命令的信息？
    a. `/etc/sudo`
    b. `/etc/su.cfg`
    c. `/etc/sudo.cfg`
    d. `/etc/sudoers`

+ 14. 为了保护你的 Linux 计算机免受网络攻击，你应该首先采取哪种操作？
    a. 修改关键系统文件的权限。
    b. 确保只有必要的服务在运行。
    c. 为网络服务使用的每个文件运行校验和和。
    d. 在 `/etc/sudoers` 文件中配置条目。

+ 15. 下列哪个命令可以扫描组织内计算机的可用端口？
    a. `traceroute`
    b. `tracert`
    c. `nmap`
    d. `sudo`

+ 16. 下列哪个 Linux 入侵检测系统可以检测被修改的文件和目录？（选择所有适用项）
    a. AIDE
    b. SWATCH
    c. tripwire
    d. Snort

+ 17. 哪个文件包含 Red Hat Fedora Core 2 上 Apache 守护进程的配置信息？
    a. `/etc/httpd.conf`
    b. `/etc/apache.conf`
    c. `/etc/httpd/conf/httpd.conf`
    d. `/etc/apache/httpd.conf`

## 第 15 章 配置网络服务与安全

+ 18. Mary 是你们组织的系统管理员。她最近更改了 DHCP 配置文件，但 DHCP 守护进程似乎没有识别新更改。她应该怎么办？
    a. 运行 `sudo` 命令切换到 root 用户并重新编辑配置文件。
    b. 运行 `sudo` 命令编辑配置文件。
    c. 重启 DHCP 守护进程。
    d. 重启 `xinetd` 守护进程。

+ 19. 安全本地 Linux 服务器的实践实践有哪些？（选择所有适用项）
    a. 将服务器锁在服务器机间内。
    b. 确保你始终以 root 用户身份登录服务器。
    c. 在服务器上设置 BIOS 密码。
    d. 将默认运行级别设置为 1（单用户模式）。

+ 20. 下列哪些是独立守护进程？（选择所有适用项）
    a. Apache (`httpd`)
    b. FTP (`ftpd`)
    c. telnet (`telnetd`)
    d. DNS (`named`)

## 实验项目

这些项目应按顺序完成。本章的实验项目总共需要三小时。要求包括：
- 一台安装了 RedHat Fedora Core 2 的计算机

### 项目 15-1

在该项目中，启用 telnet 守护进程并使用 telnet 工具连接到：

+ 1. 开启你的计算机。Linux 系统加载后，按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，使用用户名 root 和密码 secret 登录终端。

+ 2. 在命令行提示符输入 `telnet localhost`。你收到了什么错误？为什么？

+ 3. 使用 `vi` 等文本编辑器编辑 `/etc/inet.d/telnet` 文件，删除行：
```
disable = yes
```
完成后，保存更改并退出编辑器。

`img/9ee5f91f3446575a1e6ce62c54cae5d2_707_0.png`

### 实验项目 687

+ 4. 在命令行提示符输入 `telnet localhost`。你能使用 telnet 工具吗？为什么？

+ 5. 在命令行提示符输入 `/etc/init.d/xinetd start` 启动该守护进程。

+ 6. 在命令行提示符输入 `telnet localhost`。你成功了吗？使用用户名 root 和密码 secret 登录系统。你收到了什么错误信息？等待一分钟让 telnet 关闭。

+ 7. 在命令行提示符输入 `cat /etc/security`。该文件的条目代表什么？在命令行提示符输入 `rm -f /etc/security`。

+ 8. 在命令行提示符输入 `telnet localhost`。使用用户名 root 和密码 secret 登录。你成功了吗？为什么？

+ 9. 在命令行提示符输入 `date`。然后在命令行提示符输入 `who`。根据这些命令的输出，你能判断你在使用哪个终端吗？

+ 10. 输入 `exit` 退出 shell。你退出了哪个 shell？在命令行提示符输入 `who`。如何判断 telnet 会话已关闭？

+ 11. 输入 `exit` 退出 shell。

### 项目 15-2

`img/9ee5f91f3446575a1e6ce62c54cae5d2_708_0.png`

在该实验项目中，使用 NFS 导出 `/etc` 目录并通过 `mount` 命令访问它。

+ 1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，使用用户名 root 和密码 secret 登录终端。

+ 2. 使用 `vi` 等文本编辑器编辑 `/etc/exports` 文件。是否有条目？添加一行：
```
/etc server1,root_squash
```
完成后，保存更改并退出编辑器。

+ 3. 在命令行提示符输入 `exportfs -a`。

+ 4. 在命令行提示符输入 `/etc/rc.d/init.d/nfs start`。发生了什么？

+ 5. 在命令行提示符输入 `mount -t nfs localhost:/etc /mnt`。

+ 6. 在命令行提示符输入 `mount`。挂载到 `/mnt` 目录的是什么

### 第 15 章 配置网络服务与安全

+ 7. 在命令行提示符输入 `cd /mnt`。然后在命令行提示符输入 `ls -F`。你观察到哪个目录？在命令行提示符输入 `ls -F /etc`。终端屏幕上的输出相同吗？

+ 8. 在命令行提示符输入 `cd` 回到主目录。然后在命令行提示符输入 `ummount /mnt` 卸载 NFS 文件系统。

+ 9. 你输入 `exit` 退出 shell。

### 项目 15-3

在该实验项目中，你配置 Apache Web 服务器并测试守护进程对系统文件的权限。

+ 1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (`tty2`)，使用用户名 root 和密码 secret 登录终端。

+ 2. 在命令行提示符输入 `grep DocumentRoot /etc/httpd/httpd.conf`。文档根目录是什么？

+ 3. 在命令行提示符输入 `grep DirectoryIndex /etc/httpd/httpd.conf`。Apache 守护进程将从文档根目录提供哪些文件？

+ 4. 在命令行提示符输入 `grep User /etc/httpd/httpd.conf`。Apache 守护进程本地以哪个用户身份运行？

+ 5. 在命令行提示符输入 `grep Group /etc/httpd/httpd.conf`。Apache 守护进程本地以哪个用户组身份运行？
