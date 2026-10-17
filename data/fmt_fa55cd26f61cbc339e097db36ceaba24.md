
以下是与 veto 文件相关的一些问题：

- 大小写敏感（该选项对大小写敏感）。
- 类型名称对象必须完整。`veto` 功能不支持星号 (`*`)、方括号 (`[]`) 和用于匹配多个文件名的通配符。
- 如果 Samba 尝试删除仅包含 veto 文件的目录，除非你在 `/etc/samba/smb.conf` 文件中设置 `delete veto files` 参数为 `yes`，否则删除将失败（默认值为 `no`）。

## 打印机共享

你可以使用 `netatalk` 设置打印机共享，以便 Mac 客户端可以使用标准的 AppleTalk 打印服务（称为 `Printer Access Protocol`，或 `PAP`）打印到你的 Linux 计算机。为此你必须：

- 配置本地 Linux 打印机（参见第 17 章）。
- 设置 `/etc/atalk/papd.conf` 文件指向该打印机。
- 重启 `atalk` 服务（更具体地说，是 `papd` 守护进程）。

当 Mac 客户端打印到以此配置的 Linux 打印机时，打印作业将交给标准的 `lpd` 守护进程，并放入队列文件中，与该打印机的 Linux 打印作业一起打印。注意：Mac 计算机可以直接连接到 Linux 打印服务 (`LPR`)，而不需要 `netatalk` 打印。旧的 `OS 9` 客户端可能需要看到你设置的 AppleTalk 打印机。

## 故障排除 netatalk

许多工具可以检查 `netatalk` 的状态。如果 `netatalk` 没有正常工作，你可以尝试以下步骤：

- 检查 `atalk` 服务是否正在运行。
- 检查日志文件（如 `/var/log/messages`）以查找错误信息。
- 检查网络连接和防火墙设置。

如果你遇到任何关于 `netatalk` 的问题，请查阅文档或访问社区论坛。

# 第 26 章：将 Fedora 与 Apple Mac 1007 集成

```
May 14 17:45:03 toys afpd[2074] : ASIP started on 10.0.0.100:548 (1)
(1.5.5)
May 14 17:45:03 toys afpd[2074] : uam: uams_clrtxt.so loaded
May 14 17:45:03 toys afpd[2074] : uam: uams_dhx.so loaded
May 14 17:45:03 toys afpd[2074] : uam: "DHCASTI28" available
May 14 17:45:03 toys afpd[2074] : uam: "Cleartext Password" available
```

在上一个例中，你可以成功使用启动脚本启动 `atalk`、`papd` 和 `afpd` 守护进程。`atalk` 守护进程会在第一个以太网接口 (`eth0`) 上查找 AppleTalk 信息。`papd` 守护进程已启动，但没有可以注册的打印机。`afpd` 守护进程在服务器上启动了一个 Apple 文件服务器 (`toys:AFPServer`)。随后它识别了可用的用户身份验证方法 (`uams`)（明文和加密密码均可用）。

## 从 Mac 访问 NFS 服务器

多年来，网络文件系统 (`NFS`) 是 Linux 和其他 Unix 类系统之间共享文件的首选方法。尽管 Mac OS X 支持通过“连接服务器”(`Connect to server`) 窗口进行 NFS 连接，但你需要在 Linux 服务器上进行一点技巧，才能接受来自 Mac OS 计算机的连接。

以下步骤描述了如何使用 Mac OS X 的“连接服务器”访问 Linux NFS 服务器上的文件和目录。然后，你可以使用 Linux NFS 服务器上的文件和目录（也称为文件夹），就像它们存在于你的 Mac OS X 计算机上一样。

正如我提到的，该过程依赖于能够对 Linux NFS 服务器提供共享目录的方式进行细小更改。如果你没有 Linux 服务器的访问权限，你需要请求 Linux 服务器管理员进行更改，或者手动将你的 Mac 连接到 Linux NFS 服务器。（我将在节末尾描述手动操作方法。）

## 从“连接服务器”窗口连接 NFS

要在 Linux 中创建共享目录并从 Mac 客户端连接到它，请执行以下操作：

1. 在 Linux 服务器上，使用第 18 章描述的 NFS 功能导出共享目录。为了让 Mac OS X 使用该共享目录，你必须确保添加 `insecure` 选项。例如，为了共享名为 `jukebox.linuxtoys.net` 的 Linux 服务器上的 `/var/music` 目录，你可以在该服务器的 `/exports` 文件中添加如下：
