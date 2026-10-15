
## 在 Windows 上使用 Linux 文件服务器

这可能是 Linux/Windows 环境中的 Linux 管理员考虑 Samba 最常见的原因。例如，假设你想让一个名为 `/intranet` 的 Linux 分区（或目录）对局域网上的的一组 Windows 用户（john, mary, 和 phil）可用。你需要做的是：

- 1. 如果你在 `[global]` 配置部分中将安全参数设置为 `user` 或 `share`，请在 Linux 系统上创建三个用户账户（jennifer, chad 和 phil）。这些用户账户的设置需要使得每个账户的密码与其 Windows 端对应的密码匹配。例如，如果 jennifer 的密码与其 Windows 端匹配。
- 2. 现在修改 `/smb.conf` 添加以下内容：

```
[intranet]
comment = Intranet
path = /intranet
public = no
writable = yes
write list = @intranet
printable = no
```

这将指定 intranet 不公开访问，只有 `@intranet` 组的成员可以访问。

## 设置 Office 服务

如果你想与所有人共享目录，可以使用 `testpar` 确保 `/smb.conf` 没有语法错误。例如：

```
[intranet]
comment = Intranet
path = /intranet
public = yes
writable = yes
create mode = 0750
```

这将允许所有人访问共享目录。

## 在 Windows 上使用 Windows 文件服务器

如果你有一个想让 Linux 用户使用的 Windows 文件服务器，你需要在 Windows 系统上执行以下步骤：

- 1. 在 Windows 系统上，双击“我的电脑”图标打开“我的电脑”。点击 C 盘并点击鼠标右键弹出图 15-1 所示的窗口。
- 2. 从列表中选择“共享”。这将弹出一个类似于图 15-2 的对话框。
- 3. 选择“共享”选项卡（如图）。点击“共享”按钮并从共享名称列表中为共享选择一个名称。在示例中，共享名称为 C。写一行注释以便在从其他计算机浏览时识别该共享。
- 4. 点击“应用”并退出窗口。

你刚刚启用了 C 盘的共享。现在你只需要在 Linux 系统上挂载此共享。`smbfs` 文件系统带有一个名为 `smbount` 的命令，允许你挂载 SMB 共享。通用语法所示：

```
smbount //WINDOWS-SERVER/path /mount-point \
-U WindowsUser -P WindowsUserPassword
```

这里 `//WINDOWS-SERVER` 是带有共享（path）的 Windows 系统，`/mount-point` 是 Linux 系统上的挂载点，`WindowsUser` 是 Windows 系统上对共享至少具有读取权限的用户，而 `WindowsUserPassword` 是该用户的密码。如果你的 Windows NT 系统设置正确，只有管理员用户（或相应用户）应该对整个驱动器具有完全访问权限。因此，在示例中，我们将使用管理员用户挂载 C 盘。以下是一个挂载来自 PLUTO C 盘的 `smbount` 示例：

```
smbount //PLUTO/c /mnt/pluto-c -U Administrator -P gonent
```

## 第五部分：设置办公服务

当你在运行上述命令时遇到错误消息时，请确保你输入了正确的密码。此外，你可能想要尝试使用 `-I` 来指定 Windows NT 服务器的 IP 地址，以防它没有广播自己的 IP 地址。当命令执行成功时，你将在 `df` 列表中看到 `/mnt/pluto-c`，并且你可以访问 Windows 系统 C 盘中的所有文件。如果你希望挂载 C 盘，使得只有 Linux 系统上的某些用户和组可以访问该驱动，可以使用 `-u UID` 和 `-g` 选项。

```
smbount //PLUTO/c /mnt/pluto-c -U Administrator -P gowent \\u root -g admin
```

这里只有 root 和 admin 组中的任何人可以访问 PLUTO 的 C 盘，该盘挂载在 Linux 系统的 `/mnt/pluto-c` 下。

要从 Linux 系统卸载或移除 SMB 文件系统，你需要运行 `smbount` 命令。例如：

```
smbount /mnt/pluto-c
```

此命令将从 Linux 系统中卸载 `//PLUTO/c` 共享。

