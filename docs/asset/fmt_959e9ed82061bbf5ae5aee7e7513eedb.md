
## 636 附录 A: 自测答案

- A. 你的服务器没有连接到网络。
B. 区域文件中的序列号没有增加。
C. 有人在你不知情的情况下更改了区域文件。
D. 另一端的用户遇到了 ISP 问题。

B. 务必确保在每次更改区域文件时，区域文件顶部的序列号都已增加。如果未更改，外部 DNS 服务器将认为你的域名没有任何变化，从而不会提取新的资源记录（RRs）。

- A. KNFSd
B. PCNFS
C. MacNFS
D. UNFSd

C. 并没有适用于 Mac 的 NFS 这种。

- 3. 哪一个是格式正确的 MX 记录示例？
A. MX10.mail.domain.com.
B. MX mail.domain.com.
C. MX10.mail.domain.com.
D. MX10.mail.domain.com.

D. 确保定义了优先值（preference），并且记录末尾包含了 ' . '。

- 6. 在 `/etc/exports` 文件中，如果想将 `/data` 导出为只读，但授予适当服务器写入权限，正确的行是：
A. /data (rw) superst.domain.com(ro)
B. /data (rw) superst.domain.com(rw)
C. /data (ro) .domain.com(rw)
D. /data (rw) superst.domain.com(rw)

- 7. 重启时，系统将检查哪个文件来挂载 NFS 共享？
A. `/etc/exports`
B. `/etc/nfs.conf`
C. `/etc/fstab`
D. `/nfs/conf`

C. `/etc/fstab` 包含了 NFS 挂载其文件共享的所有信息。

- 4. Squid 作为哪种互联网协议的缓存服务器？
A. FTP
B. News（新闻）
C. HTTP
D. DNS

A 和 C. HTTP 和 FTP 会话会被 squid 缓存。

- 8. `/var` 满了。什么操作可以恢复新闻的运行？
A. 删除 `/var/spool/news/articles/binaries`。
B. 删除 `/var/lib/news/history.pag`。
C. 过期旧的新闻文章。
D. 创建更多的索引节点（inodes）。

C. 以新用户身份运行 `/usr/bin/news.daily delayarm`。这应该由 `/etc/cron.daily/inn-cron-expire` 每日运行。

- 5. 哪一个不是 NFS 的变体？
C. DHCP 处于回环模式。
D. DHCP 已经弃用了多播数组。

B. 确保在 DHCP 启动之前已创建了 `dhcp.leases` 文件。

- 9. 弹出一个消息显示新闻空间不足，但 `df -k` 显示 `/var/` 剩余大量空间。哪里出了问题？
A. 文件系统的索引节点耗尽。

- 12. 你想配置一个新的 IPX 用户共享打印机。哪一行应该被插入到 `nswerv.conf` 文件中？
A. User Pass合物
B. 100 roger changem
C. roger changem合物
C. 文件系统上的不可见文件。

A. 没有更多节点了。使用 `-bytes-per-nodes` 选项运行 `mkfs` 或使用 `cybuffs`。通过 `df -i` 确认此诊断。

D3. '13' 指令后面应该是用户名和密码。

- 10. 没有新流量进来，但 `innd` 仍在运行。发生了什么？
A. 你的 ISP 断开了连接。
B. TCP/IP 链路已中断。
C. 互联网消失了，没有人在在发布。
D. `innd` 负载过度

D. 使用 `cltind` 确认这一点。原因随后可以追溯到错误日志。

- 13. 哪些是可以在 `ntp.conf` 文件中使用的关键字？
- A server
- B client
- C peer
- D child

A 和 C. `server` 表示较低层级（stratum）的服务器，`peer` 表示等层级。

- 14. NTP 中的偏移文件（driftfile）其作用是：
- A. 计算本地时钟相对于真实 UTC 的平均偏移。
- B. 用于与自身同步时钟随机常数。
- C. 地球旋转偏移的测量值。
- D. 确定系统时间的“零”点。

- 11. DHCP 已安装并正确配置。网络有响应。没有防火墙或多余的服务器进程。尽管如此，客户端仍无法获取网络信息。可能是什么情况？
A. 磁盘空间不足。
B. 未创建 `dhcp.leases` 文件。

A. NTP 需要大约一天时间来计算偏移文件的内容。这确保了守护进程因某些原因关闭后可以重启。

- 17. 你的公司刚刚遭遇了外部安全漏洞。结果是，安全部门收紧了所有服务器、路由器和防火墙的限制。到目前为止，所有用户数据已通过 NFS 移动，但发生了什么？
- A. 黑客删除了 NFS 数据，并且他们获取了备份并恢复。
- B. NFS 端口不再允许通过必要的防火墙。
- C. 两者无关，请检查你的磁盘空间。

## 638 附录 A: 自测答案

## 640 附录 A：自测答案

密集的操作会导致许多密码数据库不一致。C 是错误的，因为你至少需要一个 NIS 服务器。D 是错误的，因为这显然是一种运行网络的不安全方法。

password。

A、B 和 C 都是错误的，因为用户的账户是 NIS 账户；因此，唯一有效的选项是 D。

- 2. 你将如何设置工作站作为 NIS 客户端？
- 4. 下列哪些项不是良好的基本主机安全措施？
- A. 编辑 `/etc/passwd` 并在文件末尾添加 `USE_NIS`。
- A. 将 root 密码写在你的桌面上。
- B. 启动 ybind 守护进程。
- B. 定期检查系统日志以发现异常活动。
- C. 在 `/etc/inetd.conf` 中添加一行启动 ybind 的代码。
- C. 对未使用的账户进行挂起，以防原始用户想要重新激活它们。
