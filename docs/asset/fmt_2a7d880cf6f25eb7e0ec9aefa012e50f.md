
- 5. 尝试从本地系统外的浏览器连接到你的 Apache Web 服务器。如果失败，请通过调查防火墙、`SELinux` 和其他安全功能来修正你遇到的任何问题。

- 6. 使用 `openssl` 或类似的命令创建自己的私有 RSA 密钥和自签名 SSL 证书。

- 7. 配置你的 Apache Web 服务器使用你的密钥和自签名证书来保护安全（HTTPS）内容。

- 8. 使用浏览器为你的服务器创建 HTTPS 连接，并查看你创建的证书内容。

- 9. 创建名为 `/etc/httpd/conf.d/example.org.conf` 的文件，该文件开启基于名称的虚拟主机并创建一个执行以下操作的虚拟主机：

    - 在所有接口的端口 80 上监听

    - 服务器管理员为 `joe@example.org`

    - 服务器名称为 `joe.example.org`

    - `DirectoryRoot` 为 `/var/www/html/example.org`

    - 包含 `index.html` 的 `DirectoryIndex`

- 10. 在 `DirectoryRoot` 中创建一个名为 `index.html` 的文件，内容包含“Welcome to the House of Joe”。在运行 Web 服务器的机器上将 `/etc/hosts` 文件中的 `localhost` 条目末尾添加 `joe.example.org`。然后在浏览器的地址栏中输入 `http://joe.example.org`。你应该看到“Welcome to the House of Joe”。

# 第四部分：成为 Linux 服务器管理员

当用户向 FTP 服务器进行身份验证时，其用户名和密码将通过标准的 Linux 用户账户和密码进行身份验证。FTP 服务器还有一个名为 `anonymous`（匿名）的特殊非认证账户。任何人都可以访问匿名账户，它不需要有效的密码。事实上，*匿名 FTP 服务器*一词通常用于描述一种不需要（甚至不允许）对合法用户账户进行身份验证的公共 FTP 服务器。

> 注意
>
> 尽管在 Fedora 和 Red Hat Enterprise 中，默认启用了使用普通 Linux 用户账户登录 `vsftpd` 服务器，但如果 `SELinux` 处于强制模式（enforcing mode），它将阻止登录和文件传输的成功。如果你在 `SELinux` 强制模式下仍允许 Linux 登录，你可以选择一个布尔值（参见本章稍后的“配置你的 FTP 服务器”）来允许普通用户登录成功。

在身份验证（在控制端口 TCP 端口 21 上）之后，客户端和服务器之间会建立第二个连接。FTP 服务器同时支持主动和被动连接类型。在*主动 FTP 连接*中，服务器从其 FTP 端口 20 将数据发送到客户端上 1023 以上随机选择的随机端口。在*被动 FTP 连接*中，客户端请求连接并向服务器请求一个随机端口。

许多浏览器支持 FTP 被动模式，这样如果客户端有防火墙，它将阻止主动模式下的数据端口。支持被动模式需要在服务器的防火墙上做一些额外工作，允许到服务器上 1023 以上端口的随机连接。本章稍后的“为 FTP 开放防火墙”章节描述了你需要对 Linux 防火墙进行哪些操作以支持被动和主动 FTP 连接。

在客户端和服务器之间建立连接后，将建立客户端目录。对于匿名用户，`/var/ftp` 是 RHEL 的家目录，而对于 Ubuntu 和基于 Debian 的发行版，则是 `/srv/ftp`。匿名用户无法访问 `/var/ftp` 目录结构之外。如果普通用户（例如 joe）登录到 FTP 服务器，只要他拥有权限，joe 就可以更改文件系统的任何部分。

命令行型 FTP 客户端（如 `l` 和 `ftp` 命令）在连接到服务器后会进入交互模式。从提示符处，你可以运行许多与 shell 中使用的类似的命令。你可以使用 `ls` 列出目录内容，使用 `cd` 切换目录。当你看到需要的文件时，使用 `get` 和 `put` 命令分别下载文件或将其上传到服务器。

使用图形化工具访问 FTP 服务器（如网页浏览器），你可以在浏览器的位置框中输入想要访问的网站 URL（例如 `http://docs.example.com`）。如果你不添加用户名或密码，将建立匿名连接并显示网站家目录的内容。点击目录链接以切换到相应目录。点击文件链接显示或将这些文件下载到你的本地系统。

