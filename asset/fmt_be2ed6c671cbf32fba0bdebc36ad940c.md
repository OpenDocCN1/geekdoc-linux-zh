
- `/usr/bin/`—可执行程序放置在此目录中。这包括服务器可执行文件本身以及各种工具。
- `/usr/bin/`—Apache 软件包中的某些工具放置在此处——例如用于生成身份验证文件的 `htpasswd` 程序。
- `/var/log/httpd`—日志文件放置在此目录中。默认情况下，有两个重要的日志文件（在其他几个文件之外）：`access_log` 和 `error_log`。不过，你可以定义任意数量的自定义日志，包含各种信息。更多详情请参阅本章的“日志（Logging)”部分。
- `/var/src/redhat/SOURCES/`—此目录可能包含一个包含 Apache 源代码的 tar 归档，在某些情况下还包含源码的补丁。你必须安装了 Apache SRPM 才能创建这些文件。

当 Apache 运行时，它还会在 `/var/run/` 下创建 `httpd.pid` 文件，其中包含 Apache 父进程的进程 ID（PID）。

> 注意
> 如果你正在升级到更高版本的 Apache，RPM 不会覆盖你当前的配置文件。RPM 会移动你当前的文件并在其后添加扩展名 `.rpmnew`。例如，`httpd.conf` 会变成 `httpd.conf.rpmnew`。

# 自行构建源码

有多种方法获取 Apache 源码。Fedora 项目提供了包含 Apache 源代码的 RPM，其中包含了为了使其在 Fedora Core 发行版上运行得更好的补丁。Fedora 最新的、稳定的二进制版本可以通过更新命令使用 RPM 软件包进行安装，或者从 Fedora 的源码仓库安装服务器 RPM（访问 http://fedora.redhat.com 然后点击 Download（下载）链接）。当你安装其中其中一个 RPM 时，在 `/usr/src/redhat/SOURCES/` 中会创建一个包含 Apache 源码的 tar 归档。

你也可以直接从 http://apache.org/ 下载源码。本文撰写时的最新版本（2.0.50）是一个 6MB 的压缩带归档，而 Apache 最新的 2.0 之前的版本是 1.3.31。许多网站选择旧版本（出于脚本和其他兼容性原因），许多新网站正在迁移到或从最新的稳定版开始使用。

获取 tar 文件后，你必须在临时目录（如 `/tmp`）中将其解压。解压此文件会创建一个名为 `apache_version_number` 的目录，其中 `version_number` 是你下载的版本（例如，`apache_1.3.21`）。

编译源码有两种方法——通过编辑 makefile 模板（至少对我们这些使用多年 Apache 的人来说是这是旧的、熟悉的方法），以及另一种是使用 `configure` 脚本的新型简单方法。你将首先看到如何用简单方法从源码构建 Apache。`configure` 脚本提供了一种根据你的系统自动配置源码的方法。然而，在构建和安装 Apache 之前手动编辑配置文件，可以对软件的安装方式以及在 Apache 中构建哪些功能或特性提供更多控制。

与在 Linux 和其他类 Unix 操作系统上以源码形式分发的许多软件包一样，提取源码会得到一个包含 `README` 和 `INSTALL` 文件的目录。在尝试构建和安装软件之前，务必仔细阅读 `INSTALL` 文件。

# 使用 ./configure 构建 Apache

要用简单方法构建 Apache，请刚创建的目录中运行 `./configure` 脚本。你可以为其提供 `--prefix` 参数，将其安装在默认目录（`/usr/local/apache/`）之外的目录中。使用此命令：

```bash
# ./configure --prefix=/preferred/directory/
```

这会生成用于编译服务器代码的 makefile。

接下来，输入 `make` 来编译服务器代码。编译完成后，以 root 身份输入 `make install` 来安装服务器。你现在可以通过配置文件配置服务器了。更多信息请参阅本章后部分的“运行时服务器配置设置（Runtime Server Configuration Settings）”部分。

从源码安装新版本 Apache 的更安全方法是使用 `-ln` 命令为现有文件位置（已在本章前面的“从 RPM 安装”中列出）创建符号链接，将它们指向文件的新位置。这种方法更安全，因为默认安装位置与 RPM 安装文件时使用的位置不同。不使用这种安装方法可能会导致你的 Web 服务器进程在系统启动时无法自动启动。

