
这将用于卸载你 Linux 计算机上的 *Apache2*。就是这么简单。这就是你安装和卸载 Linux 服务器所需的大多数软件的方法。随着你变得更加熟练并获得更多使用 Linux 的经验，你将开始在 Linux 世界中购买专有软件。

你可能会购买专门的备份软件，或者也许是专门的安全软件。其中一些类型的程序可能不在软件仓库中，你可能需要采取不同的步骤来安装这些程序。但对于任何人安装到 Linux 上的 99% 的程序，这个 *apt-get* 命令都适用。

这些仓库中有成千上万个 Linux 程序。弄清楚你想要安装哪些程序可能会有点棘手。如果你不知道在你的 Linux 计算机上哪些程序是最好的，最好的做法就是就此进行谷歌搜索。你会发现许多推荐给初学者的优秀 Linux 程序。

正如你现在可能已经知道的那样，每个人都嘲笑微软 Windows 背后的人们，因为他们总是有这些更新。每周的第三天或每个月，你至少会收到 10 个系统更新。很多人说这些更新是微软很糟糕的证据。然而，现实是每一个操作系统或软件都需要时不时地更新。Linux 也是如此。

因此，一旦你在 Linux 服务器上安装了所有你想要的软件并想要更新它们，你所需要做的就是使用 *upgrade* 命令。请参阅下方的语法：

```
$ sudo apt-get upgrade
```

上述命令的作用是比较仓库中的程序是否比你服务器上的版本更新。如果你拥有的程序版本比仓库中的版本旧，它会下载该信息并询问你是否希望更新你的软件。如果你选择“是”，它会自动更新你计算机上的所有软件。

关于安装和维护软件，目前你基本上需要理解的就是这些。

## 服务

正如我们之前提到的那样，Linux 最适合服务器。一旦你启动 Linux 服务器，它们就可以一直运行，直到硬件故障，字面意思上就是如此。一旦你启动 Linux 系统，你实际上需要重启它的次数非常少。当我们说非常少的时候，我们指的是一年一次；而这已经是过度了。

然而，当你进入并更改正在你的服务器上运行的软件中的配置文件时，你可能需要重启该单个软件或该单个服务。假设你在 Linux 服务器上安装了 *Apache2* 并更改了一些配置文件。这些配置文件直到你重启 *Apache2* 服务时才会被加载。

尽管计算机一直开机，但你不得不时不时地重启服务，以确保它们是最新的。我们现在将了解如何启动、停止和重启服务。

在此，你需要使用以下语法中的 stop（停止）：

```
$ sudo /etc/init.d/<name of the program or service> start
$ sudo /etc/init.d/<name of the program or service> stop
$ sudo /etc/init.d/<name of the program or service> restart
```

因此，假设你更改了服务器上 *Apache2* 程序中的配置文件，并且需要重启它。只需输入：

```
$ sudo /etc/init.d/Apache2 restart
```

这将重启 *Apache2* 服务，从而使你所做的任何配置更改生效。现在，假设你正在摆弄 Web 服务器，你正在做一些更改，并且你不想让外界的人在你进行更改时进入。因此，你希望完全停止服务，这基本上会使 Web 服务器离线。你要做的只是：

```
$ sudo /etc/init.d/Apache2 stop
```

上述命令停止了 Web 服务。然而，它不会停止其他任何东西。这意味着，虽然外界任何人都无法访问你托管的网站，但你仍然可以更改配置文件、编辑选项、修改设置等。此时，只有实际的 Web 服务器组件不在运行。

现在让我们看看在 Linux 命令提示符下实际执行时的样子。

```
Welcome to the Ubuntu Server!
* Documentation: http://www.ubuntu.com/server/doc

System information as of Fri Aug 20 11:42:30 EDT 2010

System load: 0.14
Usage of /: 11.2% of 7.49GB
Memory usage: 14%
Swap usage: 0%
Processes: 66
Users logged in: 0
IP address for lo: 127.0.0.1
IP address for eth0: 10.0.2.15

Graph this data and manage this system at https://landscape.canonical.com/

@server: $
```

