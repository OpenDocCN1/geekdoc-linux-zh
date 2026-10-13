
```sh
#!/bin/sh
#
## Apache Web Server 的启动脚本
#
# chconfig: 345 85 15
# description: Apache 是一个 World Web 服务器。 \
#   它被用于提供 HTML 文件和 CGI。
# processname: httpd
# pidfile: /var/run/httpd.pid
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf

## 引入函数库。
  /etc/rc.d/init.d/functions

# 查看我们是如何被调用的。
case "$1" in
start)
  echo -n "Starting httpd: " 
  daemon httpd
  echo
  touch /var/lock/subsystems/httpd
  ;;
stop)
  echo -n "Shutting down httpd: " 
  [ -f /var/run/httpd.pid ] && (
    kill `cat /var/run/httpd.pid`
    echo -n httpd
  )
echo
rm -f /var/lock/subsys/httpd
rm -f /var/run/httpd.pid
;;
status)
status httpd
;;
restart)
$0 stop
$0 start
;;
reload)
echo -n "Reloading httpd: "
[ -f /var/run/httpd.pid ] && (
  kill `cat /var/run/httpd.pid`
  echo -n httpd
)
echo
;;
*)
echo "Usage: $0 {start|stop|restart|reload}"
  exit 1
esac

exit 0
```

如所见，这是一个 `case` 语句。现在你可以看到如何可以在运行级别下创建新服务：

![](img/cbfef09f620ba4100baa62876f6f02b1_99.png)

- 1. 从 `/etc/rc.d/init.d/` 复制一个现有服务脚本。
- 2. 使用您喜欢的编辑器（如 `vi`），将所有 "`httpd`" 替换为 "`webmonitor`"。
- 3. 如果您在 `/etc/rc.d/init.d/` 以外的任何目录下运行脚本，请修改 PID 行。
- 4. 如果 `webmonitor` 没有创建 PID 文件 (`/var/run/webmonitor.pid`)？
- 5. 执行 `chmod 750 /etc/rc.d/init.d/webmonitor` 以允许 root 用户读取、写入和执行。

这就是创建服务所需的所有工作。您可以使用 `chkconfig`、`ntsys` 或 `linuxconf` 将其添加到运行级别。

## 总结

在本章中，你学习了 Red Hat Linux 如何启动和关闭。你学习了 `init`，它是内核启动的，并启动了所有的进程（即服务）。

# 第 4 章：理解文件和设备

## 本章内容

- 管理文件、目录权限和所有权
- 为多用户系统建立策略

许多人不喜欢 UNIX 或类 Unix 操作系统的主要原因之一是它们管理文件的方式。许多人简单地认为与其相关的概念并不直观。在担任系统管理员工作期间，我发现百分之九十的问题与文件权限和所有权有关。然而，这不应该归他们的错，因为这些人大多来自微软 Windows 3.1 或类似系统的背景，那里没有文件所有权或访问权限的概念。因此，作为服务器系统管理员，您可能会遇到很多文件问题。

### 理解文件/目录权限

与 UNIX 和类 Unix 操作系统一样，Linux 将文件或目录与用户和组关联。考虑一个示例：

```
-rw-rw-r-- 1 sheila 512 Feb 6 21:11 milkyweb.txt
```

上述行是由 `ls -l milkyweb.txt` 命令产生的。您可能已经知道 `ls` 程序列出文件和目录。`-l` 选项显示了 `milkyweb.txt` 的完整列表。现在以表 4-1 中的表格格式查看相同信息：

| 权限 | 链接数 | 所有者 | 组 | 大小 | 日期 | 时间 | 名称 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| -rw-rw-r-- | 1 | sheila | sheila | 512 | Feb 6 | 21:11 | milkyweb.txt |

## 第二部分：作为超级用户工作

### 表 4-1 示例 `ls -l` 命令的输出

