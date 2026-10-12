
在 `/etc/exports` 中做出更改后，使用 `nfsserver reload` 命令让 NFS 服务器在不重启的情况下重新读取配置。

你可以指定 IP 地址或范围，或者域名系统（DNS）名称（只要可以被解析）作为导出的客户端或客户端。因此，可以是任何以下内容：

```
/test client(rw,sync)
/test 192.168.1.26(rw,sync)
/test 192.168.1.0/255.255.255.0(rw,sync)
/test 192.168.1.0/24(rw,sync)
```

所有行都设置了 `rw`（读写）选项。然而，如果你需要，`ro` 选项允许只读访问。

正如我们所提到的，`/etc/exports` 文件仅仅是这些所示的行的集合。字符是 `#`。因此，以下可能是一个简单的完整的 `/etc/exports`：

```
# exports(5) 手册页提供了对该文件语法的描述。
# 此文件包含了所有通过 NFS（网络文件系统）导出到
# 其他计算机的目录列表。
# 此文件由 nfsd 和 rpcmount 使用。有关如何使
# 此文件中的更改生效，请参阅它们的手册。
/data2/
/home/peter/rabbit*(rw,root_squash,sync)
/home/david/*rw,root_squash,sync)
/media/cdrom/* *(sync)
```

在这个示例中，注释是你在新安装的 `/etc/exports` 中看到的全部内容。`/data2` 目录以只读导出（如果未指定 `ro` 或 `rw`，则默认如此）到仅属于他的机器 `rabbit`。Peter 的主目录以读写方式导出，并带有 `root_squash` 选项，但如果他在 `rabbit` 上启动，他将对共享中的文件没有 root 权限。CD 驱动器导出到所有主机。

一旦你对 `/etc/exports` 文件进行了更改并运行了 `nfsserver reload` 命令，你定义的共享应该对客户端可用。例如，主机 `rabbit` 应该能够通过下面的命令在 `bible` 上挂载共享 `/home/peter`：

```
root@rabbit: # mount bible:/home/peter /mnt
```

## 设置 root、用户和组客户端权限

默认情况下，客户端上的 root 用户被映射为服务器上的匿名用户 `nobody`，这意味着客户端上的 root 用户对挂载共享上的文件没有完全 root 权限。通过指定 `root_squash` 可以使此默认选项显式化。此相反的是 `no_root_squash`，它允许客户端上的 root 用户在 NFS 共享上拥有完全 root 权限。

> 除非有特殊原因，否则文件系统应该使用 `root_squash` 选项导出。

`all_squash` 选项类似，但它将所有用户映射到用户 `nobody`。当共享挂载时，客户端上的普通用户将无法对其写入。

正如我们所提到的，`/etc/exports` 文件仅仅是这些所示的行的集合。字符是 `#`。因此，以下可能是一个简单的完整的 `/etc/exports`：（注意：OCR 文本似乎在此处跳转或源处的逻辑）

在使用 `all_squash` 时，你还可以指定用户 ID `UID` 和组 ID `GID`。

## 使用 YaST 创建 Exports

你可以使用 YaST 运行级别模块（YaST 系统运行级别编辑器）来实现，或者使用以下替代方案：

```
root@client: ~ # chconfig nfsserver
root@client: ~ # chconfig portmap on
```

> 注意：在早期的 SUSE 版本中，你还需要激活 `nfslock` 和 `nfsboot`。

## exports 文件

NFS 的目录共享由 `/etc/exports` 文件控制，该文件包含一个可以导出到其他选项的主机目录列表。一个简单的 `/etc/exports` 示例可能包含以下这一行：

```
/test client(rw)
```

这将 `/test` 目录导出到主机 `client`。设置了 `rw`（读写）选项。如果你重启 NFS 服务器，可能会看到如下内容：

> 正在关闭基于内核的 NFS 服务器

> 正在启动 NFS 服务器导出：`/etc/exports [8]`: 导出 */home/* 未指定 'sync' 或 'async' 选项。

> 假设默认行为 ('sync')。

> 注意：此默认设置与之前的版本有所不同

为了避免此消息，请在选项中添加 `sync` 或 `async`：

```
/test client(rw,sync)
```

默认选项 `sync` 表示 NFS 服务器等待本地磁盘写入完成，从而在服务器突然故障时尽化数据损坏的风险。

在最新版本中，你可能会看到类似的消息：

> 导出 */:/home*/ 未指定 'subtree_check' 或 'no_subtree_check'。

