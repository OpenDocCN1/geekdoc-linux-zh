
## [homes] 部分

smb.conf 文件的下一个特殊部分是 [homes] 部分，它允许客户端在无需为每个用户单独显式指定情况下访问服务器上的用户主目录。当向 Samba 服务器发出服务请求时，服务器会搜索 smb.conf 中具有指定名称的自定义服务，如果未找到，则会搜索 [homes] 部分。如果该特殊部分存在，则请求服务名称会与用户账户名称进行比较，如果找到匹配项，则用户的主目录将在网络上共享。

以下是 [homes] 特殊部分的示例：

```
[homes]
    comment = Home Directories
    browseable = no
    read only = no
    preserve case = yes
    short preserve case = yes
    create mode = 0750
```

这与 Red Hat Linux 自带的默认设置略有不同。让我们逐一查看每个参数及其含义。

comment 参数是一个人类可读的标识字符串，将显示给浏览 Samba 服务器的客户端。请注意，此 comment 参数类似于 server string 参数，但后者仅在 [global] 特殊部分中有效。

browseable 参数设置为 no。该参数指定服务器显示的共享将不会称为 homes，而是客户端有权访问的用户目录的名称。

read only 参数控制用户在通过网络共享目录时是否可以创建和更改文件。指定此行为的两种替代方法是使用 writable 参数，将其设置为 yes，或使用 write ok 参数，也将其设置为 yes。preserve case 和 short preserve case 参数指示服务器保留写入服务器的任何新文件的大小写。这很重要，因为 Windows 文件名通常不区分大小写，而 Linux 文件名则区分。是否设置这些参数取决于文件系统主要由 Windows 客户端使用还是主要由 Linux 或 UNIX 客户端使用。

### 注意

Linux 和 Windows 在文本文件中使用不同的行尾序列。通过 Samba 编辑文件时，文本文件协议由客户端的操作系统决定。这意味着如果同一文件由两个操作系统的客户端编辑，可能会导致损坏。

最后一条条目设置在共享目录中创建的任何文件的默认文件权限。

## [printers] 部分

Samba 使打印机可供网络使用有两种方法。一种方法为 printcap 中要共享的每台打印机创建特定的共享部分。另一种方法是在 /etc/printcap 文件中使用 [printers] 特殊部分，以便共享其中定义的所有打印机。

### 注意

本节多次提及 /etc/printcap、printcap 和 printcap 打印机。/etc/printcap 是定义 Linux 系统所有打印机的文件。printcap 打印机是在 /etc/printcap 中按名称定义的打印机。

可以使用文本编辑器创建 /etc/printcap 条目，但在您的 Red Hat Linux 系统上，首选方法是使用 printtool。printtool 通过易于使用的图形界面创建本地和远程打印机。

以下是 [printers] 特殊部分的示例。它共享 printcap 文件中定义的所有打印机，并允许除访客账户外的任何人打印。

```
[printers]
comment = All Printers
browseable = no
create mode = 0700
path = /var/spool/samba
printable = yes
public = no
writable = no
```

[printers] 部分定义了如果在 smb.conf 文件中未找到特定条目时打印服务如何不受控制。与 [homes] 部分一样，如果未找到打印服务的特定条目，Samba 将使用 [printers] 部分（如果存在），允许用户连接到 /etc/printcap 中定义的任何打印机。

comment、browseable 和 create mode 参数在这里的含义与在 [homes] 部分中相同。

path 参数指定在打印前文件被复制到的 spool 目录。此 spool 目录的目录权限通常设置为允许读写，就像 /tmp 目录一样。

一个新条目是 printable 参数，它在 [printers] 特殊部分中是可选的。如果这是特定打印机的定义，则需要此条目。

下一个条目是 public 参数，在示例中设置为 no。这就是限制访客账户打印的行。要允许访客账户打印，请将此参数的值更改为 yes。

最后的参数 writable 设置为 no，这表示仅允许打印作业写入指定的 spool 目录。

## 创建自定义部分

自定义部分是 smb.conf 文件中的段落，以非通用方式共享特定的打印机或目录。这些部分通常用于为特定用户组共享目录或创建所有用户可写的公共共享目录。您也可以使用这些部分在不共享所有打印机时共享系统上的特定打印机。

