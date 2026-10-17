
你可能还会发现，安装 `subversion` 时安装 `subversion-tools` 包也很有用。此包提供了几个工具，用于在用户之间共享 `subversion` 存储库，以及将现有的源代码目录更高级地导入 `subversion` 中。然而，如果你已经在系统中安装了邮件服务器，选择此包进行安装将导致邮件服务器及相关文件被计划安装到你的系统中。该邮件服务器是 `exim`，所以我没问题，但你的情况可能因人而异。请参阅第 27 节“设置邮件服务器”获取关于 Ubuntu 上可用的不同邮件服务器以及为什么 `exim` 是一个良好选择的信息。

并从弹出菜单中选择“标记安装（Mark for Installation）”来选择这些每个包进行安装。图 18.24 显示了选择了安装 `subversion` 及其相关包。

该过程取决于你之前在 Ubuntu 系统上安装了哪些软件，你在对话框中选择的内容可能会显示出其他也必须安装的软件包列表，并请求确认。在这些此类对话框中，点击“标记（Mark）”以接受这些相关的（且必需的）包。

一旦你完成了选择，点击 Synaptic 工具栏中的“应用（Apply）”来安装 `subversion` 及其相关包。一旦安装完成，你就可以设置你的存储库了，如果你选了 `libapache2-svn` 包，就可以配置 Apache2 以支持 `subversion`。

![](img/e88880e40d650bfe19d5b6927bd86568_566_0.png)

## 创建 Subversion 存储库

一个空的 Subversion 存储库并没有什么特别有趣的。下一节将解释如何向你的存储库添加项目，以便你能够真正有源代码可以管理。

要创建一个 Subversion 存储库，你使用 `svnadmin` 命令。该命令接受一个参数，即你想创建存储库的路径。创建 Subversion 存储库时需要记住的一点是，它必须由正确的用户和组所有。

要在 `/var/svn` 中创建一个 Subversion 存储库，你将执行：

```
sudo -u www-data svnadmin create /var/svn
```

`svnadmin` 命令创建你的存储库并填充它所需的目录，所有目录都属于 `www-data` 用户。你可以通过列出指定的目录来验证这一点，如下例：

```
ls -l /var/svn
drwxr-xr-x 2 www-data www-data 4096 May 29 12:31 conf
drwxr-xr-x 2 www-data www-data 4096 May 29 12:31 dav
drwxr-xr-x 5 www-data www-data 4096 May 29 12:31 db
-r--r-- 1 www-data www-data 2 May 29 12:31 format
drwxr-xr-x 2 www-data www-data 4096 May 29 12:31 hooks
drwxr-xr-x 2 www-data www-data 4096 May 29 12:31 locks
-r--r-- 1 www-data www-data 229 May 29 12:31 README.txt
```

## 将项目导入 Subversion 存储库

存储库仅仅是构成不同项目的文件和目录的“接球手”。你可以直接将现有的文件提交到 Subversion 存储库，但将每个项目提交到独立的目录层次结构要好得多。

要将项目目录导入 Subversion，首先从该目录中删除所有非源文件，如对象文件、中间文件等。接下来，你只需使用 `svn import` 命令将项目导入到 `subversion`，如下例所示，你导入了一个包含一个 C 程序“Hello, World!”的项目：

![](img/e88880e40d650bfe19d5b6927bd86568_567_0.png)

```
svn import file:///var/svn/hello -m "Creating hello project"
认证域: <http://192.168.6.90:80> Subversion 仓库
'wvh' 的密码: 
正在添加 hello/hello.c
传输文件: 452 字节
已提交至 /var/svn/hello/hello/hello.c
```

`svn import` 命令的参数是你想要导入的项目、你想要创建项目所在仓库的 Subversion URL，以及 `-m`（消息）选项。该选项是一个包含项目初始提交消息的字符串，并被包含在引号内。当然，`-m` 选项是可选的，但它可以为你节省时间，因为否则你将必须在 `svn` 命令为你启动的文本编辑器中输入该消息。

一旦你创建了项目或将任何文件提交到 Subversion，你就可以使用 `svn list` 命令来查看仓库的内容，如下例所示。该示例使用了 `-R` 选项来递归显示仓库的内容：

```
svn list -R file:///var/svn/hello/
hello/hello.c
```

注意，此示例使用了以 `file:///` 开头的 URL，它提供了对本地文件系统的访问。在此时这是必要的，因为你还没有启动 Subversion 服务器，所以所有 URL 必须相对于当前的文件系统。如果尝试使用任何 Web 服务器访问你的 Subversion 仓库，此时将显示错误信息，要么是 `svn: PROPFIND of '/svn': could not connect to server`（如果你没有运行 Web 服务器），或者是 `svn: PROPFIND of '/svn': 405 Not Allowed`（如果你运行了 Web 服务器但没有可用的 subversion 仓库）。下一节将解释在 Ubuntu 系统上提供的两种 Subversion 服务器，以及如何配置其中一个以使你的仓库能够从其他机器进行访问。

## 设置 Subversion 服务器

Subversion 基于 WebDAV，因此使用 HTTP 协议进行基本通信。在客户端和服务器之间，你可以在不运行 Subversion 服务器的情况下访问本地 `subversion` 仓库（即物理上位于你正在使用的机器上的仓库）。但是，你需要在你想要从其他系统访问的那些仓库的机器上运行 Subversion 服务器。常见的 Subversion 服务器有两种类型：

- `Apache2`：集成了对 Subversion 支持的 Apache Web 服务器。Apache 或 Apache2 Web 服务器可以轻松添加对 Subversion 和 WebDAV 的支持，允许你通过类似 `http://host-name/repository` 或 `https://host-name/repository` 的 URL 访问你的 Subversion 仓库（如果你在 Apache2 和 Subversion 中配置了 SSL 支持）。本章示例讨论了 Apache2 的集成和配置，因为 Apache2 是更现代、强大的 Apache Web 服务器。
- `svnserve`：一个独立的 `subversion` 服务器，允许你通过类似 `svn://host-name/repository` 的 URL 访问你的 Subversion 仓库。`svnserve` 二进制文件作为 `subversion` 包的一部分安装。

这些服务器并不互斥，如果配置正确，它们可以轻松在同一台机器上同时运行并访问同一个仓库。接下来的两节将解释如何配置这些服务器，以对你在前面的章节中设置并填充的示例仓库提供访问。

### 配置 Apache2 以支持 Subversion

配置 Apache2 Web 服务器以支持 Subversion 非常简单，只需要安装正确的 Apache 模块、配置该模块并创建一个授予仓库访问权限的身份验证文件。

Apache2 Web 服务器对 Subversion 的支持在本章稍前的“安装 Subversion”部分已描述，通过使用 Synaptic 软件包管理器或 `apt-get` 工具安装 `libapache2-svn` 包来完成。Apache2 Web 服务器对 Subversion 集成的支持通过文件 `/etc/apache2/mods-available/dav_svn.load` 启用。配置文件是 `/etc/apache2/mods-available/dav_svn`。

配置 Apache2 Web 服务器以支持 Subversion 的步骤如下（只需安装正确的 Apache 模块、配置该模块并创建一个授予仓库访问权限的身份验证文件）：

- 通过 `/etc/apache2/mods-available/dav_svn.load` 文件启用 Apache2 Web 服务器对 Subversion 的集成支持。
- 配置文件是 `/etc/apache2/mods-available/dav_svn`。
- 如果你想通过 WebDAV 访问仓库，请编辑文件 `/etc/apache2/mods-available/dav_svn`。
- 使用 `Location` 元素，如果你想通过 Web URL 访问仓库。
