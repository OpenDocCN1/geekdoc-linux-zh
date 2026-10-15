
您可以使用 `configure` 脚本的选项有很多。表 12-2 显示了可用的常见配置选项。

### 表 12-2 Configure 脚本的常见选项

| 选项 | 含义 |
|---|---|
| `--help` | 打印此消息 |
| `--version` | 打印创建 `configure` 的 `autoconf` 版本 目录和文件名。 |
| `--prefix=prefix` | 在 `prefix` 中安装与体系结构无关的文件 `[/usr/local/apache2]` |
| `--disable-feature` | 不包含 `FEATURE`（与 `--enable-FEATURE=no` 相同） |
| `--enable-feature[=arg]` | 包含 `feature[arg=yes]` |
| `--with-package[=arg]` | 使用 `package [arg=yes]` |
| `--without-package` | 不使用 `package`（与 `--with-package=no` 相同） |
| `--enable-modules=module-list` | 启用一个或多个命名模块 |
| `--enable-mods-shared=module-list` | 以共享模块的形式启用一个或多个命名模块 |
| `--disable-access` | 基于主机的访问控制 |
| `--disable-auth` | 基于用户的访问控制 |
| `--disable-include` | 服务器端包含 `SSI` |
| `--disable-http` | `HTTP` 协议处理 |
| `--disable-mime` | 文件扩展名到 `MIME` 的映射 |
| `--disable-log-config` | 日志配置 |
| `--enable-vhost-alias` | 批量托管模块 |
| `--disable-negotiation` | 内容协商 |
| `--disable-dir` | 目录请求处理 |
| `--disable-imap` | 内部图像映射 |
| `--disable-actions` | 请求上的操作触发 |
| `--enable-speling` | 修正常见的 `URL` 拼写错误 |
| `--disable-userdir` | 用户请求的映射 |
| `--disable-alias` | 请求的翻译 |
| `--enable-rewrite` | 启用 `URL` 重写规则 |
| `--disable-so` | `DSO` 功能 |
| `--enable-so` | `DSO` 功能 |

### 表 12-2 继续

| 选项 | 含义 |
|---|---|
| `--disable-env` | 清除/设置 `ENV` 变量 |
| `--enable-mime-magic` | 自动确定 `MIME` 类型 |
| `--enable-cern-meta` | `CERN` 类型元文件 |
| `--enable-expires` | `Expires` 头控制 |
| `--enable-headers` | `HTTP` 头控制 |
| `--enable-usertrack` | 用户会话跟踪 |
| `--enable-unique-id` | 每个请求的唯一 `ID` |
| `--disable-setenvif` | 基于头的 `ENV` 变量 |
| `--enable-tls` | `TLS/SSL` 支持 |
| `--with-ssl` | 使用特定的 `SSL` 库安装 |
| `--with-mpm=MPM` | 选择 `Apache` 使用的进程模型：`MPM={beos threaded prefork mpm_os2 perchild}` |
| `--disable-status` | 进程/线程监控 |
| `--disable-autoindex` | 目录列表 |
| `--disable-asis` | 原样文件类型 |
| `--enable-info` | 服务器信息 |
| `--enable-suexec` | 为生成的进程设置 `UID` 和 `GID` |
| `--disable-cgid` | `CGI` 脚本 |
| `--enable-cgi` | `CGI` 脚本 |
| `--disable-cgi` | `CGI` 脚本 |
| `--enable-cgid` | `CGI` 脚本 |

这些选项中的大多数对于大多数站点来说不是必需的。通常，您只需要指定 `--prefix` 选项以及启用或禁用一个或多个模块的任何选项。例如，假设您不想在系统上安装 `CGI` 模块。您可以使用 `--disable-cgi --disable-cgid` 选项运行 `configure` 脚本以禁用 `CGI` 支持。同样，要禁用服务器端包含 `SSI` 支持，您可以使用 `--disable-include` 选项。

## 初始配置后配置 Apache 源代码

在使用 `configure` 脚本配置 `Apache` 之后，您可以使用 `config.status` 脚本代替 `configure` 来满足任何后续配置需求。通过使用 `config.status` 脚本，您可以重用之前的配置并添加或减去新选项。

例如，假设您使用以下命令配置了 `Apache`：

```
./configure --prefix=/usr/local/apache --disable-cgi --disable-cgid
```

然后，几天后您决定禁用 `SSI`。您现在可以使用以下命令：

```
./config.status --disable-include
```

当您重新编译 `Apache` 时，`CGI` 模块将不会被包含，因为 `./config.status` 存储了您之前使用 `configure` 脚本指定的选项。

## 编译和安装 Apache

在使用 `configure` 脚本配置 `Apache` 源代码后，请按照以下步骤编译和安装 `Apache`：

- 1. 运行 `make` 命令编译源代码。
- 2. 运行 `make install` 命令将 `httpd` 和支持文件安装到您使用 `--prefix` 选项指定的目录中。您可以在本章稍后“Apache 目录结构”部分看到 `Apache` 设置的目录结构。

## 从二进制包安装 Apache

您可以从 `www.apache.org/dist/httpd/binaries` 目录下载适用于您系统的 `Apache` 二进制文件。下载最新版本并将压缩文件提取到临时目录。要确定如何在特定平台上安装二进制文件，您必须阅读 `INSTALL.bindist` 文件，该文件包含在每个二进制发行版中。

如果您希望为 Linux 系统安装 `Apache` `RPM`（代表 `Red Hat Package Manager`）包，请执行以下操作：

- 1. 转到 `http://rpmfind.net` 并搜索字符串 `Apache` 以定位 `Apache` `RPM` 包。从搜索结果中，找到二进制 `Apache` `RPM` 发行版的最新版本并下载它。
- 2. 以 `root` 身份运行 `rpm -ivh apache_rpm_package.rpm` 命令安装包。例如，要为 `Red Hat Linux`（Intel）系统安装 `apache-2.0.4-i386.rpm`，请运行 `rpm -ivh apache-2.0.4-i386.rpm` 命令。

请参阅下一节以查看 `Apache` 的基本目录结构。

## Apache 目录结构

安装 `Apache` 后，您可以更改到安装 `Apache` 的目录并浏览新目录，以了解 `Apache` 的设置方式。例如，如果在源代码树配置期间使用 `--prefix=/usr/local/apache` 与 `configure` 脚本，`make install` 将创建以下目录结构：

```
/usr/local/apache
|
+---include
+---lib
+---bin
+---conf
+---htdocs
|   |
|   +--manual
|       |
|       +--developer
|       +--howto
|       +--images
|       +--misc
|       +--mod
|       +--platform
|       +--programs
|       +--search
```

```
|   +--vhosts
| 
+---icons
|   |
|   +---small
| 
+---logs
+---cgi-bin
```

以下列表简要描述了 `Apache` 目录结构中的每个目录：

- `/include` — 包含所有 `C` 头文件（`include` 文件），仅在您开发与 `Apache` 集成的 `Web` 应用程序时需要，或在您想使用需要头文件的第三方软件与 `Apache` 集成时需要。在生产服务器上，您可以在安装后删除此目录。
- `/lib` — 存放 `Apache` 可移植运行时间（`APR`）库文件。这些文件对于运行 `Apache` 以及其他支持实用程序（如 `ab`）是必需的。
- `/bin` — 包含表 12-3 中显示的程序。
- `/conf` — 存放 `Apache` 的配置文件，列在表 12-4 中。
