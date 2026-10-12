
## 设置 [printers] 参数

仅当您的红帽 Linux 系统连接了一个或多个打印机时，`[printers]` 部分才值得关注。默认的 `[printers]` 配置如下：

```
[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = no
    guest ok = no
    printable = yes
```

以下是如何更改这些参数。

- **comment.** 如其名称所示。您可以将其设置为您希望的任何值。
- **path.** 将其设置为打印机数据文件将被暂存的目录。如果您有很多用户打印大文件，请确保此目录有足够的磁盘空间。
- **browseable.** 默认情况下，打印机在浏览器（如网络邻居）或 `NET VIEW` 命令输出中不可见。要更改此行为，请将其设置为 **yes**。
- **guest ok.** 默认情况下，没有密码的来宾用户无法使用打印机服务。要更改此行为，请将其设置为 **yes**。
- **printable.** 默认情况下，此参数允许打印。如果将其设置为 **no**，则完全禁用打印功能。

默认配置包含许多注释掉的配置参数和额外的部分。请仔细检查这些选项并启用您想要使用的任何选项。但是，如果您是首次使用 Samba，请先使用默认配置使其正常工作。

## 通过 Web 管理 Samba

使用随 Samba 提供的新的基于 Web 的配置工具 SWAT，您可以使用标准的 Web 浏览器来管理 Samba。以下是如何使用 SWAT 的方法。

- 验证您的 /etc/services 文件是否包含以下行：
  swat 901/tcp
  
  如果上述行不存在，请添加此行并保存 /etc/services 文件。

- 验证您的 /etc/xinetd.d/swat 文件是否包含以下行：
  disable = no
  
  如果上述行缺失、被注释掉或设置为 yes，请添加或取消注释该行，使 disable 设置为 no。在这种情况下，使用 `killall -USR1 xinetd` 命令重新配置 xinetd 守护进程。

- 接下来，运行您最喜欢的 Web 浏览器以访问您的 Samba 服务器。输入以下 URL：
  http://your-samba-server:901/

- 系统会要求您输入用户名和密码。输入 root 作为用户名及相应的密码。如果您输入了正确的用户名/密码对，您将会看到 SWAT 欢迎屏幕。

- 单击可用的链接以管理 Samba 的各个不同方面。

## 测试 /etc/samba/smb.conf 配置

每当您更改 Samba 配置文件时，请运行 testparm 实用程序，该实用程序包含在 Samba 软件包中。当您从命令行运行这个好用的实用程序时，它会检查 /etc/samba/smb.conf 文件的语法，并为您提供有用的警告和错误消息。由于配置错误的 /etc/samba/smb.conf 文件可能是一个安全漏洞，因此在修改此文件时请始终使用该实用程序。

## 启动、停止和重启 Samba 服务

在确认您的 /etc/samba/smb.conf 文件没有错误后，您就准备好启动 Samba 了。Samba 软件包附带两个守护进程。smbd 守护进程是 Samba 服务器，nmbd 守护进程是 NetBIOS 名称服务器。要启动守护进程，请以 root 身份运行以下命令：

```
/etc/rc.d/init.d/smb start
```

然后，您可以开始从 Windows 计算机访问 Samba 服务器。要停止 Samba 服务器，请运行带有 stop 参数的相同命令。您也可以通过使用带有 restart 参数的相同命令来重启守护进程。

如果您希望在启动时启动 Samba 服务，请创建如下符号链接：

```
ln -s /etc/rc.d/init.d/smb /etc/rc.d/rc3.d/S91smb
```

当您的红帽 Linux 服务器进入运行级别 3 时，这将启动 Samba 服务，这是所有多用户系统的默认运行级别。

如果您使用基于 X Window System 的登录（使用 XDM）并希望自动启动 Samba，请创建以下链接：

```
ln -s /etc/rc.d/init.d/smb /etc/rc.d/rc5.d/S91smb
```

## 在 Windows 上使用 Linux 文件服务器

在 Windows 上使用 Linux 文件服务器可能是 Linux/Windows 环境中的 Linux 管理员考虑使用 Samba 的最常见原因。例如，假设您希望使名为 intranet 的 Linux 分区（或目录）对局域网中的一组 Windows 用户（john、jennifer 和 chad）可用。以下是您需要执行的操作：

