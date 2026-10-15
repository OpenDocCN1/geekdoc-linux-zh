
操作菜单并选择“新建文件共享”。“会话”和“打开的文件夹”的操作菜单允许您断开活动会话和文件夹。

要允许其他客户端或 Samba 服务器上的用户进行共享级开放访问，请确保在 Windows 客户端上启用 guest 用户。默认情况下未启用。通过控制面板中的“用户和密码”工具来设置 guest 用户。Guest 访问对于让其他系统访问连接到 Windows 客户端的打印机尤为重要。想要访问 Windows 系统上打印机的 Linux 系统会将其自身系统上的打印机配置为远程 Samba 打印机。访问打印机时通常输入的用户是 guest。为了让 Linux 系统访问 Windows 打印机，该 Windows 系统必须有一个 guest 用户。

## 共享 Windows 目录

要共享目录，请右键单击该目录，然后从弹出菜单中选择“共享”（在 Windows XP 中是“共享和安全”）。单击“共享此文件夹”，然后输入共享名称，即 Samba 将识别该目录所用的名称。您可以指定是否允许其他人更改共享上的文件。您还可以指定用户限制（默认是允许的最大值）。您还可以进一步单击“权限”按钮来控制用户的访问。在这里，您可以指定哪些用户拥有访问权限以及访问类型。例如，您可以只允许对目录进行只读访问。

## 共享 Windows 打印机

要共享打印机，请在“打印机”窗口中找到该打印机，右键单击它，然后选择“共享为”选项。这将打开“共享”面板，您可以在其中单击“共享为”按钮，并输入其他主机识别该打印机所用的名称。例如，在名为 lizard 的 Windows 客户端上，要将名为 Epson Stylus Color 的打印机共享为 myepson，该打印机的“共享”面板应选中“共享为”按钮，并输入名称 myepson。然后，当用户双击“附近的计算机”窗口中的 lizard 图标时，将出现标有 myepson 的打印机图标。

对于 Linux 系统要使用此打印机，必须首先在 Linux 系统上将其配置为远程 Windows 打印机。对于使用 LPRng 打印服务器的打印机，您可以使用 redhat-config-printer（系统设置菜单和窗口中的“打印”）轻松完成此操作；对于使用 CUPS 打印服务器的打印机，您可以使用 CUPS 打印配置工具（附加系统工具菜单）。

要配置远程打印机，您需要为打印机指定一个在 Linux 系统上识别的名称、Windows 客户端计算机名称、在 Windows 客户端上访问打印机所使用的名称，以及访问用户名（通常是 guest）。配置完成后，您的打印命令只需使用打印机名称即可访问它，就像访问任何其他打印机一样。例如，安装在 Windows 客户端上的 myepson 打印机也必须作为 Samba 服务器的 Linux 系统上的 CUPS 安装。对于 CUPS 打印服务器，您可以使用 redhat-config-printer 配置 Windows 打印机。如果您愿意，可以给打印机起相同的名称，然后在“队列类型”面板中选择“Windows 打印机 (SMB)”。对于“共享”，输入 lizard/myepson；对于“用户”，输入 guest；对于“工作组”，输入 Windows 客户端的工作组（通常是 WORKGROUP）。

对于 CUPS 打印服务器，您还可以使用 CUPS 打印配置工具并添加打印机。对于设备，选择“通过 Samba 的 Windows 打印机”。对于设备 URI，输入带有 smb: 协议的共享名称，smb://lizard/myepson。此外，要启用 CUPS 使用 Samba，您需要将 samba 假脱机目录链接到 CUPS 的 smb 目录。

```
ln -s /usr/bin/smbspool  /usr/lib/cups/backend/smb
```

安装完成后，您可以重新启动 CUPS 服务器。然后 lpr 命令可以直接访问远程 Windows 打印机。下一个示例将 mydoc 文件打印到 Windows 客户端的 Epson 打印机上。

```
lpr -P myepson mydoc
```

## Windows 客户端

要从 Windows 系统访问 Samba 资源，您需要确保 Windows 系统已启用 TCP/IP 网络。如果您的 Windows 客户端已连接到 Microsoft 网络，则可能已经如此。如果您需要将 Windows 系统直接连接到运行 Linux Samba 服务器的 TCP/IP 网络，则应检查该 Windows 系统上是否已启用 TCP/IP 网络。这涉及确保已安装 Microsoft 网络客户端和 TCP/IP 协议，并且您的网络接口卡（NIC 适配器）已配置为使用 TCP/IP。这些过程在 Windows 2000 和 XP 以及 Windows 95、98 和 ME 上略有不同。

连接后，您的 Samba 共享和打印机将出现在 Windows 网络窗口中。如果您要经常使用某个共享，可以为其分配一个驱动器盘符。右键单击共享并选择“映射网络驱动器”，然后选择要使用的驱动器盘符。在 XP 上，您还可以选择是否希望在登录时自动挂载该驱动器。请按照您的特定 Windows 系统上的说明访问远程共享资源，例如打印机和目录。
