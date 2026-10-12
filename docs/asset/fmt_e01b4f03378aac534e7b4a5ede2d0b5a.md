
让我们逐行分析：

- **第 1 行**：这是一行注释，由井希标记（`#`）标识，会被忽略。

- **第 2 行**：向两台计算机（`master`, `trusty`）授予了对 `/directory` 不同级别的访问权限：`master` 具有读写权限（`rw` 选项），`trusty` 启用了读写权限，并允许 root 用户对所有导出的文件和子目录具有完全访问权限（`/no_root_squash` 选项）。换句话说，`trusty` 上的 root 用户与本地系统的 root 权限相同。

- **第 3 行**：任何以 `proj` 开头且属于 `local.domain` 域的主机都获得 `/projects` 目录的读写权限。

- **第 4 行**：`local.domain` 域中的任何主机对 `/usr` 具有只读（`ro` 选项）权限。

- **第 5 行**：主机 `pc001` 被授予了 `/home/joe` 目录的读写权限。所有从 `pc001` 访问此挂载点的用户都被视为匿名用户（`all_squash` 选项），且匿名用户被认为用户 ID 为 150，组 ID 为 150（`anonid=150` 和 `anongid=150`）。

- **第 6 行**：`/pub` 对所有访问导出系统的主机可用。以只读方式授予访问，所有用户均视为匿名用户。`insecure` 选项允许不使用预留 TCP/IP 端口用于 NFS 的客户端访问挂载点。

- **第 7 行**：拒绝所有主机对 `/pub/private` 目录访问（`noaccess` 选项）。

`/etc/exports` 文件的其他选项可以在 `exports` 帮助页中找到，可以通过命令访问该帮助页：

```
$ man exports
```

一旦你在 `/etc/exports` 中指定了要导出的目录，你需要重启 `rpc.nfsd` 和 `rpc.mountd` 进程（它们通常在启动时运行）。首先，使用 `ps aux` 检查进程的 ID：

```
$ ps aux grep rpc.nfsd
root 1103 0.2 0.872 508 7 S 22:25 0:00 /usr/sbin/rpc.nfsd
$ ps aux grep rpc.mountd
root 1105 0.0 0.7 836 500 ? S 22:25 0:00 /usr/sbin/rpc.mountd
```

接下来，杀死并重启进程：

```
$ kill 1103 1105; /usr/sbin/rpc.nfsd; /usr/sbin/rpc.mountd
```

你自己运行上述的 `ps aux` 命令。你在上述输出中看到的数字可能与 1103 和 1105 不同，请相应替换。

你的新导出内容将对网络上的远程用户可用。

在 Linux 发行版中，为了重启 `rpc.nfsd` 和 `rpc.mountd`，你需要重启进程。

## 访问远程系统

当你共享目录时，不是与特定的用户共享，而是与特定的计算机共享。以下是来自 `/etc/exports` 主页的示例文件：

（根据上下文需要，此处重复内容，但遵循逻辑流）

如果你想在启动时手动创建自动挂载，请在系统上的 `/etc/fstab` 中添加一个类似的条目。

## 启动时挂载目录

如果有经常使用的远程目录，你可能希望它们自动挂载。为此，请使用 `linuxconf`。在 Config 标签下，选择 File Systems > NFS。此屏幕包含当前 NFS 挂载列表。点击 Add 按钮显示 Volume 屏幕。

### 图 28.13：卷规范

| NFS volume | Options | Misc. |
| :--- | :--- | :--- |
| Server | laptop1 | |
| Volume | home/mj | |
| Mount point | /test | |

## 基本网络安全

虽然连接网络并访问所有资源很棒，但这带来了安全风险。幸运的是，Linux 提供了一种基本机制，可以控制网络上的哪些机器实际上可以尝试连接你系统的服务。

基本安全机制由两个文件组成：`/etc/hosts.allow` 和 `/etc/hosts.deny`。这两个文件共同构成了一个三部分的基本安全链：

