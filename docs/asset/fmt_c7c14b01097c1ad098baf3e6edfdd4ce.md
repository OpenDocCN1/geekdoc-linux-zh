
# `./configure --prefix=/preferred/directory/`

这将生成用于编译服务器代码的 `Makefile`。

接下来，输入 `make` 来编译服务器代码。编译完成后，执行 `make install` 以 root 身份安装服务器。你现在可以通过配置文件来配置服务器。更多信息，请参阅本章后半部分的“运行时服务器配置设置”章节。

> 提示
> 从源码安装新版本 Apache 的安全方法是使用 `ln` 命令为现有的文件位置（列在本章较早之前的“从 RPM 安装”小节中）创建符号链接，指向它们的新位置。这种方法更安全，因为默认安装位置与 RPM 安装文件时使用的位置不同。如果不使用此方法，可能会导致你的 Web 服务器进程在启动时不会自动启动。
>
> 另一种安装新版本 Apache 的方法是备份任何重要的目录和文件（如 `/etc/httpd`），并使用 `rpm` 命令删除服务器。然后你可以安装并测试新版本，如果需要，可以轻松恢复你的原始服务器和设置。
>
> 强烈建议你使用 Fedora 的 RPM 版本 Apache，直到你真正了解系统启动时发生了什么。在从源码安装 Apache 时可以使用“uninstall（卸载）”选项！

## 编译和安装后的 Apache 位置

文件被放置在 `/usr/local/apache` 的各个目录中（如果你从源码构建服务器，则为你通过 `--prefix` 指定的目录）。

以下是 Apache 使用的目录列表及其用法的简要说明：

- `/usr/local/apache/conf`——这包含几个子目录和 Apache 配置文件 `httpd.conf`。请参本章后半部分的“编辑 httpd.conf”章节以获取更多关于配置的信息。
- `/usr/local/apache`——`cgi-bin`、`icons` 和 `htdocs` 子目录分别包含 CGI 程序、标准图标和默认的 HTML 文档。
- `/usr/local/apache/bin`——可执行程序放置在此目录中。
- `/usr/local/apache/logs`——服务器日志文件放置在此目录中。默认情况下有两个日志文件——`access_log` 和 `error_log`——但你可以定义任意数量的包含各种信息的自定义日志（参见本章后半部分的“日志”章节）。Fedora 安装的 Apache 日志默认位置为 `/var/log/httpd`。

## Apache 快速上手指南

在 Fedora 中设置、测试网页和启动 Apache 仅需几步即可完成。确保你的系统已安装 Apache。你可以在安装期间选择它，或者安装服务器及相关的 RPM 文件。接下来，通过编辑（以 root 身份）系统 `/var/http/html` 目录下的名为 `index.html` 的文件为你的系统设置主页。在开始之前，对原始页面或 `www` 目录制作备份副本，以便在必要时将你的 Web 服务器恢复到默认状态。

使用 `service` 命令配合 `httpd` 关键字，如下所示启动 Apache（再次，以 root 身份操作）：

```bash
# service httpd start
```

你也可以使用 `/etc/rc.d/init.d/` 目录下的 `httpd` 脚本，如下所示：

```bash
# /etc/rc.d/init.d/httpd start
```

你可以通过运行喜欢的浏览器并在 URL 中使用 `localhost`、你的系统主机名或其网协议 (IP) 地址来检查主页。例如，使用 links 文本浏览器，可以使用如下命令行：

```bash
# links http://localhost/
```

出于安全考虑，如果你的主机连接到互联网或公司内网，你不应该以 root 身份启动和运行 Apache。坦地说，无论如何启动，Apache 都会以特定的用户和组运行（通过 `/etc/httpd.conf` 中的用户和组设置）。尽管有此安全默认，Apache 应该由用户 apache 启动和管理，该用户在 `/etc/passwd` 中定义为：

```
apache:x:48:48::/var/www:/nologin
```

一旦你对网站满意，请使用 `setup`（选择 Services）或 `service`（选择 httpd）命令确保 Apache 已正常启动。

## 启动和停止 Apache

此时，你已经按照默认配置安装了 Apache。Fedora 在 `/var/www/html/` 目录下提供了一个名为 `index.html` 的默认主页作为测试。运行 Apache 的正确方法是将系统初始化设置为在启动后、网络配置以及任何防火墙配置之后运行服务器。有关 Fedora 如何启动的更多信息，请参阅第 11 章“自动化任务”。

现在是第一次启动 Apache 了。接下来的章节将展示如何启动和停止 Apache，或者配置 Fedora 在启动时启动或不启动 Apache。

### 手动启动 Apache 服务器

你可以从基于文本的控制台或 X 终端窗口的命令行启动 Apache，并且必须拥有 root 权限才能操作。服务器守护进程 `httpd` 识别几个你可以使用的命令行选项，用于设置某些默认值，例如指定 `httpd` 从何读取其配置指令。Apache 可执行文件还提供了其他选项，允许你选择配置文件的部分、指定实际服务器和支持文件的不同位置，以及使用不同的配置文件。

```bash
# httpd [options]
用法: httpd [options]

  -h, --help             显示帮助信息

  -b, --backlog=N        设置连接的队列长度

  -C, --config-file=FILE  使用指定的配置文件

  -D, --module=MODULE     定义要加载的模块

  -e, --encoding=CHAR    输出字符编码

  -E, --errorlog=FILE     指定的错误日志

  -F, --foreground       保持 httpd 在前台运行

  -f, --file=FILE        使用指定的配置文件

  -G, --group=GROUP       显示组

  -k, --command=COMMAND   start | stop | reload | graceful

  -L, --pidfile=FILE      指定的 pid 文件

  -l, --loglogfile=FILE  指定的访问日志

  -m, --logformat=F      指定的访问日志格式

  -M, --module=MODULE     显示已加载的模块

  -n, --name=NAME         显示服务器名称

  -N, --certfile=FILE     指定的证书文件

  -S, --sslcertfile=FILE  指定的密钥文件

  -p, --prefix=PREFIX     指定的前缀

  -q, --quiet            静默模式

  -r, --root=ROOT         指定的根目录

  -s, --statusfile=FILE  指定的状态文件

  -t, --test-only        仅测试语法并退出

  -u, --timeout=SEC      设置超时秒数

  -v, --version=STR      显示版本号

  -V, --version-full     显示完整版本

  -w, --workworkers=N     设置工作进程数量

  -X, --mpm=MODULE       选择 MPM 模块
```
