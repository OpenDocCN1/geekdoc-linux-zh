
- OS 级别（OS level）——设置一个值来控制您的 Samba 服务器（`nmbd` 守护进程）是否可以成为您工作组的本地主浏览器。提高此设置会增加 Samba 服务器控制本地广播区域浏览器列表的机会。

如果值为 0，可能会选中 Windows 机器。值 60 可确保选择 Samba 服务器而非 NT 服务器。默认值为 20。

- 首选主浏览器（Preferred master）——如果您希望强制选择主浏览器并让 Samba 服务器有更好的机会被选中，请将其设置为 Yes。（配合此选项一起，将 Domain Master 设置为 Yes，可以确保 Samba 服务器被选中。）默认设置为 `Auto`，这会导致 Samba 在承担责任之前尝试检测正确的主浏览器。

- 如果您希望 Samba 服务器成为本地浏览主，请将此项设置为 Yes（这并不是保证，但它提供了一个机会）。如果您不希望 Samba 服务器被选为本地主，则将其设置为 No。本地主默认为 `Auto`。

- 域主浏览器（Domain master）——如果您希望 Samba 服务器（`nmbd` 守护进程）识别为其工作组的域主浏览器，请将其设置为 Yes。此列表将允许分配给工作组的客户端使用子网外的 SMB 共享文件和打印机。默认设置为 No。

## 第四部分：设置 Linux 服务器

### 注意（Note）

如果浏览不起作用，请检查 `nmbd` 日志文件（`/var/log/samba/log.nmbd`）。要获取更多细节，请将调试信息级别增加到 2 或 3（在本节较早描述）。

### WINS 选项

- WINS 服务器——输入用于解析名称的 WINS 服务器 IP 地址。如果不使用 WINS 服务器，请留空。

- WINS 服务器——如果您希望 Samba 服务器充当 WINS 服务器，请将此项设置为 Yes。

### 事件选项

- 事件级别（Event level）——设置要记录的事件级别。0 表示不记录事件，1 表示错误，2 表示信息，3 表示调试。

### 杂杂选项（Miscellaneous options）

- 注释（Comment）——描述共享的注释。

- 路径（Path）——共享目录的路径。

- 无效用户（Invalid users）——不允许登录的用户名称。

- 有效用户（Valid users）——可以访问 Samba 服务的用户账户名称。

- 管理员用户（Admin users）——对共享具有管理权限的用户。

- 读取列表（Read list）——将用户添加到此列表以授予读取权限。

- 写入列表（Write list）——将用户添加到此列表以授予共享写入权限。

- 宾客账户（Guest account）——如果选择了 Guest OK，在此定义的用户名将分配给访问文件系统的用户。

- 只读（Read only）——如果为 Yes，可以从此文件系统读取文件，但远程用户无法在系统上保存或修改文件。

- 允许主机（Hosts allow）——允许访问此文件系统的计算机名称。

- Hosts deny（拒绝主机）——通过在此处列出名称来拒绝对特定计算机的访问。默认情况下，不排除任何特定计算机。以与用于 Hosts Allow（允许主机）时相同的格式输入主机名。

- Browseable（可浏览）——指示你是否可以在共享目录列表中查看此目录。默认认为开启（Yes）。

- Available（可用）——允许你保留此条目不变但关闭该服务。如果你想临时关闭对某个目录的访问，此功能非常有用。在 Fedora 中默认认为关闭（No）。选择 No 以关闭它。

- 4. 选择 Commit Changes（提交更改）。

此时，共享文件系统应该可以被能够你的 Linux Samba 服务器的 Samba 客户端计算机（Windows 9x、Windows NT、Windows 2000、OS/2、Linux 等）访问。在尝试操作之前，你可以检查你的 Samba 配置。

### 使用 SWAT 检查你的 Samba 设置

在 SWAT 窗口中，选择 STATUS（状态）按钮。

从此窗口中，你可以重启 `samba` 和 `nmbd` 进程。同样地，你可以看到活动连接、共享和打开文件的列表。启动 `samba` 和 `nmbd` 守护进程的首选方法是将 `samba` 服务设置为自动启动。对服务输入 `chkconfig sm` 使其在引导启动时启动。

### 使用 Samba 文件和命令操作

尽管你可以通过 Samba 服务器配置窗口或 SWAT 设置 Samba，但许多管理员更倾向于编辑 `/etc/samba/smb.conf` 文件。作为 root 用户，你可以查看此文件的内容并进行更改。如果你选择了 User security（用户安全，推荐），你可能对 `smusers` 和 `smpasswd` 文件（位于 `/etc/samba` 目录）也感兴趣。这些文件以及 `testpart` 和 `smbstatus` 等命令将在后续章节中介绍。

### 编辑 smb.conf 文件

你使用 Samba 服务器配置窗口或 SWAT Web 界面所更改将反映在你的 `/etc/samba/smb.conf` 文件中。以下是一个 `smb.conf` 示例（带有注释）：