以下是可供组使用的共享的示例。此条目定义了一个名为 acct 的文件系统资源，可供 accounting 组 acct 的成员使用。

```
[acct]
comment = Accounting Department Shared Directory
path = /home/acct
browseable = yes
writable = yes
printable = no
valid users = @acct
```

前述条目具有以下特征。它从目录 /home/acct 创建一个文件系统共享。此共享可由 SMB 客户端浏览，并由 comment 字符串标识。它不是打印服务，因此 printable 参数设置为 no。此列表中的新项目是 valid users 参数，它将对此目录的访问限制为组 acct 的成员。

作为下一个示例，考虑专用打印机共享的情况。此条目非常简单，由三个参数组成。其中第一个是 print ok 参数，如果您想能够打印，则必须将其设置为 yes。下一个条目指定来自 printcap 文件的打印机名称，而 path 指定 spool 目录。此 spool 目录必须可由希望使用此服务打印的人写入。

```
[exec_lp]
    print ok = yes
    printer name = exec_lp
    path = /var/spool/samba
```

在专用打印共享中，print ok 参数（或 printable 同义词）是必要的。还必须使用 printer name 行命名打印机。[printers] 的意图是让所有具有有效 ID 的用户都可以访问。专用打印机的意图通常是限制对用户或组的访问，这意味着在专用打印机共享中添加 valid users 参数行是个好主意。除此之外，[printers] 部分和专用打印共享的功能基本相同。

## Linux 和 Samba 作为客户端操作系统

Linux 和 Samba 集成到现有 Windows 网络的一种方式是作为客户端。在此角色中，Samba 不与其他系统共享任何资源；它仅访问网络资源服务器上的共享资源。为此，我们将研究使用 smbclient 程序、使用 smbmount 以及内核的 smbfs 选项以及如何使用它来访问 SMB 共享文件系统。

## 设置 smb.conf 文件

虽然您不需要运行 smbd 或 nmbd 程序即可作为客户端在 Windows 网络上运行，但您确实需要创建 smb.conf 文件，因为它是由 Samba 实用程序（如 smbclient 和 smbmount）必需的。然而，由于您不会与网络共享任何资源，因此该文件可以是最小的。以下是最小化的 smb.conf 文件示例，可使我们的 Linux 客户端被视为 ALCHEMY 域的一部分。

```
[global]
    workgroup = alchemy
```

## 从 Linux 测试配置

我们对 Linux 客户端的第一次测试将是从网络上的服务器获取服务列表。对于此测试，我们将使用带有 -L 命令行选项的 smbclient 命令。

```
[tschenk@nomad tschenk]$ smbclient -L quicksilver -U tschenk
Added interface ip=192.168.50.25 bcast=192.168.50.255 nmask=255.255.255.0
Password:
Domain=[ALCHEMY] OS=[Unix] Server=[Samba 2.0.3]

Sharename   Type      Comment
---------   ----      -------
public      Disk      Public Stuff
IPC$        IPC       IPC Service (Samba Server)
lp          Printer
tschenk     Disk      Home Directories

Server      Comment
---------   -------
QUICKSILVER Samba Server

Workgroup   Master
---------   -------
ALCHEMY     QUICKSILVER
```

此测试为我们提供了服务器 quicksilver 上用户 tschenk 可用的共享列表。输出显示有一个名为 public 的共享公共目录、一台名为 lp 的打印机以及用户 tschenk 的主目录。

知道这些信息后，让我们尝试访问公共目录并查看其中保存了什么。这次我们将再次使用 smbclient 实用程序来浏览共享。

```
[tschenk@nomad tschenk]$ smbclient //quicksilver/public -U tschenk
Added interface ip=192.168.50.25 bcast=192.168.50.255 nmask=255.255.255.0
Password:
Domain=[ALCHEMY] OS=[Unix] Server=[Samba 2.0.3]
smb: \> dir
miscellaneous          D       0   Wed Jul 14 00:00:52 1999
techops                 D       0   Tue Jul 13 23:57:41 1999
development             D       0   Tue Jul 13 23:57:48 1999
accounting              D       0   Tue Jul 13 23:57:34 1999
```