- 1. 允许 `hosts.allow` 中的任何守护进程-客户端组合访问。
- 2. 拒绝 `hosts.deny` 中的任何守护进程-客户端组合访问。
- 3. 授予其他所有人的访问。默认情况下，`hosts.allow` 或 `hosts.deny` 中没有条目，因此默认选项是 3：任何人都可以连接到系统。虽然你仍然设置 Telnet 和 FTP 等单独服务需要额外的身份验证，但这无法阻止那些连接尝试，而这些尝试可能是许多黑客在未知系统中“游荡”的开始。

为 `hosts.allow` 和 `hosts.deny` 创建条目非常直观：

守护进程列表：客户端列表

任何此类条目都指定了哪些网络守护进程（例如 `ftpd`、`in.telnet`、`in.rsh`）应该允许哪些主机（`hosts.allow`）或拒绝哪些主机（`hosts.deny`）连接。可以列出任何网络守护进程。例如，条目

```
ftp: host1
```

在 `hosts.allow` 文件中，允许来自指定主机 `host1` 的入站 FTP 连接。

一些特殊的关键字可以让操作变得简单，避免了逐个列出所有进程和客户端。`ALL` 关键字可以匹配任何客户端或任何进程。例如，以下条目：

```
ALL: ALL
```

在 `hosts.allow` 中允许任何客户端的任何类型访问，而 `hosts.deny` 中的相同条目则阻止所有访问。

`EXCEPT` 关键字允许在被 `ALL` 全面开放的网络中设置例外。例如，以下条目：

```
EXCEPT ftpd: ALL
```

在 `hosts.deny` 中拒绝所有访问除 FTP 服务以外任何服务的客户端。同样，

```
ALL: .local.domain EXCEPT foo.local.domain
```

在 `hosts.allow` 中允许访问本地 `.domain` 域内的所有机器（注意 `local.domain` 前面必要的 `.`），但 `foo.local.domain` 除外。

最后，`LOCAL` 关键字方便地为本地域内的所有机器提供访问：

```
ALL: LOCAL
```

在 `hosts.allow` 中允许来自本地域机器的任何类型访问。

`hosts.allow` 和 `hosts.deny` 文件包含一组非常丰富的条目，提供了比大多数用户需要的更精细的控制。这在 `hosts.allow` 的 man 页中有详细介绍。

```
$ man hosts.allow
```

#### 展望

在本章中，你学习了使用 TCP/IP 将 Linux PC 连接到以太网的基础知识。这使得 Linux 能够轻松地与网络上的其他 Unix 系统通信，包括其他 Linux 系统。

然而，将你的 Linux 系统与 Windows 和 Novell 网络完全集成还需要更多工作。在第 29 章“将 Red Hat Linux 7.1 集成到 Windows 和 Novell 网络”中，你将查看 Linux 系统与 Windows 和 Novell 集成的基础。

# 章节

## 二十九

# 将 Red Hat Linux 7.1 集成到 Windows 和 Novell 网络

- 与 Windows 网络共享 Linux 文件和打印机
- 从 Linux 系统访问 Windows 网络文件和打印机
- 将 Linux 连接到 Novell 网络

本章将探讨 Linux 的功能，这些功能使其成为许多现有内部网络中有吸引力的补充。

如果你的组织运行着标准的 Windows 网络，Linux 能够接入并充当有效、高效且强大的文件和打印服务器。由于其价格远低于 Windows NT/2000，且稳定性超过了 Windows 95/98/Me，Linux 可能是需要在网络 Windows 桌面之间之间共享文件的预算敏感型办公室的理想文件和打印服务器。

从另一个方向来看，Linux 也可以访问 Windows 服务器上的文件，就像它们是 Linux 系统上的本地硬盘一样。这服务于许多用途。例如，假设当 Web 开发人员在 Windows 系统上进行开发时，你运行了一个基于 Linux 的 Web 服务器。Linux 服务器将自动连接到 Windows 开发系统上的预指定目录，并将新文件复制到 Web 服务器上，从而避免手动更新 Web 服务器内容的需要。

接下来，本章将介绍将 Linux 系统集成到 Novell 网络。这些工具没有与 Windows 网络集成的工具那样成熟和健壮，但本章将讨论 Novell 的选项，并为你提供有关该主题的信息源。

# 与 Windows 网络共享 Linux 文件和打印机
