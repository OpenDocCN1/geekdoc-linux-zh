
$ `rsh upsun29 sort students > sorted_students`

$

```
在下面的命令行中，`sort` 命令从本地机器 `upsun10` 上的 `students` 文件读取输入。与前一个命令一样，输出被发送到本地机器上的 `sorted_students` 文件。
```

$ `rsh upsun29 sort < students > sorted_students`

$

如果你希望 `sort` 命令从本地文件 `students` 读取输入并将排序结果存储在远程机器上的 `sorted_students` 文件中，你必须用引号引起来远程命令并进行输出重定向，如下所示：

```
$ cat students | rsh upsun29 'sort > sorted_students'
```

你可以将 I/O 重定向运算符与管道运算符结合起来，创建强大的命令行，这些命令行可以从本地和远程文件获取输入，在本地和远程机器上执行命令，并将最终结果发送到本地或远程机器上的文件。我们在第 9 章中讨论了一些这样的命令行，现在我们应该重新回顾一下。

当 `rsh` 命令不带参数使用时（参数是可选的），它会退回到 `rlogin` 命令。在这种情况下，`rlogin` 命令的所有规则都适用，并且在正常登录期间执行的所有隐藏文件都会被执行。下面的会话展示了不带参数使用 `rsh` 命令的情况。在第一个示例中，该命令用于登录同一网络上的 `upsun29`。在第二个示例中，`rsh` 命令用于登录互联网上不同网络上的主机。

```
$ rsh upsun29

Last login: Mon Oct 20 18:31:17 from upibm7.egr.up.ed

Sun Microsystems Inc.
```

```
SunOS 5.5.1 Generic May 2014

) SPLAY 5 ( TERM 5 (vt100)

$
$ rsh cs00.syi.pcc.edu -l msarwar

msarwar's Password:

Last login: Mon Oct 20 18:56:07 PST 2014 on /dev/pts/2 from

upibm7.egr.up.edu

[ YOU HAVE NEW MAIL]
```

## 11.8.8 文件传输

你可以使用 `ftp`（文件传输协议）命令在同一网络或另一个网络上的远程机器之间传输文件。该命令通常用于在互联网上的远程主机之间传输文件。以下是该命令的简要说明。

### SYNTAX

`ftp [options] [host]`

目的：从远程主机或向远程主机传输文件
常用选项/功能：
- `d` 启用调试
- `i` 禁用多文件传输时的提示
- `v` 显示所有远程响应

正如我们在本章前面提到的，文件传输协议是一种基于 TCP 的客户端-服务器协议。当你运行 `ftp` 命令时，你的主机上会启动一个 `ftp` 客户端进程，并尝试与远程主机上运行的 `ftp` 服务器进程建立连接。如果在客户端发起连接请求之前远程主机上未运行 `ftp` 服务器进程，则连接不会建立，并且 `ftp` 命令会显示 `Unknown host` 错误消息。运行 `ftp` 服务器进程的站点称为 `ftp` 站点。当与远程 `ftp` 站点建立了 `ftp` 连接后，你可以运行多个 `ftp` 命令以有效使用此实用程序。但是，你必须具有适当的访问权限才能向远程站点传输文件。表 11.5 列出了一些有用的 `ftp` 命令。

大多数 `ftp` 站点要求你在使用该站点传输文件时拥有该站点的有效登录名和密码。一些站点允许你使用 `anonymous` 作为登录名，使用 `guest` 或你的完整电子邮件地址作为密码来建立 `ftp` 会话。此类站点被称为允许匿名 `ftp`。换句话说，匿名 `ftp` 是一种使用 `ftp` 协议下载公共文件的方法。匿名登录通常只能下载。如果你拥有 `ftp` 站点计算机上的账户（即不是匿名登录），那么你几乎肯定被允许下载和上传文件。

下面的会话说明了如何使用 `ftp` 实用程序对站点 `ftp.FreeBSD.org` 进行匿名 `ftp` 并传输 10.1 版本的压缩内核。在此过程中，

## 表 11.5 有用的 ftp 命令摘要

| 命令 | 含义 |
|---|---|
| `! [cmd]` | 在本地机器上运行 `cmd`；如果没有 `cmd` 参数，则调用交互式 shell |
| `Help [cmd]` | 显示 `cmd` 的摘要；如果没有 `cmd` 参数，则显示所有 `ftp` 命令的摘要 |
| `ascii` | 将 `ftp` 通道设为 ASCII 模式；用于传输 ASCII 类型文件，如文本文件 |
| `binary` | 将 `ftp` 通道设为二进制模式；用于传输非 ASCII 文件，如包含可执行代码或图片的文件 |
| `cd` | 更改目录；类似于 UNIX `cd` 命令 |
| `close` | 关闭与远程主机的 `ftp` 连接，但仍停留在 `ftp` 中 |
| `dir remotedir localfile` | 将 `remotedir` 的列表保存到本地主机的 `localfile` 中；对于较长的目录列表很有用，因为 `ftp` 命令不能使用管道 |
| `get remotefile [localfile]` | 将 `remotefile` 传输到本地机器当前工作目录中的 `localfile`；如果未指定 `localfile`，则使用 `remotefile` 作为本地文件名 |
| `ls [dname]` | 显示指定目录 `dname` 的内容；如果未指定则为当前目录 |
| `mget remotefiles` | 从远程主机向本地主机传输多个文件 |
| `mput localfiles` | 从本地主机向远程主机传输多个文件 |
| `open [hostname]` | 尝试与远程主机建立连接；如果未指定 `hostname` 参数则提示输入 |
| `put localfile [remotefile]` | 将 `localfile` 传输到远程主机的 `remotefile`；如果未指定 `remotefile`，则使用 `localfile` 作为远程文件名 |
| `quit` | 终止 `ftp` 会话 |
| `user [login_name]` | 如果无法通过指定 `user_name` 作为命令参数在远程主机上以用户身份登录；如果未指定 `user_name` 则出现提示 |

我们演示了 `ftp` 命令 `cd`、`get`、`ls` 和 `pwd` 的使用。我们还演示了在本地主机上执行 `ls` 命令。最后，我们使用 `quit` 命令终止 `ftp` 会话。该站点对匿名 `ftp` 不需要任何密码。因此，在提示输入密码时按 `<Enter>`。

```
% ftp ftp.FreeBSD.org

Trying 149.20.53.23:21 ...

Connected to ftp.geo.FreeBSD.org.

220 This is ftp0.isc.freebsd.org - hosted at ISC.org

Name (ftp.FreeBSD.org:sarwar): anonymous

331 Please specify the password.

Password: <Enter>

230-

230-This is ftp0.isc.FreeBSD.org, graciously hosted by

230-Internet Systems Consortium - ISC.org.

230-

230-FreeBSD files can be found in the /pub/FreeBSD directory.

230-

230 Login successful.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> cd pub/FreeBSD

250-ISO images of FreeBSD releases may be found in the releases/

ISO-IMAGES

250-directory. For independent files and tarballs, see individual

250-releases/${machine}/${machine_arch} directories. For example,

250-releases/amd64/amd64 and releases/powerpc/powerpc64.

250 Directory successfully changed.

ftp> pwd

Remote directory: /pub/FreeBSD

ftp> cd releases/i386

250 Directory successfully changed.

ftp> pwd

Remote directory: /pub/FreeBSD/releases/i386

ftp> ls

229 Entering Extended Passive Mode (|||55844||).

150 Here comes the directory listing.

lrwxr-xr-x  1 ftp  ftp  17 Jan 17  2014 10.0-RELEASE ->
