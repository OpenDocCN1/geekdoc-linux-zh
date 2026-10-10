

- `/usr/bin` — Apache 软件包中的部分实用程序放置在此处——例如，`htpasswd` 程序，用于生成认证密码文件。
- `/var/log/httpd` — 服务器日志文件放置在此目录中。默认情况下，存在两个重要的日志文件（以及其他若干文件）：`access_log` 和 `error_log`。不过，你可以定义任意数量的包含各种信息的自定义日志。有关更多详细信息，请参阅本章稍后的“日志记录”部分。
- `/usr/src/redhat/SOURCES/` — 此目录可能包含一个压缩归档文件，其中包含 Apache 的源代码，在某些情况下还包含源代码补丁。必须安装了 Apache 的 SRPM 才能创建这些文件。

当 Apache 运行时，它还会在 `/var/run/` 目录中创建文件 `httpd.pid`，其中包含 Apache 父进程的进程 ID。

> **注意**  
> 如果你正在升级到更新版本的 Apache，RPM 不会覆盖你当前的配置文件。RPM 会移动你当前的文件，并为它们添加扩展名 `.rpmnew`。例如，`srm.conf` 会变成 `srm.conf.rpmnew`。

## 自行构建源代码

获取 Apache 源代码有几种方法。Fedora 提供包含 Apache 源代码的 SRPM，其中包含使其更好地兼容 Fedora 发行版的补丁。Fedora 中最新且稳定的二进制版本可以通过 `Pirut` 安装，或者通过安装来自 Fedora 源存储库的源代码 RPM 来安装。当你安装其中一个 SRPM 时，会在 `/usr/src/redhat/SOURCES/` 中创建一个包含 Apache 源代码的压缩归档文件。

获得 `tar` 文件后，必须将其解压到临时目录中，例如 `/tmp`。解压此 tar 文件会创建一个名为 `apache_version_number` 的目录，其中 `version_number` 是你下载的版本（例如，`apache_1.3.21`）。

你也可以直接从 `http://www.apache.org/` 下载源代码。在本文写作时，最新版本 `2.2.6` 是一个 6MB 的压缩磁带归档文件，而 `2.0` 之前最新的 Apache 版本是 `1.3.31`。虽然许多网站继续使用旧版本（出于脚本和其他兼容性原因），但许多新网站正在迁移到或开始使用最新的稳定版本。

> **提示**  
> 与许多以源代码形式分发给 Linux 和其他类 Unix 操作系统的软件包一样，提取源代码会产生一个包含 `README` 和 `INSTALL` 文件的目录。在尝试构建和安装软件之前，请务必阅读 `INSTALL` 文件。

要以简单的方式构建 Apache，请在刚刚创建的目录中运行 `./configure` 脚本。你可以提供 `--prefix` 参数，将其安装到默认目录（即 `/usr/local/apache/`）之外的其他目录。使用以下命令：

```bash
# ./configure --prefix=/preferred/directory/
```

这会生成用于编译服务器代码的 makefile。

接下来，键入 `make` 以编译服务器代码。编译完成后，以 root 身份键入 `make install` 来安装服务器。现在，你可以通过配置文件来配置服务器。有关更多信息，请参阅本章稍后的“运行时服务器配置设置”部分。

> **提示**  
> 从源代码安装新版本 Apache 的一种更安全方法是使用 `ln` 命令，为现有文件位置（在本章前面“从 RPM 安装”部分中列出）创建指向新文件位置的符号链接。这种方法更安全，因为默认安装位置与 RPM 安装文件时使用的不同。如果未使用此安装方法，可能导致系统启动时 Web 服务器进程未自动启动。
>
> 安装新版本 Apache 的另一种安全方法是首先备份重要的配置目录和文件（如 `/etc/httpd`），然后使用 `rpm` 命令移除服务器。然后你可以安装并测试新版本，并在需要时轻松恢复原始服务器和设置。
>
> 强烈建议在你真正了解系统启动时发生的情况之前，使用 Fedora 的 RPM 版本的 Apache。从源代码安装 Apache 时没有“卸载”选项！

## 构建和安装后的 Apache 文件位置

如果你从源代码构建服务器，文件将放置在 `/usr/local/apache`（或你用 `--prefix` 参数指定的目录）的各个子目录中。

以下是 Apache 使用的目录列表及其用途的简要说明：

