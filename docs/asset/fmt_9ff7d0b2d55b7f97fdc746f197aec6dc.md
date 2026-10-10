
默认情况下，Linux 密码与 Samba 密码不同。

默认情况下，不带密码登录的 Windows 用户将以 Samba/Linux 用户 `nobody`（匿名用户）的身份登录；你不需要将此用户添加为 Samba 用户。你需要为所有希望访问 Samba 服务器上的共享资源的其他用户添加用户名和密码。

当 `smb.conf` 配置文件（第 839 页）中的 `guest ok`（第 845 页）参数设置为 `YES`，且 `guest account`（第 842 页）设置为 `nobody`（默认值）时，Samba 会赋予以访客身份登录的 Windows 用户 Linux 用户 `nobody` 的权限。该用户无需提供密码。名为 `nobody` 的 Samba 用户不需要存在，但名为 `nobody` 的用户必须出现在 `/etc/passwd` 文件中。该用户被称为匿名用户。

### 用户映射

你可以创建一个称为用户映射（user map）的文件，将 Windows 用户名映射到 Linux 用户名。`smb.conf` 配置文件（第 839 页）中的 `username map`（第 843 页）参数指定了此文件的位置。默认的 Samba 配置未指定用户映射。关于 `username map` 参数的示例，请参阅第 838 页。

用户映射可以将 Windows 用户名映射到 Linux 用户名，和/或将多个 Windows 用户名映射到单个 Linux 用户名，以便于文件共享。用户映射文件中的每一行都以服务器（Linux）用户名开头，接着是一个空格、一个等号、另一个空格，以及一个或多个由空格分隔的客户端（Windows）用户名。客户端侧的星号（`*`）匹配任何客户端用户名。以下是一个示例文件：

```bash
$ cat /etc/samba/smbusers
# Unix_name = SMB_name1 SMB_name2 . . .
root = administrator admin
nobody = guest pcguest smbguest
```

第一个条目将两个 Windows 用户名（`administrator` 和 `admin`）映射到 Linux 用户名 `root`。第二个条目将三个 Windows 用户名映射到 Linux 用户名 `nobody`。

将以下行添加到 `username map` 参数所指的文件中（如有必要则创建该文件），以将 Windows 用户名 `sam` 映射到 Linux 用户名 `sls`：

```bash
sls = sam
```

在此文件中添加用户后，你必须使用 `smbpasswd`（见下文）为该用户设置密码。当 Sam 以 `sam` 登录时，Samba 将 `sam` 映射到 `sls`，并在 Samba 密码数据库中查找 `sls`。假设 Sam 提供了正确的密码，他将作为 `sls` 登录到 Samba 服务器。

## `smbpasswd` 和 `pdbedit`：管理 Samba 用户和密码

Samba 可以使用 Linux 密码或 Samba 密码对用户进行身份验证。`smb.conf`（第 839 页）配置文件中的 `passdb backend`（第 842 页）参数控制 Samba 使用哪种类型的密码。将 `passdb backend` 设置为 `tdbsam`（默认值）会使 Samba 使用 Samba 密码。Samba 将密码存储在 Trivial Database（tdb.sourceforge.net）中。将 `passdb backend` 设置为 `smbpasswd` 会使 Samba 使用存储在名为 `/etc/samba/smbpasswd` 文本文件中的 Linux 密码。本节讨论如何使用 `smbpasswd` 管理 Samba 密码，以及如何使用 `pdbedit` 显示 Samba 用户。

使用 `-L` 选项，`pdbedit` 会显示一个 Samba 用户列表；安装 Samba 后，未定义任何 Samba 用户：

```bash
# pdbedit -L
#
```

名为 `nobody` 的 Samba 用户不需要存在，以便名为 `guest` 的 Windows 用户能够以匿名用户身份登录。更多信息请参阅上一节中“名为 `guest` 的用户”。

