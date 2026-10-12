
![](img/f67bdb23d5a8cb457175c8ce91ec36c2_840_1.png)

图 23-2 服务器设置窗口，Basic 选项卡

# 第 23 章 SAMBA：Linux 与 Windows 文件和打印机共享

![](img/f67bdb23d5a8cb457175c8ce91ec36c2_841_0.png)

图 23-3 Samba 用户窗口

如果 Sam 在 Windows 和 Linux 系统上都有 `sam` 账户，我们从 Unix Username 组合框中选择 `sam`，在 Windows Username 文本框中输入 `sam`，并在两个 Samba Password 文本框中输入 Sam 的 Windows 密码。点击 OK 关闭 Create New Samba User 窗口，并点击 OK 关闭 Samba Users。

## 为 Linux 用户 nobody 添加 Samba 密码

> 因为在安装 Samba 时，用户中已存在 `nobody` 用户，所以你无法通过 `system-config-samba` 添加用户 `nobody`，也无法为 `nobody` 添加密码；相反，你必须按照以下步骤从命令行使用 `smbpasswd`：

```
$ sudo smbpasswd - nobody
New SMB password:
Repeat new SMB password:
```

通常，用户 `nobody` 没有密码，因为它是访客登录。在 SMB 密码提示处按回车（不输入任何字符）即可将不带密码的 `nobody` 添加到 Samba 文件中。

Linux 接下来，你需要添加一个共享，即你想要从 Linux 系统导出到 Windows 系统的目录。点击工具栏上的绿色号 `+` 在 Create Samba Share 窗口中显示选项卡（图 23-4）。在 `directory` 文本框中，输入要共享的目录的绝对路径（`/tmp` 是一个易于练习的目录）。根据喜好输入描述。在此处输入 Linux 主机名和正在共享的目录路径是有帮助的。如果你希望从 Windows 机器向该目录写入，请指定 Writable（可写）；Visible（可见）允许从 Windows 机器看到共享。点击 Access（访问）选项卡并指定是否要限制访问用户

## 设置 Samba 服务器

![](img/f67bdb23d5a8cb457175c8ce91ec36c2_842_0.png)

图 23-4 Create Samba Share 窗口，Basic 选项卡

或指定是否允许任何人访问此共享。点击 OK。关闭 Samba 配置窗口。

你现在应该从 Windows 机器访问共享了（第814页）。不需要重启 Samba 服务器。

拥有 **`root`** 权限的用户可以使用 `smbpasswd` 更改 Linux 用户的 Samba 密码。

```
$ smbpasswd sam
New SMB password:
Repeat new SMB password:
```

此示例假设 Sam 在安装 Samba 之前已经是 Linux 系统上的用户。如果你安装 Samba，它会将所有 Linux 用户复制到 Samba 用户列表中。如果你在安装 Samba 后添加用户，你需要使用 **`-a`** 选项指示 `smbpasswd` 将用户添加到 Samba 用户列表中。以下命令将 Linux 用户 `max` 添加到 Samba 用户列表并为其分配 Samba 密码：

```
$ smbpasswd -a max
New SMB password:
Repeat new SMB password:
Added user, max.
```

# swat: 配置 SAMBA 服务器

## 制作 smb.conf 的备份

在安装时，`/etc/samba/smb.conf` 文件包含大量的注释（第 807 页）。`swat` 会覆盖此文件并移除注释。在首次运行它之前，请为 `smb.conf` 制作一个备份以防丢失。

`swat`（Samba 网页管理工具，`swat` 工具）是一个基于浏览器的图形化编辑器，用于编辑 `/etc/samba/smb.conf` 文件。对于每个可配置的参数，它都提供了帮助链接、默认值以及一个用于更改值的文本编辑器。`swat` 工具是一个设计精良工具，它忠实于你正在编辑的 `smb.conf` 中的行内容：你可以使用并从中学习 `swat`，这样如果你想使用文本编辑器修改 `smb.conf`，操作就会变得非常简单。

`swat` 并非来自 `inetd` (`openbind`-软件包)。当你安装 `swat` 软件包时，必须安装 `openbind` 作为依赖项。如有必要，在 `/etc/inetd.conf` 文件中添加以下命令：

