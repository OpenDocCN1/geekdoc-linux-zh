

共享的本地打印机定义取自 /etc/printcap 文件；打印机已加载（yes），并且使用 CUPS 打印服务（这是 Fedora 和 RHEL 使用的默认打印服务）。

为每个尝试使用该服务的主机创建独立的日志文件，位于 /var/log/samba/%m.log（其中 %m 会自动替换为每个主机名）。日志文件大小没有限制（0）。

在这种情况下，我们使用的是用户级别的安全性（security = user）。这允许用户登录一次后，即可轻松访问打印机以及 Linux 系统上该用户的家目录。密码加密已开启（encrypt passwords = yes），因为大多数 Windows 系统默认开启密码加密。密码存储在 Linux 系统的 /etc/samba/smbpasswd 文件中。

`dns proxy = no` 选项可以防止 Linux 在无法在已注册的 NetBIOS 名称中找到系统名称时，向 DNS 服务器查询系统名称（用于 TCP/IP 查询）。

`[homes]` 部分允许每个用户从局域网中的 Windows 系统访问其 Linux 家目录。用户可以写入家目录。然而，其他用户将无法看到或共享此目录。`[printers]` 部分允许所有用户向本地 Linux 系统上配置的任何打印机打印。

## 添加 Samba 用户

执行用户式的 Samba 安全性意味着为每个使用其 Windows 工作站访问 Linux 文件系统和打印机的人员分配一个 Linux 用户账户。（你可以将用户分配给来宾账户，但在本示例中，所有用户都有自己的账户。）然后你需要为每个用户添加 SMB 密码。例如，以下是如何添加一个 Windows 98 工作站登录名为 chuckp 的用户：

- 1. 在终端窗口中以 root 用户身份输入以下命令以添加 Linux 用户账户：
  ```
  # useradd -m chuckp
  ```

- 2. 按如下所示为新用户添加 Linux 密码：
  ```
  # passwd chuckp
  Changing password for user chuckp
  New UNIX password: ********
  Retype new UNIX password: ********
  ```

- 3. 重复上述步骤，为你的局域网中你希望访问你的 Linux 系统的所有 Windows 工作站的用户添加用户账户。

- 4. 输入以下命令创建 Samba 密码文件（smbpasswd）：
  ```
  # cat /etc/passwd | /usr/bin/mkasmdbpasswd.sh > /etc/samba/smbpasswd
  ```

- 5. 按如下所示为用户添加 SMB 密码：
  ```
  # smbpasswd chuckp
  New SMB password: ********
  Retype new SMB password: ********
  ```

（`smbpasswd -a user` 命令可以在你设置用户密码的同时创建 `smbpasswd` 文件。）对每个用户重复此步骤。稍后，每个用户可以登录 Linux 并重新运行 `passwd` 和 `smbpasswd` 命令以设置私密密码。

> 注意：在最新版本的 Samba 中，`smb.conf` 文件中提供了选项，可以自动同步 SMB 和 Linux 密码。请参阅本章 SWAT 部分中关于 `passwd` 程序、`passwd` chat 和 UNIX 密码同步选项的说明。

## 启动 Samba 服务

要启动 Samba SMB 和 NMB 守护进程，你可以作为 root 用户输入以下内容运行 `/etc/init.d/smb` 启动脚本：

```
# service smb start
```

这将在当前会话中运行 Samba 服务。若要设置 Samba 在你的 Linux 系统启动时自动启动，请输入以下内容：

```
# chkconfig smb on
```

这将开启 Samba 服务，使其在运行级别 3、4 或 5 下自动启动。现在你可以检查网络上的 SMB 客户端，查看它们是否可以访问你的 Samba 服务器。

## 测试你的 Samba 权限

你可以从 shell 中运行几个命令来操作 Samba。其中一个是 `testparm` 命令，你可以使用它来检查你设置的访问权限。它列出已设置的全局参数，以及任何共享目录或打印机。

## 检查共享目录的状态

`smbstatus` 命令可以查看谁正在使用你 Linux 系统提供的 Samba 共享资源。以下是 `smbstatus` 输出的示例：

```
# smbstatus

Samba version 3.0.26a-0.fc8
PID  Username   Group     Machine
----------------------------------------
25770 chris      chris     bookeer (10.0.0.50)
25833 chris      chris     10.0.0.50 (10.0.0.50)
```

| 服务 | pid   | 机器 | 连接时间 |
|:--------|:------|:----------|:----------------------|
| IPC$    | 25729 | booker    | 2008-04-22 周二 12:06:29 |
| mytmp   | 25770 | booker    | 2008-04-22 周二 12:46:03 |
| mytmp   | 25833 | 10.0.0.50 | 2008-04-22 周二 12:35:52 |
| IPC$    | 25730 | booker    | 2008-04-22 周二 12:06:29 |