安装后，没有用户拥有 Samba 密码（没有 Samba 用户）。你只能为 `/etc/passwd` 中列出的用户添加 Samba 用户及可选密码。使用 `root` 权限，使用带有 `-a` 选项的 `smbpasswd` 为 Linux 用户（`/etc/passwd` 中列出的用户）添加 Samba 用户和密码：

```bash
# smbpasswd -a sam
New SMB password:
Retype new SMB password:
Added user sam.
```

`pdbedit` 实用程序显示你刚刚添加的 Samba 用户，但它不会显示密码信息：

```bash
# pdbedit -L
sam:1000:Sam the Great
```

一旦用户拥有了 Samba 密码，他就可以不使用任何参数使用 `smbpasswd` 来更改他的密码。如果新密码过于简单，或者你输入的两个密码不匹配，`smbpasswd` 实用程序将显示一个非描述性的错误消息。

```bash
$ smbpasswd
Old SMB password:
New SMB password:
Retype new SMB password:
Password changed for user sam
```

如果用户在 Linux 和 Windows 系统上的用户名不同，你必须将 Windows 用户名映射到 Linux 用户名（见第 830 页的“用户映射”）。除了由 `guest` 账户（第 842 页）指定的 Windows 用户外，请确保所有通过 Samba 登录的 Linux 用户都有 Samba 密码。

## 运行 Samba 客户端

要在 Linux 上运行 Samba 客户端，你需要安装一个包并在客户端防火墙上打开几个端口。客户端上没有运行任何 Samba 守护进程。Samba 客户端运行在 Linux 和 Windows 上。在 Linux 下，你可以使用 `smbtree`（第 832 页）显示共享，使用 `smbclient`（第 833 页）以类似 ftp 的方式连接到共享，使用 `Nautilus`（第 833 页）浏览共享，以及挂载共享（第 834 页）。在 Windows 下，你可以浏览（第 835 页）和映射（挂载；第 835 页）共享。

## 前提条件

安装以下软件包：

- `samba-client`（默认已安装）

- `samba-common`（默认已安装）

`samba-client` 软件包没有守护进程，因此安装它时不需要运行 `systemctl`。

按照第 829 页的说明打开客户端防火墙。

你可能需要在服务器上设置用户名和密码。更多信息请参阅第 829 页的“Samba 用户、用户映射和密码”。

### 从 Linux 处理共享资源

Samba 使你能够从 Linux 系统（客户端）查看和处理服务器系统上的文件。本节讨论了从 Linux 访问 Windows 文件的几种方法。

#### `smbtree`：显示共享资源

`smbtree` 实用程序显示可用共享资源的层级图。除非使用 `-N` 选项，否则 `smbtree` 会提示你输入密码；如果你想浏览对匿名用户可见的共享资源（可浏览的），请使用 `-N` 选项或不输入密码（仅按 RETURN）。密码允许你查看受限共享资源，例如 `[homes]` 共享中的用户主目录。以下是 `smbtree` 的示例输出：

```bash
$ smbtree -N
MGS
    \\PLUM
        \\PLUM\HL-2140-series    Brother HL-2140 series
        \\PLUM\tmp                Temporary directory
        \\PLUM\IPC$               IPC Service (Samba Server Version 4.0.6)
```

在上面的输出中，`MGS` 是工作组名称，`PLUM` 是 Samba 服务器名称。工作组和机器名称始终以大写字母显示。如果 `smbtree` 不显示输出，请在 `smb.conf` 中设置 `workgroup`（第 841 页）和 `wins server`（第 845 页）参数。更多详细信息请参阅 `smbtree` 手册页。

#### `smbclient`：连接到共享资源

