
### 服务器 NTP 配置

e. 在服务器设置面板中，从下拉菜单中选择公共 NTP 服务器（`Public NTP Server`）。

公共 NTP 服务器对话框出现。

f. 从国家（`Country`）下拉菜单中选择你的国家或地理位置附近的国家。

g. 从公共 NTP 服务器下拉菜单中选择一个根据策略允许你作为时间源的公共 NTP 服务器。

点击测试其可用性。结果取决于你课程环境的互联网连接。点击确定确认测试结果。

h. 点击确定 > 确定。

你返回到高级 NTP 配置对话框。

i. 点击确定 保存 NTP 配置。

- 5. 在终端窗口，输入 `rntp status` 查看 NTP 时间同步状态。

输出结果将取决于 `ntpd` 启动以来经过的时间，以及你配置的 NTP 服务器是否可以从你的计算机访问。

- 6. 输入以下命令查看 NTP 服务器的日志：

```bash
tail -f /var/log/ntp
```

按下 `Ctrl+c` 停止跟踪。

- 7. 输入 `less /etc/ntp.conf` 查看 `/etc/ntp.conf` 文件的更改。

请注意，NTP 服务器是你之前选择的服务器。

- 8. 输入 `hwclock` 检查硬件时钟。

- 9. 输入以下命令从系统时间设置硬件时钟：`hwclock --systohc`

- 10. 输入 `hwclock` 检查新的硬件时钟。

- 11. 关闭所有打开的窗口。

（练习结束）

## 练习 7-8 配置 xinetd

在练习中，你将配置 `xinetd` 提供 `Telnet` 和 `Finger` 服务。此练习包含两个部分。

在练习的第一部分，使用 YaST 网络服务 (`xinetd`) 模块在你的计算机上设置 Telnet 服务器。

在第二部分，安装 Finger 服务，并编辑 `/etc/xinetd.d/` 中的配置以激活该服务。

### 完成练习的详细步骤

- 第一部分：使用 YaST 启用 xinetd 服务
- 第二部分：手动启用 xinetd 服务

## 第一部分：使用 YaST 启用 xinetd 服务

在 `da-host` 上执行以下操作：

1. YaST 控制中心并选择 网络服务 > 网络服务 (`xinetd`)。

出现网络服务配置 (`xinetd`) 对话框。

2. 选择“启用”。

当前可用服务列表将变为激活状态。

3. 向滚动并选择服务 `telnet (Server:/usr/sbin/in.xinetd)`，然后通过选择“切换状态（开启或关闭）”将服务设置为“开启”。

如果尚未安装 `telnet-server` 软件包，它现在将会被安装。根据需要插入 SUSE Linux Enterprise Server 11 安装 DVD 并选择“安装”。

4. 选择“完成”将配置保存到系统。

5. 测试配置。

a. 打开终端窗口并输入 `telnet localhost` 登录到本地主机。

b. 以 `geeko` 身份登录（密码：`novell`）。

c. 输入 `exit` 退出。

d. 在 `dal` 上，打开终端窗口并输入 `telnet 172.17.8.1` 登录到 `da-host.digitalairirlines.com`。

e. 以 `geeko` 身份登录（密码：`novell`）。

f. 输入 `exit` 退出。

## 第二部分：手动启用 xinetd 服务

通过以下操作在 `da-host` 上启用 `finger` 服务器：

1. 在终端窗口，使用 `su --` 变为 `root`（密码：`novell`）。

2. 如果尚未安装 `finger-server` 软件包，请安装：

`rpm -q finger-server || rpm -i finger-server`

3. 在终端窗口，输入 `vi /etc/xinetd.d/finger` 编辑 `/etc/xinetd.d/finger` 文件。

4. 在文件底部，将 `disable = yes` 设置更改为：

`disable = no`

5. 保存更改并关闭 `vi`。

6. 输入 `rcinetd restart` 重启 `xinetd` 服务。

7. 通过以下操作测试 Finger 服务：

a. 在 `dal` 上，打开终端窗口。

b. 输入 `finger @172.17.8.1` 获取 `da-host` 可用的 `finger` 信息。

