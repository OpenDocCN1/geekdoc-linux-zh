
你还可以提供访问服务的密码。将其作为服务名后的参数输入。如果你不提供密码，系统会提示你输入。

**注意**

你还可以使用 Nautilus（GNOME 文件管理器）来访问 Samba 共享。使用 `smb://` 协议，例如 `smb://lizard/windata`。仅输入 `smb://` 将显示所有 Samba 共享。

# 使用 smbclient 访问共享

你可以添加多个选项来访问共享、用户名或可用服务列表。
使用 `-I` 选项，你通过 IP 地址指定系统。使用 `-U` 选项并指定你想在远程系统上使用的远程登录名称。如果需要密码，请在密码后附加 `%`。
使用 `-L` 选项，你可以获取服务器上的服务列表，例如共享目录和指针。
以下命令将列出 `turtle.mytrek.com` 主机上的可用共享：

```
smclient -U turtle.mytrek.com
```

要访问远程系统上的特定目录，将目录作为 `smclient` 命令的参数输入，后跟任何选项。对于 Windows 文件，路径名使用反斜杠，对于 Unix/Linux 文件使用正斜杠。一旦连接成功，将显示 shell 提示符，你可以使用 `smclient` 命令如 `get` 和 `put` 来传输文件。`quit` 或 `exit` 命令将终止 `smclient` 程序。在以下示例中，`smclient` 使用 `dylan` 访问 `turtle.mytrek.com`：
`smbclient://turtle.mytrek.com/myreports -I 192.168.0.1`

在大多数情况下，你可以直接使用服务器名称来引用服务器，如下：
`smbclient //turtle.mytrek.com/myreports -U dylan`

如果你正在访问 Samba 服务器上特定账户的家目录，只需指定服务。在下一个示例中，用户以 `aleina` 账户访问 Samba 服务器上的家目录：
`smbclient //turtle.mytrek.com/home -U aleina`

你还可以使用 `smbount` 挂载 Windows 客户端上的共享文件夹。只需指定文件夹的计算机。如果文件夹名称包含空格，请用单引号括起来。在以下示例中，用户将 `windata` 文件夹挂载到 Linux 的 `/mylinus` 目录。对于允许任何人访问的文件夹，只需在密码提示处按回车键：
```
$ smbclient ///windata /mylinus

Password:

$ ls /mylinus

_hi_mynewdoc_my_report.txt
```

完成共享文件夹的操作后，使用 `smbount` 命令将其卸载。
`smbount /mylinus`

不要显式使用 `smbount`，而是使用文件系统类型为 `smbfs` 的 `mount` 命令。`mount` 然后将运行 `/sbin/mount.smfs` 命令，该命令将调用 `smbclient` 来挂载文件系统：
`mount -t smbfs -o username=chris password=mypass //linux/windata /mylinus`

# smclient 命令

登录后，你可以执行 `smclient` 命令来管理文件和更改目录。Shell 命令可以使用 `!` 算符执行。传输文件时，使用 `get` 和 `mget` 命令，正如在 FTP 程序中使用的那样。`recursive` 命令允许你递归复制子目录。你可以使用文件匹配算符 `*` 和 `?`（见第 8 章）来选择文件集。默认掩码为 `*`，匹配所有。以下示例使用 `mget` 复制所有 `.c` 结尾的文件：

在传输期间，你可以使用 `smclient` 提示每个文件或直接传输所有选中的文件。该提示可以开启或关闭。

要访问使用创建的特定打印机，将打印机作为 `smbclient` 命令的参数，后跟任何选项。在以下示例中，`smclient` 使用 `dylan` 登录访问 `turtle.mytrek.com`：
`smbclient //turtle.mytrek.com/ -U dylan`

一旦连接，将显示 SMB 文件夹，你可以使用 `smclient` 命令如 `print` 来打印文件，并使用 `printmode` 指定图形或文本。在下一个示例中，用户在访问 `turtle.mytrek.com` 后打印名为 `myfile` 的文件：
`smb> printmode myfile`

# smbount

通过 `smbount` 命令，Linux 或 Unix 客户端可以将共享目录挂载到其本地系统。`smbount` 命令的语法与 `smbclient` 类似，具有许多相应选项。`smbount` 命令接受的参数为 Samba 服务器和共享目录，随后是你挂载目录的本地目录。以下示例将 `myreports` 目录挂载到本地系统的 `/mnt/myre` 目录：
`smbount //turtle.mytrek.com/myreports /mnt/myre -U dylan`

要卸载目录，使用带有本地名称的 `smbount` 命令如下：
`smbount /mnt/myre`

