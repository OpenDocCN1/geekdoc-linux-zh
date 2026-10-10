
## 启动守护进程

```bash
echo -n "Starting httpd: "

$APACHECTL start

touch /var/lock/subsys/httpd

echo

;;

stop)

# 停止守护进程。

echo -n "Shutting down httpd: "

$APACHECTL stop

echo "done"

rm -f /var/lock/subsys/httpd

;;

*)

echo "Usage: httpd {start|stop}"

exit 1

esac

exit 0
```

> **提示**
>
> 要在系统启动时自动启动 Apache，只需运行一次此命令：
>
> `ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/S99httpd`
>
> 该命令在 `/etc/rc.d/rc3.d`（运行级别 3）目录中创建一个名为 `S99httpd` 的特殊链接，指向 `/etc/rc.d/init.d/httpd` 脚本。当系统启动时，该脚本将以 `start` 参数执行，从而自动启动 Apache。

### 重启 Apache

要重启 Apache 服务器，请运行 `/usr/local/apache/bin/apachectl restart` 命令。

您也可以如下使用 `kill` 命令：

```bash
kill -HUP `cat /usr/local/apache/logs/httpd.pid`
```

当使用 `apachectl restart` 或通过 `kill` 使用 `HUP` 信号重启时，父 Apache 进程（以 root 用户运行）会终止其所有子进程，读取配置文件，并根据需要重启新一代的子进程。

> **注意**
>
> 这种重启方式对于当时由仍存活的子进程提供服务的 Web 客户端来说是突然的。因此，您可能需要考虑使用 `apachectl` 的 `graceful` 选项代替 `restart`，以及在 `kill` 命令中使用 `WINCH` 代替 `HUP` 信号。在这两种情况下，父 Apache 进程都会通知其子进程完成当前请求，然后终止，以便它可以重新读取配置文件并重启一批新的子进程。在繁忙的站点上，这可能需要一些时间。

### 停止 Apache

您可以在系统重启时自动停止 Apache，或在任何时间手动停止它。以下部分将讨论这两种停止 Apache 的方法。

## 自动停止 Apache

要在系统重启时自动终止 Apache，请运行一次此命令：

```bash
ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/K99httpd
```

该命令确保在系统关闭时，以 `stop` 参数运行 `httpd` 脚本。

## 手动停止 Apache 服务器

要停止 Apache 服务器，请运行 `/usr/local/apache/bin/apachectl stop` 命令。

Apache 服务器还为您方便地查找根 Web 服务器进程的 PID。该 PID 写入分配给 `PidFile` 指令的文件中。这是主 `httpd` 进程的 PID。不要尝试手动逐个终止子进程，因为父进程会在需要时重新创建它们。停止 Apache 服务器的另一种方法是运行：

```bash
kill `cat /usr/local/apache/logs/httpd.pid`
```

该命令使用 `-TERM` 信号（即 -15）运行 `kill` 命令，针对由 `cat /usr/local/apache/logs/httpd.pid`（即 `cat %PidFile%`）命令返回的进程 ID。

## 测试 Apache

在启动 Apache 服务器后，请使用合适的主机名通过 Web 浏览器访问它。例如，如果您在服务器本身上运行 Web 浏览器，则使用 `http://localhost/` 访问服务器。但是，如果您想从远程主机访问服务器，请使用服务器的完全限定主机名。例如，要访问名为 `apache.pcn1td.com` 的服务器，请使用 `http://apache.pcn1td.com`。如果您将 `Port` 指令设置为非标准端口（即 80 以外的端口），请记得在 URL 中包含 `:port`。例如，`http://localhost:8080` 将访问 8080 端口上的 Apache 服务器。

如果您没有对默认的 `htdocs` 目录进行任何更改，您将看到如图 3-4 所示的页面。该页面随 Apache 发行版一起提供，需要替换为您自己的内容。

最后，您需要确保日志文件正确更新。要检查您的日志文件，请输入 `log` 目录并运行以下命令：

```bash
tail -f `path_to_access_log`
```

该命令中的 `tail` 部分是一个 Unix 实用程序，允许查看正在增长的文件（当指定 -f 选项时）。请确保将 `path_to_access_log` 更改为访问日志的完全限定路径名。现在，使用 Web 浏览器访问该站点；如果您已经在该站点上，只需重新加载当前在浏览器上的页面。您应该看到屏幕上添加了条目。多按几次重新加载按钮，以确保访问文件适当更新。如果您看到更新的记录，您的访问日志文件正在正常工作。按 Ctrl+C 退出 `tail` 命令会话。如果您没有看到文件中的任何新记录，应该检查日志文件及其所在目录的权限设置。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_84_0.png)

**图 3-4：** 默认的 Apache 主页

另一个需要检查的日志是错误日志文件。使用：

```bash
tail -f path_to_error_log
```

命令来实时查看错误日志条目。只需在 Web 浏览器中请求不存在的资源（例如您没有的文件），您就会看到有日志条目被添加。如果您观察到有日志条目被添加，则说明错误日志文件配置正确。

如果所有这些测试都成功，那么您已成功配置了您的 Apache 服务器。恭喜！

◆   ◆   ◆

## 使用 Winnt MPM 指令配置 Apache

指令简单来说就是供 Apache 执行的命令。Apache 从第 3 章中提到的配置文件中读取指令。通过使用指令，Apache 管理员可以控制 Web 服务器的行为。Apache 提供许多指令，这使得它成为一个高度可配置的 Web 服务器。Apache 基础安装中包含的指令被称为*核心指令*。这些指令始终可用。

> **交叉引用**
>
> 标准模块（它们是 Apache 标准发行版的一部分）中也提供了其他一些指令。有关这些基于标准模块的指令的讨论将在第 5 章中进行。

本章讨论指令（核心指令及其他所有指令）适用的标准上下文，详细讲解核心指令，以及 Apache 2.0 中引入的各种多处理模块（或 *MPM*）中可用的指令。我没有按字母顺序列出所有可能的核心指令，而是根据它们的用途对它们进行了分类；类别包括一般配置；性能和资源配置；标准容器；虚拟主机特定项；日志记录；以及身份验证和安全性。每个指令描述提供以下信息：

## 第 4 章

## 本章内容

- 理解 Apache 指令上下文
- 熟悉核心指令
- 使用线程式 MPM 指令配置 Apache
- 使用预派生（prefork）MPM 指令配置 Apache
- 使用 perchild MPM 指令配置 Apache

**语法：** 显示指令名称及其接受的所有可能参数或值。

**默认设置：** 该行显示指令的默认值。仅在适用时显示。

**上下文：** 指定指令适用的上下文（或范围）。

**AllowOverride：** 在每目录访问配置文件中启用该指令所需的值（默认为 `.htaccess`）。仅在适用时显示。

本章首先介绍您可以使用指令的上下文。

> **注意**
>
> 一些指令被列出了多次；除了其中一次之外，其余所有条目都指向该指令在章节其他位置的主要讨论。这是因为有些指令不属于单一类别，我希望您能够看到查看这些类型指令的各种方式。

### Apache 指令上下文

在使用任何核心指令之前，了解指令在哪个上下文中可用非常重要；换句话说，您需要知道指令的*上下文*（或*范围*）。在讨论核心指令所需的术语之后，我将描述核心指令本身。

使用指令主要有三个上下文，包括：

- **服务器配置上下文**：指令可以出现在主服务器配置文件中的任何位置（这是所谓的），且不在任何容器（看起来非常像 HTML 标签）内部。
- **容器上下文**：指令包含在看起来如下的容器中：
  ```html
  <Container_name>
      Directive
  </Container_name>
  ```
