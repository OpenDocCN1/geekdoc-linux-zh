
CUPS 在网络上发布并准备好接受任务。当然，如果你愿意可以更改它，但目前是开启的。

# 第 19 章 使用 CUPS 设置打印

在这种情况下，我们假设打印机已连接。

1. 启动 YaST 模块。如果没有设置打印机，你将看到这样的对话框![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_579_0.png)

图 19-5：选择打印机

2. 选择通过 SMB 网络打印，然后在下一个屏幕中选择它。

3. 点击确定和完成后，你应该能够图 19-6 所示进行打印。

## 启动和停止 CUPS

在 SUSE 上，通过 `start` 和 `stop` 命令启动和停止 CUPS。如果你对配置文件进行了更改，将需要重启 CUPS。

# 第四部分 ♦ 在 SUSE Linux 中实现网络服务

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_580_0.png)

## 检查远程服务器是否可用

从客户端，你可能想确保 CUPS 正在运行并可用。你可以使用类似命令进行检查：

```
telnet hatter 631
```

如果你看到这样的输出，说明 CUPS 跨网络是可用的：

```
Trying hatter...

Connected to hatter.

Escape character is '^'.
```

现在使用 Ctrl+] 断开连接。

如果有问题，你会看到这个：

```
Trying 192.168.2.6...

telnet: connect to address 192.168.2.6: Connection refused
```

在这种情况下，可能是网络问题，CUPS 可能没有运行，或者存在防火墙规则阻止了连接。

图 19-6：在 YaST 中设置远程服务器

## 设置 Windows 客户端打印到 CUPS 服务器

最近版本的 Windows 支持 IPP 协议，因此你可以设置它们打印到 CUPS 服务器。

要在 Windows 95 和 98 上使用 IPP 打印，你需要从 http://www.microsoft.com/window98/downloads/WUPreviews/IPP/ 下载 `wpnins.exe` 文件。

使用 IPP 打印是 Samba 的替代方案。从 Windows 的角度来看，打印机并不是 Windows 共享打印机，这意味着你无法像寻找 Windows 共享打印机或 Samba 打印机那样浏览它。你必须在添加打印机向导中输入特定的 URI。图 19-7 显示了预期内容。所需的 URI 由 CUPS 服务器名称或 IP 地址组成，后接 `:631`（IP 端口号），最后是服务器上的队列名称。例如我们示例中的 `http://hatter:631/printers/laserjet1`。

## 从 Linux 打印到其他类型的远程打印机

当你使用 YaST 添加打印机时，会出现令人眼花缭乱的选择。在大多数情况下，如果你需要特定的协议或连接类型，你会提前知道。你可能设置的最常见情况是打印到 Windows 或 Samba 共享打印机以及直接打印到网络打印机。在 YaST 中，这些对应于“通过 SMB 网络服务器打印”和“直接打印到网络打印机”选项。

## 打印到 SMB 服务器

这可能是一台共享打印机的 Windows 机器，也可以是一个 Samba 服务器。从客户端的角度来看，它们是相同的。这里需要注意的是，YaST 能够通过 DNS 在网络上找到服务器；在某些情况下，你可能需要向 `/etc/hosts` 添加一个条目，以便服务器能够找到它。否则，这也可以正常工作。

## 直接打印到网络打印机

直接连接到网络的打印机通常使用直接 TCP 打印，并监听端口 `9100`（选项中的第一个）。设置此项将向你显示想要打印的打印打印机。YaST 将扫描网络并显示可用打印机列表供你选择。

## 使用 CUPS Web 界面

可以通过浏览器使用端口 `631` 访问 CUPS Web 界面（见图 19-8）。默认情况下，SUSE 的设置仅允许从本地机器连接时通过浏览器进行管理更改。这可以在 `cupsd.conf` 文件中进行更改，但目前我们将查看如何从运行在自身上的浏览器来管理服务器。从本地机器，你需要访问 `http://localhost:631`。

![](img/e4e45c9f32e76fb35abbd21a9f582_0.png) 图 19-8: CUPS Web 界面

## 使用 CUPS 设置打印

