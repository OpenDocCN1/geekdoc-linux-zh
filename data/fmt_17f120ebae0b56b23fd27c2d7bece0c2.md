
浏览列表是可用计算机的列表。要获取更多详细信息，请将调试级别增加到 2 或 3（如前文所述）并重启 Samba。如果浏览无法工作，请检查 `nmbd` 日志。

这里是一些全局选项：

- `os level`（操作系统级别）——设置一个值来控制你的 Samba 服务器是否为主节点。如果值为 0，可能会选中 Windows 机器。值 60 可能会确保服务器被选中。默认值为 20。

- `preferred master`（首选主）——如果你想强制选择主节点，请将此项设置为 Yes。通过设置此项，你的 Samba 服务器也有机会被选中。默认设置为 Auto，这会导致 Samba 尝试检测当前的主节点。

- `local master`（本地主）——如果你希望 Samba 服务器成为本地主节点，请将此项设置为 Yes。（这不是保证，但提供了机会）。如果你不希望选择 Samba 服务器作为本地主，请将值设置为 No。Local Master 默认为 Auto。

- `domain master`（域主）——如果你希望 Samba 服务器（`nmbd` 守护进程）自标识为工作组的域浏览器，请将此项设置为 Yes。这将允许分配到工作组的客户端计算机使用来自子网外的 SMB 共享文件和打印机。默认设置为 No。

### WINS 选项

如果你希望由特定的 WINS 服务器为 SMB 客户端使用的 NetBIOS 名称提供地址转换，请使用 WINS 选项。如所述，如果你的工作组所有客户端和服务器都在同一个子网内，你可能不需要使用 WINS 服务器。这是因为 NetBIOS 名称可以通过广播地址获取。可以由你的 Samba 服务器提供 WINS 服务。

- `wins server`（WINS 服务器）——如果你的网络上有一个你想用于工作组 NetBIOS 名称的 WINS 服务器，你可以在此处输入该服务器的 IP 地址。再次，如果你的工作组扩展到本地子网之外，你可能需要使用 WINS 服务器。

- `wins support`（WINS 支持）——如果你希望你的 Samba 服务器充当 WINS 服务器，请将此项设置为 Yes。（默认为 No）。再次，如果工作组中的所有计算机都在同一个子网内，则不需要此项。网络上只有一台计算机应该被分配为 WINS 服务器。

除了此处描述的值外，你还可以点击“Advanced View”（高级视图）按钮访问更多选项。当你填写完所有需要的字段后，点击屏幕上的“Commit Changes”（提交更改），将更改更改写入 `/etc/samba/smb.conf` 文件。

# 使用 SWAT 配置共享目录

要让你的共享目录其他人可用，你可以在 SWAT 窗口中添加条目。使用 SWAT 设置 Samba 共享目录，请执行以下操作：

> 注意：在此过程中，你可能会看到一个或多个安全警告。这些消息提示你有人可能会查看你发送到 SWAT 的数据。如果你在本地主机或私有局域网上工作，风险是很小的。

1. 从 SWAT 主窗口，点击 SHARES（共享）按钮。

2. 在 Create Share（创建共享）框中输入你想共享的目录名称，然后点击 Create Share（创建共享）。

3. 添加任意选项：

- `comment` — 描述共享目录的几个字（可选）。

- `path` — 你正在共享的目录路径。

- `guest account` — 如果选择了 Guest OK（允许访客），则在此定义的用户名将分配给访问文件系统的用户。访问共享不需要密码。`nobody` 用户账户（仅供远程访问你计算机的用户使用）是默认用户名。（FTP 用户也是一个推荐值。）

- `read only` — 如果选择 Yes（是），则只能从此文件系统读取文件，远程用户无法在文件系统上保存或修改文件。如果你想允许用户通过网络向此目录保存文件，请选择 No（否）。

- `guest ok` — 选择 Yes 任何人访问此目录而无需密码。

