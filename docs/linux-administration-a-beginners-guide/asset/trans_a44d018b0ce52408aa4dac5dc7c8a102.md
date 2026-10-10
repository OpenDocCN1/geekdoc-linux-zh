

## 进程所有权

当网站在非标准端口上运行 Web 服务器时，你可以在网站 URL 中看到该端口号。例如，地址 `http://www.redhat.com/` 如果添加了端口号，将显示为 `http://www.redhat.com:80/`。

> 警告：不要犯“通过隐蔽性获取安全”的错误。如果你的服务器位于非标准端口上，这并不能保证互联网上的捣乱者找不到你的网站。由于攻击网站所用工具的自动化性质，扫描服务器并查找哪些端口正在运行 Web 服务器所需的 C 代码不到 100 行。使用非标准端口并不能使你的网站“安全”。

正如在其他章节中讨论的那样，在 UNIX 上运行 Web 服务器迫使你处理 Linux（以及通用 UNIX）模型。就权限而言，这意味着每个进程都有一个所有者，并且该所有者在系统上拥有有限的权限。

每当启动一个程序（进程）时，它都会继承其父进程的权限。例如，如果你以 root 身份登录，你用来执行所有工作的 shell 都具有与 root 用户相同的所有权限。此外，从这个 shell 启动的任何进程都将继承 root 用户的所有权限。进程可以放弃权限，但不能获取权限。

> 注意：Linux 继承原则有一个例外：配置了 setuid 位的程序（见第 6 章中的 `chmod` 命令）不会从父进程继承权限，而是以文件所有者本身指定的权限启动。例如，包含程序 `su` 的文件（`/bin/su`）由 root 拥有并设置了 setuid 位。如果用户 `sshah` 运行程序 `su`，该程序不会继承 `sshah` 的权限，而是将以 root 的权限启动。

## Apache 进程所有权

对于网络设置，Apache HTTP 服务器必须以 root 权限启动。具体来说，它需要绑定到端口 80，以便能够监听请求并接受连接。完成此操作后，Apache 可以放弃其权限并以非 root 用户身份运行，如配置文件中所指定。默认情况下，这是用户 `nobody`。

作为用户 `nobody`，Apache 只能读取用户 `nobody` 有权限读取的文件。因此，如果文件的权限设置为仅文件所有者可读，则所有者必须是 `nobody`。对于任何你想让用户 `nobody` 访问的文件，请将该文件的权限设置为可被所有人读取：

```
chmod a+r filename
```

其中 `filename` 是文件名。

对于使用 CGI 脚本的网站，安全性尤为重要。通过限制 Web 服务器的权限，你可以降低有人向服务器发送恶意请求的可能性。而且，服务器进程和相应的 CGI 脚本只能破坏它们可以访问的内容。作为用户 `nobody`，脚本和进程无法访问 root 可以访问的关键文件。（请记住：root 可以访问所有内容，无论权限如何。）

> 注意：如果你决定在服务器上允许 CGI 脚本，请严格关注其编写方式。务必确保通过网络输入的数据不能让 CGI 脚本执行它不应该做的事情。虽然没有这方面的统计数据，但大多数成功的网站攻击通常是因为 Web 服务器配置不当和/或 CGI 脚本编写不良所致。

## 安装 Apache HTTP 服务器

虽然大多数 Linux 发行版都预装了 Apache HTTP 服务器，但你可能需要执行升级或调整配置。本节将指导你完成下载 Apache 源代码、编译它并最终安装它的过程。Apache 配置命令将在后续章节中介绍。

如果你想继续使用 Linux 发行版默认的 Apache 安装，可以跳过本节。你只需要知道 Apache 配置文件和顶层页面的位置，以及如何重启服务器。对于 Red Hat Linux，这些位置如下：

-   配置文件：`/etc/httpd/conf`
-   顶层页面：`/home/httpd`
-   重启服务器：`/etc/rc.d/init.d/httpd restart`

Apache HTTP 服务器的最新版本始终位于 `http://www.apache.org/dist`。截稿时，最新版本是 Apache 1.3.9，可在 `apache_1.3.9.tar.gz` 归档文件中找到。

1.  下载 Apache 归档文件并将其放入工作目录。通常，`/usr/local/src` 是用于存储和编译程序的位置。
2.  使用以下命令解包程序：
    ```
    [root@ford src]$ tar -xzvf apache_1.3.9.tar.gz
    ```
    这将创建 `apache_1.3.9` 目录，其中包含编译程序所需的文件。

