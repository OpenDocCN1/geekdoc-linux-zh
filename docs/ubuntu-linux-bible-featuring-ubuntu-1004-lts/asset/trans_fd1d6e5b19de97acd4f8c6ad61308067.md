

# 第23 章：在 Ubuntu 上软件开发

```
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 dav
drwxr-xr-x 5 www-data www-data 4096 2010-01-29 12:31 db
-r--r--r-- 1 www-data www-data 2 2010-01-29 12:31 format
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 hooks
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 locks
-rw-r--r-- 1 www-data www-data. 229 2010-01-29 12:31 README.txt
```

当然，一个空的 Subversion 存储库并不是最重要的。下一节将解释如何将现有的项目添加到你的存储库中，这样你实际上就有一些源代码可以管理了。

# 将项目导入到 Subversion 存储库

Subversion 存储库就像是组成不同项目的文件和目录的“接手套”。你可以直接将现有的文件提交到 Subversion 存储库，但最好是为项目使用独立的目录层级结构来提交文件。

```
$ svn import hello file:///var/svn/hello -m "Creating hello project"
Authentication realm: <http://192.168.6.90:80> Subversion Repository
Password for 'www':
Adding
hello/hello.c
```

`svn import` 命令接受你想要导入的项目、在存储库中创建该项目位置的 Subversion URL，以及 `-m`（消息）选项，后面跟着一个包含项目初始提交消息的字符串，该字符串需用引号括起来。`-m` 选项是可选的，但它可以节省时间，否则你将必须在 `svn` 命令启动的文本编辑器中输入此消息。

一旦你创建了项目或将任何文件提交到 Subversion，就可以使用 `svn list` 命令来显示存储库的内容，如下例所示，该示例使用了 `-R` 选项来递归显示存储库的内容：

```
$ svn list -R file:///var/svn
hello/
hello/hello.c
```

你会注意到这个示例使用了以 `file://` 开头的 URL，它提供了对本地存储库的访问。这在此时是必要的，因为你还没有启动 Subversion 服务器，所以所有 URL 必须相对于当前的文件系统。尝试使用基于 Web 的 URL 访问你的 Subversion 存储库将导致此处显示错误信息，要么是 `svn: PROPFIND of '/svn': could not connect to server`（如果你没有运行 Web 服务器），或者是 `svn: PROPFIND of '/svn': 405 Method Not Allowed`（如果你运行了服务器，但没有可用的 Subversion 存储库）。下一节将解释为 Ubuntu 系统提供的两个 Subversion 服务器，以及如何配置它们以便从其他机器访问你的存储库。

# 第二部分：面向桌面用户的 Ubuntu

# 搭建 Subversion 服务器

尽管 Subversion 是基于 WebDAV 的，因此使用 HTTP 协议进行客户端与服务器之间的基础通信，但你可以在不运行 Subversion 服务器的情况下访问本地 Subversion 存储库（即物理上位于你正在使用的同一台机器上的存储库）。你需要在希望从其他系统访问其存储库的机器上运行 Subversion 服务器。Subversion 服务器有两种常见类型：

- **Apache2**：集成了 Subversion 支持的 Apache Web 服务器。Subversion 和 WebDAV 可以很容易地添加到 Apache 或 Apache2 Web 服务器中，这使得你能够通过 `http://host-name/repository` 或 `https://host-name/repository`（如果你在 Apache2 和 Subversion 中配置了 SSL）通过 Web 访问 Subversion 存储库。本章中的示例了 Apache2 的集成和配置，因为 Apache2 更现代、更强大。

- **svnsned**：一个独立的 Subversion 服务器，允许你通过类似 `svn://host-name/repository` 的 URL 通过 Web 访问你的 Subversion 存储库。`svnns` 二进制文件作为 Subversion 软件包的一部分安装。

这两个服务器并不互斥，可以很容易在同一台机器上同时运行，如果配置得当，可以提供对同一个存储库的访问。接下来的章节将解释如何配置每一个服务器，以访问你在之前的几节中设置并填充的示例存储库。

# 配置 Apache2 支持 Subversion

配置 Apache2 Web 服务器以支持 Subversion 非常简单，只需要安装并集成正确的 Apache2 模块、配置该模块，并创建控制存储库访问的身份验证文件。

安装 Apache2 Web 服务器的 Subversion 支持在本章较早前的“安装 Subversion”节中描述过，并通过使用 Synaptic 软件包管理器或 `apt-get` 工具安装 `libapache2-svn` 软件包来完成。与 Apache2 集成的 Subversion Apache2 Web 服务器由文件 `/etc/apache2/mods-available/dav_svn.conf` 加载。该模块的配置文件是 `/etc/apache2/mods-available/dav_svn.conf`。

在安装 Apache2 Web 服务器的 Subversion 支持后，使用 `sudo` 编辑此文件并...