另一种安装新版本 Apache 的安全方法是备份任何重要的配置目录和文件（例如 `/etc/httpd`），并使用 `rpm` 命令删除服务器。然后你可以安装并测试新版本，并在需要时恢复原始服务器和设置。

强烈建议在你真正了解系统启动时发生了什么之前，一直使用 Fedora 的 Apache RPM 版本。从源码安装 Apache 时，没有“卸载”选项。

# 构建和安装后的 Apache 文件位置

如果你从源码构建服务器，文件将位于 `/usr/local/apache`（或你用 `--prefix` 参数指定的任何目录）的各个子目录下。在 1.3.4 版本之前，文件被放置在 `/usr/local/etc/httpd`。

以下是 Apache 使用的目录列表以及对其用途的简要注释：

- `/usr/local/apache/conf`—包含几个子目录和配置文件 `httpd.conf`。了解更多信息请参阅本章后面的“编辑 httpd.conf”部分。
- `/usr/local/apache`—`cgi`、`icons` 和 `htdocs` 子目录分别包含 CGI 程序、图标和默认文档。
- `/usr/local/apache/bin`—可执行程序放置在此目录。
- `/usr/local/apache/logs`—服务器日志文件放置在此目录。默认情况下，有两个日志文件——`access_log` 和 `error_log`，但你可以定义任意数量包含各种信息的自定义日志（参见本章后面的“日志”部分）。通过 Fedora 安装的 Apache 日志默认位置为 `/var/log/httpd`。

# Apache 快速指南

使用 Fedora 设置、测试网页和启动 Apache 只需几个步骤。首先，确保你的系统已安装 Apache。你可以在安装时选择它，或者安装服务及相关的 RPM 文件（如有需要请参考 7 章）。

接下来：以 root 身份编辑系统 `/var/www/html/` 目录下名为 `index.html` 的文件来设置主页。在开始之前，备份原始页面或 www 目录，以便在需要时恢复服务器的默认状态。

再次以 root 身份使用 `service` 命令配合 `httpd` 和 `start` 关键字启动 Apache：

```bash
# service httpd start
```

你也可以使用 `/etc/rc.d/init.d/` 目录下的 `httpd` 脚本，如下：

```bash
# /etc/rc.d/init.d/httpd start
```

现在你可以运行喜欢的浏览器并使用 localhost、系统主机名或其网协议（IP）地址来检查主页。例如，使用 `links` 浏览器，可以使用命令行：

```bash
# links http://localhost/
```

出于安全考虑，如果你的主机连接到互联网或互联网连接，不应以 root 身份运行 Apache。幸运的是，Apache 被设置为始终以 `apache` 用户和组身份运行（通过 `/etc/httpd/httpd.conf` 中的 `User` 和 `Group` 设置）。

# 启动与停止 Apache

出于安全考虑，Apache 应该由用户 `apache` 启动并管理，该用户定义在 `/etc/passwd` 中：

`apache:x:48:48:Apache:/var/www:/sbin/nologin`

在你对网站表示满意后，使用 `setup`（选择 Services）或 `ntsys`（选择 `httpd`）命令来确保 Apache 正常启动。

此时，你已经安装了带有默认配置的 Apache 服务器。Fedora 在 `/var/www/html/usage` 目录 下提供了一个名为 `index.html` 的默认首页作为测试。运行 Apache 的正确方法是设置系统初始化，让服务器在启动、网络配置以及任何防火墙配置完成之后运行。有关 Fedora 如何启动的更多详细信息，请参阅第 15 章“自动化任务”。

现在是时候首次启动了。接下来的章节将展示如何启动和停止 Apache，或者配置 Fedora 在启动时启动或不启动 Apache。

# 手动启动 Apache 服务器

你可以从文本控制台的命令行或 X 终端窗口启动 Apache，你必须拥有 root 权限才能操作。服务器守护进程 `httpd` 识别几个你可以使用的命令行选项，用于设置某些默认值，例如指定 httpd 从何处读取配置指令。Apache `httpd` 可执行文件还理解其他选项，允许你选择配置文件的部分、指定实际服务器及支持文件的不同位置、使用不同的配置文件（可能用于测试）、以及将启动错误保存到特定日志。`-v` 选项导致 Apache 打印其开发版本并退出。`-V` 选项显示服务器编译时生效的所有设置。
