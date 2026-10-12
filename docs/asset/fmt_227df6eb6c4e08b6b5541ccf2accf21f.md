
你是否曾不小心将 CUPS 假脱机目录设置为同一位置（`cupsd.conf` 中的 `RequestRoot` `/var/spool/samba/`，或者反过来：在 `printers` 部分中将 `/var/spool/cups/` 设置为 `path`）？这些必须不同。在 `cupsd.conf` 中将 `RequestRoot` 设置为 `/var/spool/cups/`，并在 `smb.conf` 的 `printers` 部分将 `path` 设置为 `/var/spool/samba`。否则，`cupsd` 会在每次重启时对其假脱机目录的权限进行清理，导致打印无法可靠工作。

## 21.19.19 名为 "lp" 的打印队列错误处理打印任务

在这种情况下，名为 "lp" 的打印队列会间歇性地吞掉任务，并吐出与发送的完全不同的任务。

将任何打印机命名为 "lp" 都是个坏主意。这是默认打印机的传统 UNIX 名称。CUPS 可能被配置为自动创建隐式类。这意味着，将具有相同名称的所有打印机分组到一个设备池中，并以轮询方式在这些设备之间均衡分配任务。其他人也有可能存在名为 "lp" 的打印机。你可能会收到此人的任务，并无意中将你的任务发送到他的设备。为了严格控制打印机名称，请设置 `BrowseShortNames No`。这将防止任何以 `printername@cupshot` 形式出现的打印机，从而让你更好地控制大型网络环境中可能发生的情况。

## 21.19.20 "cupaddsmmb" 的 Adobe PostScript 驱动程序文件位置

使用 `smbclient` 连接到任何具有共享 PostScript 打印机的 Windows 机器：`smbclient //windowsbox/print/$ -U guest`。你可以导航到 `W32X86/2` 子目录，`mget ADOBE\*` 及其他文件，或者导航到 `WIN40/0` 执行相同操作。另一个选项是从 Adobe 网站下载 `\*.exe` 打包文件。

## 21.20 CUPS 打印流程概览

CUPS 打印流程的完整概述见图 21.19。

### 图 21.18 带有 cupsomatic 的过滤链

![](img/86d74c6cc862465e3a42e6dc3c90935a_483_0.png)

请注意，`cupsomatic` 在 `application/vnd.cups-postscript` 阶段之后“劫持”打印文件，并将其重定向到 CUPS 外部的系统级 Ghostscript 安装，从而绕过“pstoraster”过滤器（因此也绕过了 CUPS 光栅驱动程序“rastertosomething”，并将光栅化文件直接交给 CUPS 后端……

`cupsomatic` 并非由 CUPS 开发人员制作。它是打印开发领域的一个独立贡献，由 Linuxprinting.org 的人员制作（另见 http://www.cups.org/cups-help.html）

### 图 21.19 CUPS 打印概览。

![](img/86d74c6cc862465e3a42e6dc3c90935a_484_0.png)

## 可堆叠 VFS 模块

### 22.1 特性和优势

可堆叠 VFS（虚拟文件系统）模块支持是 Samba-3 的新功能，并证明非常受欢迎。Samba 将通过加载的 VFS 模块将每个访问 UNIX 文件系统的请求传递下去。本章介绍随 Samba 源代码一起提供的模块，并提供了一些外部模块的参考。

### 22.2 讨论

如果未随你的平台分发二进制 Samba 软件包提供，你可能会在编译这些模块时遇到问题，因为共享库在不同系统上以不同的方式编译和链接。它们目前已在 GNU/Linux 和 IRIX 上进行了测试。

要使用 VFS 模块，请创建一个类似于下面的共享。重要的参数是 `vfs objects` 参数，你可以在其中按名称列出一个或多个 VFS 模块。例如，要记录所有文件访问并将删除的文件放入回收站，请参见示例 22.2.1：

#### 示例 22.2.1 带有 VFS 模块的 smb.conf

```
[audit]
    comment = Audited /data directory
    path = /data
    vfs objects = audit recycle
    writeable = yes
    browsable = yes
```

