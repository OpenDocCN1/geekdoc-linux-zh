
## **recurse** 命令允许你开启递归模式，以一次性复制整个子目录
你可以使用文件匹配运算符（这里称为*掩码*）来选择一组特定的文件。文件匹配（掩码）运算符包括 *、[ ] 和 ?（参见第 8 章）。默认掩码是 *，它匹配所有文件。以下示例使用 **mget** 命令复制所有后缀为 .c 的文件，例如 **myprog.c**：

```
smb> mget *.c
```

在传输过程中，你可以让 smbclient 对每个单独的文件进行提示，或者直接传输所有选定的文件。**prompt** 命令用于切换此文件提示的开启或关闭。

### 访问远程打印机
要访问远程系统上的特定打印机，请将打印机名称作为 **smbclient** 命令的参数输入，随后跟随任意选项。在以下示例中，smbclient 访问 **turtle.mytrek.com** 系统上的 myepson 打印机，使用登录名 **dylan**：

```
smbclient //turtle.mytrek.com/myepson -U dylan
```

连接成功后，将显示一个 smb 提示符，你可以使用 smbclient 命令，如 **print** 来打印文件，或使用 **printmode** 来指定图形或文本。在下一个示例中，用户在访问了 **turtle.mytrek.com** 上的 myepson 打印机后，打印了一个名为 **myfile** 的文件：

```
smb> print myfile
```

## mount.cifs: mount -t cifs
使用带有 **-t cifs** 选项的 **mount** 命令，Linux 或 Unix 客户端可以将共享目录挂载到其本地系统上。**cifs** 选项会调用 **mount.cifs** 命令来执行挂载操作。**mount.cifs** 命令的语法与 **smbclient** 命令相似，具有许多对应的选项。**mount.cifs** 命令以 Samba 服务器和共享目录作为参数，后接你想要挂载该目录的本地目录。以下示例将 **myreports** 目录挂载到本地系统的 /mnt/myreps 目录：

与其显式使用 **mount.cifs**，你应使用文件系统类型为 **cifs** 的 **mount** 命令。`mount` 随后将运行 /sbin/mount.cifs 命令，该命令会调用 **smbclient** 来挂载文件系统：

```
mount -t cifs //turtle.mytrek.com/myreports /mnt/myreps -U dylan
```

要卸载目录，请使用带有本地目录名称的 **cifs.umount** 命令，如下所示：

```
umount /mnt/myreps
```

要挂载服务器上特定用户的主目录，请指定 **homes** 服务以及用户的登录名。以下示例将用户 **larisa** 的主目录挂载到本地系统的 /home/chris/larisastuff 目录：

```
mount -t cifs //turtle.mytrek.com/homes /home/chris/larisastuff -U larisa
```

### 在 Linux 上挂载 Windows 共享文件夹
你也可以挂载 Windows 客户端上的共享文件夹。只需指定 Windows 客户端的计算机名称及其文件夹即可。如果文件夹名称包含空格，请用单引号将其括起来。在以下示例中，用户将 **lizard** 上的 **windata** 文件夹挂载为 **/mylinux** 目录。对于任何人均可访问的文件夹，只需在密码提示符处按 ENTER 键即可：

```
$ mount -t cifs //lizard/windata /mylinux
Password:
$ ls /mylinux
_hi_mynewdoc.doc_myreport.txt
```

当使用完共享文件夹时，请使用 `cifs.umount` 命令将其卸载。

```
umount /mylinux
```

如果需要用户级访问权限，你还可以将用户名和密码作为选项指定：

```
mount -t cifs -o username=chris,passwd=mypass //lizard/windata /mylinux
```

你还可以在 `/etc/fstab` 条目中使用 cifs 类型，以自动挂载 Samba 文件系统：

```
//lizard/windata /mylinux cifs defaults 0 0
```

## 使用 Samba 客户端共享 Windows 目录和打印机
要管理目录共享，请在控制面板的管理窗口中打开计算机管理工具。点击“共享文件夹”，在那里你可以看到“共享”、“会话”和“打开的文件夹”。要添加新的共享，请点击“共享”文件夹，然后点击“操作”菜单并选择“新建文件共享”。“会话”和“打开的文件夹”的“操作”菜单允许你断开活动会话和文件夹。

