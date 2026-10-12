
这与你给 `route` 的网络地址以及你给 `config` 的子网掩码是相同的。你机器 `config` 上的设备 `eth0` 应该是：

```
| eth0 Link encap:10Mbps Ethernet Haddr 00:60:9C:D5:56 |
| inet addr:129.240.223.254 Bcast:129.240.223.255 Mask:255.255.255.0 |
| UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1 |
| RX packets:36031S errors:0 dropped:0 overflows:0 |
| TX packets:179274 errors:0 dropped:0 overflows:0 |
| Interrupt:10 Base address:0x320 |
```

并且 `netstat -rn` 应该显示

## 7 挂载检查清单

```
| Kernel routing table | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Destination | Genmask | Flags Metric Ref Use Iface | | |
| 129.240.223.0 | 255.255.255.0 | U 0 0 174412 eth0 | | |
```

（第一列为网络地址）。

`hosts.deny` 和 `allow` 文件

**重要：在这些文件的 `portmap` 行中，不要放入 IP 数字以外的任何内容**。主机名查找会间接导致 `portmap` 活动，从而触发主机名查找，继而再次间接导致 `portmap` 活动，从而触发……

上述措施应该让你的服务器更严密。剩下的唯一问题（呵呵，真的！）是有人在受信任的机器上破解了 `root`（或启动的 `MS-DOS`），并利用该权限从安全端口以他们想成为的任何身份发送请求。

## 6.4 NFS 与防火墙

在你的路由器或防火墙中释放 `nfs` 和 `portmap` 端口是一个非常主意意。`nfsd` 运行在端口 `2049`，同时支持 `udp` 和 `tcp` 协议。`portmap` 端口 `111`（`tcp` 和 `udp`），`mounted` 位于端口 `745` 和 `747`（`tcp` 和 `udp`）。你应该使用 `rpcinfo -p` 命令检查这些端口。

另一方面，如果你想让 NFS 通过防火墙，较新版本的 `NFSD` 和 `mountds` 有选项可以使它们使用特定的（非标准）端口，该端口可以在防火墙中开放。

## 6.5 总结

如果你在 `portmap/nfs` 软件中使用 `hosts.allow/deny`、`root_squash`、`nosuid` 和特权端口功能，可以避免许多目前已知的 NFS Bug，并几乎可以感到安全。尽管如此，归结底：当入侵者访问你的网络时，他/她可以在你的 `.forward` 或 `/home` 或 `/var/spool/mount` 中通过 NFS 挂载的 `map` 文件构造字符串命令。出于同样的原因，你应该在 NFS 上使用你的 PGP 私钥。至少你应该知道涉及的风险。现在你了解了一点。

NFS 和 `portmapper` 构成了一个复杂的系统，因此发现新的漏洞并非没有可能，即使在我们正在使用的基础设计或实现中也是如此。现在可能已经存在某些漏洞且有人正在滥用。为了跟上形势，你至少应该阅读 `comp.os.linux.announce <news:comp.os.announce>` 和 `comp.security.announce <news:comp.security.announce>`。

## 7 挂载检查清单

本节基于 IBM 公司。感谢他们为本 HOWTO 提供支持。每个项目都描述了一种故障模式和修复方法。

- 1. 文件系统未导出，或未导出到指定的客户端。修复：导出它。
- 2. 名称解析与 NFS 启动后挂载文件系统的导出不匹配（在那个服务器上）。修复：关闭 NFS 并让其重启。
- 3. 两台机器的时间偏差离谱（这让我很头疼）。修复：校正时间。HOWTO 建议使用 `NTP` 同步时钟。由于美国对 `NTP` 有导出限制，你必须从 `ftp://hacknic.nl/pub/replay/pub/nfs` 或镜像站点获取 `debian`、`redhat` 或 `slackware` 的 `NTP`。
- 4. 在 NFS 启动后，日期与导出不匹配。修复：校正时间。
- 5. 导出限制在 `NTP` 上。
- 6. 文件系统未导出，或未导出到指定的客户端。修复：导出它。
- 7. 名称解析与 NFS 启动后挂载文件系统的导出不匹配（在该服务器上）。

## 8 常见问题 (FAQs)

此章节由 `Alan Cox` 编写。

- 1. 当使用 Linux 作为 NFS 服务器时，挂载时会收到大量的“stale handle”（过期句柄）错误。这是旧版本 `nfs` 的 Bug。
- 2. 当我尝试挂载 Caldera 系统时，`nfs-beta16` 及更高版本修复了此。
- 3. 为什么我在向 NFS 服务器复制文件后仍然无法执行它？是因为 `nfs` 为了性能会缓存句柄（记住，它运行在用户空间）。`nfs` 会持有这些句柄好几天。
- 4. 我的 NFS 文件全是只读的。`nfs` 服务器默认是只读。
- 5. 在 `/etc/exports` 中修改，`nfsd` 会释放文件。
- 6. 从 Linux 挂载到超过 5 组的用户时。修复：减少用户组数量。
- 7. 导出限制在 `NTP` 上。
- 8. Linux 可以通过 `TCP` 运行 NFS 吗？目前不可以。
- 9. 当我重启机器时，有时会在卸载 NFS 服务器时挂起。在重启或关机时不要卸载它们，不会产生任何影响。命令是 `um -av nfs`。
- 10. Linux NFS 客户端向 `BSD` 系统写入时非常慢。NFS 服务器通常是同步的（如果你不在乎丢失数据，可以禁用此）。更糟糕的是衍生内核倾向于无法以小块工作。当你从 Linux 以 `1K` 包写入 `4K` 数据时，`BSD` 执行以下操作：

```
read 4K page
alter 1K
write 4K back to physical disk
```

## 9 导出文件系统

通过 NFS 导出文件系统在不同平台之间并不完全一致。在这种情况下，Linux 和 `Solaris 2` 是异类。本节粗略列出了大多数系统的操作方法。如果你使用的系统没有被涵盖，你必须检查相应的 `OS` `man-pages`。关键词是：`nfsd`、系统管理工具、`rc`脚本、启动脚本、启动序列、`/etc/exports`、`exportfs`。我将在本节中使用同一个示例：如何将 `/mn/eris/local` 导出到 `apollon/write`。

## 9.1 IRIX, HP-UX, Digital-UNIX, Ultrix, SunOS 4 (Solaris 1), AIX

这些操作系统使用传统的 格式。在 `/etc/exports` 中写入：

```
/mn/eris/local -ru=apollon
```

完整的文档在 `exports` 手书中。编辑文件后运行 `exportfs -av` 来导出文件系统。

或者使用类似于退化的写法，例如：

```
/mn/eris/local rw=apoll
```

我建议采用正式的写法。你可能会面临 `exportfs` 的下一个版本变得严格得多，从而导致所有功能突然停止工作。

## 9.2 Solaris 2

`Sun` 在开发 `Solaris 2` 时完全重新发明了轮子。因此，它与其他所有操作系统都完全不同。你需要编辑文件 `/etc/dfs/dfstab`。在其中，按照 `share(1M)` 手册页中的文档放置 `share` 命令。如下：

```
share -o rwapollon "Eris Local" /mn/eris/local
```
