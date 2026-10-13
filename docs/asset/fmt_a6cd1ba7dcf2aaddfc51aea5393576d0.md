
```
# Password Level allows matching of _n_ characters of the password for
# all combinations of upper and lower case.
; password level = 8
; username level = 8
```

从 Windows 95 OSR2 及以后版本开始，包括当然的 Windows NT，密码默认是加密的。在此版本之前，密码以明文形式传递。然而，如果使用随 Red Hat 提供的 `smb.conf` 文件，Samba 服务器的密码加密默认是未启用的，如以下行所示：

```
# You may wish to use password encryption. Please read
# ENCRYPTION.txt, Win95.txt and WinNT.txt in the Samba documentation.
# Do not enable this option unless you have read those documents
; encrypt passwords = yes
; smb passwd file = /etc/smbpasswd
```

这意味着你必须决定是否支持此功能。你有几种处理此情况的选项。下面描述了其中两种。

```
smbpasswd -a userid
```

另一个选项，也是需要你付出更多努力的，是在 Windows 客户端上禁用加密密码。这项工作所需的工作量当然取决于你必须更改的客户端数量。此外，由于该过程涉及在每个客户端上编辑注册表，因此此过程更容易出错。以下是涉及的步骤。

> **警告**
>
> 如果你可以在 Samba 服务器上更改设置，这比更改 Windows 客户端更可取。编辑注册表可能导致数据丢失或操作系统无法运行。

- 1. 在你的 Windows 客户端上，运行注册表编辑器 `regedit` 并导航到条目 `[HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\VNetsup]`。
- 2. 如果此处已存在名为 `EnablePlainTextPassword` 的对象，它的值将为 0 或 1。
- 3. 值 0 表示系统正在使用加密密码。要禁用此功能，请将值设置为 1。
- 4. 如果对象不存在，请将其创建为 `DWORD` 并将值设置为 1。
- 5. 保存更改，退出 `regedit` 并重新启动 Windows 系统以使此更改生效。

Samba 可以通过 `smb.conf` 文件中的以下条目配置为域服务器。这将允许你的 Linux 机器对网络上的 Windows 客户端进行身份验证。你还可以设置每台机器的登录脚本以及每个用户的登录批处理文件。默认情况下，这些条目在你的 Red Hat 系统上被注释掉了。

```
# Enable this if you want Samba to be a domain logon server for
# Windows98 workstations.
; domain logons = yes

# if you enable domain logons then you may want a per-machine or
# per user logon script
# run a specific logon batch file per workstation (machine)
; logon script = %m.bat

# run a specific logon batch file per username
; logon script = %U.bat
```

## [homes] 部分

`smb.conf` 文件的下一个特殊部分是 `[homes]` 部分，它允许客户端在无需为每个用户单独显式指定情况下访问服务器上的用户主目录。当向 Samba 服务器发出服务请求时，服务器会搜索 `smb.conf` 中具有指定名称的自定义服务，如果未找到，则会搜索 `[homes]` 部分。如果该特殊部分存在，则请求服务名称会与用户账户名称进行比较，如果找到匹配项，则用户的主目录将在网络上共享。

以下是 `[homes]` 特殊部分的示例：

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

`comment` 参数是一个人类可读的标识字符串，将显示给浏览 Samba 服务器的客户端。请注意，此 `comment` 参数类似于 `server string` 参数，但后者仅在 `[global]` 特殊部分中有效。

`browseable` 参数设置为 `no`。该参数指定服务器显示的共享将不会称为 `homes`，而是客户端有权访问的用户目录的名称。

`read only` 参数控制用户在通过网络共享目录时是否可以创建和更改文件。指定此行为的两种替代方法是使用 `writable` 参数，将其设置为 `yes`，或使用 `write ok` 参数，也将其设置为 `yes`。`preserve case` 和 `short preserve case` 参数指示服务器保留写入服务器的任何新文件的大小写。这很重要，因为 Windows 文件名通常不区分大小写，而 Linux 文件名则区分。是否设置这些参数取决于文件系统主要由 Windows 客户端使用还是主要由 Linux 或 UNIX 客户端使用。

### 注意

Linux 和 Windows 在文本文件中使用不同的行尾序列。通过 Samba 编辑文件时，文本文件协议由客户端的操作系统决定。这意味着如果同一文件由两个操作系统的客户端编辑，可能会导致损坏。

最后一条条目设置在共享目录中创建的任何文件的默认文件权限。

## [printers] 部分

Samba 使打印机可供网络使用有两种方法。一种方法为 `printcap` 中要共享的每台打印机创建特定的共享部分。另一种方法是在 `/etc/printcap` 文件中使用 `[printers]` 特殊部分，以便共享其中定义的所有打印机。

### 注意

本节多次提及 `/etc/printcap`、`printcap` 和 `printcap` 打印机。`/etc/printcap` 是定义 Linux 系统所有打印机的文件。`printcap` 打印机是在 `/etc/printcap` 中按名称定义的打印机。

可以使用文本编辑器创建 `/etc/printcap` 条目，但在您的 Red Hat Linux 系统上，首选方法是使用 `printtool`。`printtool` 通过易于使用的图形界面创建本地和远程打印机。

以下是 `[printers]` 特殊部分的示例。它共享 `printcap` 文件中定义的所有打印机，并允许除访客账户外的任何人打印。

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

`[printers]` 部分定义了如果在 `smb.conf` 文件中未找到特定条目时打印服务如何不受控制。与 `[homes]` 部分一样，如果未找到打印服务的特定条目，Samba 将使用 `[printers]` 部分（如果存在），允许用户连接到 `/etc/printcap` 中定义的任何打印机。

`comment`、`browseable` 和 `create mode` 参数在这里的含义与在 `[homes]` 部分中相同。

`path` 参数指定在打印前文件被复制到的 spool 目录。此 spool 目录的目录权限通常设置为允许读写，就像 `/tmp` 目录一样。

一个新条目是 `printable` 参数，它在 `[printers]` 特殊部分中是可选的。如果这是特定打印机的定义，则需要此条目。

下一个条目是 `public` 参数，在示例中设置为 `no`。这就是限制访客账户打印的行。要允许访客账户打印，请将此参数的值更改为 `yes`。

最后的参数 `writable` 设置为 `no`，这表示仅允许打印作业写入指定的 spool 目录。

## 创建自定义部分

自定义部分是 `smb.conf` 文件中的段落，以非通用方式共享特定的打印机或目录。这些部分通常用于为特定用户组共享目录或创建所有用户可写的公共共享目录。您也可以使用这些部分在不共享所有打印机时共享系统上的特定打印机。

以下是可供组使用的共享的示例。此条目定义了一个名为 `acct` 的文件系统资源，可供 `accounting` 组 `acct` 的成员使用。
