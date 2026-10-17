
CUPS 服务器在本地网络上宣告自己，并准备好在其他机器正确配置为打印到该服务器后接收其作业。当然，如果你愿意，可以更改此行为，但目前我们假设你在带有打印机的机器上运行的是默认配置。

在本示例中，打印机连接到名为 `hatter` 的机器，而我们正在另一台 SUSE Linux 机器上设置打印。执行以下操作：

- 启动 YaST 打印机模块。如果之前没有设置过打印机，且没有检测到本地打印机，选择“Add”（添加）。你将看到一个界面，可以在添加本地打印机或网络打印机之间进行选择。选择“Network Printers”（网络打印机），会出现一个类似于图 19-5 的对话框。
- 通过 CUPS Network Server 选择，并在下一个屏幕中选择 CUPS Client-Only（CUPS 仅客户端）配置。系统会要求提供服务器名称，如图 19-6 所示（你也可以允许 YaST 自动检测，或从网络上所有主机列表中选择）。
- 点击“OK”（确定）和“Finish”（完成）后，你应该能够跨网络打印到连接在名为 `hatter` 服务器上的打印机。

# 第四部分 在 SUSE Linux 中实现网络服务

## 图 19-5

选择打印机类型：远程 CUPS 服务器

![](img/e749d3c47634a5bbb94e11699efbe992_559_0.png)

## 图 19-6

在 YaST 中设置远程 CUPS 服务器

![](img/e749d3c47634a5bbb94e11699efbe992_559_1.png)

530

## 启动和停止 CUPS 服务器

在 SUSE 上，通过 `rcups start` 和 `rcups stop` 命令启动和停止 CUPS。它是另一个以通常方式控制的服务。如果你对 CUPS 配置文件进行了更改，将需要重启 CUPS 以使更改生效。

你可以使用 `rcups status` 命令检查 CUPS 是否运行。默认情况下，CUPS 在运行级别（runlevels）2、3 和 5 中启动。

## 检查远程 CUPS 服务器是否可用

从客户端机器，你可能想确保 CUPS 在服务器上运行并在网络上可用。对于其他服务，你可以通过使用下面的命令检查是否可以连接到相关端口来确认：

```
telnet hatter 631
```

如果你看到如下输出，则说明 CUPS 在网络上是用的：

```
Trying 192.168.2.6 ...
Connected to hatter.
Escape character is ' ]'.
```

现在使用 `Ctrl+-` 并退出以断开连接。

如果有问题，你可能会看到：

```
Trying 192.168.2.6 ...
telnet: connect to address 192.168.2.6: Connection refused
```

此类代码出现有多个原因：网络可能存在问题、CUPS 可能没有运行，或者 `hatter` 上可能有防火墙规则阻止了连接。

## 设置 Windows 客户端打印到 CUPS 服务器

较新版本的 Windows 支持 IPP 协议，你可以将其配置为打印到 CUPS 服务器。

> 较旧版本的 Windows 需要额外的程序来使用 IPP。要在 Windows 95 和 98 上使用 IPP 打印，你需要从 www.microsoft.com/windows98/downloads/contents/WUPref/IPP/ 下载文件 `wppnins.exe`。

使用 IPP 从 Windows 打印是在 Linux 上使用 Samba 作为打印服务器的替代方案。从 Windows 客户端的角度来看，打印机显示为 Windows 共享打印机，遗憾的是这意味着你不能像查找 Windows 共享打印机或 Samba 打印机那样浏览它。你必须在 Windows 的“添加打印机”对话框中输入特定的 URL。图 19-7 显示了预期情况。所需的 URL

# 在 SUSE Linux 中实现网络服务

由 CUPS 服务器的名称或 IP 号组成，后面跟上 `/printers/`，最后是服务器名称。因此，我们看到 `http://hatter:631/printers/`。

## 图 19-7

在 Windows 中设置远程 CUPS 服务器

![](img/e749d3c47634a5bbb94e11699efbe992_561_0.png)

532

533

某些可用函数仅提供信息。其他函数可以更改设置。在 CUPS 服务器上需要管理权限，当你访问这些函数时会显示验证对话框（见图 19-9）。

