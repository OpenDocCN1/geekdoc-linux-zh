

## 特定主机配置

Host db1.example.com
IdentityFile ~/.ssh/id_rsa-db1
$ ssh db1.example.com

您可以在主机规格说明中使用通配符。

```
$ cat ~/.ssh/config
Host db*
IdentityFile ~/.ssh/id_rsa-db1
Host *.work.net
IdentityFile ~/work-files/keys/id_rsa
$ ssh jim@jumboj.work.net
```

如果您的 SSH 密钥以相关主机的完全限定域名命名，您可以使用 % 转义字符来简化您的 ~/.ssh/config 文件。无需为每台服务器都创建一个主机条目，% 语法会扩展为您所连接主机的完全限定域名。

```
$ cat ~/.ssh/config
Host *.example.com
IdentityFile ~/.ssh/id_rsa-%h
$ ls -1 ~/.ssh/id_rsa-*
id_rsa-lax-db-01.example.com
id_rsa-lax-db-01.example.com.pub
id_rsa-lax-web-01.example.com
id_rsa-lax-web-01.example.com.pub
$ ssh lax-db-01.example.com
```

# 避免在通过 SSH 连接时输入用户名

将以下内容放入 `~/.ssh/config` 文件中。

```
Host remote-host
  User username
```

如果您在本地 Linux 机器上的用户名与远程 Linux 机器上的用户名不同，您在通过 SSH 连接时必须指定它。它看起来像这样。

```
$ ssh jim@server1.example.com
```

为了避免每次都要输入 "username@"，请在您的 `~/.ssh/config` 文件中添加一个主机条目。

```
Host server1.example.com
  User jim
```

一旦您配置了该主机条目，您就可以简单地 ssh 到远程主机。

```
$ whoami
james
$ ssh server1.example.com
$ whoami
jim
$
```

# 简化多跳 SSH 连接并透明地代理 SSH 连接

将以下内容放入 `~/.ssh/config` 文件中。

```
Host jump-host.example.com
ProxyCommand none
Host *.example.com
ProxyCommand ssh -W %h:%p jump-host.example.com
```

如果您需要访问位于 SSH 网关服务器或跳板服务器后面的主机，您可以通过指示 SSH 在您连接最终远程主机时自动使用 SSH 网关来简化操作。无需先连接网关，然后输入另一个 `ssh` 命令来连接目标主机，您只需在本地机器上输入 "ssh destination-host"。使用上述配置，此命令将通过 jump-host 将您的 ssh 连接代理到 server1。

```
$ ssh server1.example.com
$ uname -n
server1
$
```

# 断开远程会话并在稍后重新连接，从断点处继续

```
$ ssh remote-host
$ screen
ctrl-a, d
$ exit
$ ssh remote-host
$ screen -r
```

当我有一个需要在远程主机上完成的长时间运行进程时，我在启动该进程之前总是先启动一个 screen 会话。我不希望网络连接的中断干扰远程主机上正在执行的工作。有时我会启动一个进程，从会话中分离出来，然后稍后重新连接，以检查我不在场时产生的所有输出。

首先，ssh 到远程主机。接下来，启动一个 screen 会话。开始在远程主机上执行您的工作。通过输入 ctrl-a 然后按 d 来从 screen 会话中分离。您启动的进程在您离开时仍将在 screen 会话中运行。此外，生成的任何输出都可以在稍后查看。

```
$ ssh remote-host
$ screen
$ /usr/local/bin/migrate-db
Starting DB migration at Sun Apr 13 21:02:50 EDT 2014
<ctrl-a,d>
[detached]
$ exit
$ ssh remote-host
$ screen -r
Starting DB migration at 21:02
table1 migrated at 21:34
table2 migrated at 22:11
table3 migrated at 22:54
DB migration completed at 23:04
$ exit
[screen is terminating]
$ exit
```

要重新连接到您的 screen 会话，请连接到远程主机并输入 screen -r。如果有输出滚出了屏幕顶部之外，您可以通过输入 ctrl-a 然后按 escape 键来查看。现在使用 vi 导航键绑定来查看输出历史。例如，您可以输入 k 向上移动一行，或按 ctrl-b 向上翻一页。当您查看完输出历史后，按 escape 键返回实时会话。要退出您的 screen 会话，请输入 exit。