如果你点击“管理任务”或其他需要管理权限的链接，将显示身份验证框（见图 19-9）。

![](img/e4e45c9f32e76fb35abbd21a9f583_0.png) 图 19-9: 带有身份验证框的 CUPS Web 界面

除非你通过命令行使用类似下面的命令创建了 CUPS 用户，否则 SUSE 的默认设置将不允许你通过这一步：

```
lpadmin -a
```

这会添加一个 CUPS 用户并提示你输入密码（它对接受的密码类型非常挑）。执行此操作后，用户不需要重启 CUPS。这有点类似于设置身份验证。现在你可以以该用户身份登录管理界面并管理 CUPS 服务器。登录后，你可以从 Web 界面执行所有管理任务，包括添加打印机。你所做的更改将写回 CUPS 配置文件。用户信息特定于 CUPS，并存储在文件 `/etc/cupsd` 中。

## 在 CUPS 中处理类

CUPS 的优秀功能之一是你可以创建一个打印机类（例如，某个位置的一组打印机）。该类由一组打印机组成，CUPS 服务器可以向这些打印机打印，无论是本地连接还是跨网络连接。设置类后，用户的打印作业将在类中的任何一个打印机上打印。

在 Web 界面中，你可以添加一个类（系统会提示你输入名称和描述，这些是任意的）。然后你可以从 CUPS 已知的的列表中向类中添加打印机。图 19-10 显示了在 CUPS Web 界面中添加类。

![](img/e4e45c9f32e76fb35abbd21a9f584_0.png) 图 19-10: 在 CUPS Web 界面中添加类

类设置完成后，CUPS 服务器会将该类作为打印队列提供。从客户端，你可以在 YaST 打印机模块中选择该队列进行打印（见图 19-11）。例如，如果你正在配置 Windows 系统打印到名为 `sales` 的类，你将选择 `http://localhost:631/printers/sales`。

## 允许远程访问 CUPS Web 界面

正如章节前面提到的，默认情况下，CUPS 不允许你从远程位置登录其 Web 界面。如果你想更改此设置，必须编辑文件 `/etc/cups/cupsd.conf`。在以以下开头的部分

`<Location /admin>`

添加一行 `Allow from LOCAL`

![](img/e4e45c9f32e76fb35abbd21a9f585_0.png)

然后保存文件并重启 CUPS：

```
service cups restart
```

现在你可以从本地网络上的其他机器使用 Web 界面。当然，你可以通过将 `LOCAL` 替换为该 IP 地址来限制它。

## CUPS 命令行工具和配置文件

CUPS 还提供了一系列命令行工具，可以执行 Web 界面允许的所有管理操作。这些是由 `cups-client` 软件包提供的命令；特别是 `lpinfo`、`lpadmin` 和 `lpoptions` 提供了 Web 界面提供的功能，但是通过命令行界面提供的。通常情况下，为了避免问题，你应该按照以下优先级顺序使用可用工具：

- 用于基本设置的 YaST 打印机模块
- CUPS Web 界面
- CUPS 命令行工具

换句话说，用 YaST 能做什么？如果你无法用 YaST 完成某项任务，请使用 CUPS Web 界面，仅在必要时使用命令行工具。

## lpinfo

`lpinfo` 显示可用的潜在打印方式。`lpinfo -v` 显示可用于打印的潜在设备。`lpinfo -m` 显示可用的打印机驱动。

## lpadmin

`lpadmin` 命令有大量的选项来管理打印。你可能更倾向于使用 Web 界面，但这里有一两个例子：

```
lpadmin -h localhost -p laserjet41 -u allow:roger,justin
```

允许用户 `roger` 和 `justin` 打印到 `localhost` CUPS 服务器上的 `laserjet41` 队列。

```
lpadmin -h localhost -p laserjet41 -u deny:badman
```

防止用户 `badman` 打印到 `localhost` CUPS 服务器上的 `laserjet41` 队列。

```
lpadmin -p newprinter -c sales
```

在 `localhost` 上输入此命令将将打印机 `newprinter` 添加到我们之前设置的 `sales` 打印机类中。

## lpoptions

`lpoptions` 命令可用于查看队列的当前选项或设置选项。
