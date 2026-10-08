
回到列表 29.1 的第 13 行，你调用了 `getservbyname()`，它提供了形成完整网络地址所需的另一个值。此值被称为“服务端口号”，是你想要通信的地址部分。端口号是一个 16 位整数，成为应用程序用于形成连接端点的源地址和目标（客户端或服务器）IP 地址的一部分。如果你执行 `netstat`，你会看到多个带有关联端口号的 IP 地址对（这些数字实际上可能会被 `etc/services` 文件中的服务端口名称替换）。这种 IP 地址和端口号的组合被称为套接字（socket）。

就像主机地址一样，服务端口可以通过名称而不是数字引用。`getservbyname()` 从 `etc/services` 文件检索与指定名称关联的数字。如果可用 NIS，也可以从网络数据库中检索该数字。此数据库中列出的端口号被称为“常用端口”（0 到 1023）。理论上，任何主机都可以连接到任何机器上的任何这些服务，端口号通常保持一致（例如，无论你使用 UNIX 还是 Windows，Telnet 都使用端口 23）。尽管这在 99% 的情况下都是 true实的，但 `etc/services` 文件可以被轻易修改，因此要注意损坏。不依赖于常用端口的应用程序被称为“临时端口”，被认为可供任何应用程序使用。应用程序使用的端口号不需要列在该数据库中或从该数据库中检索；将它们列在 `/etc/services` 中并共享以防止冲突被认为是一个主意。

在你获取了构建完全地址所需的两个组件后，你将它们提供给 `sockaddr_in` 函数，该函数为你构建一个 `SOCKADDR_IN` 结构。`SOCKADDR_IN` 是大多数套接字系统调用所需的网络地址的程序表示。

# 套接字

在使用你的地址信息之前，你需要先……。第 27 行的 `socket()` 函数说明了如何创建一个套接字。可能的套接字类型有 `SOCK_STREAM`、`SOCK_GRAM`、`SOCK_RAW`、`SOCK_RDM` 和 `SOCK_PACKET`。最后三个用于低级高级操作，超出了本章的范围。

`SOCK_STREAM` 套接字是端端连接的，是可靠的，且它们之间的消息是有序的。“可靠”和“有序”在网络中有特殊含义。可靠性是指网络保证交付的事实：应用程序可以写一个数据包并理解它将到达另一端，除非连接因灾难性事件突然中断，例如主机的意外关闭或网络本身的断裂。有序意味着所有消息都按照发送顺序交付给另一个应用程序（它并不意味着）。

`SOCK_DGRAM` 套接字支持无连接且不可靠的数据报。数据报通常是固定长度的小消息。应用程序无法保证数据报会被交付，或者即使交付了，是否有序。从表面上看，似乎没有应用程序想要使用 `SOCK_DGRAM`，但正如你将看到的，许多应用程序确实这样做，且理由充分。

套接字类型与所使用的协议密切相关。在互联网套接字的情况下，`SOCK_STREAM` 始终实现 TCP，`SOCK_DGRAM` 套接字实现 UDP。

# 协议与套接字类型

在下面的 `socket()` 调用中，你指定协议族、套接字类型和协议。我已经涵盖了你将使用的协议族，对于互联网是 `PF_INET`。

```
socket (CONNFD, PF_INET, SOCK_STREAM, $proto);
```

TCP 协议的特性与 `SOCK_STREAM` 的特性相匹配。TCP 数据包保证交付，除非发生网络灾难（连接另一端的工作站掉线或网络本身遭遇严重的……

## 网络编程

## 第 29 章

（可用性中断）。数据包总是按照发送应用程序写入的顺序交付给应用程序的。显然，这些属性使得网络开发人员的工作变得简单，因为消息可以被写入后基本上就被置之不理，但是有代价的：在网络和计算资源方面，TCP 消息比 UDP 消息昂贵得多（要求也更高）。会话两端的工作站必须确认它们已接收到正确信息，这导致操作系统的工作量增加，网络流量增加。两个系统还必须跟踪消息发送的顺序，并且取决于网络“地形”的状态，很可能必须存储消息直到其他消息到达。（当消息在等待其他 TCP 连接因错误而重传时，新消息已经到达）。此外，TCP 连接仅仅是——连接——这本身也是代价的。每次对话都有与之关联的端点，因此拥有多个客户端的服务器必须在多个套接字之间进行调度，这可能非常困难（本章稍后将介绍 TCP 的 I/O 多路复用细节）。