| 信息类型 | 是否输出 |
|---|---|
| 文件访问权限 | -rw-rw-r- |
| 链接数 | 1 |
| 用户（文件所有者） | sheila |
| 组 | intranet |
| 文件大小（字节） | 512 |
| 最后修改日期 | 2月 6日 |
| 最后修改时间 | 21:11 |
| 文件名 | Milkyweb.txt |

在这里，`milkyweb.txt` 文件属于一个名为 `sheila` 的用户。她是唯一一个可以更改此文件访问权限的普通用户。另一个可以更改权限的用户是超级用户。该文件的所属组为 `intranet`。任何属于 `intranet` 组的用户都可以根据（所有者）设置的组权限来访问（读取、写入或执行）该文件。

要成为文件的所有者，用户必须创建文件。在红帽 Linux（Red Hat Linux）中，用户创建一个文件或目录时，其组也会被设置为用户的默认组，而该默认组恰好是与用户名同名的私有组。为了更清楚一点，假设我以 `kabir` 的身份登录我的红帽 Linux 系统，并使用文本编辑器创建了一个名为 `todo.txt` 的文件。如果我执行 `-l todo.txt`，会出现以下输出：

```
-rw-rw-r- 1 kabir kabir 4848 Feb 6 21:37 todo.txt
```

如你所见，文件所有者和组名是相同的。这是因为在红帽 Linux 中，你的用户默认（私有）组也叫 `kabir`。这可能有点让人困惑，但这样做是为了让你少一些烦恼，而且你可以很轻松地更改这种行为。然而，这里的点在于，当创建一个新文件时，该文件所有者是文件的创建者，而组是用户的默认组。现在来看看你可以如何更改文件的所有权。

作为普通用户，你不能将文件或目录的所有权重新分配给他人。例如，我不能以用户 `kabir` 的身份创建一个文件，并将其所有权重新分配给名为 `sheila` 的用户。为什么会这样？智者的回答无疑是安全性。如果允许普通用户重新分配文件所有权给他人，有人可能会创建一个删除文件的恶意程序，将其所有权更改为超级用户，从而删除整个文件系统。只有超级用户才能重新分配文件或目录的所有权。

# 第4章：理解 UNIX 文件和设备

## 使用 `chown` 更改文件/目录的所有权

作为超级用户，你可以使用 `chown` 命令更改文件/目录的所有权。要更改文件或目录的所有权，请如下所示运行命令：

```
chown newuser file or directory
```

例如：

```
chown sheila kabirs_plans.txt
```

该命令使用户 `sheila` 文件 `kabirs_plans.txt` 的新所有者。如果超级用户还想更改文件或目录的组，可以使用如下的 `chown` 命令：

```
chown newuser.newgroup file or directory
```

例如：

```
chown sheila.admin kabirs_plans.txt
```

前述命令不仅使 `sheila` 成为新所有者，还将文件的组重置为 `admin`。如果超级用户想要更改指定目录下所有文件或目录的用户和/组所有权，可以使用 `-R` 选项以递归模式运行 `chown` 命令。例如：

```
chown -R sheila.admin /home/kabir/plans/
```

前述命令更改了 `/home/kabir/plans` 目录及其所有文件和子目录的用户和组所有权。虽然你必须是超级用户才能更改文件或目录的组，但普通用户可以使用 `chgrp` 命令。

## 使用 `chgrp` 更改文件/目录的组

`chgrp` 命令允许你更改文件或目录的组所有权，只要你是新组的一部分。换句话说，只有当你同时属于旧组和新组时，才能更改组。例如：

```
chgrp httpd *.html
```

如果我运行上述命令来更改目录下所有 HTML 文件的组，我也必须是 `httpd` 组的一部分。你可以通过不带参数的 `groups` 命令查看你正在使用哪些组。与 `chown` 命令一样，`chgrp` 也使用 `-R` 来递归更改一个或多个文件或目录的组名。

现在你已经知道用户是如何关联文件和目录的，请查看文件和目录的访问权限是如何工作的。查看文件/目录权限有两种。

## 使用八进制数字理解访问权限
