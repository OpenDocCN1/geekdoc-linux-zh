

## swat: 配置 SAMBA 服务器

## 备份 /etc/samba/smb.conf

在默认安装下，/etc/samba/smb.conf 包含了大量的注释（第 207 页）。`swat` 实用工具会覆盖它并移除注释。在第一次运行 swat 之前，请为 smb.conf 创建一个备份以备。

`swat`（Samba 网页管理工具，swat 包）实用工具是一个用于 /etc/samba/smb.conf 文件的浏览器图形化编辑器。对于每个可配置参数，它都提供了帮助链接、默认值以及用于更改值的文本框。`swat` 实用工具是一个设计良好的工具，它忠实于你所编辑的 smb.conf 文件中的行内容：你可以使用并学习 swat，这样如果你想使用文本编辑器修改 smb.conf，其翻译对应关系将非常直观易懂。

当你安装 swat 包时，`swat` 实用工具位于 inetd 中，该包会安装 opensamba-inetd 作为依赖项，并遵循与 /etc/inetd.conf 一致的策略。

```
swat stream tcp nowait.400 root /usr/sbin/tcpd /usr/sbin/swat
```

此行在 swat 运行时启用。如有必要，使用以下命令重启 inetd 以其重新加载配置：

```bash
$ sudo service opensbd-inet restart superserver inetd
```

- * 正在重启 inetd 互联网超级服务器 inetd [ OK ] *

![](img/45ff4cd21497435daa35084a84b95d07_854_0.png)

欢迎使用 SWAT！

请使用下方按钮之一选择一个配置操作

## S 文档说明

- 守护进程 (Daemons)
  - smbd - SMB 守护进程
  - nmbd - NetBIOS 节点服务器
  - winbind - winbind 守护进程
- 配置文件 (Configuration File)
  - smb.conf - Samba 主配置文件
  - hosts - NetBIOS 主机文件
  - mypassword - SMB 密码文件
- 管理实用工具 (Administrative Utilities)

图 23-5 本地 swat 主页

## 设置 SAMBA 服务器 805

现在你应该可以运行 swat 了：从本地系统，打开浏览器并在地址栏中输入 http://127.0.0.1:901 或 http://localhost:901。在提示提示时，输入 *root* 用户名和 *root* 密码。（你必须使用 *root* 密码才能 swat 更改 Samba 配置；请查看第 431 页的说明。）如果你使用 *root* 以外的用户名，你将能够某些配置信息，但无法进行更改。从远程系统，请将 `127.0.0.1` 替换为服务器的 IP 地址（但请查看相邻的安全提示）。如果本地系统运行着防火墙，且你想从远程系统访问 *swat*，请使用 gufw 使用 TCP 端口 901（详见第 876 页）。

## 不要允许对 swat 进行非加密访问

不要允许从不安全网络上的远程系统访问 swat。当你这样做并登录时，*root* 密码将以明文通过你所使用的任何连接发送，并很容易被嗅获。如果你想在不安全的网络上访问 swat，请使用 ssh 转发端口 901（详见第 681 页）。

浏览器显示本地 Samba/swat 主页（图 23-5）。此页面包含指向本地 Samba 文档以及下方按钮的链接。

- HOME 链接本地 Samba 文档。当你点击 *Samba* 单词（不是图标，而是 Samba/swat 主页中 *Documentation* 单词之前的那个）时，*swat* 会显示 Samba 页面，该页面定义了每个 Samba 程序。

- GLOBALS 编辑 `smb.conf` 中的全局参数（变量）。

- SHARES 编辑共享信息。

- PRINTER 重写 `smb.conf`，移除所有注释和指定默认值的行。

- STATUS 显示活跃的连接、共享和打开的文件。停止并重启 *smbd* 和 *nmbd* 守护进程。

- VIEW 显示 `smb.conf` 中默认设置的全部或部分参数（点击 VIEW）。

- PASSWORD 管理密码。可以简易地建立基本的 Samba 设置，以便从 Windows 系统使用 Linux 层级。设置安全连接或使用特殊功能需要更多工作。以下示例是基于 Ubuntu 自带的 smb.conf 文件的基础设置。

每个参数 *swat* 会显示一个 *Next* 按钮。点击 *Help* 将打开一个包含参数说明的新浏览器窗口。每个参数都有一个 *Set Default* 按钮，将其设置为默认值（不一定是 Ubuntu 提供的初始值）。

对于此示例，不要点击任何 *Set Default* 按钮。在完成更改后，确保在页面顶部点击 *Commit Changes*。

![](img/45ff4cd21497435daa35084a84b95d07_855_0.png)

## 806 第23 章 SAMBA：Linux 与 Windows 文件及打印机共享

![](img/45ff4cd21497435daa35084a84b95d07_856_0.png)

图 23-5 本地 swat 主页

浏览器显示本地 Samba/swat 主页（图 23-5）。此页面包含指向本地 Samba 文档以及下方按钮的链接。

- HOME 链接本地 Samba 文档。当你点击 *Samba* 单词（不是图标，而是 Samba/swat 主页中 *Documentation* 单词之前的那个）时，*swat* 会显示 Samba 页面，该页面定义了每个 Samba 程序。

- GLOBALS 编辑 `smb.conf` 中的全局参数（变量）。

- SHARES 编辑共享信息。

- PRINTER 重写 `smb.conf`，移除所有注释和指定默认值的行。

- STATUS 显示活跃的连接、共享和打开的文件。停止并重启 *smbd* 和 *nmbd* 守护进程。

- VIEW 显示 `smb.conf` 中默认设置的全部或部分参数（点击 VIEW）。

- PASSWORD 管理密码。可以简易地建立基本的 Samba 设置，以便从 Windows 系统使用 Linux 层级。设置安全连接或使用特殊功能需要更多工作。以下示例是基于 Ubuntu 自带的 smb.conf 文件的基础设置。

每个参数 *swat* 会显示一个 *Next* 按钮。点击 *Help* 将打开一个包含参数说明的新浏览器窗口。每个参数都有一个 *Set Default* 按钮，将其设置为默认值（不一定是 Ubuntu 提供的初始值）。

对于此示例，不要点击任何 *Set Default* 按钮。在完成更改后，确保在页面顶部点击 *Commit Changes*。

## 857 如果你无法再次 swat

如果你无法再次使用 swat，可能是错误地更改了 hosts allow。在这种情况下，你需要手动编辑 /etc/samba/smb.conf 并修复该行：

```bash
$ grep hosts smb.conf
hosts allow = 127.0.0.1, 192.168.0.8
hosts deny = ALL
```

前面的项目仅允许 192.168.0.8。它们允许 swat 正常工作。更改 smb.conf 后不需要重启 Samba。

