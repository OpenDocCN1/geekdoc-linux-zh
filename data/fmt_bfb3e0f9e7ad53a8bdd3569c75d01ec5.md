
- 拒绝除这些用户的所有打印（Deny Printing for Everyone Except These Users）—— 选中此项后，所有用户都被排除在打印之外。在用户框中输入用户名并点击“添加”，仅允许您输入的这些名称访问打印机。

您可以按照“设置打印机”节中的描述，配置其他计算机使用您的打印机。如果尝试从另一台计算机上打印但没有成功，以下是一些故障排除提示：

- 打开您的防火墙。如果您使用了限制严格的防火墙，它可能不允许打印。您必须启用对端口 `513`（UDP 和 TCP）以及可能的端口 `631` 的访问，以允许在您的计算机上进行打印。有关配置防火墙的信息请参见第 17 章。
- 启用 LPD 风格打印。某些应用程序可能需要 LPD 风格打印服务才能在共享打印机上打印。要在 CUPS 服务器上启用 LPD 风格打印，必须运行 `cups-lpd` 服务。包含 CUPS 的 Linux 发行版也包含 `cups-lpd`。在 Fedora 和其他 Red Hat 系统中，以 root 身份输入 `httpconfig cups-lpd`。然后重启 inet 守护进程（`service xinetd`）。
- 检查名称和地址。确保您在另一台计算机上配置时，正确启用了计算机的名称和打印队列。尝试使用 IP 地址而不是主机名。（如果有效，则表明存在 DNS 解析问题。）运行 `ethereal` 等工具允许您查看事务在何处失败。

对共享打印机的访问更改在 `/etc/cups/cupsd.conf` 文件中进行。

# 配置共享 Samba 打印机

您的打印机可以配置为共享 SMB 打印机。要将打印机共享为类似于 Samba (SMB) 打印机，只需按照第 27 章描述配置基础 Samba 服务器即可。默认情况下，您的所有打印机应在本地网络上共享。下一节将显示结果的外以及您可能想要更改的地方。

# 理解用于打印的 smb.conf

当配置 Samba 时，会构建 `/etc/samba/smb.conf` 文件以启用所有已配置打印机的共享。以下是 `smb.conf` 文件中与打印相关的几行：

```
printcap name = /etc/printcap
load printers = yes
printing = cups
encrypt passwords = yes
smb passwd file = /etc/samba/smpasswd
unix password sync = Yes
[printers]
  comment = All Printers
  path = /var/spool/samba
  browseable = yes
  writeable = no
  printable = yes
```

这些示例显示了从 Fedora Samba 服务器配置配置 Samba 的结果。这些行显示已加载来自 `/etc/printcap` 的打印机并正在使用 CUPS 服务。密码加密已开启，`/etc/samba/smbpasswd` 文件存储了加密后的密码。由于启用了密码同步，每个用户的 Samba 密码都会与用户的本地 UNIX 密码同步。

最后几行是实际的打印机定义。最后一行显示用户可以打印到所有打印机（`printable = yes`）。

# 设置 SMB 客户端

很有可能您正在您的 Linux 计算机上配置 Samba 打印机，并希望将其与 Windows 客户端共享。如果您的计算机上的 Samba 设置恰当，且客户端计算机可以通过网络连接，查找和使用您的打印机应该非常简单。

客户端查找共享 Samba 打印机的第一个地方是“网络邻域”（Network Neighborhood，或 Windows 2000 中的“我的位置”）。从 Windows 9 桌面开始，双击“网络邻域”图标。（从 Windows 2000 或 XP 开始，双击“我的位置”图标。）在 Windows Vista 中，打开“网络”。您的主机计算机名称（NetBIOS 名称，可能是您的 TCP/IP 名称）会出现在屏幕上或屏幕上的工作组文件夹中。打开代表您的计算机的图标。显示您的共享打印机和文件夹的窗口。

如果您的计算机图标没有出现在“网络邻域”或“我的网络位置”中，请尝试使用搜索窗口。从 Windows XP 开始，选择“开始” -> “搜索计算机或人员” -> “网络上的计算机”。在“计算机名称”框中输入您的计算机名称并点击“搜索”。在搜索窗口结果面板中双击您的计算机。将出现一个显示来自计算机共享打印机和文件夹的窗口（见图 26-4）。

## 图 26-4

您可以搜索您的计算机的打印机。

![](img/a90dc0c1392c27f587fa6c88e)
