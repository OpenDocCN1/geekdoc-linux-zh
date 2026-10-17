
## Table 3.1 VESA Mode Numbers

| Colors | 640×480 | 800×600 | 1024×768 | 1280×1024 |
|---|---|---|---|---|
| 256 | 0x301 | 0x303 | 0x305 | 0x307 |
| 32k | 0x310 | 0x313 | 0x316 | 0x319 |
| 64k | 0x311 | 0x314 | 0x317 | 0x31A |
| 16M | 0x312 | 0x315 | 0x318 | 0x31B |

`frame buffer device X server`可以使用`SaX`轻松配置。按照上一节“SaX”中描述的相同程序，直到到达`Card configuration`。在`Card configuration`选项卡中，选择`Vendor Generic Server Selection`。从`Name`列表中，选择`Framebuffer server`。继续设置你的`X`服务器的步骤。

## X Display 提示

本节涉及一些面向初学者的`X Window System`提示。

### Tip #1: Adding Hosts to the Access Control List

假设你在`X`会话中，并且想要以`root`身份启动一个`X`程序。你收到的消息将类似于以下内容：

```
Error: Can't open display
```

这是因为`X`所做的限制只允许启动`X`的用户启动基于`X`的应用程序。在这种情况下，你应该使用命令`xhost`启用将启动应用程序的主机。要启用主机在服务器上启动`X`应用程序，请使用以下命令：

```
bash$xhost + hostname
```

前面的命令添加了允许连接到`X`服务器的主机的主机名。要允许从`localhost`连接的用户，请使用以下命令：

```
bash$xhost + localhost
```

从`localhost`连接的用户将能够启动`X`程序，如果他们导出了正确的`DISPLAY`环境变量。

### Tip #2: Exporting the DISPLAY Environment Variable

在将`localhost`添加到控制访问列表之后，`root`用户必须导出正确的`DISPLAY`环境变量以连接到`X`服务器。这可以按如下方式完成：

```
bash#export DISPLAY=:0
```

### Tip #3: Starting X Programs on Other Servers and Exporting the DISPLAY Variable to Your X Server

假设你想要访问另一台机器上的一些`X`程序并希望它们显示在你的`X`服务器上。如果你的`IP`是`192.186.186.5`，而你想要启动程序的机器是`192.186.186.6`，你可以执行以下操作：

- 1. 使用`telnet`登录到`192.186.186.6`服务器。
- 2. 在你的机器上，通过在另一个`xterm`中发出命令`xhost + 192.186.186.6`允许`192.186.186.6`连接到你的`X`服务器。
- 3. 在`telnet`窗口中，发出命令`export DISPLAY= 192.186.186.5:0`。
- 4. 启动程序，它将显示在你的`X Window System`上。

## Troubleshooting the X Window System

*My card is not supported by X, what should I do?*

如果你显卡支持`VESA`版本`2`，你可以使用`Frame Buffer Device X Server`，或者你可以购买另一块受支持的显卡。

*Whenever I try to configure the X Window System, I get a server not found in SaX and XF86Setup.*

你没有安装包含你的`X`服务器的软件包。检查本章“Installing the X Window System”部分中系统要求的列表。

*The X Window System starts in a different mode than the one I want, what should I do?*

如果你使用`SaX`配置了`X Window System`，请确保你已安排好想要的分辨率。最上面的模式将首先使用。如果你使用`XF86Setup`，请确保你在`/etc/XF86Config`的`Screen`部分中添加了以下行：

```
DefaultColorDepth
```

*When I set up XDM/KDM, the system keeps flashing and I can't access the system.*

如果在未先执行完整的工作`X`系统测试的情况下开始使用`XDM/KDM`，就会发生这种情况。尝试通过按住`Ctrl+Alt+Del`组合键直到它捕获重启信号来重启系统，或通过`telnet`到系统并重启它。在`lilo`提示符下，输入`linux 2`。当系统以控制台模式启动时，重新配置`X Window System`并确保它能工作。如果它不能工作，使用`YaST`将你的系统启动为`ASCII`登录。

