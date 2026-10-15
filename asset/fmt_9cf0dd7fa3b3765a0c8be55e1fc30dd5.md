
`$NETFD = makeconn($ARGV[0], $ARGV[1]);`

# 获取消息

`sysread $NETFD, $message, 32768 or die "error getting message : $"`

`print "$message \n"`

`close $NETFD;`

# 网络编程

第 28 章

使用两个命令行参数运行此程序：运行 sendmail 的 Linux 主机名称以及邮件端口 smp：

```
$ client1 i smtp

220 jest.home.mxn ESMTP Sendmail 8.8.5/8.8.5; Sat, 4 Oct 1997 18:25:08 -0400
```

此程序使用 `makeconn()` 连接到运行在指定主机上的 sendmail 程序，并使用 `sysread()` 函数读取在连接时发送给新客户端的问候语。

`sysread()` 是用于从 socket 提取网络消息的函数之一。它是 UNIX `read` 系统调封装。你不能使用 Perl 的 `read()` 函数，因为它是为标准 I/O 设计的，使用了缓冲和其他高级特性，这些特性会干扰网络通信。在实际应用中，如果你跟踪了刚刚读取的内容，可能会使用 `sysread()` 在缓冲区中进出地读取消息，因为读取调用可能会被信号中断。（你还会安装信号处理器。）正如这个示例所展示，建立客户端连接并检索某些数据非常简单。

> 提示
> 使用 Perl 进行网络编程的优势之一是它隐藏了不同架构之间的字节序问题。例如，Intel x86 芯片和 Sun SPARC 芯片表示值的方式不同。网络字节序的创建者要求程序在传输前将值放入其中，并在读取消息时必须将其转换回网络格式。Perl 为我们完成了这些。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_616_0.png)

# 一个 TCP 服务器示例

现在你将编写一个供 `client1` 连接的服务器。首先，你必须将 socket 置于监听状态。你将使用另一个在 `network.pl` 中的函数 `makelist()`，它显示在列表 28.4 中。

## 列表 28.4. makelist().

```
1: sub makelist { 
2:
3:     my ($hostname, $port, $proto, $servaddr);
4:     $hostname = \$_[0];
5:
6:     #
7:     # port and protocol
8:
9:     $port = getservbyname($hostname, 'tcp') or
```

## 列表 28.4. 继续

```
10:    die getservbyname: cannot get port : $!';
11:    $proto = getprotobyname('tcp') or
12:    die 'getprotobyname: cannot get proto : $!';
13:
14:
15:    # 绑定一个 inet 地址
16:     #
17:    socket(LISTFD, AF_INET, SOCK_STREAM, $proto) or
18:    bind(LISTFD, sockaddr_in($port, INADDR_ANY)) or die "bind: $!";
19:    listen(LISTFD, SOMAX) or die "listen: $!";
20:
21:    return LISTFD;
22: }
```

# 自动化、编程与修改源代码

## 列表 28.6. makeudpcli().

```perl
sub makeudpcli {
  my ($proto, $servaddr);
  $proto = getprotobyname('udp') or
  die 'getprotobyname: cannot get proto : $!';
  # 绑定 UDP 端口
  #
  socket(DGF, PF_INET, SOCK_DGRAM, $proto);
  bind($DGF, sockaddr_in(0, INADDR_ANY)) or die 'bind: $!';
  return $DGF;
}
```

在 28.6 中，获取了 UDP 的协议信息并创建一个 `SOCK_DGRAM` 套接字。然后对其进行绑定，但你告诉系统直接绑定到任何地址和任何服务端口；换句话说，你希望套接字被绑定，但不在乎它的名称是什么。

这种绑定的原因非常直观。因为 UDP 是无连接的，在发送和接收数据报时必须特别注意地址。当读取到数据报消息时，读取者也会接收到发送者的地址，以便知道将回复发送到哪里。如果你想接收对你消息的回复，你需要确保这些回复来自一个唯一的地址。`bind()` 调用确保了系统为为你分配一个唯一的地址。

现在你已经创建了一个数据报套接字，可以与服务器进行通信，列表 28.7 中的程序 `client2` 就是此类示例，可以在光盘中找到。

## 列表 28.7. client2.

```perl
1: #!/usr/bin/perl
2:
3: use Socket;
4: require "./network.pl";
5:
6: $poke = "yo!\n";
7:
8: $SNETFD = makeudpcli();
9:
10: # 计算服务器地址
11: #
12: $addr = gethostbyname($ARGV[0]);
13: $port = getservbyname($ARGV[1], 'udp');
14:
15: $servaddr = sockaddr_in($port, $addr);
16:
17: #
18: # 向服务器发送探测包
19: #
20: send $SNETFD, $poke, 0, $servaddr;
21:
22: #
23: # 接收回复
24: #
25: recv $SNETFD, $message, 32768, 0 or "error getting message : $!";
26: print "$message\n";
27: close $SNETFD;
```

在你创建套接字后，你必须解析服务器地址，但不是将此地址提供给 `connect()` 函数，而是必须将其提供给第 21 行的 `send()` 函数，以便它知道要将消息发送到哪里。但你为什么要向服务器发送任何东西呢？在查看列表 28.3 的 TCP 示例之后，通信是单向的。

在 TCP 示例中，服务器会在你连接后立即发送消息并关闭会话。连接消息的行为实际上是从客户端到服务器的。因为 UDP 是无连接的，你必须使用客户端的消息来完成对话。

服务器创建 UDP 套接字的方式略有不同，因为它需要绑定一个已知端口。它使用 `getservbyname()` 来获取端口号，并将其作为 `bind()` 代码的一部分指定。详细信息请查看 `network.pl` 中的 `makeudpserv()`。

服务器的主循环实际上与 TCP 服务器非常相似，显示在列表 28.8 中。

## 列表 28.8. server2.

```perl
#!/usr/bin/perl
#
#
use Socket;
require "./network.pl";
$hello = "Hello world!";
$LISTFD = makeudpserv("test");
while (1) {
  $scliaddr = recv $LISTFD, $message, 32768, 0;
  print "Received $message from client\n";
  send $LISTFD, $hello, 0, $scliaddr;
}
```

服务器不是通过循环 `accept()` 函数来等待客户端，而是循环 `recv()` 函数。在向客户端发送回复后，也没有新的套接字需要关闭。

当这些程序运行时，你将看到以下内容：

```
$ ./server2
./client2 list test
Received yo! from client
Hello world!
```