要挂载服务器上特定用户的目录，使用 `homes` 服务器和用户的登录名。以下示例将用户 `larisa` 的家目录挂载到本地系统的 `/home/chris/larastuff` 目录：
`smbount //turtle.mytrek.com/homes /home/chris/larastuff -U larisa`

你还可以使用 `smbount` 挂载 Windows 客户端上的共享文件夹。只需指定文件夹的计算机名称。如果文件夹名称包含空格，请用单引号括起来。在以下示例中，用户将 `windata` 文件夹挂载到 Linux 的 `/mylinus` 目录。对于任何人可访问的文件夹，只需在密码提示处按回车键。

```
$ smbclient ///windata /mylinus

Password:

$ ls /mylinus

_hi_mynewdoc_my_report.txt
```

完成共享文件夹的操作后，使用 `smbount` 命令将其卸载。
`smbount /mylinus`

不要显式地使用 `smbount`，而是使用文件系统类型为 `smbfs` 的 `mount` 命令。`mount` 然后将运行 `/sbin/mount.smfs` 命令，该命令将调用 `smbclient` 来挂载文件系统：
`mount -t smbfs -o username=chris password=mypass //linux/windata /mylinus`

你还可以在 `/etc/fstab` 条目中使用 `smbfs` 类型来自动挂载 Samba 文件系统：
//linux/windata /mylinus smbfs defaults 0 0

要管理目录共享，请在控制面板的管理员窗口中打开“计算机管理”工具。点击“共享文件夹”，然后你就可以看到“共享”、“会话”和“打开的”文件夹。要添加新共享，点击“共享”文件夹，点击“操作”菜单并选择“新建文件共享”。“会话”和“打开的”文件夹的“操作”菜单允许断开活动会话和文件夹。

为了允许其他客户端或在 Samba 服务器上进行共享级别的打开访问，请确保在你的 Windows 客户端上已启用了访客用户。该功能默认情况下是禁用的。访问控制面板中的“用户和密码”工具来设置访客用户。对于连接到 Windows 客户端的打印机，访客访问尤为重要。想要访问 Windows 系统上打印机的 Linux 系统将在其系统中将该打印机配置为远程 Samba 打印机。通常访问打印机输入的用户是访客。为了让 Linux 系统能够访问 Windows 打印机，Windows 系统必须有一个访客用户。

## 共享 Windows 目录

要共享目录

## 共享 Windows 打印机

要共享打印机，在“打印机”窗口中找到该打印机并右键点击它，选择“共享为”选项。这将打开“共享”面板，在其中你可以点击“共享为”按钮并输入他人识别该打印机的名称。例如，在名为 `lizard` 的 Windows 客户端上，有一个名为 `Epson Stylus Color` 的打印机，名称为 `mepson`，则该打印机的“共享”面板将选中“共享为”按钮，并输入了名称 `mepson`。当用户双击“我附近的计算机”中的 `lizard` 图标时，标记为 `mepson` 的打印机就会出现。

Linux 系统若要使用此打印机，必须在该 Linux 系统上将其配置为远程打印机。对于打印机，你可以通过 `redhat-config`（“系统设置”菜单和窗口中的打印）轻松完成；对于使用 CUPS 打印服务器的打印机，请使用 CUPS 打印配置工具（“额外工具”菜单）。

要配置你的远程打印机，你需要为打印机指定一个在 Linux 系统上的名称、Windows 客户端名称、在 Windows 客户端上访问时的打印机名称，以及用户名（通常为 `guest`）。一旦配置完成，你的打印命令就可以直接使用打印机名称访问它，就像访问其他打印机一样。例如，安装在 Windows 上的 `mepson` 打印机也将作为 Samba 服务器安装在 Linux 操作系统的 CUPS 中。对于 CUPS 打印服务器，你可以使用 `redhat-config` 配置你的 Windows 打印机。如果你愿意，可以给打印机相同的名称，并在“队列类型”面板中选择“Windows 打印机 (SMB)”。对于“共享”，输入 `/lizard/mepson`；对于“用户”，输入 `guest`；对于“工作组”，输入 Windows 客户端的工作组（通常为 `WORKGROUP`）。

对于 CUPS 打印服务器，你也可以使用 CUPS 打印配置工具并添加打印机。对于设备，通过 Samba 选择 Windows 打印机。使用 URI URL 输入带协议的共享名称：`smb://lizard/mepson`。此外，为了让 CUPS 使用 Samba，你需要将 Samba 共享目录链接到 CUPS smb 目录。

```
ln -s /usr/bin/smbspool /usr/lib/cups/backend
```

安装完成后，你可以重启 CUPS。然后 `prpr` 命令就可以访问远程 Windows 打印机。下一个示例是在 Windows 客户端的 Epson 打印机上打印 `mydoc` 文件。
```
lpr -P mypson mydoc
```
