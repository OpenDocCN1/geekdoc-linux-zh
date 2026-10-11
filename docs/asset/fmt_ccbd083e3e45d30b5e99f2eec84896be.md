
该包的源代码包含在 `/Source/Samba` 目录。

## 39 从 Linux 访问 Windows NT 服务器

Samba 为你提供了一种强大的方法，可以将 Linux 作为文件和打印服务器，你所有的 Windows 客户端都可以访问它，但许多网络已经广泛地使用了 Windows NT 服务器。Samba 允许你作为客户端连接到这些 Windows NT 服务器和其他 Windows 系统。

### 214 仿造 WINDOWS NT

使用这些功能，你可以将 Windows NT 作为共享文件服务器，访问任何 Windows 客户端（你已获得访问权限）上的共享，打印（Windows 打印机等等）。这些功能也适用于任何运行 Samba 服务器的其他系统。例如，一个 Linux 系统可以作为另一个运行 Samba 服务器的 Linux 系统的客户端。

在设置 Samba 服务器时，访问 Windows NT 等其他 SMB 系统最可靠的方法是在命令行上进行，如下文节所示。随后显示了辅助该过程的图形化实用工具（见图 39.1）。

### 连接到 SMB 文件服务器

要连接到 SMB 服务器（包括运行在任何平台上的 Samba 服务器），请使用 `smbclient` 工具。该命令行具有一个结合了命令行 FTP 客户端命令和标准 Linux Shell 的接口。表 39.1 显示了几个最常用的命令。

#### 表 39.1 smbclient 实用程序的常用命令

| smbclient 命令 | 描述 |
|---|---|
| `help` | 打印所有 smbclient 命令列表。 |
| `ls` | 列出远程服务器当前目录下的文件。 |
| `get filename` | 从远程服务器下载文件，并将其复制到本地工作目录。 |
| `put filename` | 将文件上传到当前远程目录（这需要在远程服务器上写入文件的权限）。 |
| `!command` | 在保持 smbclient 界面的同时执行 Linux 命令（例如，使用 `ipwd` 查看你的 Linux 工作目录）。 |
| `exit` | 关闭 smbclient 实用工具。 |

### 从 LINUX 访问 WINDOWS NT 服务器 215

要使用 `smbclient` 命令，你需要知道想要连接的服务器名称以及在该服务器上有效的用户名。输入此命令：

```
$ smbclient -L servername -U username
```

已添加接口 `ip=192.168.100.3 bcast=192.168.100.255 nmask=255.255.255.0`

服务器时间为 `Tue Jul 6 12:44:34 1999`
时区为 `UTC-6.0`。
密码：

`Domain=[WELLS] OS=[Unix] Server=[Samba 1.9.18p8]`
`security=user`

`Server=[BRIGHTON] User=[nwells] Workgroup=[WELLS]`

| 名称 | 类型 | 注释 |
| --- | --- | --- |
| `homes` | Disk | 主目录 |
| `IPC$` | IPC | IPC 服务 (Toshiba-Caldera-Linux-Samba Server) |
| `jet-direct` | Printer | |
| `lp` | Printer | |
| `nwells` | Disk | 主目录 |
| `public` | Disk | 公共内容 |

此机器有一个浏览列表：

| 服务器 | 注释 |
| --- | --- |
| `BRIGHTON` | Toshiba-Caldera-Linux-Samba Server |

此机器有一个工作组列表：

| 工作组 | 注释 |
| --- | --- |
| `WELLS` | 主节点 |

当请求密码时（如列表中的第六行所示），请使用你在连接的 SMB (Windows) 系统上用户账户的密码。

![](img/ba933c244f3be8993f8191427d25c74c_230_0.png)

### 216 仿造 WINDOWS NT

如所示，该命令列出了你指定的服务器上的可用共享。这对于测试你是否能到达 SMB 服务器是一个很好的测试。你甚至可以省略 `-U` 参数来了解服务器的共享情况。如果你已经知道想要连接的共享名称，可以跳过上述步骤，并使用以下命令建立连接并开始作为文件服务器访问 SMB 系统。

```
$ smclient //sundance -u mwells

Added interface=192.168.100.3 bcast=192.168.100.255 mask=255.255.255.

Server time is Tue Jul 6 12:47:04 1999

Timezone is UTC-6.0

密码：

smb:
```

该格式是 SMB 标准，以两个斜杠开头，并用一个斜杠分隔服务器和共享。如果你看到提示符，说明你已成功连接到远程服务器。你可以尝试使用表 39.1 中列出的某些命令来下载和上传文件。

除了表 39.1 中的命令外，许多常用的 Linux 命令在 `smbclient` 中均有效。如果你有权限在远程服务器上创建和更新文件，可以使用其中任何一个命令，包括 `mkdir`、`rmdir`、`rm` 和 `del`。在许多情况下，一个功能会提供多个命令（例如 `ls` 和 `dir`）。`smbclient` 实用工具对于集成运行 Samba 服务器的 Linux 系统非常有用。例如，一个 Linux 系统可以作为运行 Samba 服务器的另一个 Linux 系统的客户端。

设置 Samba 服务器，访问 Windows NT 等其他 SMB 系统最可靠的方法是在命令行上进行。

![](img/ba933c244f3be8993f8191427d25c74c_230.png)

```
添加接口 ip=192.168.100.3 bcast=192.168.100.255 nmask=255.255.255.0

服务器时间为 Tue Jul 6 12:44:34 1999
时区为 UTC-6.0。
密码：

Domain=[WELLS] OS=[Unix] Server=[Samba 1.9.18p8]
security=user

Server=[BRIGHTON] User=[nwells] Workgroup=[WELLS]
```

| 名称 | 类型 | 注释 |
| --- | --- | --- |
| `homes` | Disk | 主目录 |
| `IPC$` | IPC | IPC 服务 (Toshiba-Caldera-Linux-Samba Server) |
| `jet-direct` | Printer | |
| `lp` | Printer | |
| `nwells` | Disk | 主目录 |
| `public` | Disk | 公共内容 |

此机器有一个浏览列表：

| 服务器 | 注释 |
| --- | --- |
| `BRIGHTON` | Toshiba-Caldera-Linux-Samba Server |

此机器有一个工作组列表：

| 工作组 | 注释 |
| --- | --- |
| `WELLS` | 主节点 |

当请求密码时（如列表中的第六行所示），请使用你在连接的 SMB (Windows) 系统上用户账户的密码。

![](img/ba933c244f3be8993f8191427d25c74c_230_0.png)

### 216 仿造 WINDOWS NT

如所示，该命令列出了你指定的服务器上的可用共享。这对于测试你是否能到达 SMB 服务器是一个很好的测试。你甚至可以省略 `-U` 参数来了解服务器的共享情况。如果你已经知道想要连接的共享名称，可以跳过上述步骤，并使用以下命令建立连接并开始作为文件服务器访问 SMB 系统。

```
$ smclient //sundance -u mwells

Added interface=192.168.100.3 bcast=192.168.100.255 mask=255.255.255.

Server time is Tue Jul 6 12:47:04 1999

Timezone is UTC-6.0

密码：

smb:
```