> 假设默认行为 ('no_subtree_check')。

`subtree_check` 选项确保请求的文件始终位于导出的子目录下。同样，信息提示行为已更改，你可能需要修复 `/etc/exports` 中的选项以避免此错误消息。

请注意，客户端名称与选项之间不能有空格。如果有空格，NFS 服务器将以不同的方式解释该行；在前面的示例中，它将把 `/test` 提供给带有默认选项的 `client` 机器，以及带有 `rw` 和 `sync` 选项的任何其他机器。这很遗憾，因为在创建该文件时很容易犯错。

（注：*Wait, I am still overthinking. I will provide the final output one last time.*）

```
100021 1 udp 32771 nlockmgr
100021 3 udp 32771 nlockmgr
100021 4 udp 32771 nlockmgr
100024 1 udp 32771 status
100021 1 tcp 32830 nlockmgr
100021 3 tcp 32830 nlockmgr
100024 4 tcp 32830 status
100024 1 udp 629 mountd
100005 1 tcp 633 mountd
100005 2 udp 629 mountd
100005 2 tcp 633 mountd
100005 3 udp 629 mountd
100005 3 tcp 633 mountd
```

如果你在这些列表中没有看到 nfs 的条目，说明出了问题；可能 NFS 服务器没有向 portmapper 注册。尝试停止 NFS 服务器、`portmap` 服务和网络，并按照相反的顺序启动它们。

# NFS 安全考虑

NFS 存在固有的安全问题。对于 SMB 共享，你绝对不应该将其放到私有网络之外。

`exports` 文件中允许的客户端 IP 或主机名列表无法防御那些能够修改机器 IP 地址的人（具有物理访问权限，意味着任何人）。前面提到的服务器和客户端之间 UID 不匹配的问题意味着用户可能在服务器的另一个用户文件上拥有错误的权限，但如果用户对客户端拥有 root 权限（具有物理访问权限，意味着任何人），他就可以变成你的用户。

当客户端完全符合 NFS 第 4 版时，NFS 安全将得到改进。未来

最近的密集使用使用了 `nfsidmap` 软件包，可以用于在运行 Kerberos 认证的环境中保护 NFS 连接。

最后，NFS 提供了一种非常简单且透明的跨网络共享文件系统的方法。它可能是任何网络基础设施的重要部分，其中包括作为客户端和服务器的 Linux 或 Unix 系统。本章中的信息将使你能够在客户端和服务器上进行 NFS 工作。

# 第 23 章

# 在 SUSE 上运行 FTP 服务器

FTP 是文件传输协议（File Transfer Protocol），广为人知的是允许从公共互联网服务器进行匿名下载的一种。

传统上，Unix 系统默认运行 FTP 守护进程，用户期望使用来自外部的 FTP 客户端在他们的主目录之间移动文件。这是一种无需登录即可访问系统的方便方法，并且可以从任何客户端使用。以这种方式使用 FTP 已经变得既不安全又没有必要。它不安全是因为通常用户名/密码对是以明文形式在网络上传输的，这开启了通过网络嗅探窃密码的可能性。仅仅 `telnet` 和 `rsh` 就应该被认为是不安全的，在公共网络上使用 FTP 通常应该被非常谨慎。

然而，这种类型的 FTP 通常是没有必要的，原因仅仅由于 `ssh` 系列程序（`ssh`, `scp`, `sftp`）的可用，`telnet` 和 `rsh` 变得不再需要，这些程序提供了实现相同目的的完全安全的方法。（良好的客户端实现，如 KDE 的 "fish" iosave，也意味着你可以在传输文件时，从客户端图形化地查看服务器上的目录。）

FTP 糟糕的安全声誉因以下事实而变得糟糕：某些 FTP 实现有时会受到严重漏洞的影响，包括通过缓冲区溢出等利用程序允许获得完全 root 权限的漏洞。

### 本章内容
