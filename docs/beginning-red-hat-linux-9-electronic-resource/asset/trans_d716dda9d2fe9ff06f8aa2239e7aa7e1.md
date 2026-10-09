

## 通过系统账户进行 FTP 身份验证

我们已经看到了一些使用匿名访问 vsftpd FTP 服务器的示例（通过匿名或 ftp 用户名），但如果用户拥有系统账户并试图获取访问权限会发生什么？好吧，默认情况下，vsftpd 允许这样做，并以此方式授予用户访问其主目录的权限。例如，假设你的系统中有一个名为 eziiodm 的用户账户。该用户可以通过 FTP 客户端登录，并通过 vsftpd 像下面这样访问其主目录 /home/eziiodm：

```
# ftp 192.168.0.99
Connected to 192.168.0.99 (192.168.0.99).
220 (vsFTPD 1.1.3)
Name (192.168.0.99:none): eziiodm
331 Please specify the password.
Password:
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
...lists contents of /home/eziiodm directory...
```

如果这种情况是你的需求，这可能很有用。例如，你可以将一台机器设置为专用 FTP 服务器，并为每个需要执行 FTP 操作的用户创建一个账户：

```
# useradd -m -d /home/eddie
# passwd eddie
Changing password for user eddie.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

从而，你为每个用户分配了各自的独立 FTP 空间。

## 禁用用于 FTP 的本地系统用户账户

默认情况下，这些用户通过 FTP 读取、写入和执行其主目录内容的权限，与他们坐在电脑前直接访问该目录时的权限相同。更重要的是，通过 FTP 进行身份验证时是不加密的，因此如果你有任何敏感信息需要保护，允许通过用户账户进行 FTP 访问实际上并不是保护系统的最佳方式。

因此，在大多数情况下，建议禁用通过用户账户进行的 FTP 访问。这很容易做到——你只需更改配置文件 /etc/vsftpd/vsftpd.conf 中的相应设置。当你打开该文件时，定位到以下行：

```
# Uncomment this to allow local users to log in.
local_enable=YES
```

将指令更改为如下内容：

```
local_enable=NO
```

然后使用 **Server Configuration**（服务器配置）对话框或通过在命令行输入以下内容来重启 vsftpd 服务：

```
# service vsftpd restart
```

现在，如果你尝试使用 FTP 客户端通过系统用户账户获取 FTP 访问权限，你会被拒绝：

```
$ ftp 192.168.0.99
Connected to 192.168.0.99 (192.168.0.99).
220 (vsFTPD 1.1.3).
Name (192.168.0.99:none): eziiodm
530 This FTP server is anonymous only.
Login failed.
```

### 阻止用户账户的 FTP 访问

或者，我们可以拒绝个别用户（而非所有用户）的 FTP 访问权限。我们使用文件 /etc/vsftpd.ftppers 来控制这一点，该文件包含*不允许*访问服务器的用户列表。

为了尝试这个操作，首先将 /etc/vsftpd/vsftpd.conf 中的 local_enable 指令从 NO 改回 YES，以启用通过系统账户进行 FTP 访问：

```
# Uncomment this to allow local users to log in.
local_enable=YES
```

然后，打开 /etc/vsftpd.ftppers 文件（使用 root 权限），在底部添加一个账户名称，并保存该文件。无需重启 vsftpd 服务；对 /etc/vsftpd.ftppers 文件的更改立即生效。

然后使用该账户尝试通过 FTP 客户端获取 FTP 访问权限：

```
# ftp 192.168.0.99
Connected to 192.168.0.99 (192.168.0.99).
220 (vsFTPD 1.1.3).
Name (192.168.0.99:none): eziiodm
331 Please specify the password.
Password:
530 Login incorrect.
Login failed.
```

## 配置 FTP 欢迎横幅

一旦你安装了 `vsftpd` FTP 服务器，就有各种方法可以配置它以满足你的需求。这里有一个简单的示例。我们只需更改 /etc/vsftpd/vsftpd.conf 中 `ftpd_banner` 指令的值，就可以更改 FTP 服务器在客户端连接时发出的默认欢迎消息。例如，尝试将其更改为以下内容：

```
# You may fully customize the login banner string:
ftpd_banner=Welcome to the Wrox Press FTP service.
```

然后重启 `vsftpd` 服务，以便更改生效。现在使用你的 FTP 客户端登录到 FTP 服务器，你将看到这条新消息：

```
$ ftp 192.168.0.99
Connected to 192.168.0.99 (192.168.0.99).
220 Welcome to the Wrox Press FTP service.
. . .
```

关于 `vsftpd` FTP 服务器的更多信息以及所有配置可能性，请参考手册页，通过输入 `man vsftpd` 和 `man vsftpd.conf` 来查看。你还可以在 [http://vsftpd.beasts.org/](http://vsftpd.beasts.org/) 上找到关于 `vsftpd` FTP 服务器的更多信息。

## 设置打印服务器

如果你想在一组用户之间共享一台打印机（或一组打印机），那么你需要的是一个**打印服务器**。打印服务器管理打印请求并将它们放入队列中进行处理。它可以管理：

-   在多个用户之间共享打印机
-   身份验证，以便只有被允许的用户才能打印到特定打印机
-   打印队列
-   在单个位置配置多台打印机

在本节中，我们将探讨如何配置我们的 Linux 机器作为管理打印作业的打印服务器。

## Red Hat Linux 9 上的打印服务器

Red Hat Linux 9 提供两个不同的打印服务器软件包：**cups** 和 **LPRng**。**LPRng** 包涉及旧的行式打印机守护进程，虽然多年来很受欢迎，但现在正被较新的 **Common UNIX Printing System**（通用 UNIX 打印系统，即 CUPS）所取代。CUPS 是用于基于 Unix 平台的服务，能够管理打印机作业和队列，并支持网络打印机浏览。

Red Hat Linux 9 的安装过程默认应安装 cups 软件包。若要检查，请启动 RPM（例如，使用主菜单 | 系统设置 | 添加/删除应用程序），定位到“打印支持”软件包组（位于“系统”类别下），点击其“详细信息”按钮，并确保勾选了该复选框（在 cups 选项旁边）：

![](img/b852150740856958b10aff9e8c9d2adc_368_0.png)

点击“关闭”退出此对话框，并点击“更新”以更新已安装的软件包。如有必要，系统会提示你插入 Red Hat Linux 发行版光盘以完成安装。

### 安装打印机

当你首次安装 CUPS 时，你会在 /etc/cups 中获得一组默认的示例配置文件。然而，使用 Red Hat 提供的打印机配置工具来管理你的打印机更容易。每台打印机都有其自己的打印队列，因此我们通过使用打印机配置工具为每台打印机添加一个打印队列来配置打印服务器。

1.  要启动打印机配置工具，请选择主菜单 | 系统设置 | 打印，或在命令行输入以下命令：

```
$ redhat-config-printer
```

除非你已经以管理权限登录，否则它将要求输入 root 密码。将出现打印机配置窗口：

![](img/b852150740856958b10aff9e8c9d2adc_369_0.png)

2.  要为新打印机添加打印队列，请单击“New”（新建）按钮。这将打开“添加新打印队列”向导。点击“Forward”（下一步）跳过欢迎屏幕。

3.  首先提示你输入要添加的打印队列的名称。为打印机输入一个唯一的名称（例如，类似 `pntr_queue-1` 的名称）。如果需要，你还可以输入描述，这将有助于识别该打印机。点击“Forward”（下一步）。

![](img/b852150740856958b10aff9e8c9d2adc_369_1.png)

4.  下一个屏幕允许你从以下选项中选择合适的队列类型：

| 标签 | 类型 | 描述 |
| :--- | :--- | :--- |
| Locally-connected（本地连接） | LOCAL | 用于通过并行端口或 USB 端口直接连接到计算机的打印机 |
| Networked CUPS（网络 CUPS） | IPP | 用于连接到不同的 CUPS 系统并可通过 TCP/IP 访问的打印机 |
| Networked Unix（网络 Unix） | LPD | 用于连接到远程 Unix 系统并可通过 TCP/IP 访问的打印机 |