## 图 19-9

CUPS 界面交互验证对话框

![](img/e749d3c47634a5bbb94e11699efbe992_563_0.png)

SUSE 默认设置在此接受 root 用户和 root 密码。或者，你可以使用下面的命令行创建 CUPS 用户：

```
lpadmin -g sys -a roger
```

这将现有的系统用户 `roger` 添加为 CUPS 用户并提示你输入密码。在此之后，`roger` 成为可以通过 界面管理 CUPS 的 CUPS 用户。然而，在最近的 SUSE 版本中，使用的验证机制是系统标准验证，因此你为 `lpadmin` 使用的密码无关。登录后，你可以从 界面执行所有管理任务，包括添加打印机。你所做的更改将写回 CUPS 配置文件 `/etc/cups/`。

用户信息是 CUPS 特有的，并存储在文件 `/etc/cups/passwd.md5` 中。

## 在 CUPS 中使用类（Classes）

CUPS 的优秀功能之一是你可以创建一个打印机类（例如特定位置的打印机组）。该类由一组 CUPS 服务器可以打印的打印机组成，无论是本地连接还是通过网络。设置类后，用户的作业将打印到其具有访问权限的类中的某个打印机上。

在界面中，你可以添加类（系统会提示输入名称、位置和描述，这些是任意的）。然后从 CUPS 已知的打印机列表中添加打印机。图 19-10 显示了如何在 CUPS 界面中添加类。

## 图 19-10

在 CUPS Web 界面中添加类

![](img/e749d3c47634a5bbb94e11699efbe992_564_0.png)

类设置好后，CUPS 服务器会将该类作为打印队列提供。随后，在客户端，我们可以在 YaST 打印模块中选择该队列进行打印（见图 19-11）。

## 图 19-11

在 YaST 中选择一个类作为默认队列

![](img/e749d3c47634a5bbb94e11699efbe992_564_1.png)

# 第四部分 在 SUSE Linux 中实现网络服务

例如，如果你正在配置 Windows 系统以打印到名为 sales 的类队列，你将选择 `http://hatter:631/printers/sales`。

## 允许远程访问 CUPS Web 界面

本章前面提到，CUPS 默认不允许你从远程位置登录其 Web 界面。如果你想更改此设置，必须编辑文件 `/etc/cups/cupsd.conf`。在以下起始的部分中：

```
<Location /admin>
```

添加一行：

```
Allow from @LOCAL
```

然后保存文件并重启 CUPS：

```
rcups restart
```

现在，你可以从局域网上的其他机器使用 Web 界面。当然，如果你愿意，可以将 `@LOCAL` 替换为特定的 IP 地址，从而将其限制在单个 IP 上。

## CUPS 命令行工具与配置文件

CUPS 还提供了一套命令行工具，可以完成 Web 界面允许的所有管理操作。这些是由 `cups-client` 软件包提供的命令。特别是 `lpinfo`、`lpadmin` 和 `lpoptions` 提供了 Web 界面相同的功能，但是通过命令行执行的。

通常情况下，为了避免问题，你应该按照以下优先级顺序使用可用工具：

- 使用 YaST 打印模块进行基础设置
- 使用 CUPS Web 界面
- 使用 CUPS 命令行工具

换句话说，能用 YaST 完成的。如果你无法通过 YaST 完成某项任务，请使用 CUPS Web 界面，仅在必要时才使用命令行工具。

## lpinfo

`lpinfo` 显示可用的打印选项。`lpinfo -v` 显示可用于打印的潜在设备。`lpinfo -m` 显示可用的打印机驱动。

## lpadmin

`lpadmin` 命令有大量的选项用于管理。你可能更倾向于使用 Web 界面，但这里有一两个示例。如下所示：

```
lpadmin -h hatter -p laserjet41 -u allow:roger.junior
```

这允许用户 `roger` 和 `justin` 向 CUPS 服务器 `hatter` 上的 `laserjet41` 队列打印。而这个命令：

```
lpadmin -h hatter -p laserjet41 -u deny:badman
```

防止用户 `badman` 向 CUPS 服务器 `hatter` 上的 `laserjet41` 队列打印。