- `hosts allows` — 添加允许访问此文件系统的计算机名称。你可以通过名称、逗号、空格或制表符分隔不同的主机。以下是输入主机名的有效方式：

  - `localhost` — 允许访问本地主机。

  - `192.168.74.18` — IP 地址。输入单个 IP 地址。

  - `192.168.74.` — 输入网络地址以包含网络上的所有主机。（务必在网络数字末尾加上点，否则它将不起作用！）

  - `maple, pine` — 通过名称启用对单个主机的访问。

  - `EXCEPT host` — 如果你允许一组主机（例如通过输入网络地址），使用 EXCEPT 特别拒绝该组中某一个主机的访问。

- `hosts deny` — 通过在此处放置名称来拒绝访问特定计算机。默认情况下，不排除任何特定计算机。使用与 Hosts Allow 相同的格式输入主机名。

- `browseable` — 表示你可以在共享目录列表中查看此目录。默认开启 (Yes)。

- `available` — 允许你保持此条目完整，但关闭服务。如果你想临时关闭对目录的访问，这很有。默认开启 (Yes)。选择 No 将其关闭。

4. 选择 Commit Changes（提交更改）。

此时，共享文件系统应该可以供访问你的 Linux Samba 服务器的 Samba 客户端（Windows 9x, Windows NT, Windows 2000, OS/2, Linux 等）。在尝试之前，你可以检查关于你的 Samba 配置的几点。

# 使用 SWAT 检查你的 Samba 设置

从 SWAT 窗口，选择 STATUS（状态）按钮。

从此窗口，你可以重启 `smbd` 和 `nmbd` 进程。同样，你还可以看到活动连接、活动共享和打开文件的列表。（启动 `smbd` 和 `nmbd` 守护进程的首选方法是将 `smbd` 服务设置为自动启动。输入 `chkconfig smb on` 设置服务在启动时启动。）

# 使用 Samba 文件和命令操作

尽管你可以通过 Samba 服务器配置窗口或 SWAT 设置 Samba，但许多管理员更倾向于直接编辑 `/etc/samba/smb.conf`。作为 root 用户，你可以查看此文件的内容并进行所需的更改。如果选择了用户安全（推荐），你也会对 `smembusers` 和 `smbpasswd` 文件（同样在 `/etc/samba` 目录下）感兴趣。这些文件以及 `testparm`、`smbstat` 等命令将在接下来的章节中描述。

## 编辑 smb.conf 文件

你使用 Samba 服务器配置窗口或 SWAT 界面所更改将反映在你的 `/etc/samba/smb.conf` 文件中。这是一个 `smb.conf` 文件的示例（已删除注释）：

```
[global]
workgroup = ESTREET
server string = Samba Server on Maple
hosts allow = 192.168.0.
printcap name = /etc/printcap
load printers = yes
```

```
printing = cups
log file = /var/log/samba/%m.log
max log size = 0
smb password file = /etc/samba/smbpasswd
security = user
encrypt passwords = Yes
unix password sync = /usr/bin/passwd
passwd swd chat = *Newpassword* %n\n*Retype*newpassword* %n\nnpasswd:
*all*authentication*tokens*updated*successfully*
pam password change = yes
obey pam restrictions = yes
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
username map = /etc/samba/smbpasswd
dns proxy = no

[homes]
comment = Home Directories
browseable = no
writable = no
valid users = %S
create mode = 0664
directory mode = 0775

[printers]
comment = All Printers
browseable = no
writable = no
valid users = %S
```

在 `[global]` 部分中，`workgroup` 设置为 STREET，`server string` 为 Samba Server on Maple，`hosts allow` 为 `192.168.0.*` 允许访问局域网。`printing` 服务为 `cups`，`log file` 为 `/var/log/samba/%m.log`，`max log size` 为 0，`smb password file` 为 `/etc/samba/smbpasswd`，`security` 为 `user`，`encrypt passwords` 为 Yes，`unix password sync` 为 `/usr/bin/passwd`。`socket options` 为 `TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192`，`username map` 为 `/etc/samba/smbpasswd`，`dns proxy` 为 no 防止在 DNS 中查找。