现在我们在 Linux 服务器操作系统的命令提示符或终端处。在这个例子中，让我们假设你的系统上安装了 Apache2，并且你想要停止该服务。你应该做的第一件事是输入单词 sudo，在 sudo 后加一个空格，然后输入 /etc/init.d/Apache2，再在后面加一个空格，然后是单词 stop。

在你输入上述命令并按下 ENTER 之后，你会看到下面的屏幕：

```
Welcome to the Ubuntu Server!
* Documentation: http://www.ubuntu.com/server/doc

System information as of Fri Aug 20 11:42:30 EDT 2010

System load: 0.14
Usage of /: 11.2% of 7.49GB
Memory usage: 14%
Swap usage: 0%
Processes: 66
Users logged in: 0
IP address for lo: 127.0.0.1
IP address for eth0: 10.0.2.15

Graph this data and manage this system at https://landscape.canonical.com/

@server: $ sudo /etc/init.d/apache2 stop
* Stopping web server apache2
apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1 for ServerName
... waiting [ OK ]
@server: $ _
```

正如你在上面的屏幕中看到的，Linux 已成功停止该服务。此时，该 Web 服务器托管的域名在互联网上不可访问。网站当前处于离线状态。要启动服务，你只需要输入我们停止服务时输入的相同命令，只不过在末尾将 stop 替换为 start 即可。

```
Welcome to the Ubuntu Server!
* Documentation: http://www.ubuntu.com/server/doc
System information as of Fri Aug 20 11:42:30 EDT 2010
System load: 0.14
Processes: 66
Usage of /: 11.2% of 7.49GB Users logged in: 0
Memory usage: 14%
IP address for lo: 127.0.0.1
Swap usage: 0%
IP address for eth0: 19.0.2.15

Graph this data and manage this system at https://landscape.canonical.com/
@server: $ sudo /etc/init.d/apache2 stop
* Stopping web server apache2
apache2: Could not reliably determine the server's fully qualified domain name,
using 127.0.1.1 for ServerName
... waiting...
[ OK ]
@server: $ sudo /etc/init.d/apache2 start
* Starting web server apache2
apache2: Could not reliably determine the server's fully qualified domain name,
using 127.0.1.1 for ServerName
[ OK ]
@server: $
```

重启服务——自动启动和停止服务——只需输入相同的命令。唯一的例外是，在末尾不是输入 *start* 或 *stop*，而是输入 *restart*。再次强调，Linux 中这一点非常棒的是，你不必重启整个服务器。

如果你重启整个服务器，无论操作系统有多快，在一切恢复在线之前都需要几分钟。如果你只需要重启服务，一切将在几秒钟内恢复在线。

```
Welcome to the Ubuntu Server!
* Documentation: http://www.ubuntu.com/server/doc
System information as of Fri Aug 20 11:42:30 EDT 2010
System load: 0.14
Processes: 66
Usage of /: 11.2% of 7.49GB Users logged in: 0
Memory usage: 14%
IP address for lo: 127.0.0.1
Swap usage: 0%
IP address for eth0: 19.0.2.15

Graph this data and manage this system at https://landscape.canonical.com/
@server: $ sudo /etc/init.d/apache2 stop
* Stopping web server apache2
apache2: Could not reliably determine the server's fully qualified domain name,
using 127.0.1.1 for ServerName
[ OK ]
@server: $ sudo /etc/init.d/apache2 start
* Starting web server apache2
apache2: Could not reliably determine the server's fully qualified domain name,
using 127.0.1.1 for ServerName
[ OK ]
@server: $ sudo /etc/init.d/apache2 restart
* Restarting web server apache2
apache2: Could not reliably determine the server's fully qualified domain name,
using 127.0.1.1 for ServerName
apache2: Could not reliably determine the server's fully qualified domain name,
using 127.0.1.1 for ServerName
[ OK ]
@server: $
```