`smbclient` 实用程序的功能类似于 `ftp`（第 713 页），并连接到共享资源。但是，`smbclient` 使用 Linux 风格的前向斜杠（`/`）作为路径分隔符，而不是 Windows 风格的后斜杠（`\`）。与 `smbtree` 一样，输入密码可以查看受限共享资源。`-N` 选项可防止 `smbclient` 请求密码。下一个示例连接到 `PLUM` 上的一个受限共享资源：

```bash
$ smbclient //plum/sam
    Enter sam’s password: password (RETURN)

    Domain=[MGS] OS=[Unix] Server=[Samba 4.0.6]
    smb: \> ls

      D     0  Thu Jun 27 15:19:19  2013
    ..
      D     0  Fri Jun 21 05:52:24  2013
    .bashrc
      H   124  Mon Mar 11 12:53:01  2013
    .config
      DH
    .bash_profile
      H   193  Mon Jun 11 12:53:01  2013
    ...
    .local
      DH  0  Tue Jun 11 19:30:00  2013
    .mozilla
      DH  0  Tue Jun 4 19:28:00  2013

    37645 blocks of size 1048576.  31993 blocks available

    smb: \>
```

你可以使用大多数 `ftp` 命令在 `smbclient` 中。有关 `ftp` 命令的示例，请参阅第 717 页的“教程会话”。或者，输入命令 `help` 以显示命令列表，或输入 `help` 后跟一个命令以获取特定命令的信息：

```bash
smb: \> help history
    HELP history:
        displays the command history
```

#### 浏览共享资源

使用 `smbtree` 和 `smbclient` 浏览共享资源与从 Windows 浏览网络相比显得相当笨拙；`GNOME` 提供了更用户友好的替代方案。通过在终端模拟器或“输入命令”窗口（ALT+R2）中输入 `nautilus` 来显示 Nautilus 文件浏览器窗口。选择**连接到服务器**（在左侧）以显示“连接到服务器”窗口。在标记为**服务器地址**的文本框中输入 `smb://` 后跟服务器名称或 IP 地址，然后单击**连接**以显示服务器上的 Windows 共享资源。或者，在服务器名称后跟用户名（例如 `smb://plum/sam`），然后单击**连接**。Nautilus 将显示一个窗口，允许你输入该用户的域（工作组）和密码。输入该信息并单击**连接**以显示该用户的目录。

Nautilus 使用虚拟文件系统插件，这些插件是桌面环境的一部分，而不是原生 Linux 系统的一部分。因此，只有原生 `GNOME` 应用程序可以打开远程共享资源上的文件；普通的 Linux 程序则不能。例如，`gedit` 可以打开远程共享资源上的文件；`LibreOffice`、`mplayer` 和 `xedit` 则不能。

## 挂载共享

使用 `-t cifs` 选项的 `mount` 实用程序（第 520 页）可以像挂载 Linux 目录层级一样挂载共享。有关 CIFS 协议的更多信息，请参阅第 1242 页。挂载共享时，您可以写入共享上的文件；但是，使用 `smbclient` 时无法写入共享上的文件。

挂载共享的命令语法如下（必须以 `root` 权限运行此命令）：

```bash
mount -t cifs //host/share dir
```

其中 `host` 是共享所在系统的名称，`share` 是你要挂载的共享的名称，`dir` 是将共享挂载到其上的 Linux 目录的绝对路径名（即挂载点）。

以下命令在 `root` 权限下运行时，会将 `plum` 上的 `sam` 共享挂载到 `/plum.sam` 目录：

```bash
# mount -t cifs //plum.sam /plum.sam -o username=sam
Password for sam@/plum.sam: ****** RETURN
# ls /plum.sam
Desktop Documents Downloads Music Pictures Public ...
```

省略用户名参数并提供空密码，即可挂载对匿名用户可见的共享。

使用 `uid`、`file_mode` 和 `dir_mode` 挂载选项配合 cifs 类型的文件系统，以建立已挂载文件的所有权和权限：

```bash
# mount -t cifs //plum.sam /plum.sam -o username=sam,uid=sam,file_mode=0644,dir_mode=0755
```

权限必须表示为以零开头的八进制数。更多信息请参考 `mount.cifs` 手册页。

