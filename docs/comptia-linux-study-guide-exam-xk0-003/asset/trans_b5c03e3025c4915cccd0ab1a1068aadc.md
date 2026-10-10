
3.11 执行 DHCP 服务器的基本管理任务（`/etc/dhcpd.conf`, `dhcpd`, `.leases`）。

3.12 给定一个场景，排查与 NTP 相关的问题（`/etc/ntp.conf`, `ntpdate`, `date`, `ntpq -p`）。

# 领域 4.0 网络

4.1 识别常见的网络端口及其关联的服务（20, 21, 22, 23, 25, 53, 80, 110, 123, 143, 443, 631, 3306, `/etc/services`）。

4.2 使用以下工具执行网络接口配置（`dhclient`, `dhcpd`, `ifconfig`, `ifconfig`, `route`, `ifup`, `ifdown`, 网络配置文件）。

4.3 针对以下内容实施配置和/或配置更改（数据包过滤：`iptables`；主机名查找：`/etc/hosts`, `/etc/nsswitch.conf`, `/etc/resolv.conf`）。

4.4 解释不同的 DNS 记录类型及 DNS 解析过程（本地解析、TTL/缓存、根名称服务器、A、MX、PTR、CNAME、NS、TXT）。

4.5 使用以下工具排查基本的连接问题（`netstat`, `ping`, `traceroute`, `arp`, `telnet`, `route`）。

4.6 使用以下工具排查名称解析问题（`dig`, `host`, `nslookup`, `hostname`）。

# 领域 5.0 安全

5.1 使用以下工具管理和监控用户及组账户（工具：`useradd`, `userdel`, `usermod`, `groupadd`, `groupdel`, `groupmod`, `lock`, `who`, `w`, `last`, `whoami`。文件：`/etc/skel`, `/etc/passwd`, `/etc/shadow`, `/etc/group`）。

5.2 给定一个场景，选择合适的文件权限和所有权，并排查常见问题（工具：`chmod`, `chown`, `chroot`, `chgrp`, `lsattr`, `chattr`, `umask`。特殊权限：`setuid`, `setgid`, `sticky bit`）。

5.3 解释 SELinux 的基础知识（运行模式 [已启用、已禁用、宽容模式]）。

5.4 给定一个场景，使用以下内容实施权限提升（`sudo`, `su`）。

5.5 解释以下与安全相关的实用程序的适当用法（`nmap`, `Wireshark`, `Nessus`, `Snort`, `Tripwire`）。

5.6 使用校验和及文件验证实用程序（`md5sum`, `sha1sum`, `gpg`）。

5.7 使用以下内容部署远程访问功能（SSH：安全隧道、SFTP、X11 转发、Keygen；VNC）。

5.8 解释身份验证的方法（PAM、LDAP、NIS、RADIUS、双因素身份验证）。

# 评估测试

1. GRUB 可能安装在哪里？
   - A. MBR、Linux 分区的引导扇区或软盘
   - B. MBR、Linux 分区的引导扇区或 Windows 分区的引导扇区
   - C. Linux 分区的引导扇区或 Windows 分区的引导扇区
   - D. MBR、软盘或交换分区

2. 在紧急恢复磁盘上，以下哪个工具是*最重要*的？
   - A. fdformat
   - B. OpenOffice.org
   - C. mkfs
   - D. traceroute

3. 你有可能在日志文件中看到以下哪些类型的信息？（选择所有适用项。）
   - A. 关于用户启动文本编辑器以编辑其目录中文件的信息
   - B. 使用 `su` 命令成功获取 root 权限的记录
   - C. 通过 `xinetd` 控制的服务器登录失败尝试
   - D. 用户通过 `cat` 命令读取其他用户文件的失败尝试

4. `telinit` 命令的 `-t` 参数控制什么？
   - A. 对无需保留的服务进行礼貌关闭（通过 `SIGTERM`）与强制关闭（通过 `SIGKILL`）之间的时间间隔
   - B. 发出 `telinit` 命令与运行级别更改发生之间的时间
   - C. 命令完成后要进入的运行级别
   - D. 在运行级别更改实施前发送给用户的信息

