

# 140 · 第 9 章

- 它能立即释放服务器进程，使其返回端口等待另一个请求。
- 它能让 Web 服务器更安全，因为请求是由受 `httpd.conf` 文件中用户权限限制的进程处理的，并使用了 `User` 和 `Group` 指令。

| | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|
| root | 2959 | 0.0 | 0.2 | 3748 | 1076 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2960 | 0.0 | 0.2 | 3940 | 1268 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2961 | 0.0 | 0.2 | 3928 | 1268 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2962 | 0.0 | 0.2 | 3928 | 1268 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2963 | 0.0 | 0.2 | 3892 | 1152 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2964 | 0.0 | 0.2 | 3892 | 1152 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2969 | 0.0 | 0.2 | 3900 | 1168 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2970 | 0.0 | 0.2 | 3900 | 1168 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |
| nobody | 2971 | 0.0 | 0.2 | 3900 | 1168 | ? | S | 09:37 | 0:00 /usr/bin/httpd - |

图 9.2：`ps aux | grep` 命令字符串列出了所有的 http 进程。

如果你以 root 用户身份运行它，所有所有的子进程都将自动终止。此外，根据图 9.2 中的进程 ID，你可以使用以下命令结束 Apache 服务器：

```
kill 2959
```

这里的最小配置对于理解 Apache 配置过程的工作原理非常有用。对于生产服务器，可能从 `/etc/httpd` 下默认的 `httpd.conf` 配置文件开始，然后使用 `/etc/rc.d/httpd` 脚本启动和停止 Apache 更好。`/etc/httpd/conf/httpd.conf` 文件很长，但包含了大量的注释，能够很好地解释每个指令的含义。不要忘记查看 www.apache.org 网站上的文档。

# 支持

如果你对这些不受支持的 Web 服务器内容有些顾虑（没错，Apache 的作者们并没有自愿负责技术支持电话），你可能想考虑 Apache HTTP Server 的商业实现版本。IBM 提供了此类服务，即 IBM HTTP Server，如图 9.3 所示。IBM HTTP Server 提供了 Apache HTTP 服务器的质量和功能，以及你对 IBM 商业产品所预期的支持。

将 IBM HTTP Server 视为一个具有简单安装和全方位支持的封装版 Apache 服务器。此外，由于 IBM HTTP Server 是一款付费产品，IBM 能够合法地捆绑对 SSL 支持（尽管美国政府不允许它提供 SSL Apache 模块的源代码）；

IBM 与 Apache Group 保持联系；该公司为 Apache Group 核心的两个全职成员支付薪水。IBM 还拥有一个完整的程序员团队对 IBM HTTP Server 进行增强。为了确保与 Apache HTTP 服务器兼容，这些增强会被提交给 Apache Group。一旦这些增强被接受，它们将成为 Apache 服务器和 IBM HTTP Server 的永久部分。

# Apache Web 服务器 141

![](img/069cd06404ac5e90171e6d857bf3ad28_156_0.png)

图 9.3：IBM HTTP Server 产品标志明确标明它是“由 Apache 驱动”，表明它是基于开源的 Apache HTTP 服务器。

# Tomcat Apache 插件

