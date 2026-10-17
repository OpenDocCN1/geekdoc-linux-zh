
要将 Linux 系统作为 Web 服务器使用，你必须在你的系统上安装服务器软件。最流行的 Unix 服务器软件包是 Apache 和 NCSA。

## 674 第 35 章 Apache 入门

这是一个集中存放所有服务器相关内容的地方。此外，如果服务器崩溃并留下了转储文件（core file），它将在服务器根目录中找到。

第二个决策是文档根目录（document root，即存放所有 HTML 和其他媒体文件的目录）位于何处。文档根目录下名为 `myfile.html` 的文件将通过 `http://host/index.html` 被引用。该目录可以是服务器根目录的子目录，也可以是位于服务器根目录之外并拥有独立的目录。它通常位于服务器根目录的子目录下，并命名为 `hdocs`。为了更大的磁盘空间或其他原因，你选择将文档根设置在服务器根目录之外，这会给它一个很短的名字——例如 `/home/www` 或 `/www/hdocs`。例如，如果你在 FTP 服务器上实现 Web 服务器，你可能希望将文档根放置在 `/home/ftp/`。

最后，你需要决定服务器将日志保存在哪里。根据服务器的繁忙程度，该空间应该有一个较大的工作区域。作为一个参考，一个每天有 10 万次访问的网站（相对而言属于中等流量）预计每天会产生 15MB 的日志信息。为了性能考虑，最好将日志目录放在单独的分区上，甚至是完全独立的磁盘驱动器上，即使在中等繁忙的服务器上，访问日志每秒也可以写入几次。

## 执行基础配置

本节涵盖了为了启动基础 Web 网站你需要对配置文件进行的最少一组更改。

Apache 有多个独立的配置文件。这种模型可以追溯到 NCSA，其原因是合理的：管理配置很大程度上有三个主要区域，因此将它们设为单独的文件允许 Web 站员根据需要为每个文件赋予不同的权限。

你可以在服务器根目录的 `conf/` 子目录下找到 Apache 的配置文件。每个文件都带有一个 `-dist` 文件名后缀；建议你创建一个不带 `-dist` 的副本，并编辑这些新文件，将带有 `-dist` 版本作为备份和参考。

配置文件的基本格式是类 Shell 界面和伪 HTML 的结合。基本单元是指令（directive），它可以接受多个参数——本质上，

指令 参数 参数...

即，

或者

```apache
AddIcon /icons/back.gif ..
```

你也可以将某些指令组合在特定的伪 HTML 标签内部。与 HTML 不同，这些标签应该像下面的示例那样单独成行：

```
<Virtualhost /www.myhost.com>
DocumentRoot /www/hdocs
ServerName www.myhost.com
</Virtualhost>
```

# 678 第35章 入门 Apache

```bash
# chkconfig: 345 85 15
# description: Apache is a World Wide Web server. It is used to serve \
# HTML files and CGI.
#
#
```

```bash
# Source function library.
/etc/rc.d/init.d/functions
```

```bash
# See how we were called.
case $1 in
start)
	echo -n "Starting httpd: "
	daemon httpd
	echo
	touch /var/lock/subsys/httpd
	;
stop)
	echo -n "Shutting down httpd: "
	kill /var/run/httpd.pid
	httpd
	rm -f /var/lock/subsys/httpd /var/run/httpd.pid
	;
status)
	status httpd
	;
restart)
	$0 stop
	$0 start
	;
*)
	echo "Usage: httpd.init {start|stop|restart|status}"
	exit 1
esac
```

此时，使用 `ps` 命令查看 `httpd` 是否正在运行可能是个好主意。通常，使用类似 `ps -aux | grep` 就足够了。让你惊讶的是，你会看到多个同时运行的 `httpd` 进程。这是什么？

早期的 Web 服务器（如 CERN 和 NCSA）采用的是每当有一个请求进来就克隆一个主 Web 服务器的模式。克隆体响应请求，而原始服务器则返回监听端口以等待另一个请求。虽然这种设计非常简单且健壮，但克隆操作（在 UNIX 术语中称为 `fork`）在 UNIX 上是一项开销巨大的操作，因此当负载超过每秒几次请求时，即使是对最好的硬件也显得非常吃力。此外，也很难实现任何形式的节流来减少克隆的发生。当克隆数量很高时，原始服务器很难跟踪还有多少克隆进程仍在运行。因此，服务器没有简单的方法根据资源短缺来拒绝或延迟连接。

## 调试服务器启动过程

类似 Apache 的 NCSA 1.4+、Netscape Web 服务器以及其他几个基于 UNIX 的 Web 服务器——而是使用一组并行运行的持久子进程模型。子进程由一个父进程协调，父进程可以知道有多少个存活子进程、在需要时创建新的子进程，并根据情况在有很多空闲子进程时终止旧的子进程。（父进程和子进程是真正的 UNIX 术语。）

回到服务器。启动你的 Web 浏览器并指向你的本地服务器。（使用通常的 `http://` 格式并附加在 `httpd.conf` 文件中定义的 `ServerName` 参数。）成功了吗？如果一切顺利，你应该能够看到文档根目录下所有内容的目录列表，或者如果该目录下有一个 `index.html`，你将看到该文件的内容。

表 35.1 显示了其他命令行选项。

| 表 35.1 httpd 命令行选项 |
|---|---|
| `-d serverroot` | 设置 `ServerRoot` 的初始值。 |
| `-X` | 在单进程模式下运行服务器。（这对于调试很有用，但不要在此模式下运行服务器向外部世界提供内容。） |
| `-v` | 打印服务器版本并退出。 |
| `-?` | 打印 Apache 可用的命令行参数列表。 |

在检查确保 Apache 正确启动后，你可能想将启动命令添加到系统启动脚本中，以便 Apache 在系统内核启动时自动启动。启动命令的典型位置是 `/etc/rc.d/rc.local` 文件。

## 调试服务器启动过程

Apache 通常很能提供有意义的错误信息，但某些错误将在接下来的章节中详细解释。

### 文件打开错误消息

```
httpd: could not open document config file ....
open: No such file or directory
```

这些文件错误消息通常是由于给 `-f` 参数只提供了相对路径导致的，因此 Apache 会相对于编译时的服务器根目录（在 `src/httpd.h` 中设置的内容）查找文件，而不是相对于你当前所在的目录。你必须提供完整路径或相对于编译时服务器根目录的路径。

### 端口和绑定错误消息

```
httpd: could not bind to port [X]
bind: Operation not permitted
```