5. 你输入 `ifconfig eth0` 并在输出中看到以下行。此输出意味着什么？
   ```
   Link encap:Ethernet  HWaddr 00:A0:CC:24:BA:02
   ```
   - A. 以太网卡故障，错误代码为 00:A0:CC:24:BA:02。
   - B. 以太网卡的硬件地址为 00:A0:CC:24:BA:02。
   - C. 硬件无法与其他设备建立以太网连接。
   - D. `HWaddr` 开头的 `00` 表示接口尚未激活。

6. 在使用 userdel 删除账户时，明智的做法是什么？
   - A. 确保该用户的密码未在 /etc/passwd 或 /etc/shadow 中重复。
   - B. 在计算机上搜索由前用户拥有的残留文件。
   - C. 更改系统文件权限，以防前用户远程访问它们。
   - D. 使用一个用随机数据覆盖用户文件内容的实用程序删除用户的文件。

7. 一个 `ls -l` 命令显示 `loud` 文件的权限字符串为 `crw-rw---`，且所有者为用户 root，组为 audio。关于此文件，以下哪项陈述是正确的？
   - A. 只有 root 和创建该文件的账户可以读取或写入该文件。
   - B. 由于以 `c` 开头，该文件是一个目录。
   - C. audio 组中的任何人都可以读取和写入该文件。
   - D. 命令 `chmod 660 loud` 将使其对更多用户可访问。

8. 以下哪一项通常出现在 /etc/inetd.conf 的服务器条目中，但不出现在 /etc/xinetd.conf 或 /etc/xinetd.d 中文件的等效条目中？
   - A. 对 `tcpd` 的调用
   - B. 协议的指定，例如 `tcp`
   - C. 用户的指定，例如 `nobody`
   - D. 传递给目标服务器的参数

9. 在以下哪种情况下 `chmod` 命令将无法工作？
   - A. 发出命令的用户不拥有该文件，但拥有该文件所在目录的拥有权和写入权限。
   - B. root 用户在一个读写文件系统中的文件上发出命令，尽管该文件本身没有激活的写入权限。
   - C. 文件所有者发出命令，但文件权限未授予所有者对文件的写入访问权限。
   - D. 文件所有者发出命令，但文件位于一个所有者有读取但无写入访问权限的目录中。

10. `su` 命令的功能是什么？
    - A. 它授予指定用户超级用户权限。
    - B. 它获取指定用户的权限，如果未指定用户名，则获取超级用户的权限。
    - C. 它为运行该命令的用户获取超级用户权限。
    - D. 它授予当前所有登录用户超级用户权限。

11. 在以下哪种情况下，你最可能需要编辑 `/etc/fstab` 文件的内容？
    - A. 你向计算机添加了硬盘。
    - B. 你向计算机的 Zip 驱动器插入了 Zip 磁盘。
    - C. 系统执行磁盘检查并报告没有错误。
    - D. 你更改了 `/boot/grub/menu.lst` 引导选项。

12. 哪一类攻击会拒绝你使用你的设备？
    - A. DoS
    - B. Core
    - C. Rooted
    - D. Phish

13. 你想在 Linux 计算机上设置防火墙。以下哪个工具可能用于完成此任务？
    - A. Apache
    - B. iptables
    - C. wall
    - D. TCP Wrappers

14. `rc.local` 或 `boot.local` 启动脚本的预期目的是什么？
    - A. 它设置系统时区和语言默认值。
    - B. 它保存为其特定计算机创建的启动命令。
    - C. 它显示启动消息以助调试。
    - D. 它验证所有其他启动脚本是否正确运行。

15. BIND 起什么作用？
    - A. 它允许程序使用动态链接库文件。
    - B. 它在主机名和 IP 地址之间进行转换。
    - C. 它将 POP 和 SMTP 服务器连接在一起。
    - D. 它将 IP 地址绑定到网络接口。

16. 你怀疑你与 `ftp.abigisp.net` 之间的路由器出现了故障并阻止了连接。你可以使用哪个工具来追踪哪个系统出了问题？
    - A. nslookup
    - B. ping
    - C. traceroute
    - D. netstat