模块按照指定的顺序使用。假设你希望同时拥有病毒扫描器模块和回收站模块。明智的做法是将病毒扫描器模块放在第一位，使其最先运行，并在对该文件执行任何操作之前立即检测到病毒。`vfs objects = vscan-clamav recycle` Samba 将尝试从 Samba 安装根目录中的 /lib 目录加载模块（通常是 /usr/lib/samba/vfs 或 /usr/local/samba/lib/vfs）。

某些模块可以对同一共享使用两次。可以使用类似示例 22.2.2 中所示的配置来完成此操作。

#### 示例 22.2.2 带有多个 VFS 模块的 smb.conf

```
[test]
    comment = VFS TEST
    path = /data
    writeable = yes
    browseable = yes
    vfs objects = example:example1 example example:test
    example1: parameter = 1
    example: parameter = 5
    test: parameter = 7
```

### 22.3 包含的模块

#### 22.3.1 audit

一个简单的模块，用于将文件访问审计到 syslog 设施。记录以下操作：

- 共享

- 连接/断开

- 目录打开/创建/删除

- 文件打开/关闭/重命名/删除/权限更改

#### 22.3.2 extd_audit

此模块与上述 `audit` 模块相同，只是它将审计日志同时发送到 syslog 以及 `smbd` 日志文件。此模块的 `日志级别` 在 `smb.conf` 文件中设置。

表 22.1 中显示了有效设置以及将记录的信息。

##### 表 22.1 扩展审计日志信息

| 日志级别 | 日志详细信息 - 文件和目录操作 |

| :--- | :--- |

| 0 | 创建目录、删除目录、删除文件 |

| 1 | 打开目录、重命名文件、更改权限/ACL |

| 2 | 打开和关闭文件 |

| 10 | 最大调试级别 |

## 22.3.2.1 审计配置

大多数人尚未意识到，此审计工具比一般认知中更为灵活。存在多种方式可以记录有用的日志信息。

- Syslog 可用于记录所有事务。通过在 `smb.conf` 文件中设置 `syslog = 0` 可以禁用此功能。

- 仅通过在 `smb.conf` 文件中设置 `log_level = 0 vfs:x`（其中 x 为日志级别），即可为所有已加载的 VFS 模块记录到默认日志文件（`/logs.smbd`）。这将禁用通用日志记录，同时按指定日志级别激活所有 VFS 模块活动的日志记录。

- 可以按用户、按客户端机器等获取详细日志记录。这需要上述方法以及创造性地使用 `log_file` 设置。

    - 通过在 `log_file = /var/log/samba/%U:%m.log` 中设置，即可获取按用户和按机器详细日志记录的示例

审计信息通常需要长期保存。因此，为了防止日志文件被轮转，必须在 `smb.conf` 文件中设置 `max_log_size=0`。

## 22.3.3 fake_perms

此模块的创建是为了允许将漫游配置文件（Roaming Profile）的文件和目录（在 UNIX 下的 Samba 服务器上）设置为只读。如果在配置文件共享上安装了此模块，它会向客户端报告配置文件文件和目录是可写的。尽管当客户端注销或关机时这些文件永远不会被覆盖，但这样也能满足客户端的需求。

## 22.3.4 recycle

一个类似回收站的模块。在使用时，unlink 调用会被拦截，文件被移动到回收目录而不是被删除。这提供了与 Windows 计算机上回收站相同的效果。

`回收站` 不会出现在 Windows 资源管理器对网络文件系统（共享）或任何映射驱动器的视图中。相反，当第一个文件被删除时，会自动创建一个名为 `.recycle` 的目录。用户可以从 `.recycle` 目录中恢复文件。如果指定了 `recycle:keeptree`，则删除的文件将出现在与文件删除来源相同的路径中。

`recycle` 模块支持的选项如下：

- `recycle:repository` 应移动已删除文件的目录的相对路径。

- `recycle:keeptree` 指定是否保留目录结构，或者将正在删除的目录中的文件单独保留在回收站中。