UDP 与 SOCK_DGRAM 不同，它是无连接的，这意味着传输层并不保证发送的每个数据包都能到达目标机器。尝试将 UDP 想象成一种“发后即忘”协议。在某种程度上，它被认为是不可靠的，但在如今的局域网（LAN）中，UDP 通常被认为是非常可靠的。广域网（WAN）中的 UDP 通常更容易出错，因为你不知道数据包在 WAN 中经过的网络和机器的可靠性。

使用 UDP 时，应用程序必须为其执行的任务提供任何必要的可靠性机制。对于某些应用程序来说，这是一个优势，因为 TCP 提供的机制并不总是需要的。例如，使用 UDP 的 DNS 仅仅是发送消息并并在预定间隔内等待响应；因为 DNS 是一种一对一的消息与响应协议，所以客户端和服务器之间的序列化排序并不是必须的。UDP 是无连接的，因此服务器可以使用一个套接字与许多客户端通信。所有客户端向服务器的同一个地址写入数据，服务器通过向特定的客户端地址写入数据来单独响应。

UDP 消息还可以广播到整个网络——这对于需要与许多用户通信的工作站来说是福音，但对于不需要该消息但必须弄出它不属于自己的工作站来说却是灾梦。由于 UDP 不需要预先连接，它被认为比 TCP 快得多；然而，供应商正在努力提高 TCP 的速度，因此在未来这可能不再总是成立。

## 建立连接

逻辑上，如果你正在创建一个像列表 29.1 中 `makeconn()` 函数那样的连接，你需要创建一个 `SOCK_STREAM` 套接字，并使用第 15 行通过 `getprotobyname()` 获取的 TCP 协议信息。查看列表 29.1 的第 27 和 28 行，此处此处：

```
27: socket(CONFNFD, AF_INET, SOCK_STREAM, $proto);
28: connect(CONFNFD, $servaddr) or die "connect : $1";
```

在第 27 行创建套接字后，你将其由 `sockaddr_in()` 创建的地址结构传递给 `connect()`。`connect()` 函数实际上会联系结构中指定的地址，并建立 TCP 支持的虚拟电路。

## 一个 TCP 客户端示例

列表 29.3 在示例程序中使用 `makeconn()`。`client1` 可以在书籍的 CD-ROM 中找到。

- 列表 29.3 client1

```perl
#!/usr/bin/perl
use Socket;
require "./network.pl";

$NETFD = makeconn($ARGV[0],$ARGV[1]);

#
# 获取消息
#
sysread $NETFD, $message, 32768 or die "error getting message : $!"
print "$message\n"
close $NETFD;
```

使用两个命令行参数运行此程序：运行着 sendmail 的 Linux 主机名称和邮件端口名称，smtp：

```
$ ./client1 iest smtp

220 jest.home.mxr.com ESMTP Sendmail 8.8.5/8.8.5; Sat, 4 Oct 1997 18:25:08

-0400
```

此程序使用 `makeconn()` 连接到运行在指定主机上的 sendmail 程序，并使用 `sysread()` 函数读取主机在首次连接时发送给新客户端的问候语。

`sysread()` 是从套接字中提取网络消息的函数之一。它是 UNIX `read()` 系统调用的封装。你不能使用 Perl 的 `read()` 函数，因为它是为标准 I/O 设计的，使用了缓冲和其他高级功能，这些功能会干扰网络通信。在实际应用中，你可能会使用 `sysread()` 从你自己的缓冲区中读取消息，并仔细跟踪你刚刚读取的内容，因为你在 `read` 调用期间可能会被信号中断。（你还会安装信号处理程序。）如此示例所示，建立客户端连接并检索一些数据非常简单。

> 提示
> 使用 Perl 进行网络编程的好处之一是它隐藏了不同架构之间的字节序问题。例如，Intel x86 芯片和 Sun SPARC 芯片对值的表示方式不同。互联网的创建者引入了“网络序”的概念，在这种序中，程序应该将其转换回自己的格式。

## 一个 TCP 服务器示例

现在你将编写自己的服务器，客户端可以连接到该服务器。首先，你必须使用 `makelisten()` 将套接字置于监听状态，这是列表 29.4 所示的另一个函数。

- 列表 29.4 makelisten()

```perl
1: sub makelisten {
2:     my $portname = $_[0];
3:     my $port = getportname($portname) or die "getportname : $!";
4:     
5:     my $proto = getprotobyname('tcp') or die "getprotobyname : $!";
6:     
7:     my $LISTFD = socket(AF_INET, SOCK_STREAM, $proto);
8:     
9:     #
10:    # 绑定 inet 地址
11:    my $servaddr = sockaddr_in($port, INADDR_ANY);
12:        bind($LISTFD, $servaddr) or die "bind : $!";
13:    listen($LISTFD, SOMAXCONN) or die "listen : $!";
14:    return $LISTFD;
15: }
```