```
[global]
workgroup = ESTREET
server string = Samba Server on Maple
hosts allow = 192.168.0.0
printcap name = /etc/printcap
load printers = yes
printing = cups
log file = /var/log/samba/%m.log
```

```
max log size = 0
smb passwd file = /etc/samba/smbpasswd
security = user
ncrypt passwords = Yes
unix password sync = Yes
passwd program = /usr/bin/passwd %u
passwd chat = "*password* %n\n*Retype*newpassword* %n\n*password:\n  *authentication*tokens*updated*successfully"
pam password change = yes
obey restrictions = -yes
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
username map = /etc/samba/smbusers
dns proxy = no
```

```
[homes]
comment = Home Directories
browseable = no
writable = yes
valid users = %
create mode = 0664
directory mode = 0775
```

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes
```

我将逐行讲解这个示例，但这里有一些观察结果。在 `[global]` 部分中，`workgroup` 被设置为 ESTREET，服务器被标识为 Samba Server on Maple，且只有位于本地网络（192.168.0.0）的计算机被允许访问 Samba 服务。你必须更改本地网络以匹配你的网络。

将共享的本地打印机的定义取自 `/etc/printcap` 文件，打印机已加载（yes），并使用了 CUPS 打印服务。

此示例使用了用户级安全（`security = user`），这允许用户登录一次，然后轻松地访问 Linux 系统上的打印机和该用户的主目录。密码加密已开启（`encrypt passwords = yes`），因为大多数 Windows 系统默认开启了密码加密。密码存储在 Linux 系统的 `/etc/samba/smbpasswd` 文件中。

`dns proxy = no` 选项防止 Linux 在 DNS 服务器上查找系统主机名（用于 TCP/IP 查找）。

`[homes]` 部分允许每个用户从局域网（LAN）上的 Windows 系统访问其 Linux 主目录。该用户将能够向主目录写入内容。然而，其他用户将无法看到或共享此目录。`[printers]` 部分允许所有用户向本地 Linux 系统上配置的任何打印机打印。

### 添加 Samba 用户

执行用户级 Samba 安全意味着为每个从其 Windows 工作站使用 Linux 系统和打印机的人分配一个 Linux 用户帐户（你可以将用户分配给访客账户，但在本示例中，所有用户都有自己的账户）。然后，你需要为每个用户添加 SMB 密码。例如，以下是添加一个 Windows 登录位置为 `chuckp` 的用户的方法：

- 1. 在终端窗口中以 root 用户身份输入以下内容以添加 Linux 用户帐户：

```
useradd -m chuckp
```

- 2. 按照如下方式为新用户添加 Linux 密码：

```
passwd chuckp
Changing password for user chuckp
New UNIX password: ********
Retype UNIX password: ********
```

- 3. 为每个用户重复此操作。

- 4. 为每个用户添加 SMB 密码：

```
smbpasswd -a chuckp
```

- 5. 为每个用户重复此操作。

### 启动 Samba 服务

当你配置好 Samba 服务后，按照之前“获取和安装 Samba”中的描述重启 Samba 服务。现在你可以检查你的服务器。

## 第1章：运行文件服务器

### 测试你的 Samba 权限

你可以从 shell 运行多个命令来操作 Samba。其中一个是 `testparam` 命令，它可以检查权限。它列出了设置的全局参数。

### 检查共享目录的状态

`smstatus` 命令可以查看谁正在使用 Samba 资源。以下是 `smstatus` 的输出示例：

```
smstatus

Samba version 3.5.2-60

