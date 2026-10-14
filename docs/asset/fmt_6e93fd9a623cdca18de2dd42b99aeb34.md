
Subversion（`http://subversion.apache.org`）是一个极其流行的源码控制系统。除了强大和丰富的命令集外，Subversion 的流行之处在于它是 WebDAV（Web 分布式创作与版本控制），这是一个基于 Web 的协议，允许你在任何 Web 浏览器中查看和访问 Subversion 仓库。这包括从你的 Web 浏览器拖放文件到桌面以进行检出（`checkout`），反之亦然以进行提交（`check`）。正如你将在后续章节中看到的，设置 Subversion 仓库并将其集成到你的 Web 服务器是非常简单的，就像 Subversion 在桌面或命令行中使用一样简单。

# 提示

设置 Subversion 的另一种方法是通过 SSH（安全外壳）访问其仓库。关于以这种方式设置 Subversion 的极佳解释，请参阅 `www.startupto.com/server-subversion/setting-up-svn`。它讨论了在 CentOS 而非 Ubuntu 上安装 Subversion，初始安装步骤之后，指令是不取决于发行版的。■

# 安装 Subversion

你可以使用第 19 章中描述的任何命令安装 Subversion。在安装 Subversion 时，我通常会安装以下软件包，并非所有都是必需的。我对列表中每个包的理由遵循该列表中的包名：

- `libapache2-svn`（可选）：只有当你想要通过你的 Web 服务器访问一个 Subversion 仓库时，此包才是必需的。选择此项会导致 Apache2 Web 服务器和相关文件安装到你的系统中。我总是发现能够通过 Web 访问我的仓库非常方便，可以一次性配置好一切，而且 Apache2 消耗的额外磁盘空间总是值得的；不过，你也可以以后再添加。请参见第 29 章“设置 Web 服务器”获取有关手动安装不同版本的 Apache Web 的信息。

- `rapidsvn`, `esvn` 或 `ksvn`（可选）：Subversion 的图形客户端。只有在你想要使用图形客户端时才必要。`rapidsvn` 客户端非常流行，是一个 GNOME 客户端。`esvn` 客户端使用 Qt 图形界面，因此在 GNOME 或 KDE 桌面没有任何负担。`ksvn` 客户端是 KDE 客户端，因此要求在系统中安装 KDE 库，但它是唯一接受命令行参数的 Subversion 客户端。然而，如果你想将图形化 Subversion 客户端集成到 Firefox 中以处理 `svn:URL`，`ksvn` 客户端会很有用。请参见标题为“在 Firefox 中处理 svn:URL”的侧边栏。

- `subversion`（强制）：这是 Subversion 的核心包，提供了从命令行使用 Subversion 所需的一切。

887

## 第二部分：面向桌面用户的 Ubuntu

# 提示

在安装 Subversion 时，你可能发现安装 `subwoofer` 工具也很有帮助。它提供了几个在用户之间共享 Subversion 的工具。然而，如果你尚未在系统上安装邮件服务器，选择此包会导致 `sendmail` 服务器和相关文件被安排安装。我更倾向于 Postfix 邮件送器，所以我总是安装并配置你的系统。

一旦安装完成，你就准备好使用仓库了，如果你安装了 `libapache2-svn`，请配置 Apache2 以支持 Subversion。

第 19 章。

# 设置 Subversion 仓库

创建 Subversion 仓库是通过 `svnadmin` 命令完成的，该命令创建组成 Subversion 仓库的目录结构。该命令接受一个参数，即你希望创建 Subversion 仓库的目录名称。

创建 Subversion 仓库时需要记住的一点是，由于 Subversion 依赖于 WebDAV，而 WebDAV 依赖于 HTTP 协议，你的 Subversion 仓库必须由通过该协议通信的用户组所有。在 Ubuntu 上，这是 `www-data` 用户和 `www-data` 组。

# 提示

如果你创建一个名为 `svn` 的 Subversion 仓库并计划通过该名称通过 Web 服务器导出，你不能在 Web 服务器的 DocRoot 目录中创建它。你将在本节后面看到在 Apache 的配置文件中指定 Subversion 仓库的完整路径。尝试使用位于用户 DocRoot 目录的名为 `svn` 的仓库将导致 301 永久移动（`http://server-name`）错误，这并不直观。

例如，要在 `/var/svn` 目录创建 Subversion 仓库，你需要执行以下命令：

```
$ sudo svnadmin create /var/svn
```

在提供密码后，`svnadmin create` 命令将创建你的仓库并填充它所需的子目录，所有目录都属于该用户和组。你可以通过列出指定目录的内容来验证这一点，如下例所示：

```
$ ls -l /var/svn
total 28
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 conf
```

848

## 第 23 章：在 Ubuntu 上进行软件开发

```
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 dav
drwxr-xr-x 5 www-data www-data 4096 2010-01-29 12:31 db
-r--r--r-- 1 www-data www-data 2 2010-01-29 12:31 format
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 hooks
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 locks
-rw-r--r-- 1 www-data www-data 229 2010-01-29 12:31 README.txt
```

当然，一个空的 Subversion 仓库并不十分有趣。接下来的部分将解释如何将一个已经拥有源代码的项目添加到你的仓库中。

## 将项目导入到 Subversion 仓库

Subversion 仓库简单来说就是存放不同项目差异的文件和目录的“捕手套”。你可以直接将现有文件提交到 Subversion 仓库，但为每个项目使用独立的层级结构进行提交会更好。

要将一个项目提交到 Subversion，首先要删除所有非源文件，如目标文件、中间文件、二进制文件等。接下来，你只需使用 `svn import` 命令将项目导入 Subversion 即可，如下例所示，我们导入了一个包含标准 C 程序“Hello, World!”的项目：

```
$ svn import file:///var/svn/hello -m "Creating hello project"
Authentication realm: <http://192.168.6.90:80> Subversion Repository
Password for 'vwh':
Adding
hello.c
```

`svn import` 命令的参数是：你想要导入的项目、你希望创建项目所在的 Subversion URL，以及 `-m`（`message`）选项，后面跟着一个用引号括起来的字符串，该字符串包含项目的初始提交信息。当然，`-m` 选项是可选的，但它可以节省时间，因为否则你必须在 `svn` 命令为你启动的文本编辑器中输入此消息。

一旦你创建了项目或向 Subversion 提交了任何文件，就可以使用 `svn list` 命令显示仓库的内容，如下例所示，示例使用了 `-R` 选项来递归显示仓库内容：

```
$ svn list -R file:///var/svn
hello/
hello.c
```

你会注意到这个示例使用了以 `file://` 开头的 URL，这提供了对本地仓库的访问。在当前阶段这是必要的，因为你还没有启动 Subversion 服务器，所以所有 URL 必须相对于当前文件系统。尝试使用任何基于 Web 的 URL 访问你的 Subversion 仓库将导致此处显示错误信息，错误信息为 `svn: PRPOFIND OF '/svn': could not connect to server`（如果你没有运行 Web 服务器）或 `svn: PRPOFIND OF '/svn": 405 Method Not Allowed`（如果你运行了 Web 服务器但没有可用的 Subversion）。下一节将解释为 Ubuntu 系统提供的两种 Subversion 服务器，以及如何配置它们以便从其他机器访问你的仓库。

## 设置 Subversion 服务器