```
swat stream tcp nowait 408 root /usr/sbin/tcpd /usr/sbin/swat
```

此行允许 `inetd` 运行时启用 `swat`。如有必要：

```
$ sudo service openbind-inetd restart
* 正在重启 Internet superuser inetd
```

![](img/f67bdb23d5a8cb457175c8ce91ec36c2_843_0.png)

欢迎使用 SWAT！

请使用上述按钮之一选择一个配置操作

## Samba 文档

- edit - `smbd` 守护进程
- enable - Netbind 域名服务器
- restart - `openbind` 守护进程
- 配置文件
- `smb.conf` - Samba 配置文件
  - hosts - Netbind hosts 文件
  - hosts - Netbind 记录文件
- 管理工具

图 23-5 本地 swat 主页

## 建立 SAMBA 服务器

你应该能够运行 `swat`。从本地系统开始，打开浏览器并在地址栏输入 `http://127.0.0.1:901` 或 `https://localhost:901`。根据提示，输入用户名 `root` 和 `root` 密码。（你必须设置 `root` 密码才能更改 Samba 主页，见第 431 页）。如果你使用 `root` 以外的用户名，将能够查看配置信息但无法更改。从远程系统，将 `127.0.0.1` 替换为服务器的 IP 地址（但请参见相邻的安全说明）。如果本地系统运行了防火墙且你正从远程系统访问 `swat`，请使用 `gufw` 使用 TCP 端口 `901`（第 876 页）。

不要允许从不安全的网络对 `swat` 进行未加密的远程访问。当你这样做并登录时，`root` 密码将通过你使用的任何连接以明文发送并可能被嗅探。如果你想通过不安全的网络访问 `swat`，请使用 `ssh` 转发端口 `901`（第 681 页）。

浏览器显示本地 Samba/`swat` 主页（图 23-5）。此页面包含指向 Samba 文档的链接以及下面的按钮。

- HOME 链接到本地 Samba 文档。当你点击 Samba 单词（不是图标，而是 Samba/`swat` 主页中 Documentation 之前的单词）时，`swat` 会显示主页面，该页面定义了每个 Samba 程序。
- GLOBALS 编辑 `smb.conf` 中的参数（变量）。
- SHARES 编辑 `smb.conf` 中的信息。
- PRINTERS 编辑 `smb.conf` 中的打印机信息。
- WIZARD 重写 `smb.conf` 文件，移除所有注释行和指定默认值的行。
- STATUS 显示活动的连接、活动共享和打开的文件。停止并重启 `smbd` 和 `smbd` 守护进程。
- VIEW 根据 `smb.conf` 中的默认值和设置，显示子集（点击 View）或所有配置参数（点击 Normal View）。
- PASSWORD 管理共享。从 Windows 系统出发，可以轻松地建立一个基础的 Samba 设置来与 Linux 层次结构协同工作。设置安全连接或具有特殊功能的连接需要更多工作。以下示例基于 Ubuntu Linux 随带的 `smb.conf` 文件创建了一个基础设置。

`swat` defaults 每个参数旁边都有一个标记为“Help”的气泡。点击 Help 会打开一个新浏览器窗口，其中包含该参数的说明。每个参数还有一个“Default”按钮，可以将参数设置为其默认值（不一定是由 Ubuntu 提供的初始值）。对于此示例，不要点击任何“Set Default”按钮。在你对页面进行更改后，确保在每个页面顶部点击“Commit Changes”（提交更改）。

![](img/f67bdb23d5a8cb457175c8ce91ec36c2_845_0.png)

图 23-6 共享参数页

在你点击页面顶部的菜单按钮之前。否则，`swat` 将放弃你的更改。

GLOBALS 要遵循此示例，首先点击 Samba/`swat` 主页顶部的 GLOBALS。保持所有当前设置不变，但有两个例外：`hosts allow` 和 `hosts deny`。这些参数通过限制允许的客户端名称来使服务器更安全。前面的 `allow` 和 `deny` 条目（如果有）取自全局参数。