第 8 章引入了 Apache 的开源 Web 服务器 Tomcat。在 true章节的练习中，你安装并测试了 Tomcat。Tomcat 产品包含一个基础的 HTTP 服务器。对于生产环境，应该将 Tomcat 作为插件添加到 Apache 服务器中。你可以从 Apache 的 Jakarta 项目网站 (http://jakarta.apache.org) 下载插件。获取适用于你版本 Tomcat 的下载链接（注意，4.0 及更高版本使用了本节课程中未涵盖的插件策略），然后按照 `/bin/linux/i386/` 路径获取 `mod_jk.so`。

`mod_jk.so` 模块允许 Apache 与 Tomcat 通信。你需要使用以下命令将其移动到 `/etc/httpd/libexec/` 目录：

```
mv <download-dir>/mod_jk.so /etc/httpd/libexec/mod_jk.so
```

注意，你可能需要创建 `libexec` 目录。此外，注意 `mod_jk.so` 有 ANSI 版本和非 ANSI 版本供下载。最后，通过在 Apache 的 `/etc/httpd/conf/httpd.conf` 文件末尾添加此行来包含 Tomcat所需的项：

```
Include /etc/httpd/conf/mod_jk.conf
```

现在 Apache 已准备好配合 Tomcat，你准备好测试安装了。为了这两个包正常工作，你需要先启动 Tomcat，然后启动 Apache。确保 Apache 当前已停止。在 Red Hat 系统上，可以通过执行以下命令来实现：

1. 使用 `/etc/rc.d/init.d` 目录下的启动工具启动 Apache。
2. 访问：

# 练习 2：自定义 Apache

1. 在你的主目录下创建以下目录结构：

```
www
conf
htdocs
logs
```

2. 在 `conf` 目录下创建一个名为 `httpd.conf` 的文件，放入图 9.1 所示的最小 Apache 指令。
3. 在 `htdocs` 目录下创建一个首页（HTML 页面）。
4. 替换 `httpd.conf` 文件中的 `Directory` 指令以指定你的首页。
5. 启动 Apache，指定你的配置文件位置。
6. 从浏览器测试 Apache。注意图 9.1 中的 `Port` 指令为 8888，所以你的 URL 需要标识该端口：

```
http://127.0.0.1:8888
```

# 练习 3：安装 Tomcat 插件

1. 按照章节说明下载并安装 Tomcat 插件。
2. 启动 Tomcat，然后启动 Apache。
3. 从浏览器测试插件：

```http://localhost/test/jsp/HelloWorld.jsp
```

# 练习 4（可选）：下载并安装 IBM HTTP Server

1. 从 www.ibm.com/software/webservers/download.html 下载 `HTTPServer.linux.1.39.0.EN.gz`（其中 EN 是语言标识）。
2. 使用 `gunzip` 解压 `.tar` 文件：

```
$ gunzip HTTPServer.linux.1.39.0.EN.tar.gz
```

`gunzip` 工具会将 `HTTPServer.linux.1.39.0.EN.gz` 替换为 `HTTPServer.linux.1.39.0.EN.tar`。

3. 以 root 身份登录。
4. 切换目录到 `/opt`，使用 `tar` 工具提取 `.tar` 文件：

```
# cd /opt
# tar -xf HTTPServer.linux.1.39.0.EN.tar
```

`tar` 工具将创建一个名为 `IHS.319.0` 的目录，并填充大约十个 RPM 包。

5. 将工作目录切换到 `IHS.319.0`。

```
# cd IHS.319.0
```

6. 对于每个 RPM，以以下格式运行 `rpm` 工具：

```
# rpm -U -nodeps <rpm file>
```

7. 启动 IBM HTTP Server：

```
# /opt/IBMHTTPServer/bin/apachectl start
```

或者

```bash
# /etc/rc.d/init.d/ibmhttpd start
```

8. 测试 IBM HTTP Server：

```
http://127.0.0.1
```

9. 停止 IBM HTTP Server：

```
# /opt/IBMHTTPServer/bin/apachectl stop
```

或者

```bash
# /etc/rc.d/init.d/ibmhttpd stop
```

注意，在 `/opt/IBMHTTPServer` 目录下，你会发现与标准 Apache 服务器相同的 `conf`、`htdocs` 和 `logs` 子目录。

# 10

# Linux 操作、配置与管理

通过你精心规划的安装得到的 Linux 系统将包含你所需的一切，让你在未来很长一段时间内都能稳定。但最终，你会想要做一些更改。你可能想更改桌面的外观和行为，也许添加额外的软件，或者对基础 Linux 系统进行配置更改。无论如何，熵最终也会攻击你的系统，迫使你深入系统配置。本章将向你介绍用于这些更改的工具。

# 用户界面

在处理基于 Linux 的 Web 托管的书中有一个用户界面的章节似乎显得格格不入。毕竟，大多数 Linux 服务器在没有键盘和屏幕的情况下运行（即所谓的“无头”模式），因此唯一的可用界面是通过浏览器或远程命令行 Shell 获取的。我们意识到，你构建的第一个服务器可能托管在你自己的工作站上。考虑到这一点，让我们快速查看一眼 Linux GUI 并发现它为什么如此强大。

# X 简介

任何使用过 Windows 操作系统的人都已经熟悉图形用户界面（GUI）。与微软的方案不同，GUI 不是操作系统的不可分割的一部分，而 Linux GUI 是一个称为 X Window 系统（或简称 X）的插件。

