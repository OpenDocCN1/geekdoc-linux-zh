
```sh
exit 0
:;
esac
echo "The root.hints file has been updated to contain the following information:"
echo
cat root.hints.new

own root.root root.hints.new
chmod 444 root.hints.new
rm -f root.hints.old
mv root.hints root.hints.old
mv root.hints.new root.hints
ndc restart
echo
echo "The nameserver has been restarted to ensure that:the update is complete."
echo "The previous root.hints file is now called /var/named/root.hints.old."
) 2>&+1 | /usr/lib/sendmail -t
exit 0
```

## 练习 9-1 DNS/Bind

参考之前显示的示例文件，建立你自己的 DNS 服务器。为名为 `rhce.test` 的域名服务。

- 1. 编辑 `/etc/named.conf` 文件以反映新信息。将区域文件命名为 `pz/rhce.test`，并将其设置为主域。
- 2. 编辑 `/var/named/pz/rhce.test` 文件，并在其中放置正确的区域信息。从添加包含序列号和过期信息的头开始。
- 3. 在区域文件中添加带有正确联系主管理员的 SOA RR。
- 4. 为该域名添加 NS 和 MX RR。使用 `192.168.**` 地址范围。
- 5. 添加几个带有 A、HINFO 和 TXT RR 的主机。使用 `www`、`ftp` 和 `mail` 作为其中几个。
- 6. 保存区域文件，然后使用 `ndc` 命令重启 Named。
- 7. 启动 `nslookup` 检查 `rhce.test`。

## 478 第 9 章：网络管理

## 认证目标 9.02 Squid 服务器

Squid 是一个高性能的缓存代理。它符合 Harvest 架构并使用 HTTP 请求。它可以被用作传统代理，也可以作为前端。Squid 在减少带宽（通过缓存命中）方面最有用。研究表明，Squid 在大型部署中可以减少 10%-20% 的带宽。

### 需要的软件包

以下软件包应该已经安装在你的服务器上。如果没有它们，Squid 将无法运行：

- `/etc/rc.init.d/squid` 脚本
- `/etc/squid/` 配置目录
- `/usr/doc/squid-version` 文档，主要是 HTML 格式
- `/usr/lib/squid` 支持文件和国际化消息
- `/usr/sbin/squid` 命令行诊断客户端
- `/usr/sbin/squid` 主程序
- `/var/log/squid` 日志目录
- `/var/spool/squid` 缓存目录（100 MB 或更多）

### 初始化

从 Red Hat 6.x 软件包首次启动时，`/etc/rc.init.d/squid` 会运行 `squid -z` 在 `/var/spool/squid` 创建缓存目录，然后开始启动 Squid。此时 Squid 将作为监听端口 3128 的代理运行。Web 客户端可以使用端口 3128 作为其显式代理。

### 在 Linux 服务器上启动和停止 Squid

在 Red Hat 6.x 系统上，通过 `/etc/rc.init.d/squid start` 和 `/etc/rc.init.d/squid stop` 启动和停止 Squid。启动可能需要一些时间，因为它首先要检查许多目录。

### 配置选项

高级配置功能通过 `/etc/squid/squid.conf` 文件调整。这允许调整许多调优和安全参数。关键配置部分包含 `cache_host` 行，指定了父级和兄弟缓存服务器，在获取新对象之前应该查询这些服务器。以下示例设置了一个父级和三个兄弟缓存：

* `squid.conf` - 在主机上：`childcache.example.com`
* 格式：`hostname type http_port`
* `cache_host parentcache.example.com parent 3128 3130`
* `cache_host childcache2.example.com sibling 3128`
* `cache_host childcache3.example.com sibling 3130`

Squid 首先检查自己的缓存，然后查询其兄弟节点和父级。如果缓存及其兄弟节点都没有该对象，其中一个父级是否会从源获取（如果没有响应请求的父级，则由它去获取）。

