
- Apache 安装目录。默认值为 `C:\Program Files\Apache Group\Apache\`，但你可以更改为 `C:\Apache\` 或其他位置。

- 开始菜单上显示的名称。默认值为 Apache Web Server。

- 安装类型：典型、最小或自定义。

根据你的安装做出选择并继续。Apache 安装程序将一组默认配置文件放在安装目录下的 `conf` 目录中（例如 `C:\Program Files\Apache Group\Apache\conf`）。默认配置文件将包含你在安装过程中指示的自定义信息（如目录位置）。对于 Windows 上的基础安装，不需要额外的配置。如果你修改了配置文件，必须重启 Apache 更改才会生效。务必备份你的原始文件！

除了其他系统目录外，安装程序还会创建默认文档根目录 `htdocs`。Web 服务器的文档根是存放你的 HTML 文档的目录。

接下来，尝试运行 Apache。有两种选项：将 Apache 作为 Windows NT 服务运行，或者从控制台窗口运行 Apache（这是 Windows 95/98 用户唯一选项）。要将 Apache 作为 Windows NT 服务安装并运行，请执行以下操作：

- 1. 从“开始”菜单中选择“安装 Apache 作为服务（仅限 NT）”。

- 2. 安装完成后，通过打开控制面板中的“服务”，选择 Apache 并点击“启动”按钮来启动名为 Apache 的服务。

- 3. Apache Web 服务器将持续在后台运行，并在每当你的机器启动时自动启动。

- 4. 当 Apache 作为服务运行时要停止它，你可以在命令行中发出 `NET STOP` 命令，也可以进入控制面板的“服务”窗口，选择 Apache 并点击“停止”按钮。

要从控制台窗口运行 Apache，请执行以下操作：

- 1. 从开始菜单的文件夹中选择“启动 Apache”或“作为控制台程序启动 Apache”。控制台窗口将打开，Apache 开始运行。请保持此窗口打开！

- 2. 要停止 Apache，从开始菜单的文件夹中选择“关闭控制台程序”，或手动关闭窗口（尽管这是关闭 Apache 的一种不方式）。阅读 Apache 文档获取有关从命令行向 Apache 发送信号的其他说明。

现在 Apache 已经安装并运行，打开你的 Web 浏览器并输入 `http://127.0.0.1/`。

你将看到“Welcome to Apache!”页面，其中包含指向 Apache 网站和 Apache 手册的链接。如果你没有看到欢迎页，或者安装在任何阶段失败，请阅读 Apache 文档和 Apache 常见问题解答以尝试确定你的问题，然后重试。

### UNIX 上的 Apache

如果你使用任何版本的 UNIX 并且决定 Apache 适合你，请前往 `http://www.apache.org/` 开始下载过程。你有两个选择：下载预编译的二进制文件，或者下载源代码并自己编译 Apache。

# 第 1 章：开始使用 PHP

要安装预编译的二进制文件，请访问 `http://apache.org/dist/get` 发行目录并选择适用于你操作系统的二进制发行。如果你正在使用 Linux，你需要从 Linux 目录获取文件；如果你正在使用 Solaris，你需要从 Solaris 目录获取文件；依此类推。

一旦你下载了压缩的 tar 文件，将其放置在可访问的目录中（例如 `/usr/local/`），并使用以下命令进行解压：

```
gunzip [filename].gz
```

此命令将创建一个 `*.tar` 文件。要解包它，请使用此命令：

```
tar -xvf [filename].tar
```

此命令将创建 `/usr/local/apache_[version]/` 目录，包含以下子目录：`cgi-bin`, `conf`, `htdocs`, `icons` 和 `src`。每个子目录都带有其他好东西。

除了系统目录外，还创建了默认文档根目录：`htdocs`。Web 服务器的文档根是存放你的 HTML 文档的目录。你应该在 `src` 目录下拥有一个名为 `httpd` 的二进制文件。这很好；它是让 Apache 运行起来的文件。