- `/usr/local/apache/conf/` — 其中包含几个子目录以及 Apache 配置文件 `httpd.conf`。要了解有关配置文件的更多信息，请参阅本章稍后的“编辑 httpd.conf”部分。
- `/usr/local/apache/` — `cgi-bin`、`icons` 和 `htdocs` 子目录分别包含 CGI 程序、标准图标和默认 HTML 文档。
- `/usr/local/apache/bin/` — 可执行程序放置在此目录中。
- `/usr/local/apache/logs/` — 服务器日志文件放置在此目录中。默认情况下，有两个日志文件——`access_log` 和 `error_log`——但你可以定义任意数量的包含各种信息的自定义日志（请参阅本章稍后的“日志记录”部分）。Fedora 安装的 Apache 日志的默认位置是 `/var/log/httpd`。

## Apache 入门快速指南

使用 Fedora 设置、测试网页并启动 Apache 只需几个步骤即可完成。首先，确保你的系统上已安装 Apache。可以在安装过程中选择它，或者安装服务器及相关 RPM 文件。

接下来，通过编辑（以 root 身份）系统 `/var/www/html` 目录下的 `index.html` 文件来为你的系统设置主页。在开始之前，请对原始页面或 www 目录制作备份副本，以便在必要时可以将 Web 服务器恢复为默认状态。

通过服务命令使用关键字 `httpd` 和 `start`（再次以 root 身份）来启动 Apache，如下所示：

```bash
# service httpd start
```

你也可以使用 `/etc/rc.d/init.d/` 目录下的 `httpd` 脚本，如下所示：

```bash
# /etc/rc.d/init.d/httpd start
```

然后，你可以运行一个喜欢的浏览器，并在 URL 中使用 `localhost`、你的系统主机名或其互联网协议（IP）地址来检查你的主页。例如，使用 `links` 文本浏览器时，使用如下命令行：

```bash
# links http://localhost/
```

出于安全原因，如果你的主机连接到互联网或公司内网，你不应该以 root 身份启动和运行 Apache。幸运的是，无论 Apache 如何启动（通过 `/etc/httpd/httpd.conf` 中的 `user` 和 `group` 设置），它都设置为以用户和组 `apache` 运行。尽管有这种安全的默认设置，Apache 应该由在 `/etc/passwd` 中定义的用户 `apache` 启动和管理，其定义为：

```
apache:x:48:48:Apache:/var/www:/sbin/nologin
```

当你满意于你的网站后，使用 `setup`（选择 Services）或 `ntsysv`（选择 httpd）命令来确保 Apache 正确启动。

现在是第一次启动 Apache 的时候了。接下来的章节展示了如何启动和停止 Apache，或者配置 Fedora 在引导时是否启动 Apache。

### 手动启动 Apache 服务器

你可以在基于文本的控制台或 X 终端窗口的命令行中启动 Apache，并且你必须拥有 root 权限才能这样做。服务器守护进程 httpd 识别几个你可以使用的命令行选项，以设置一些默认值，例如指定 httpd 从何处读取其配置指令。Apache httpd 可执行文件还理解其他选项，使你能够选择性地使用其配置文件的一部分，指定实际服务器和支持文件的不同位置，使用不同的配置文件（可能用于测试），并将启动错误保存到特定日志。-v 选项会导致 Apache 打印其开发版本并退出。-V 选项显示服务器编译时生效的所有设置。

-h 选项会打印以下服务器使用说明（假设你以 root 身份运行该命令）：

```bash
# httpd -h

Usage: httpd [-D name] [-d directory] [-f file]
  [-C "directive" | -c "directive"]
  [-k start|restart|graceful|stop]
  [-v] [-V] [-h] [-l] [-L] [-t]

Options:
 -D name        : define a name for use in <IfDefine name> directives
 -d directory   : specify an alternate initial ServerRoot
 -f file         : specify an alternate ServerConfigFile
 -C "directive" : process directive before reading config files
 -c "directive" : process directive after reading config files
 -e level        : show startup errors of level (see LogLevel)
 -E file         : log startup errors to file
 -v              : show version number
 -V              : show compile settings
 -h              : list available command-line options (this page)
 -l              : list compiled in modules
 -L              : list available configuration directives
 -t -D DUMP_VHOSTS : show parsed settings (currently only vhost settings)
 -t              : run syntax check for config files
```

其他选项包括列出 Apache 的*静态模块*，或者特殊的内置独立服务器部分，以及可用于模块的选项。这些选项被称为*配置指令*，是控制静态模块如何工作的命令。请注意，Apache 还包含近 50 个*动态模块*，即服务器可以在运行时选择加载和使用的软件部分。

-t 选项用于检查你的配置文件。在重启服务器之前运行此检查是个好主意，特别是如果你已经对配置文件进行了更改。

