
221 Thank you for using the FTP service on phoenix.

这是一个简单的示例，但典型的 FTP 会话通常也是微不足道的。在 FTP 会话期间还有其他可用的命令，但它们很少被使用。FTP 具有接收脚本输入并定义宏的功能，从而允许进行更复杂的会话。

> **提示**
> FTP 的信息页面与 Linux 中几乎每个命令都附带的手册（man）页面非常相似。可以在命令的源代码包中找到更详细的信息。

## 使用 `lftp` 命令进行文件传输

`lftp` 命令可用于使用 FTP、HTTP 以及各种安全协议（如 HTTPS 和 FTP）进行文件传输（如果启用了远程代理）。此命令的两个强大功能是能够重新启动停滞的下载（在文件传输中途），以及能够在单个会话中启动和运行多个下载（带作业控制）。

例如，下面是一个简单的会话，展示了从运行 Apache Web 服务器的远程计算机通过 HTTP 获取文件：

```bash
$ lftp http://192.168.2.37

cd ok, cwd=/ 

lftp 192.168.2.37:/> ls

-rw-r--r--  --  manual/mod/core.html

-rw-r--r--  --  manual/index.html

-rw-r--r--  --  icons/apache_pb.gif

-rw-r--r--  --  poweredby.png

lftp 192.168.2.37:/> get poweredby.png

1154 bytes transferred

lftp 192.168.2.37:/> bye
```

`lftp` 命令也可以用作传统的 FTP 客户端，但具有一些有趣的功能：

```bash
$ lftp 192.168.2.67 -u phudson

Password:

lftp phudson@192.168.2.67:~> cd /d2/isos/redhat/limbo

cd ok, cwd=/d2/isos/redhat/limbo

lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> mget disc1 &

[0] mget *disc1* &

lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> jobs

[0] mget *disc1*
    'limbo-1386-disc1.iso' at 56436448 (8%) 1.08Mi/s eta:9m [Receiving data]

lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> bye

[1843] Moving to background to complete transfers...

$ ps aux | grep lftp

phudson 1843 7.6 1.0 5456 2404 ? S 19:09 0:02 lftp 192.168.2.67
```

可以使用 `-u` 选项在命令行上传递用户名（和密码）。您可以使用此功能来减少获取远程文件时所需的交互式输入量，作为在 shell 脚本中使用 `lftp` 的辅助，以及当作为后台进程使用 `lftp` 获取文件时。

通过使用 ampersand（`&`），获取操作在后台进行，如前面的示例所示。`jobs` 命令用于显示当前的传输。如果用户注销会话（使用 `bye` 命令），文件传输将作为后台进程继续，直到完成。（这可以通过使用 `ps` 命令来验证。）

`lftp` 客户端具有许多额外功能，可以使文件传输工作比使用其他 FTP 客户端更容易。

> **注意**
> 另一个随 Fedora 提供的便捷的基于文本的文件传输实用程序是 `curl`，它支持使用 HTTP 进行文件获取。

## 使用 `wget` 命令进行文件传输

`wget` 命令用于使用 FTP、HTTP 以及各种安全协议（如 HTTPS 和 HTTP，如果启用了远程代理）进行文件传输。然而，与其他 FTP 客户端不同，`wget` 仅支持非交互式传输。这实际上是一个功能，因为 `wget` 可以作为后台进程下载文件，并递归复制远程文件目录。该命令还支持完成部分下载的文件，这可以在连接中断或不稳定的期间节省大量时间。

例如，下面是一个示例调用，展示了使用 `wget` 和 FTP URL 从远程计算机进行 FTP 获取：

```bash
$ wget ftp://phudson:mypasswd@stinky/mp3/*

--13:13:28--  ftp://phudson:*password*@stinky/mp3/*

             => '.listing'

Resolving stinky... done.

Connecting to stinky[192.168.2.33]:21... connected.

Logging in as phudson ... Logged in!

=> SYST ... done.     => PWD ... done.

=> TYPE I ... done.    => CWD /home/paul/mp3 ... done.

=> PORT ... done.      => LIST ... done.

 [ <=>                             ] 648          632.81K/s

13:13:28 (632.81 KB/s) - '.listing' saved [648]

Removed '.listing'.

--13:13:28--  ftp://phudson:*password*@stinky/mp3/C318121-01A.mp3

              => 'C318121-01A.mp3'
```