下一步是根据需要编辑配置文件。如果你查看你的 Apache 安装目录下的 `conf` 子目录，你将找到三个通用配置文件：`httpd.conf`、`conf-dist`、`access.conf-dist` 和 `httpd.conf-dist`。将这些文件复制为 `httpd.conf`、`access.conf` 和 `httpd.conf`，并在 `httpd.conf` 中进行以下修改以生成基础的 Web 服务器配置：

- 1. 修改 `ServerRoot` 条目，使其指向 Apache 的顶层目录。

- 2. 修改 `ServerAdmin` 条目，使其与你的电子邮件地址（或另一个系统管理员的电子邮件地址）匹配。

- 3. 修改 `ServerName` 条目，使其与 Web 服务器的名称匹配。

- 4. 修改 `DocumentRoot` 条目，使其指向存放你 HTML 文件的目录。

这些修改是在 UNIX 上基础安装 Apache 所唯一必须的更改。每当你修改修改配置文件时，必须重启 Apache 以使更改生效。务必备份你的原始文件！

现在，尝试通过运行 `httpd` 来运行 Apache：

```
/usr/local/apache_[version]/httpd
```

## 安装 Web 服务器

`httpd` 程序默认会在 `/usr/local/apache/conf/` 目录下查找 `httpd.conf` 文件。如果你的 `httpd.conf` 位于其他地方，你可以通过改为发出以下启动命令来指定位置：

```
/usr/local/apache_[version]/httpd -f /path/to/httpd.conf
```

其中 `/path/to/` 被替换为你自定义的 Apache 配置文件路径。发出启动命令后，你将返回命令行提示符且没有任何错误，服务器将开始运行。你也可以使用 `apachectl` 脚本启动 Apache，该脚本通常位于 `/usr/local/apache_[version]/bin/`：

```
../apachectl start
```

现在 Apache 已经安装并运行，打开你的 Web 浏览器并输入 `http://127.0.0.1`。

你应该能看到包含指向 Apache 网站和 Apache 手册链接的欢迎页。如果你没有看到欢迎页，或者你的安装在任何阶段失败，请阅读 Apache 文档和 Apache 常见问题解答以确定你的问题，然后重试。随时停止 Apache，发送 kill 信号：

```
kill -TERM 'cat /path/to/logs/httpd.pid'
```

其中 `/path/to/` 被替换为你自定义的日志 文件路径。或者，你可以使用 `apachectl` 脚本，它位于 `/usr/local/apache_[version]/bin`：

```
../apachectl stop
```

要编译 Apache 源代码，请访问 `http://www.apache.org/dist/` 发行目录并获取你需要的 Apache 服务器的 gzipped 版本；将其放置在可访问的目录中（例如 `/usr/local/`），并使用以下命令进行解压：

```
gunzip [filename].gz
```

此命令将创建一个 `*.tar` 文件。要解包它，请使用此命令：

```
tar -xvf [filename].tar
```

此命令将创建 `/usr/local/apache_[version]/` 目录，包含以下子目录：`cgi-bin`, `conf`, `htdocs`, `icons` 和 `src`。每个子目录都装满了好东西。

## 安装 Web 服务器

`apachectl` 脚本位于 `/usr/local/apache_[version]/bin/` 目录下：

`./apachectl start`

现在 Apache 已安装并运行，请打开 Web 浏览器并输入 `http://127.0.0.1/`。

你应该能看到“Welcome to Apache!”页面，其中包含指向 Apache 网站和 Apache 手册的链接。如果你没有看到欢迎页，或者你的安装在任何一点失败，请阅读 Apache 文档和 Apache 常见问题解答（FAQ）以确定你的问题，然后重试。要随时停止 Apache，请结束 kill 信号：

```
kill -TERM /path/to/logs/httpd.pid
```

其中 `/path/to/` 替换为 Apache 日志文件的自定义路径。或者，你可以使用 `/usr/local/apache_[version]/bin/` 目录下的 `apachectl` 脚本：`./apachectl stop`

# 下载并安装 Xitami