`[homes]` 部分允许每个用户从 Windows 系统访问其家目录。用户将能够向家目录写入。但是，其他用户将无法查看或共享此目录。`[printers]` 部分允许所有用户打印到 Linux 上配置的任何打印机。

# 添加 Samba 用户

执行用户级 安全，为使用 Linux 系统和打印机的每个人分配用户账户（你也可以将其分配给访客账户，但在示例中，所有用户都有账户）。然后你需要为每个用户添加 SMB 密码。例如，以下是添加 Windows 98 工作站登录名为 `chuckp` 的用户的方法：

1. 在终端作为 root 用户输入以下命令添加用户账户：

```
# useradd -m chuckp
```

2. 按照以下方式为新用户添加 Linux 密码：

```
# passwd chuckp
Changing password for user chuckp
New UNIX password: ********
Retype new UNIX password: ********
```

3. 重复前面的步骤，为局域网上所有想要访问 Linux 系统的 Windows 工作站添加用户账户。

4. 输入以下命令创建 Samba 密码文件（`smbpasswd`）：

```
# cat /etc/passwd | /usr/bin/mkmspasswd.sh > /etc/samba/smbpasswd
```

5. 按照以下方式为用户添加 SMB 密码：

```
# smbpasswd chuckp
New SMB password: ********
Retype new SMB password: ********
```

为每个用户重复此步骤。以后，每个用户可以登录 Linux 并重新运行 `passwd` 和 `smpasswd` 命令来设置私有密码。

## 启动 Samba 服务

要启动 Samba SMB 和 NMB 守护进程，你可以以 root 用户身份输入以下命令运行 `/etc/init.d/smb` 启动脚本：

```bash
# service smb start
```

这会在当前会话中运行 Samba 服务。要设置 Samba 在你的 Linux 系统启动时自动启动，请输入以下命令：

```bash
# config smb on
```

这将开启 Samba 服务在运行级别 3、4 或 5 时自动启动。现在，你可以检查网络上的 SMB 客户端，查看它们是否可以访问你的 Samba 服务器。

## 测试 Samba 权限

你可以从 shell 运行多个命令来操作 Samba。其中之一是 `testparm` 命令，你可以用它来检查已设置的访问权限。它会列出已设置的全局参数以及任何共享目录或打印机。

## 检查共享目录状态

`smbstatus` 命令可以查看谁正在使用你的 Linux 系统提供的 Samba 共享资源。以下是 `smbstatus` 的输出示例：

Samba version 3.0.3-4 Machine

| PID | Username | Group | Machine | Connected at |

| :--- | :--- | :--- | :--- | :--- |

| IPC$ | 10865 | shuttle | RDWR NONE | Thu May 13 15:12:12 2004 |

| tmp | 10866 | shuttle | RDWR NONE | Thu May 13 15:12:14 2004 |

| tmp | 10874 | 10.0.0.218 | | Thu May 13 15:18:01 2004 |

锁定的文件：

| Pid | DenyMode | Access R/W | Oplock | Name |

| :--- | :--- | :--- | :--- | :--- |

| 10874 | DENY | FCB 0X3 | RDWR NONE | /tmp/.m.swap Thu May 13 15:18:20 2004 |

| 10874 | DENY | NONE 0x1 | RDWR NONE | /tmp/m Thu May 13 15:18:30 2004 |

此输出显示，从你的 Linux 服务器来看，samba 服务（`/tmp` 目录的共享）目前正被名为 `shuttle` 的计算机打开。PID 10874 是 Linux 服务器上处理该服务的 `smbd` 守护进程的进程号。打开的文件是 `/tmp/m` 和 `/tmp/.m.swap`，它们恰好是由 `vi` 命令打开的。均具有读/写权限。

