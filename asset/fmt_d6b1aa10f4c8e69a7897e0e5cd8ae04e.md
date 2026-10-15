
`smbtar` 程序是一个基于 `smclient` 之上的小型 shell 脚本，可以直接将 SMB 共享转储到磁带。

以下是可用选项：

- `-s server`：指定的 SMB 共享。
- `-p password`：密码。
- `-x service`：指定的服务。
- `-X`：排除。
- `-d directory`：目录。
- `-u user`：用户。
- `-t tape`：磁带。
- `-b blocksize`：块大小。
- `-N filename`：文件名。
- `-i`：交互。
- `-r`：恢复。
- `-l log level`：日志级别。
- `-v`：详细输出。
- `filenames`：文件名。

# smclient

`smclient` 程序的语法所示：

```
smclient -s server [-p password] [-x service] [-X] [-d directory] [-u user]
-t tape [-b blocksize] [-N filename] [-i] [-r] [-l log level] [-v]
filenames
```

以下是选项：

- `-s server`：指定的 SMB 共享。
- `-p password`：用于访问共享的密码。
- `-x service`：指定的服务。
- `-X`：排除。
- `-d directory`：目录。
- `-u user`：用户。
- `-t tape`：磁带。
- `-b blocksize`：块大小。
- `-N filename`：文件名。
- `-i`：交互。
- `-r`：恢复。
- `-l log level`：日志级别。
- `-v`：详细输出。

# 第10章 高级主题与管理问题

## smbtar 示例

- 为 `users/docs` 下的文件创建一个 tar 文件：
  `smbclient // telpc/someshare "" -N -Tc backup.tar users/docs`

- 创建与前一个项目相同的 tar 文件，但现在使用 DOS 路径：
  `smbclient // telpc/someshare "" -N -tc backup.tar users\edocs`

- 创建共享目录中所有文件和目录的 tar 文件：
  `smbclient // telpc/someshare "" -N -Tc backup.tar *`

## 使用 Samba 备份 Oracle 数据库

在带有可用 Samba 服务器的 NT 服务器上运行 Oracle 数据库时，可以使用 Samba 服务器来协助保护数据库。此过程也可以通过额外的程序或存档以类似的方式用于任何数据库或软件。通过结合 `smbclient`、`smbtar` 以及一个将驱动器映射到 Samba 宿机的 NT 服务器，可以将导出文件和日志从 NT 服务器移动到 Linux 服务器（该服务器可以专门用于此任务）。这听起来可能有些笨，但 Unix 相比非 Unix 系统有一个巨大的优势：非 Unix 系统通常无法将物理设备磁带驱动器。这意味着导出文件和日志可以直接写入磁带，而无需占用磁盘空间。对于每天24小时、每年365天运行的数据库，这对于存档日志非常有用。

## 将 Samba 作为打印机服务器

Samba 作为打印机服务器的配置在第5章已介绍；然而，这里将讨论一些未包含的高级主题。

### 打印机驱动程序

Windows 95 和 98 能够在不先安装打印机驱动程序的情况下使用打印机。当使用此类打印机时，Windows 会自动安装所需的打印机驱动程序文件。

表10.3 显示了影响打印机操作的 `smb.conf` 参数。

### 表10.3 与打印共享相关的 smb.conf 参数

| 参数 |  |
| --- | --- |
| load printers | 如果设置为 yes（默认值），则在 `/etc/printcap` 中定义的所有打印机都将被加载并供浏览。如果你不想让所有人使用你的打印机，请将此参数设置为 no。 |
| Ippause command | 这是许多参数之一，通过写入适当的命令行代码来在打印机上执行操作。它用于停止打印作业。 |
| Ipsum command | 此参数使用 Ippause 命令恢复已停止的打印作业。 |
| lpq command | 此参数为客户端读取打印机队列状态。对于 BSD，默认是 lpq。 |
| lprm command | 此参数从队列中删除打印作业。 |
| min print space | 该参数以千字节为单位，设置了在从客户端接受新打印作业之前，溢存文件位置必须可用的最小空间。当在繁忙的打印机上产生大型文档时，此参数非常有用。默认情况下，此参数通常设置为 0，意味着接受所有作业。 |
| postscript | 有时，不是 PostScript 的打印机可能会被打印作业开头处的 Ctrl+D 字符困扰。结果是打印的 PostScript 布局并不是 PostScript。默认情况下，此参数设置为 no，此时会在每个打印作业的开头添加一个 %，强制进行 PostScript 打印。众这会导致真实的 PostScript 打印机混乱。 |
| printer | 此参数设置要使用的打印机样式。如果 `/etc/printcap` 文件没有你定义的打印共享的条目，此参数将告诉 Samba 在溢存后发送打印作业。 |
| printable | 此参数定义什么是或可能不是打印共享，从而定义什么是或可能不是打印的。默认是 no |
| printcap name | 与 `[printers]` 部分结合使用，通知 Samba 打印机定义文件的位置。这是 `/etc/printcap` 的替代方案。 |
| printer | 此参数定义要打印溢存的打印机名称。 |
| printer driver | Windows 客户端需要知道打印机的驱动程序名称。 |
| printer driver file | 此参数定义打印机驱动程序文件的位置。 |
| printer driver location | 此参数定义打印机驱动程序文件。 |
| queuepause command | 此参数定义用于暂停打印队列的命令。 |
| queuesume command | 此参数定义恢复打印队列的命令 |

与其他章节一样，打印机参数可以使用宏。表10.4 显示了打印共享中使用的宏。

为 Windows 9x 客户端选择打印机驱动程序需要对第5章提供的打印共享 `smb.conf` 示例进行一些修改。要使用自动打印机驱动程序安装，需要创建一个额外的共享 `[printer$]`。此共享可以放在服务器的任何位置，并且用户应对其目录具有读取权限。打印机驱动程序文件将复制到此目录。列表10.6 显示了一个示例的 `[printer$]` 共享。

### 列表10.6 一个 `[printer$]` 共享

```
[printer$]
comment = printer drivers
path=/var/spool/lpd/printerdrives
browable = yes
public = yes
writable = no
```

系统中的打印机定义文件需要为你系统上的打印机创建 `printer driver file` 参数。打印机定义文件是根据 `printerprint.inf`、`msprint2.inf` 以及可能随打印机的任何不支持文件的副本创建的。

打印宏及其描述如下：

| 宏 | 描述 |
| --- | --- |
| `%p` | 替换为打印机名称 |
| `%j` | 替换为作业号 |
| `%s` | 替换为溢存文件的完整路径和文件名 |
| `%S` | 替换为溢存文件名 |

## 打印机计数

要启用打印机计数，首先编辑 `/etc/printcap` 条目以提供打印机计数。列表10.8 显示了对于 LPT1 端口带有 DeskJet 打印机的 Red Hat Linux 系统的 `/etc/printcap` 文件。

### 列表10.8 启用了计数的 /etc/printcap 文件

```
##PRINTTOOL03# LOCAL djet500 300x300 a () DeskJetMono 1 ()
hp deskjet:
```