### 编译 Apache

Apache HTTP 服务器实际上是一个核心系统，具有支持动态加载模块的基本功能。模块执行诸如动态 URL 拼写纠正、URL 重写、cookie 跟踪等任务。默认配置由最流行的模块组成。由于 Apache 正在持续开发，请参阅程序的 *install* 文件以了解当前默认设置和可用的可选模块。

在本示例中，我们将使用默认配置。

1.  首先运行随 Apache 附带的 `configure` 脚本。如果你不确定系统上是否存在现有的 Web 服务器，你应该配置 Apache 安装到 `/usr/local/apache` 目录，如下所示：
    ```
    [root@ford apache_1.3.9]# ./configure --prefix=/usr/local/apache
    ```
2.  配置完成后，运行 `make` 编译程序：
    ```
    [root@ford apache_1.3.9]# make
    ```
3.  将 Apache 安装到相应目录：
    ```
    [root@ford apache_1.3.9]# make install
    ```

就这样。你现在已经安装了 Apache。

### 在繁忙系统上安装 Apache

在 *流量* 较大的系统上，你可能需要“在线”升级 Web 服务器，这意味着 Web 服务器因升级而停止服务的时间应等于关闭旧版本并启动新版本所需的时间。

为了适应这种情况，创建目录 `/usr/local/apache_version`，其中 *version* 是你正在安装的 Apache 版本号。在我们的示例中，我们将创建目录 `/usr/local/apache_1.3.9` 并在那里安装 Apache。为此，在运行 `configure` 时更改 `--prefix` 选项指定的目录。一旦创建了这个特殊目录，就从 `/usr/local/apache` 创建指向 `/usr/local/apache_1.3.9` 的符号链接。

下次你需要升级 Apache 时，你可以配置并安装到新目录——例如 `/usr/local/apache_1.4.0`——同时 `/usr/local/apache_1.3.9` 保持活动状态。一旦在 `/usr/local/apache_1.4.0` 中 *一切* 都设置好，你可以停止服务器进程（本章后面会讨论），更改符号链接使其指向 `/usr/local/apache_1.4.0`，然后启动新的 Apache。这使得升级停机时间仅为你输入三条命令的时间！更好的是，如果 1.4.0 版本不适合你，退回旧版本将很容易。只需关闭服务器，将 `/usr/local/apache` 指回 `/usr/local/apache_1.3.9`，然后再次启动。

## 第 14 章：使用 Apache 设置 Web 服务器

287

### 确保没有“nobody”用户冲突！

如前所述，Apache 默认以用户 `nobody` 身份运行。通过查看 `/etc/passwd` 文件并查找该条目来确保此用户存在。（如果需要，请参阅第 5 章了解如何确认特定用户是否存在。）

### 启动和关闭 Apache

Linux 的一个最棒的功能是能够启动和关闭系统服务而无需重新启动。这在 Apache 服务器中很容易做到。

启动 Apache：

```text
[root@ford root]# /usr/local/apache/bin/apachectl start
```

关闭 Apache：

```text
[root@ford root]# /usr/local/apache/bin/apachectl stop
```

### 在启动时启动 Apache

由于许多 Linux 发行版都预装了 Apache，如果你想运行新编译的版本，就需要禁用现有配置。为此，检查 `rc.d` 目录并找到指向现有 Apache 启动脚本的符号链接。现有脚本通常命名为 `httpd` 或 `apache`。

例如，在 Red Hat Linux 中，`/etc/rc.d/rc3.d/S85httpd` 脚本指向 `/etc/rc.d/init.d/httpd`，后者启动默认的 Apache 安装。要将此更改为运行最近编译的版本，我们需要替换该链接，使其指向 `/usr/local/apache/bin/apachectl`。

在 Red Hat Linux 中，实现此更新的命令如下：

```text
[root@ford apache_1.3.9]# cd /etc/rc.d/rc3.d
[root@ford rc3.d]# rm S85httpd
[root@ford rc3.d]# ln -s /usr/local/apache/bin/apachectl S85httpd
```

不要忘记对关闭脚本执行相同操作。以下是 Red Hat Linux 下的相应命令：

```text
[root@ford rc3.d]# cd /etc/rc.d/rc6.d
[root@ford rc6.d]# rm K15httpd
[root@ford rc6.d]# ln -s /usr/local/apache/bin/apachectl K15httpd
```

有关启动和关闭脚本的详细信息，请参阅第 7 章。

