
```
[0] mget *disc1*
  'limbo:1386-disc1.iso' at 56436448 (8%) 1.08M/s eta:9m [Receiving data]
lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> quit
[1843] Moving to background to complete transfers...
$ ps aux | fgrep lftp
phudson   1843  7.6  1.0  5456 2404 ?        S    19:09   0:02 lftp 192.168.2.67
```

可以通过 `-u` 选项在命令行上传入用户名（和密码）。利用此功能，可以在检索远程文件时减少所需的交互式输入，有助于在 Shell 脚本中使用 lftp，以及通过 lftp 在后台检索文件。

如前面的示例所示，通过使用与号（&），可以在后台执行检索。然后使用 `jobs` 命令显示当前传输。如果用户（使用 `quit` 命令）退出会话，则尚未完成的文件传输将继续作为后台进程运行。（这可通过 `ps` 命令验证。）

lftp 客户端还具有许多其他功能，这使得传输文件的工作比使用其他 FTP 客户端更加容易。

## 注意

Ubuntu 中另一个方便的基于文本的文件传输实用程序是 curl，它支持通过 HTTP 进行文件检索。

## 使用 wget 命令进行文件传输

wget 命令用于通过 FTP、HTTP 以及各种安全协议（如 HTTPS 和 HTFP，如果启用了远程代理）进行文件传输。然而，与其他 FTP 客户端不同，wget 仅支持非交互式传输。这实际上是一个特性，因为 wget 可用于在后台下载文件，并递归复制远程文件目录。该命令还支持对已部分下载的文件进行续传，这在连接间歇性中断或连接断开期间可以节省大量时间。

例如，下面是一个简单的调用示例，演示如何使用 wget 和 FTP URL 从远程计算机进行 FTP 检索：

```
$ wget ftp://phudson:mypassword@stinky/mp3/*
--13:13:28--  ftp://phudson:*password*@stinky/mp3/*
    => '.listing'
Resolving stinky... done.
Connecting to stinky[192.168.2.33]:21... connected.
Logging in as phudson ... Logged in!
==> SYST ... done.     ==> PWD ... done.
==> TYPE I ... done.   ==> CWD /home/paul/mp3 ... done.
==> PORT ... done.     ==> LIST ... done.
```

```
13:13:28 (632.81 KB/s) - `.listing` saved [648]

Removed `.listing`.
--13:13:28--  ftp://phudson:*password*@stinky/mp3/C31821-01A.mp3
    => `C31821-01A.mp3`

==>
CWD not required.
==>
PORT ... done.  ==> RETR C31821-01A.mp3 ... done.
Length: 5,172,089

60% [====================>          ] 3,123,680  264.80K/s  ETA 00:07
```

在此示例中，用户检索名为 stinky 的远程主机上名为 mp3 的目录（位于 /home/paul 下）中的所有文件。wget 命令将首先获取目录列表，然后继续下载指定的文件（在此示例中所有以 `*` 标记的文件）。请注意，您可以在命令行上指定用户名和密码（示例中的 mypassword）。这通常不是一个好主意。更好的做法（但仍然不够安全）是将密码保存在主目录中名为 `.wgetrc` 的文件中。有关更多信息，请参阅 wget 手册页，或查看位于 http://www.gnu.org/software/wget/manual/wget-1.8.1/html_mono/wget.html 的唯一文档。

## 提示

wget 的另一个常见用途是下载网站的完整副本以供离线阅读，尽管这对那些不得不为所有带宽付费的网站所有者来说不太友好！

要下载整个网站，您需要指定 --mirror、--convert-links 和 -p 参数，后跟要下载的网站的 URL。第一个参数告诉 wget 下载网站中的所有页面和图片，并尽可能跟踪链接。第二个参数告诉它重写 HTML，使其在本地浏览时能够正常工作。最后一个参数 -p 告诉 wget 下载 HTML 中引用的所有文件，例如声音、CSS 文件和其他相关文档。您可能还想指定 -w 参数，该参数允许您指定每次 wget 请求之间的间隔秒数；这样可以避免下载使 Web 服务器过载。因此，下载网站的完整命令是 wget --mirror --convert-links -p -w 2 http://www.example.com/。

## 使用图形化 FTP 客户端

Linux 下有许多图形化 FTP 客户端可用。Ubuntu 包含了图形化的 gFTP 客户端（位于 gftp-gtk 软件包中）以及 GNOME 和 KDE 自带的支持网络的浏览器。这些浏览器具有内置的拖放功能，因此可以提供 FTP 功能。其他可用于 FTP 的图形界面客户端包括 Firefox 网络浏览器（尤其以 FireFTP 扩展为佳）、KDE 的 Konqueror、GNOME 的 Epiphany 以及 Nautilus 文件管理器。