Locked files:
Pid   Uid  DenyMode  Access      R/W  Oplock  SharePath                       Name                    Time
----- ---  --------  ----------  ---- ------  ------------------------------  ------------------------ ----------------
25833 501  DENY_NONE 0x120196    RDWR NONE   /home/chris/files/.b.txt.swp     2008-04-22 周二 12:26:18

该输出表明，从你的 Linux Samba 服务器来看，`my` 服务（即 /home/chris/files 目录的共享）目前由名为 booker 的计算机打开。PID 25833 是处理该服务的 Linux 服务器上 smbd 守护进程的进程号。打开的文件是 /home/chris/files/.b.txt.swp，碰巧是由 vi 命令打开的。它具有读写权限。

## 设置 Samba 客户端

配置好 Samba 服务器后，你可以尝试从网络中的客户端计算机使用共享目录。以下章节介绍了如何从另一个 Linux 系统或各种 Windows 系统使用你的 Samba 服务器。

## 从 Linux 使用 Samba 共享目录

有几种方法可以从你的 Samba 客户端连接到共享目录。以下章节讨论了这些方法。

### 从 Nautilus 使用 Samba

要从 Nautilus 连接到 Samba 共享，请使用打开位置框，方法是点击 文件 → 打开位置。然后在 Nautilus 文件管理器的打开位置框中输入 smb:。

窗口中会显示网络中可用的 SMB 工作组列表。你可以选择一个工作组，选择一个服务器，然后选择一个要使用的资源。对于不需要密码的共享，这应该可以正常工作。

Nautilus 接口要求你要么发送明文密码，要么在你的位置框中输入用户名和密码。例如，要通过 Nautilus 访问我的家目录（/home/chris），我可以输入我的用户名、密码、服务器名称和共享名称，如下所示：

```
smb://chris:my72mgb@toys/chris
```

除了将这些信息直接输入到位置框中，你还可以使用 Nautilus 的“连接到服务器”功能。选择 文件 → 连接到服务器。从出现的“连接到服务器”窗口中，将服务类型选择为 Windows 共享，并输入服务器名称以从该窗口查看所有可用的共享。可选地，你可以请求特定的共享、文件夹或用户名。然后你也可以选择一个特定的名称用于连接。你还可以省略密码部分（例如 smb://chris@toys/chris），系统会提示你输入密码。

### 在 Linux 中挂载 Samba 目录

Linux 可以像对待任何其他介质（硬盘、NFS 共享、CD-ROM 等）一样查看你的 Samba 共享目录。使用 mount 命令，你可以挂载 Samba 共享文件系统，使其永久连接到你的 Linux 文件系统。

以下 mount 命令示例展示了如何从名为 toys 的计算机将我的家目录（/home/chris）挂载到本地目录（/mnt/toys）。作为 root 用户，在终端窗口中输入：

```
# mkdir /mnt/toys
# mount -t cifs -o username=chris,password=a72mg //toys/chris /mnt/toys
```

Samba 共享的文件系统类型是 cifs（-t cifs）。我将用户名（chris）和密码（a72mg）作为选项（-o）传递。toys 上我的家目录的远程共享是 //toys/chris。本地挂载点是 /mnt/toys。此时，你可以像访问本地任何文件或目录一样访问 toys 上 /home/chris 的内容。你将拥有与作为用户 chris 直接从 toys 使用这些内容时相同的权限来访问和更改该目录（及其子目录）的内容。

若要永久挂载 Samba 共享目录，你可以在 /etc/fstab 文件中添加一个条目。对于刚才描述的示例，你可以添加以下行（作为 root 用户）：

```
//toys/chris   /mnt/toys   cifs   username=chris,password=a72mg
```

你可以添加一个凭据文件并使用它来包含你的用户名和密码，而不是在命令行中公开这些信息。这样，在你的系统上运行 ps 命令的人将无法看到这些信息。例如，你可以创建一个名为 /etc/samba/creds.smbpub 的文件，其中包含以下两行：

```
username=chris
password=a72mg
```

然后你可以将前面显示的 mount 命令更改为如下所示：

```
# mount -t cifs -o credentials=/etc/samba/creds.smbpub //toys/chris
```

### 从 Windows 使用 Samba 共享目录

在使用 Windows 系统时，若要查看你的 Linux Samba 服务器（以及网络上的其他计算机）提供的文件和打印服务，请打开“我的网络位置”窗口（Windows XP）或“网上邻居”（Windows 98 及更早版本的 Windows 系统）。在 Windows XP 中，选择 开始 → 我的网络位置以打开该窗口。