Screen 是最广泛使用和易于获取的屏幕复用器之一。然而，也有诸如 tmux、dtach 和 byobu 等替代方案。

# 配置 SSH 根据模式将域名附加到主机名

`~/.ssh/config` 的内容：

```
host-prefix*  !*.domain.com
    HostName %.domain.com
```

如果您通过 ssh 连接到多个域中的主机，每次都输入完全限定域名可能会令人疲惫。解决此问题的一种方法是将每个域添加到 /etc/resolv.conf 中的搜索列表中。解析器将尝试在搜索列表中的每个域中解析指定的主机名，直到找到一个能解析的域。

```
$ cat /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
search domain1.com domain2.com domain3.com
domain4.com domain5.com domain6.com domain7.com
```

当在上述 resolv.conf 配置下输入 "ssh remote-host" 时，解析器将尝试将 remote-host.domain1.com 转换为 IP 地址。如果失败，它将尝试解析 remote-host.domain2.com，等等。上述 resolv.conf 的问题在于搜索列表仅限于六个域。因此，remote-host.domain7.com 永远不会被尝试。此外，无论域的数量多少，搜索列表都限制在 256 个字符以内。

如何绕过六个域搜索列表的限制？如果幸运的话，您的主机名具有与域名相关联的模式，您可以配置 ssh 来进行解析。例如，对于像 "ny-www1.newyork.company.com" 和 "ny-mysql-07.newyork.company.com" 这样的 FQDN，您可以创建一个规则，将 "newyork.company.com" 附加到任何以 "ny." 开头的主机上。您还需要告诉 ssh 忽略任何已经附加了 "newyork.company.com" 的以 “ny” 开头的主机。以下是一个执行此操作的 ~/.ssh/config 文件示例。

```
$ cat ~/.ssh/config

ny* !*.newyork.company.com
      HostName %h.newyork.company.com
db* !*.databases.company.com
      HostName %h.databases.company.com
jump* !*.company.com
      HostName %h.company.com
```

现在，当您输入 `"ssh ny-test"` 时，ssh 将尝试连接到 `"ny-test.newyork.company.com"`。对于以 `"db"` 开头的主机，ssh 将 `".databases.company.com"` 附加到主机名。以 `"jump"` 开头的主机将附加 `".company.com"` 域名。

```
$ ssh ny-wwl
$ hostname -f
ny-wwl.newyork.company.com
$ exit
$ ssh jump-ny-01
$ hostname -f
jump-ny-01.company.com
$ exit
$
```

# 运行一个不受挂断影响的命令，允许在您断开连接后任务继续运行

```
$ nohup command &
```

通常，当您在后台启动一个任务并注销您的会话时，该任务会被终止。确保命令在您从主机断开连接后继续运行的一种方法是使用 nohup 命令。No hub 代表 no hang up（无挂断）。默认情况下，命令的输出存储在一个名为 `"nohup.out"` 的文件中，位于启动该程序的目录中。您可以稍后检查该文件的内容以查看命令的输出。若要使用不同的文件名，请使用重定向。

```
$ ssh db-server
$ nohup /usr/local/bin/upgradedb.sh &
[1] 13370
$ exit
$ ssh db-server
$ cat nohup.out
Starting database upgrade.
...
Database upgrade complete.
$ nohup /usr/local/bin/post-upgrade.sh >
/tmp/post.log &
[1] 16711
$ exit
$ ssh db-server
$ cat /tmp/post.log
Post processing completed.
$ ssh -D PORT remote-host
```

# 使用 SSH SOCKS 代理加密您的 Web 浏览数据

如果您正在使用开放的无线热点，并希望确保您的 Web 浏览数据被加密，您可以通过 SSH 将您的 Web 浏览流量重定向到另一台主机。使用 "-D" 选项启动 ssh，并提供要在本地计算机上打开以用于代理连接的端口。如果您只想执行端口转发而不实际登录到远程主机的 shell，请使用 ssh 的 "-N" 选项。配置您的 Web 浏览器使用 SOCKS 5 代理，使用 localhost 作为主机以及您提供给 ssh 的端口。