c. 输入 `finger geeko@172.17.8.1` 获取特定用户的 `finger` 信息。

8. 可选：更改 Finger 配置以仅允许在一天中的特定时间访问。测试你的配置。

9. 输入 `rcinetd stop` 停止 `xinetd` 服务。

（练习结束）

### 复习题

1. 你可以运行两个命令来激活对 `/etc/samba/smb.conf` 文件的更改？

a) `smbclient --restart`

b) `rscmb restart`

c) `nmbclient --restart`

d) `rcnmb restart`

2. 你可以使用什么命令检查 `/etc/samba/smb.conf` 文件的错误？

3. 使用什么命令可以使用 SMB 将服务器 `arfa` 上的 `acctg` 共享目录挂载到本地 `/mnt` 目录？

4. SLES for Apache Web 服务器上的默认文档根目录是什么？

5. 使用哪个 Apache 指令设置 Apache 虚拟主机 IP 地址和端口？

a) `Listen`

b) `NameVirtualHost`

c) `VirtualHostIP`

d) `VirtualHost`

6. 什么文件可以包含 Apache 的特定目录访问限制？

a) `htpasswd`

b) `AllowOverride`

c) `.htaccess`

d) `http.conf`

7. 哪些主机允许连接到目录？

```apache
<Directory /var/www/website>
Order allow,deny
Deny from all
</Directory>
```

a) 所有主机

b) 无主机

c) 仅允许执行反 DNS 查询的主机

d) 仅允许列在 `<Allowedhosts>` 部分的主机

8. 什么 Apache 文件记录 Web 服务器访问？

a) `custom_log`

b) `access_log`

c) `server_log`

d) `error_log`

9. 你可以使用什么命令向 MySQL 表插入条目？

a) `mysql`

b) `dbadmin`

c) `insert`

d) `update`

10. 下列哪些是可以生成动态内容的技术？

a) `CGI`

b) `Perl`

c) `PHP`

d) (以上所有)

11. SLES 上 NTP 的默认配置文件是什么？

12. 你可以运行什么命令将你的时间与 `/etc/ntp.conf` 中列出的源手动同步？

13. 下列哪些是 DNS 解析的有效命令？

a) `nslookup`

b) `dig`

c) `host`

d) (以上所有)

14. 哪个术语指的是时间服务器距离原子钟等实时时间源的跳数距离？

15. MUA 通常使用什么协议来检索电子邮件？

16. MUA 通常使用什么协议来发送邮件？

17. 你最近修改了 `/etc/aliases` 文件。你可以运行什么命令来更新别名？

a) `newaliases`

b) `alias`

c) `postmap`

d) `list`

18. 区域文件中的哪种记录用于将名称映射到 IP 地址？

a) `SOA`

b) `NS`

c) `MX`

d) `A`

19. 你的计算机作为 DNS 服务器运行时，必须安装哪些软件包？

a) `bind`

b) `bind-chroot`

c) `bind-utils`

d) (以上所有)

20. 从 DNS 服务器如何知道主服务器发生了更改？

a) 向主 DNS 服务器广播

b) 查询主服务器上 SOA 的序列号

c) 接收主服务器的区域通知

d) 从主服务器获取 NS 记录

21. 哪个 `xinetd` 文件可以配置 `telnet` 守护进程？

a) `/etc/telnet.d`

b) `/etc/xinetd`

c) `/etc/xinetd.d/telnet`

d) `/etc/xinetd`

22. 假设你的 `xinetd` 守护进程配置为 `telnet` 连接使用 TCP wrappers，可以在 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中添加哪些行以允许主机 `arfa` 在连接你的服务器时使用 `telnet` 工具？（选择两个答案）

a) `/etc/hosts.allow:in.telnetd: arfa`

b) `/etc/hosts.allow:in.telnetd: ALL`

c) `/etc/hosts.deny:in.telnetd: arfa`

d) `/etc/hosts.deny:in.telnetd: ALL`

23. `/etc/squid.conf` 文件中使用哪些标签来控制对 Web内容的访问？（选择两个答案）

a) `access_list`

b) `ad`

c) `http_access`

d) `allow_list`

### 探索练习

## 测试 Apache 文件系统限制