为了允许其他客户端或 Samba 服务器上的用户以共享级别进行访问，请确保在你的 Windows 客户端上启用了 guest（来宾）用户。默认情况下它并未启用。访问控制面板中的“用户和密码”工具来设置 guest 用户。来宾访问对于提供连接到 Windows 客户端的打印机访问权限尤为重要。想要访问 Windows 系统上打印机的 Linux 系统会将该打印机在其自身系统中配置为远程 Samba 打印机。通常用于访问打印机的用户是 `guest`。为了让 Linux 系统访问 Windows 打印机，该 Windows 系统必须拥有一个 guest 用户。

### 共享 Windows 目录
要共享一个目录，请右键单击该目录，并从弹出菜单中选择“共享”（在 Windows XP 上为“共享和安全”）。点击“共享此文件夹”，然后输入共享名称，即 Samba 将使用该名称来识别该目录。你可以指定是否允许他人更改共享中的文件。你还可以指定用户限制（默认允许的最大值为最大值）。你还可以进一步点击“权限”按钮来控制用户的访问。在这里，你可以指定哪些用户有权访问，以及访问类型。例如，你可以只允许对该目录进行只读访问。

### 共享 Windows 打印机
要共享打印机，请在“打印机”窗口中找到该打印机，右键单击它，并选择“共享为”选项。这将打开“共享”面板，在那里你可以点击“共享为”按钮并输入其他主机将用以识别该打印机的名称。例如，在名为 lizard 的 Windows 客户端上，若要将名为 Epson Stylus Color 的打印机共享为 myepson，该打印机的“共享”面板应选择“共享为”按钮并输入名称 myepson。然后，当用户双击“附近计算机”窗口中的 lizard 图标时，标有 myepson 的打印机图标将出现。

为了让 Linux 系统使用该打印机，必须首先在该 Linux 系统上将其配置为远程 Windows 打印机。你可以使用 system-config-printer（系统 | 管理 菜单下的“打印”）轻松完成此操作。你也可以使用 CUPS 打印配置工具。

要配置远程打印机，你需要提供打印机在 Linux 系统上的名称、Windows 客户端计算机名称、在 Windows 客户端上访问该打印机的名称，以及访问所用的用户名（通常是 **guest**）。配置完成后，你的打印命令可以通过打印机名称直接访问它，就像访问其他任何打印机一样。例如，安装在 Windows 客户端上的 **myepson** 打印机也必须作为 CUPS 安装在作为 Samba 服务器运行的 Linux 系统上。对于 CUPS 打印服务器，你可以使用 system-config-printer 来配置你的 Windows 打印机。如果你愿意，可以为打印机指定相同的名称。在“新打印机”窗口中，你在“选择连接”面板中选择“通过 Samba 的 Windows 打印机”条目。在相对的面板中，你输入 SMB 共享名称，例如 //lizard/myepson。你还可以使用此条目下方的共享浏览器来定位你的打印机。在这里你也选择使用的工作组。一旦选中，SMB 共享名称将被自动填入。对于身份验证，用户请输入 **guest**。

安装完成后，你可以重启 CUPS 服务器。然后，**lpr** 命令可以直接访问远程 Windows 打印机。下一个示例在 Windows 客户端的 Epson 打印机上打印 **mydoc** 文件：

```
lpr -P myepson mydoc
```

## Windows 客户端
要从 Windows 系统访问 Samba 资源，你需要确保你的 Windows 系统已启用 TCP/IP 网络。如果你的 Windows 客户端连接到 Microsoft 网络，这可能已经满足。如果你需要将 Windows 系统直接连接到你的 Linux Samba 服务器所在的 TCP/IP 网络，你应该检查该 Windows 系统是否已启用 TCP/IP 网络。这包括确保安装了 Microsoft 网络客户端和 TCP/IP 协议，并且你的网络接口卡（NIC 适配器）已配置为使用 TCP/IP。这些步骤在 Windows 2000 和 XP 上，以及 Windows 95、98 和 ME 上略有不同。

连接后，你的 Samba 共享和打印机将出现在 Windows 网络窗口中。在 Windows XP 上，你可以选择“我的网络位置”，它会列出你 Linux Samba 服务器上的 Samba 共享。如果你打开“查看工作组计算机”，它将列出你的 Samba 服务器（以及工作组中的任何其他 Samba 或 Windows 系统）。Samba 服务器将具有在 **server string** 选项中赋予的名称，加上 netbios 名称（主机名）。请遵循你特定 Windows 系统上的说明，以访问打印机和目录等远程共享资源。