## 第 18 章：设置文件服务器

## 设置 Samba 客户端

一旦你配置了 Samba 服务器，就可以尝试从网络上的客户端计算机使用共享目录。以下章节描述了如何从任何 Linux 系统或各种 Windows 系统使用你的 Samba 服务器。

## 从 Linux 使用 Samba 共享目录

从 Samba 客户端连接到共享目录有多种方法。以下章节介绍了这些方法。

### 通过 Nautilus 使用 Samba

要从 Nautilus 连接到 Samba 共享，请点击“文件（File）-> 打开位置（Open Location)”使用“打开位置”框。然后在你的 Nautilus 文件管理器的“打开位置”框中输入 `smb:`。

窗口中会出现你网络上的 SMB 组列表。你可以选择一个工作组，选择一个服务器，然后选择一个要使用的资源。这对于不需要密码的共享应该是有效的。

当你需要输入密码时，Nautilus 界面似乎存在 Bug。此外，它还要求你发送明文密码或在位置框中输入用户和密码。例如，要通过 Nautilus 访问我的主目录（`/home/chris`），我可以按如下格式输入我的用户名、密码、服务器名和共享名：

```
smb://chris:my72mgb@chris
```

### 在 Linux 中挂载 Samba 目录

Linux 可以像查看其他介质（硬盘、NFS 共享、光驱等）一样查看你的 Samba 目录。使用 `mount` 命令，你可以挂载 Samba 共享文件系统，将其永久连接到你的 Linux 文件系统中。

`mount` 命令的示例显示了如何如何从名为 `toys` 的计算机上挂载我的主目录（`/home/chris`）到本地目录（`/mnt/toys`）。作为 root 用户，在终端中执行：

```bash
# mkdir /mnt/toys
# mount -t smbfs -o username=chris,password=a72mg //toys/chris /mnt/toys
```

Samba 共享的文件系统类型为 `smbfs`，我通过选项 (`-o`) 传递了用户名 (`chris`) 和密码 (`a72mg`)。在 `toys` 上的主目录共享是 `//toys/chris`。本地挂载点是 `/mnt/toys`。此时，你可以像访问本地文件或目录一样访问 `/home/chris` 的内容。你对访问和更改该目录（及子目录）内容的权限，将与你作为用户 `chris` 直接从 `toys` 使用这些内容时的权限完全相同。

要永久挂载 Samba 共享目录，你可以向 `/etc/fstab` 文件添加一个条目。对于上述示例，你可以以 root 用户身份添加以下行：

//toys/chris /mnt/toys smbfs username=chris,password=a72mg

## 从 Windows 使用 Samba 共享目录

若要在网络上将 Linux 系统的 Samba 文件系统共享给 Windows 客户端用户，需要对这些客户端进行一些配置。在 Windows 95/98 及类似系统中，大部分配置是在“网络”窗口中完成的。在 Windows 95/98 中执行以下操作打开“网络”窗口：

- 1. 选择“开始（Start）-> 设置（Settings）”。

- 2. 双击“网络（Network）”。

网络窗口显示谁正在使用你的 Linux 系统提供的 Samba 共享资源。以下是 `smbstatus` 的输出示例：

网络窗口显示 Windows 在网络上找到计算机。如果你的服务器出现在屏幕上（在我的中中服务器名为 `pine`），双击它。否则，你可能需要双击“整个网络（Entire Network）”，然后打开服务器所在的工作组来找到你的服务器。服务器应该显示两种资源：

- **打印机** —— 名称和打印机图标代表从服务器共享的打印机。要访问它，双击即可。Windows 将为你的电脑设置打印机。之后，你可以像使用本地打印机一样使用它。

- **目录** —— 名称和文件夹图标代表从服务器共享的目录。打开文件夹查看该目录下的文件和文件夹。