绑定套接字后，你可以执行 `listen()`，它通知系统你已准备好接受客户端连接。

使用 `makelisten()` 的 `server1` 与客户端一样简单，所示如列表 29.5。

```perl
#!/usr/bin/perl
use Socket;
require "./network.pl";
$hello = "Hello world!";
$LISTFD = makelisten("test");
```

```
LOOP: while ($1) {
  unless ($paddr = accept(NEWFD, $LISTFD)) {
    next LOOP;
  }
  syswrite(NEWFD, $hello, length($hello));
  close NEWFD;
}
```

在列表 29.5 中，你只需使用 `makelist()` 将套接字设置为监听状态，然后进入一个以 `accept()` 函数为中心的 `while` 循环。`accept()` 的目的正如其名，即接受客户端连接。你向 `accept()` 传递了两个参数：一个新变量（`NEWFD`），它包含已接受连接的套接字标识符；以及通过 `listen()` 设置的套接字（`LISTFD`）。

每当 `accept()` 返回连接时，你就向新套接字写入一个字符串并立即关闭它。

在测试服务器之前，你需要为它所使用的测试服务添加条目。在 `/etc/services` 文件中添加以下三行。你需要 root 权限才能编辑此文件。

```
test    8000/tcp
test    8000/udp
test1   8001/udp
```

你为你的测试程序添加了三个条目，一个用于 TCP，另外两个用于稍后将使用的 UDP。

现在，为了测试你的服务器，你需要执行以下命令：

```
$ ./server1& test
$ ./client1 test
Hello world!
```

`test` 是你工作站的主机。服务器写回你的问候并退出。由于服务器在 `while` 循环中执行，你可以反复运行 `./client1`。当测试完成后，使用 `kill` 停止服务器：

```
$ ps ax grep server! | awk '{ print $1 }'
pid pid
$ kill pid
```

# 一个 UDP 示例

为了在 UDP 中实现相同的测试，你必须为客户端和服务器都设置一个 `SOCK_DGRAM` 套接字。这个函数 `makeudpcli()` 也可以在 `network.pl` 中找到，并显示在列表 29.6 中。

![](img/7675e31a0e104594fbf0bbbebdf7e922_724_0.png)

# 列表 29.6 makeudpcli()

```
sub makeudpcli {
    my ($proto, $servaddr);
    $proto = getprotobyname('udp') or
    die 'getprotobyname: cannot get proto: $!';
    #
    # 绑定一个 UDP 端口
    #
    socket(DFGD, PF_INET, SOCK_DGRAM, $proto);
    bind(DFGD, sockaddr_in(0, INADDR_ANY)) or die "bind: $!";
    return DFGD;
}
```

在列表 29.6 中，获取 UDP 的协议信息，然后创建一个 `SOCK_DGRAM` 套接字。你对其进行了绑定，但你告诉系统绑定到任何地址和任何服务端口；换句话之，你想要这个套接字，但不在乎名字具体是什么。

之所以额外进行 `bind()` 的原因非常简单。因为 UDP 是无连接的，因此在发送和接收数据报时，必须特别注意地址。当读取数据报消息时，读取者也会接收到源者的地址，以便知道将任何回复发送到哪里。如果你想接收消息的回复，`bind()` 调用将确保系统为你分配一个唯一的地址。

现在你已经创建了一个数据报套接字，你可以使用列表 29.7 中的程序 `client2` 与服务器通信，该程序可以在 CD-ROM 中找到。

# 列表 29.7 client2

```
1: #!/usr/bin/perl
2:
3: use Socket;
4: require ".network.pl";
5:
6: $spoke = "you";
7:
8: $NETFD = makeudpcli();
9:
10: #
11: # 计算服务器地址
12: #
13: $addr = gethostbyname($ARGV[0]);
14: $port = getservbyname($ARGV[1], 'udp');
15:
16: $servaddr = sockaddr_in($port, $addr);
17:
18: #
19: # 探测服务器
20: #
21: send $NETFD, $poke, 0, $servaddr;
22:
23: #
24: # 接收回复
25: #
26: recv $NETFD, $message, 32768, 0 or die "error getting message : !"
27: print "$message \n"
28: close $NETFD;
```