您还可以将用户名、密码以及可选的工作组（域）存储在凭据文件中。为了防止其他用户挂载此共享，凭据文件应归 `root` 所有，且仅允许具有 `root` 权限的用户读取和写入（权限为 `600`）。如果在 `fstab`（第 524 页）中指定了凭据文件，则系统启动时会自动挂载该共享。以下是前例中共享的凭据文件：

```bash
# cat /etc/plum.sam.credentials
username=sam
password=password
domain=MC5
# ls -l /etc/plum.sam.credentials
-rw------- 1 root root 40 06-27 17:38 /etc/plum.sam.credentials
```

以下命令使用凭据文件挂载此共享：

```bash
# mount -t cifs //plum/sam /plum.sam -o credentials=/etc/plum.sam.credentials
```

`/etc/fstab` 中的以下行会导致系统启动时挂载该共享：

`//plum/sam /plum.sam cifs defaults,credentials=/etc/plum.sam.credentials`

除非某个共享使用与其他共享相同的登录信息，否则每个共享必须拥有其自己的凭据文件；如果是这种情况，则这些文件可以使用同一个凭据文件。

## 从 Windows 操作共享

本节描述了如何从 Windows 机器访问 Linux（或 Windows）目录。你不需要设置 Linux 客户端就能从 Windows 机器浏览或映射 Linux 共享。

### 浏览共享

要从 Windows 访问 Samba 服务器上的共享，请在 Windows 系统上打开“我的电脑”或资源管理器，并在标记为“地址”的文本框中输入 `\\` 后跟 Samba 服务器的 NetBIOS 名称（如果未分配不同的 NetBIOS 名称，则只需输入主机名）。随后，Windows 将显示远程系统正在共享的目录的共享名称。例如，要查看名为 `plum` 的 Linux 系统上的共享，请输入 `\\plum`。从此窗口，你可以查看，如果允许，还可以浏览远程系统上可用的共享。如果你设置服务器上的共享使其不可浏览，你需要使用 `\\servername\\sharename` 格式输入共享的路径才能显示该共享。

### 映射共享

从 Windows 机器访问 Samba 服务器上的共享的另一种方法是映射（挂载）共享。在 Windows 系统上打开“我的电脑”或资源管理器，点击窗口顶部的“映射网络驱动器”，或从菜单栏的下拉列表中选择（在许多 Windows 机器上位于“工具”菜单中）。Windows 将显示“映射网络驱动器”窗口。从标记为“驱动器”的列表框中选择一个未使用的 Windows 驱动器字母，并在标记为“文件夹”的文本框中输入你要映射的共享的 Windows 路径。（当你使用 `system-config-samba` [仅限 Fedora] 创建共享时，共享的名称与你正在共享的目录的名称相同。）Windows 路径的格式为 `\\hostname\\sharename`。例如，要将 `plum` 上的 `\\tmp` 映射到 Windows 驱动器 `J`，假设共享名为 `tmp`，请在标记为“驱动器”的列表框中选择 `J`，在标记为“文件夹”的文本框中输入 `\\plum\tmp`，然后点击“完成”。在提供用户名和密码后，你应该能够从 Windows 机器上将 `plum` 的 `/tmp` 目录作为 `J (tmp)` 进行访问。如果无法映射驱动器，请参阅第 846 页的“故障排除”。

## 设置 Samba 服务器

本节描述了如何使用 `system-config-samba` 图形界面（仅限 Fedora）和编辑器编辑配置文件来安装和配置 Samba 服务器。

## 前提条件

安装以下软件包：

- `samba`

- `system-config-samba`（可选；仅限 Fedora）

- `samba-common`（随 `samba` 一起安装）

**启用并启动 smb**

运行 `systemctl` 使 `smb` 服务（`smbd` 守护进程）在系统每次进入多用户模式时启动，然后启动 `smb` 服务。使用 `systemctl status` 命令确保服务正在运行。
