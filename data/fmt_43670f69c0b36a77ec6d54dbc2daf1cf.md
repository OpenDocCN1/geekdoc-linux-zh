
$ rpm -qa | grep httpd

redhat-config-httpd-1.1.0-1.1

httpd-devel-2.0.45-14

你看到的版本号可能不同。开始时你只需要 `httpd` 包。我推荐 `httpd-manual`，因为它对整个 Apache 设置提供了极好的信息。`httpd-devel` 包包含用于构建和安装扩展模块的 `apxs` 工具。`redhat-config-httpd` 包包含一个基于 GUI 的 Apache 配置工具。

- 2. 建议为你的 Apache 服务器使用一个有效的主机名（例如，`abc.handsonhistory.com`）。如果没有真正的完全限定域名，你可以编辑 `/etc/httpd/conf/httpd.conf` 文件并将 `ServerName` 定义为计算机的 IP 地址。以 root 用户身份用任何文本编辑器打开 `httpd.conf` 文件，搜索包含 `ServerName new.host.name:80` 的行，并取消其注释。它应如下所示：

```
ServerName new.host.name:80
```

为了使 Web 服务器可供你的局域网访问，你可以使用 IP 地址代替 `new.host.name`（例如，`ServerName 10.0.0.1`）。`:80` 表示端口号（默认为此）。对于公共 Web 服务器，请获取一个真正的 DNS 主机名。

- 3. 添加一个管理员电子邮件地址，以便在服务器出现错误时有人可以联系你。在 `/etc/httpd/conf/httpd.conf` 文件中，默认的管理员地址如下所示：

```
ServerAdmin root@localhost
```

将 `root@localhost` 更改为你的 Apache 管理员的电子邮件地址。

- 4. 启动 `httpd` 服务器。作为 root 用户，输入以下命令：

```
# /etc/init.d/httpd start
```

如果一切顺利，应出现以下消息：`Starting httpd: [OK]`。现在你可以开始使用了。

- 5. 要使 `httpd` 在每次启动系统时自动启动，请以 root 用户身份运行以下命令。

```
# chkconfig httpd on
```

- 6. 为确保 Web 服务器正在工作，打开 Mozilla（或其他 Web 浏览器），在地址栏中输入以下内容并按 Enter：

```
http://localhost/
```

- 7. 你应该会看到 Apache Web 服务器的测试页面，如图 21-1 所示。要从另一台计算机访问此页面，你需要输入 Apache 服务器的主机名或 IP 地址。

![](img/27a85d56d393921ced6412ae6e8336bf_817_0.png)

> **TIP:** 不必连接到网络（甚至不需要网络连接）即可测试服务器或查看机器上的文件。与其在 URL 中指定服务器的真实名称，不如在同一台计算机上的浏览器中使用“localhost”（即 `http://localhost/`）。事实上，最好在将服务器暴露在未受保护的网络上之前完全测试配置。

- 8. 测试页面实际上是一个错误状态，表明你尚未向网站添加任何内容。要开始使用，你应该在 `/var/www/html` 目录中添加一个包含你自己主页内容的 `index.html` 文件。然后你可以继续向该目录结构添加自己的内容。

现在你已经让 Web 服务器工作了（或者至少我希望你已经做到了），你应该逐步阅读下一节。它有助于你了解如何设置更复杂的 Web 服务器配置并保护服务器免遭滥用。逐步阅读该部分也有助于你在 Web 服务器无法工作时进行故障排除。

> **TIP:** 如果你的 Web 服务器可以从本地主机访问，但 LAN 或 Internet 上的其他用户无法访问，你可能需要更改防火墙规则以允许更大的访问。附录 C 包含可供你操作的步骤，以使你的 Web 或其他服务器可访问。特别是，你需要打开端口 80。

## 配置 Apache 服务器

主要用于配置 Apache Web 服务器的文件是 `httpd.conf`（位于 `/etc/httpd/conf` 目录中）。对于旧版安装，你可能还配置了 `srm.conf` 和 `access.conf` 文件。然而在最近的版本中，Apache 开发者建议你将所有指令都放入 `httpd.conf` 中，不要创建另外两个文件。

所有 Apache 配置文件都是纯文本文件，可以使用你喜欢的文本编辑器进行编辑。`/etc/httpd/conf/httpd.conf` 文件在下一节中完整重现，并在相关选项块之后插入了解释（旨在补充每个文件中提供的注释）。

Apache 中的某些单独模块，如 `perl`、`php` 和 `mysql`，有单独的配置文件可能引起你的兴趣。这些文件包含在 `/etc/httpd/conf.d` 目录中。本章后面“配置模块（`/etc/httpd/conf.d/*.conf`）”部分将讨论模块。

> **CROSS-REFERENCE:** 更多关于 Apache 的信息可以从你自己的 Web 服务器上获得，网址为 `http://localhost/manual/`（如果安装了 `httpd-manual` 包）。

### 配置 Web 服务器（httpd.conf）

`httpd.conf` 文件是 Apache Web 服务器的主要配置文件。它包含与服务器总体运行相关的选项。默认文件名（`/etc/httpd/conf/httpd.conf`）可以通过 `httpd` 守护进程的 `-f filename` 命令行参数或 `ServerConfigFile` 指令来覆盖。以下各节列出了 `httpd.conf` 文件的内容并描述了如何使用该文件。

第一部分包含有关 `httpd.conf` 文件的注释：

```
# Based on the NCSA server configuration files originally by Rob McCool

# This is the main Apache server configuration file. It contains the configuration directives that give the server its instructions. See <URL:http://httpd.apache.org/docs-2.0/> for detailed information about the directives.

# Do NOT simply read the instructions in here without understanding what they do. They're here only as hints or reminders. If you are unsure consult the online docs. You have been warned.

# The configuration directives are grouped into three basic sections: 1. Directives that control the operation of the Apache server process as a whole (the 'global environment'). 2. Directives that define parameters of the main or default server, which responds to requests that aren't handled by a virtual host. These directives also provide default values for the settings of all virtual hosts. 3. Settings for virtual hosts, which allow Web requests to be sent to different IP addresses or hostnames and have them handled by the same Apache server process.

# Configuration and logfile names: If the filenames you specify for

# many of the server's control files begin with "/" (or "drive:/" for

# Win32), the server will use that explicit path.  If the filenames do

# *not* begin with "/", the value of ServerRoot is prepended -- so
```