1. 如果您将 [global] 配置部分中的 security 参数设置为 user 或 share，请在 Linux 系统上创建三个用户帐户（john、jennifer 和 chad）。需要设置这些用户帐户，使每个帐户的密码与其 Windows 对应项匹配。例如，如果 jennifer 在 Windows 系统上的密码设置为 tsk!tsk，则必须使用相同的密码设置她的 Linux 帐户。此外，在 /etc/group 中创建一个名为 intranet 的组，该组仅包含用户 jennifer、chad 和 phil 作为成员。

2. 修改 /etc/samba/smb.conf 文件以添加以下内容：
   ```
   [Intranet]
   comment = Intranet Directory
   path = /intranet
   public = no
   writable = yes
   write list = @intranet
   printable = no
   ```

前述 [Intranet] 配置指定 /intranet 不可公开访问，并为 intranet 组授予写入权限。在运行 testparm 确保 /etc/samba/smb.conf 文件没有语法错误后，您可以重启 Samba 服务。

现在，您可以让 john、mary 和 phil 从他们的 Windows 机器访问 /intranet 分区或目录。如果您想创建一个只读文件服务器，请将 writable 参数设置为 no，并从前述配置中删除 write list 参数。若要强制此共享分区（或目录）中的文件权限保持不变，请使用 force create mode 参数。例如，

```
force create mode 0750
```

确保在共享空间中创建的所有文件对所有者具有完全访问权限（读取、写入和执行），对组内所有人具有读取和执行访问权限。组外的任何人都无权访问这些文件。

## 在 Linux 系统上使用 Windows 文件服务器

如果您有一个希望提供给 Linux 用户使用的 Windows 文件服务器，请使用 smbfs（SMB 文件系统）将 Windows 磁盘和目录挂载到 Linux 系统上。例如，要在 Linux Samba 服务器上挂载名为 PLUTO 的 Windows NT/2000 服务器的默认驱动器（C:），请执行以下操作：

1. 在 Windows NT/2000 系统上，双击“我的电脑”图标以打开“我的电脑”窗口。选择 C:\ 驱动器图标，然后右键单击。在弹出的窗口中，选择“共享”选项。这将打开属性对话框，并选中“共享”选项卡。
2. 单击“作为共享”单选按钮，并从下拉的“共享名称”列表中选择一个共享名称。在此示例中，共享名称为 C。编写一行注释，以便在从其他计算机浏览时帮助识别该共享。
3. 单击“应用”并退出窗口。

您刚刚启用了 C:\ 驱动器的 SMB 共享。现在，只需将此共享挂载到 Linux 系统上即可。smbfs 文件系统附带一个名为 smbmount 的命令，该命令允许您挂载 SMB 共享。常见语法如下所示：

```
smbmount //WINDOWS-SERVER/path /mount-point -U WindowsUser -P WindowsUserPassword
```

//WINDOWS-SERVER 是拥有共享（路径）的 Windows 系统；/mount-point 是 Linux 系统上的挂载目录；WindowsUser 是 Windows 系统上至少具有读取共享权限的用户；WindowsUserPassword 是该用户的密码。如果您的 Windows NT/2000 设置正确，只有 Administrator 用户（或等效用户）应该具有整个驱动器的完全访问权限。因此，此示例使用 Administrator 用户来挂载 C 驱动器。以下是从 PLUTO 挂载 C:\ 驱动器的 smbmount 示例：

```
smbmount //PLUTO/c /mnt/pluto-c -U Administrator -P gowent
```

如果运行上述命令版本时出现错误消息，请确保您输入了正确的密码。另外，尝试使用 -I 选项指定 Windows NT/2000 服务器的 IP 地址，以防它未广播其 IP 地址。当命令成功时，您将在 df 列表中看到 /mnt/pluto-c，并能够访问 Windows 系统 C:\ 驱动器上的所有文件。如果您偏好挂载 C:\ 驱动器，使得只有 Linux 系统中的某些用户和组可以访问该驱动器，请使用 -u UID 和 -g GID 选项，如下例所示：

```
smbmount //PLUTO/c /mnt/pluto-c -U Administrator -P gowent -u root -g admin
```