PID     Username    Group      Machine
25770   chris       chris        booker      (10.0.0.50)
25833   chris       chris        10.0.0.50
```

```
Service     pid         machine     Connected at               Name        Time
IPC$       25729       booker                               Wed Aug 25 12:06:29 2010
tymtp       25770       booker                               Wed Aug 25 16:06:03 2010
tymtp       25833       10.0.0.50                  Wed Aug 25 12:25:52 2010
IPC$       25730       booker                               Wed Aug 25 12:06:29 2010
```

Locked files:

Pid Uid DenyMode Access R/W Oplock SharePath Name Time

```
25833 501 DENY_NONE 0x1201f RDWR /tmp .b.txt.swap Wed Aug 25 12:26:18 2010
```

此输出显示从你的 Linux Samba 服务器，`tymtp` 服务（`/tmp` 的共享）正被命名用户 `booker` 使用。PID 25833 是处理该服务的 `sm` 守护进程的进程号。打开 `/tmp/.b.txt.swap` 文件的是由 `vi` 命令打开的。它具有读写权限。

### 使用 Samba 共享目录

在配置好 Samba 服务器后，你可以从网络上的客户端计算机使用共享目录。接下来的章节描述了如何从另一个 Linux 系统或各种 Windows 系统使用你的 Samba 服务器。

### 从 Nautilus 使用 Samba

要在 Nautilus 文件管理器中连接到 Samba，请通过点击文件（File）-> 打开位置（Open Location）使用位置框。然后在你的 Nautilus 文件管理器框中输入 `smb:`。作为替代方案，你可以从 GNOME 顶栏选择位置（Places）-> 网络 Windows（Network Windows Network）。

窗口中会显示你网络上的 SMB 工作组列表。你可以选择一个工作组，选择一台服务器，然后选择一个要使用的资源。这对于不需要密码的共享应该是可以运行的。

当你需要输入密码时，Nautilus 界面似乎存在 Bug。它要求你要么发送明文密码，要么在你的位置框中输入用户名和密码。例如，若要通过 Nautilus 访问我的主目录（`/home/chris`），我可以按照如下方式输入我的用户名、密码、服务器名称和共享名称：

```
smb://chris:my72mgb@arc/chris
```

### 在 Linux 中挂载 Samba 目录

Linux 可以像查看任何其他介质（硬盘、NFS、CD-ROM 等）一样查看你的 Samba 共享目录。使用 `mount` 命令来挂载 Samba 文件系统，使其永久地连接到你的 Linux 文件系统。

这里有一个 `mount` 命令的示例，它将一台名为 `toys` 的计算机上的主目录（`/home/chris`）挂载到本地目录（`/mnt/toys`）上。该命令是以 root 用户身份从终端窗口中输入的：

```
@ mkdir /mnt/toys
@ mount -t cifs -o username=chris.password=a72mg /toys /mnt/toys
```

Samba 共享的文件系统是 `cifs`（`-t cifs`）。用户名（`chris`）和密码（`a72mg`）作为选项传递（`-o`）。`toys` 计算机上主目录的远程共享路径是 `/toys/chris`。本地挂载点是 `/mnt/toys`。此时，你可以像访问本地任何文件或目录一样访问 `toys` 上的 `/home/chris` 的内容。你对访问和更改该目录（及其子目录）内容的权限将与你作为用户 `chris` 直接从 `toys` 使用这些内容时的权限相同。

要永久挂载 Samba 共享目录，请向你的 `/etc/fstab` 文件添加一个条目。对于上述描述的示例，你将添加以下行（作为 root 用户）：

```
//toys/chris smbfs username=chris.password=a72mg
```

与其将用户名放在所有人都可以读取的 `/etc/fstab` 文件中，你可以将用户名和密码行放在一个单独文件中。例如，你可以将用户名和密码行写入 `cred.txt` 文件。然后将 `"credentials"/etc/samba/cred.txt` 放入挂载选项文件中，以便在文件系统挂载时自动使用这些选项。

### 故障排除你的 Samba 服务器

Samba 服务器可能会出现很多问题。如果你的 Samba 服务器运行不正常，本节中的描述应该帮助你定位问题。

### 网络网络已就绪？

没有网络，你就无法与其他计算机共享任何内容。在计算机从 Samba 共享目录和打印机之前，它们必须能够与你的局域网（LAN）通信。

## 第 18 章：运行文件服务器

你的 Samba 服务器可以使用 TCP/IP 名称作为 NetBIOS 名称（Windows 网络用于文件和打印机共享），也可以在 `smb.conf` 文件中使用单独的 NetBIOS 名称。然而，至关重要的是，广播地址必须与与你的 Samba 通信的所有客户端的广播地址相同。查看你的广播地址，请输入以下命令：

```
# ifconfig a
eth0
 Link encap:Ethernet HWadd 00:D1:B3:75:A5:1B
  inet addr:10.0.0.1 Bcast:10.0.0.255 Mask:255.255.255.0
```

重要信息是广播地址（`Bcast: 10.0.0.255`），它由子掩码（`Mask:255.255.255`）决定。如果 Samba 服务器和局域网客户端的广播地址不同，客户端将无法看到 Samba 服务器有可共享的目录或打印机。

### Samba 服务正在运行？

基础故障排除检查是查看服务是否正在运行。尝试从你的 Linux 系统使用 `smclient` 命令，查看一切是否如你预期那样运行并共享。`smclient` 命令是获取 Samba 服务器信息的极佳工具，甚至可以从 Linux 和 Windows 计算机访问共享目录。以 root 或访问你 Samba 服务器的任何身份登录后，输入以下内容：

```
$ smclient -L localhost
Password: *************
Domain=[ESTREET] OS=[Unix] Server=[Samba 3.5.2-60]
```

| Sharename | Type | Comment |
| --- | --- | --- |
| homes | Disk | Home Directories |
| IPC$ | IPC | IPC Service (Samba Server) |
| ADMIN$ | Disk | IPC Service (Samba Server) |
| hp nsl | | Printer |
| Domain=[ESTREET] OS=[Unix] Server=[Samba 3.5.2-60] | | |
| Server | Comment |