# 第 18 章：配置 FTP 服务器

在对 FTP 工作原理有了了解后，你现在准备好在你的 Linux 系统上安装 FTP 服务器（`vsftpd` 程序包）。

# 安装 vsftpd FTP 服务器

在 Fedora、RHEL 以及其他 Linux 发行版中，设置 Very Secure FTP 服务器只需要一个包：`vsftpd`。假设你已经连接到软件存储库，只需为 Fedora 或 RHEL 输入以下 root 权限命令来安装 `vsftpd`：

```
# yum install vsftpd
```

如果你正在使用 Ubuntu（或另一个基于 Debian 包的 Linux 发行版），输入以下命令安装 `vsftpd`：

```
# sudo apt-get install vsftpd
```

以下是在安装 `vsftpd` 程序包后可以运行的命令，以熟悉该包的内容。在 Fedora 或 RHEL 中运行此命令可以获取有关该包的一些通用信息：

```
# rpm -qi vsftpd
```

| 打包者 | Fedora Project |

| :--- | :--- |

| 供应商 | Fedora Project |

| URL | https://security.appspot.com/vsftpd.html |

| 摘要 | Very Secure FTP Daemon |

|or | vsftpd 是一个非常安全的 FTP 守护。它是完全从零开始写的。 |

如果你想获取更多关于 `vsftpd` 的信息，请访问 URL 相关网站 (`https://security.appspot.com/vsftpd.html`)。你可以获取关于 `vsftpd` 最新版本的额外文档和信息。

你可以查看 `vsftpd` 程序包的完整内容 (`rpm -ql vsftpd`)，也可以查看文档 (`-qd`) 或配置 (`-qc`) 文件。要查看 `vsftpd` 包中的文档，请使用以下命令：

```
# rpm -qd vsftpd
/usr/share/doc/vsftpd/EXAMPLE/INTERNET_SITE/README
/usr/share/doc/vsftpd/EXAMPLE/PER_IP_CONFIG/README
/usr/share/doc/vsftpd/EXAMPLE/VIRTUAL_HOSTS/README
/usr/share/doc/vsftpd/EXAMPLE/VIRTUAL_USERS/README
/usr/share/doc/vsftpd/FAQ
/usr/share/doc/vsftpd/vsftpd.xinetd
/usr/share/man/man5/vsftpd.conf.5gz
/usr/share/man/man8/vsftpd.8.gz
```

在 `/usr/share/doc/vsftpd` 目录结构中，包含了示例配置文件，帮助你以适用于互联网站点、多 IP 地址站点和虚拟主机的方式配置 `vsftpd`。主 `/usr/share/doc/vsftpd` 目录包含 FAQ（常见问题）、安装提示和版本信息。

当你想要设置 `vsftpd` 服务器时，这些页面可能包含最有用的信息。输入 `man vsftpd.conf` 读取关于配置文件，输入 `man vsftpd` 读取关于守护进程以及如何将其作为 systemd 服务进行管理的内容。

要列出配置文件，输入以下命令：

```
# rpm -qc vsftpd
/etc/logrotate.d/vsftpd
/etc/pam.d/vsftpd
/etc/vsftpd/ftusers
/etc/vsftpd/user_list
/etc/vsftpd.conf
```

主配置文件是 `/etc/vsftpd/vsftpd.conf`（RHEL 和 Fedora 中）或 `/etc/vsftpd.conf`（Ubuntu 中）。同一目录下的 `ftusers` 和 `user_list` 存储有关用户的信息。`/etc/pam.d/vsftpd` 设置如何进行身份验证。`/etc/logrotate.d/vsftpd` 配置日志轮转。

现在你安装了 `vsftpd` 并进行了快速查看。下一步是启动服务。

# 启动 vsftpd 服务

如果你只想使用默认设置，则不需要配置启动 `vsftpd`。如果你想先更改某些设置，请查看本章稍后的“配置你的服务器”章节，然后返回此处获取启用服务器的指令。

- 1. 检查 `vsftpd` 服务。在启动 `vsftpd` 服务之前，你可以检查它是否已经运行。在 Fedora 或 Red Enterprise Linux 7 或 8 中，执行以下操作：