Squid 可以极大提高企业内网的性能。如果你的公司有许多员工上网，Squid 服务器将减少你 ISP 连接的带宽消耗。

## 认证目标 9.03

## NFS

NFS 是由 Sun Microsystems 在 20 世纪 80 代中期开发的文件共享协议。它基于 Sun 的 XDR（外部数据表示，一种与字节序无关的数据格式标准）和 RPC（远程过程调用）技术。Sun 提供了工作参考源码，这使得 NFS 迅速成为几乎所有 UNIX 版本以及 VMS 等其他多用户操作系统的首选文件共享协议。Linux 从很早开始就支持 NFS（同时作为客户端和服务器），且 NFS 在使用基于 UNIX 网络的组织中继续保持流行。

### NFS 的变体

与其他服务器协议一样，NFS 有若干种常见的变体，这些变体在不同情况下被证明非常有用。对最常见的变体有一般的了解将有助于根据具体情况进行配置，构建更稳定的系统。

### 通用 NFS 守护进程 (UNFSD)

NFS 服务器作为用户态进程运行，而不是内核态。这在灵活性方面提供了一些优势，但在性能和扩展性方面存在巨大的缺点。即使在服务器上，一个 UNFSD 也只能有效处理一到两个客户端；即使只有一个客户端，其吞吐量也是在同一服务器上使用内核态 NFS 守护进程时的几分之一。UNFSD 的瓶颈包括文件名查找、内核与用户地址空间之间的额外拷贝，以及单线程 NFS 守护进程。

UNFSD（相对于内核态 NFS 守护进程）的“灵活性”优势之一是它可以导出位于同一个文件系统中的任意数量挂载点，这些点是彼此的子集或超集。然而，这是一个次要的问题，在商业 UNIX（第 9 章：网络管理）上学习 NFS 的管理员通常会觉得 UNFSD 有点陌生。此外，UNFSD 中的守护进程变体仅在启动时读取配置文件；要更改导出的文件系统列表，必须停止并重新整个 NFS 服务（可能会干扰客户端）。

所有主要的 Linux 发行版在 1998 年之前都分发 UNFSD。随着 2.2 内核系列的出现，UNFSD 正在被快速淘汰，并且不再像 KNFS 那样活跃地维护。

### 内核态 NFS 守护进程 (KNFS)

内核态 NFS 服务器与大多数商业 UNIX 实现一样，运行内核进程来处理来自客户端的 NFS 请求。这意味着 NFS 进程使用内核数据结构（dentry、inode 和设备），而不是其用户态等价物（文件名、文件描述符）。这消除了 UNFSD 中存在的严重瓶颈，使得廉价服务器能够实现 1000// 的吞吐量，并为数十个同时活跃的客户端提供服务（受磁盘和网络 IO、CPU 使用率或协议瓶颈限制）。

Linux KNFS 实现起始于对 2.0.x 内核的补丁，并在 2.1 开发系列中大量开发。从 2.2 内核开始，它成为标准的内核功能，并迅速成为大多数 Linux 发行版的默认 NFS 实现。

### FS 版本 3 (NFS v3)

NFS 协议第 2 版本自 20 世纪 80 代末以来一直在使用。到 90 年代初，更高带宽的网络和对更好性能的需求促使 Sun Microsystems 修改了该协议。NFSv3 的关键特性包括支持客户端数据缓存、使用更大的块大小进行更高效的传输、具有多个待处理写请求的能力，以及通过 TCP 而非 UDP 运行的能力。NFS v3 极大提高了大型忙碌网络上的写入性能和扩展性，并对低流量网络上的读取性能进行了大部分改进。

FS v3 要求对客户端和服务器实现都进行更改。某些 NFS v3 特性在 Linux 2.2 内核中实现（包括客户端和 KNFSD），但重要的例外是 KNFSD 尚未支持 TCP。服务器和客户端会自动协商使用 v3 还是 v2，以及使用 TCP 还是 UDP，因此新旧实现之间的兼容性很少成为问题。

### PC-NFS