## PART II

## 系统管理

- 4 管理用户和组 87
- 5 管理文件系统 107
- 6 备份系统 121
- 7 系统升级 131
- 8 安装新内核 157
- 9 配置系统启动序列 185
- 10 声音卡配置 201
- 11 打印 225
- 12 配置外设 241

## 管理用户和组

## 本章内容

- Linux：多用户操作系统 88
- 什么是账户？ 88
- 管理用户 89
- 管理组 92
- 管理主目录 95
- 控制你的用户 96
- 故障排除 104

## Linux：多用户操作系统

`Linux`是一种多用户操作系统，这意味着它可以同时为多个用户提供服务。这种能够充分利用系统为尽可能多的用户提供服务的能力，是多用户操作系统的优势之一。大多数多用户操作系统通过使用用户账户的概念来实现这一点。

常见的多用户操作系统采用用户账户来允许多个人同时使用系统。不同的用户被归入不同的组。这使得系统管理员能够轻松控制系统的使用方式并实现最佳利用。

## 什么是账户？

要拥有多用户操作系统，你需要有用户账户。账户是你系统上的一个逻辑分区。每个将使用你系统的用户都将拥有这样一个逻辑分区或账户。账户可以充当该用户的隔间。用户拥有自己的空间，并且可以共享附近可用的工具——并非所有工具他都可以使用。用户在未经其他用户许可的情况下无法查看其他用户在其空间中的内容。资源由更高级别的用户即管理员或`root`来在用户之间进行控制。

现在你知道了账户背后的逻辑，你需要知道账户在物理上是什么。账户首先通过为用户提供用户名和密码来创建，从而使他们能够登录系统。用户必须登录才能使用系统。用户名和密码有助于控制谁应该使用系统，谁不应该使用。当用户登录系统时，他会被定位到所谓的其主目录中。在典型的`Linux/Unix`系统中，你会有一个名为`/home`的目录。在该目录内部，你会找到若干以系统中的用户命名的其他目录。每个用户都有自己的`/home/username`目录。例如，一个名为`John`的用户，其主目录在`/home/john`，如果还有另一个名为`Mary`的用户，她的主目录将是`/home/mary`。

为每个用户提供自己的目录的想法非常有帮助。每个用户在其目录内存储文件。用户通常除了自己的主目录和`/tmp`目录外，不被允许在整个系统中的其他地方写入。

当你拥有用户时，你需要一种控制他们的方式。这就是`root`账户的作用。每个`Linux`系统都有一个默认且关键的账户，称为`root`账户。`root`账户属于将管理和控制整个系统的人。

拥有`root`账户的目的是维护和升级系统。例如，要安装一个将由所有用户共享的应用程序，你必须以`root`身份登录。要能够彻底破坏系统，你必须以`root`身份登录。这就是成为`root`非常危险的原因——一个错误，你就可能轻易抹掉整个系统。虽然成为`root`感觉很不错，但在真实的多用户系统中，这是最糟糕的工作之一。你有很大的责任。

## 管理用户

管理你的用户是一个非常简单的过程，并且由于`SuSE YaST`而变得更加简单。`YaST`提供了非常简单的用户管理界面。你可以在一个地方添加、修改和删除用户。

### 添加新用户

要向系统添加用户，你使用`YaST`。记住，因为你维护系统，你必须以`root`身份登录。例如，要添加一个名为`John Gear`、用户名为`john`的用户，请按照以下步骤操作：

- 1. 要运行`YaST`的用户管理模块，你可以通过选择`系统管理`，`用户管理`来导航到它；或直接运行`YaST`以加载用户模块：
- 2. 用户管理模块加载（见图 4.1）。

```
### yast --mask user
```