## 在 Linux 和 Windows 之间共享打印机

共享打印机是局域网环境的一个常见优势。使用 Samba，你现在可以在 Linux 和 Windows 之间共享打印机。让我们先看看如何在 Linux 系统上共享 Windows 打印机。

### 与 LINUX 共享 Windows 打印机

在连接到打印机的 Windows 系统上，创建一个可以使用打印机且不需要密码的账户。例如，在 Windows NT 工作站（workstation）或服务器上，你可以按照以下步骤创建账户：

- 1. 使用用户管理员程序创建一个名为 `printeruser` 的账户。不要为此用户分配任何密码，并仅将该用户分配到普通用户组。
- 2. 从“我的电脑”文件夹选择你的打印机，并点击右键打开打印机属性窗口。选择“安全”选项卡并点击“权限”。此对话框看起来如图 15-3 所示。

## 第 15 章：使用 Samba 共享文件和打印机

![](img/cbfef09f620ba4100baa62876f6f02b1_530_0.png)

如果你看到“所有人都有打印访问权限”，你不需要做任何事情。如果你设置的“所有人”没有打印访问权限，你将需要在列表中添加打印机并授予所选打印机权限。一旦你配置好 Windows NT 账户进行打印，就可以进行测试了：

- 1. 在 Linux 系统上使用 `smbclient` 程序按如下方式连接打印机：

```
smbclient //WINDOWS-SYSTEM/SharedPrinter -U printer -N -P
```

不要忘记将 `WINDOWS-SYSTEM` 替换为你的 Windows 系统名称，将 `SharedPrinter` 替换为打印机名称。`-N` 和 `-P` 选项用于指示 `smbclient` 程序使用空密码进行连接。
- 2. 一旦你建立了连接并进入了 `smbclient` 程序提示符，你可以输入 `printmode` 将打印模式设置为文本，并输入类似 `/path/to/a/linux/textfile` 的命令来打印文件。如果你的打印机打印出了该文件，你就完成了一大半。
- 3. 现在你需要配置 Linux 端。配置基于 SMB 的打印机最简单的方法是使用 Red Hat 自带的基于 X Windows 的 `printtool` 实用程序。从 xterm 中运行 `printtool` 并点击“Add”。你会看到一个如图 15-4 所示的对话框。选择 Lan Manager Printer (SMB) 选项并点击 OK 继续。

## 第五部分：设置办公服务

![](img/cbfef09f620ba4100baa62876f6f02b1_531_0.png)

图 15-4：使用 printtool 添加 SMB 机

- 4. 你将看到一个如图 15-5 所示的对话框。![](img/cbfef09f620ba4100baa62876f6f02b1_531_1.png) 图 15-5：编辑打印机配置
- 5. 如果这是你的第一个打印机，名称将设置为 `lp`。你可以将其更改为任何你想要的名称。该名称将被如 `lpr` 等命令用于识别。打印机目录应该设置为 `/var/spool/lp`。如果你更改了打印机名称，请确保也更改了打印目录路径。除非你正在通过发送大文件来滥用打印机，否则文件限制选项应保持为合理的限制，例如 2048KB (2MB)。打印机的主机应设置为连接打印机时的 Windows NT 系统。打印机名称是你为打印机创建的共享名称。用户名应该是你创建的打印机用户（printeruser）。由于你没有为用户分配密码，密码字段应留空。
- 6. 现在点击“Input Filter”来修改输入过滤器。配置对话框与图 15-6 类似。
- 7. 选择适当的打印机类型和选项。点击 OK 完成过滤器配置，最后点击 OK 添加新打印机。

## 第 15 章：使用 Samba 共享文件和打印机

![](img/cbfef09f620ba4100baa62876f6f02b1_532_0.png) 图 15-6：配置输入过滤器

- 8. 现在你可以进行测试了。在 Red Hat 系统上，点击选择新创建的打印机。如果有输出，说明你的配置工作正常。然而，如果你希望让一个或多个打印机对一个或多个用户私可用，可以为这些用户指定单独的段。例如，假设我想为名为 `bigboss` 的用户创建一个私有的打印机访问（fancyjet），我可以创建如下配置：
