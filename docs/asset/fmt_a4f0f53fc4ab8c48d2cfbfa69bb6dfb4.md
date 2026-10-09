
这一行告诉`make`运行多个进程来`buildworld`。

似乎无论如何，系统似乎从没有同时使用过一个CPU。`top`程序将显示系统无论如何都是50%的空闲状态。

相信你的眼睛。如果系统看起来有一半是空闲的，你就只在使用其中一个。处理软件构建命令的`make`程序等待响应，然后执行另一个命令。这些子任务中的每一个都可以被分配给不同的CPU，但实际的`make`命令在原始进程成功返回之前不会尝试执行任何操作。它一次只执行一个。

你可以通过`make`的`-j`标志解决这个问题，它告诉你可以运行多个进程。`-j`标志带有自己的参数，即运行的`make`进程数：

```bash
make -j4 buildworld
```

## 高级软件管理

## 第12章：通过 DNS 查找主机

域名系统服务（DNS）是那些默默工作、不受关注的后台程序之一。大多数用户从未听说过，DNS是我们所知的Internet运行的基础。DNS提供了主机名和IP地址之间的映射。没有DNS，你将不得不输入IP地址。任何你实现的Internet服务都需要DNS。

### DNS 如何工作

DNS只是将IP地址映射到主机名，并将主机名映射到IP地址。例如，用户不想知道`http://www.com/`实际上是`209.69.178`；她只想输入URL到浏览器中。DNS完成了翻译。作为系统管理员，你必须能够安装、检查和验证DNS信息，并且必须理解你的系统如何执行这些操作。

DNS信息可以在任何地方可用：本地系统、本地DNS服务器、远程服务器。UNIX系统使用解析器来提供这些信息，这是一个了解所有这些信息源并与之通信的程序。当程序知道主机的IP地址或IP地址的主机名时，它会询问解析器，解析器咨询相应的信息源并将信息返回给需要的程序。我们将在本章后续部分介绍如何配置解析器。

如果指定的服务器没有该信息，它会询问根服务器，根服务器维护着网络中每个域名的服务器列表。在一个被称为递归查询的过程中，根服务器告诉服务器去获取相应的服务器，这些服务器可能会反过来将查询指向其他服务器。最终，查询被指向该域名的权威服务器，原始服务器得到了答案。

**注意** 当你注册域名时，必须列出两个DNS服务器。主机期望能够从这些DNS服务器获取信息。如果其中一个失败了，另一个应该接管负载；如果一个域名的所有服务器都失效了，该域名将从Internet上消失。如果发生这种情况，下次有人浏览`www.yourdomain.com`时，他们将收到“未找到域名”错误。邮件将退回。世界将认为你不存在。即使是像微软这样的大公司，在这种情况下也会如此。注意你的名称服务！

# 基础 DNS 工具

FreeBSD包含了几个用于检查DNS信息的工具。由于大多数DNS运行在用户数据报协议（UDP）上，你无法像我们之后处理电子邮件和Web服务那样使用`telnet`手动查询服务器。你访问实时DNS信息的唯一途径是通过`host(1)`和`dig(1)`。

## Host 命令

要快速检查主机的IP地址，我们使用`host(1)`命令。例如，若要检查我出版商的网页，我会执行以下操作：

```bash
host www.nostarch.com is a nickname for nostarch.com

www.nostarch.com has address 66.80.60.21

nostarch.com is handled (pri=20) by smtp.lax.megapath.net

nostarch.com is handled (pri=10) by mail.nostarch.com
```

这非常很有意思，因为它表明在DNS之下，一个主机可以有多个名称，并在同一个IP地址上拥有多个网页。此输出告诉我们，No Starch的网页实际上是另一个主机`http://nostarch.com/`的别名；一个IP地址可以拥有任意数量的名称。这就像典型家庭中的电话系统，几个人共用一部电话。这些人人被称为主机名，而电话号码就像IP地址。主机确实有一个规范名称，就像一个人被注册到特定的身份下一样。

- 许多服务器运行需要比IP地址更多的标识信息。例如，如果你在浏览器中输入`http://66.80.60.21/`，你打开的是No Starch Press托管供应商的页面，而不是No Starch Press的页面。我们将在第15章介绍流行的Web服务器如何将多个网站复用到单个IP地址上，但你现在应该记住这一点，以备日后参考。

## 使用 Dig 获取详细信息

虽然`host`命令很有用，但它并不详尽。而且，你不知道信息源自哪里——是来自缓存，还是名称服务器从另一台名称服务器挖掘出来的。获取DNS信息的标准程序是`dig(1)`。（另一个工具`nlookup(1)`曾流行过多年，但已不再被采用。）`dig`拥有多种选项，允许你调试各种名称服务问题，我在这里只介绍最基础的几个。

在最基础的形式下，命令简单就是`dig`加上主机名。例如，要查询我出版商的信息，我会输入此命令：

```bash
dig www.nostarch.com
```

输出示例：

```text
; <<>> DIG 8.3 <<>>; www.nostarch.com

;; res options: init rec defnam dnsarch

;; got answer:

; <<HEADER<< opcode, QUERY, status: NOERROR, id: 4

;; flags: qr ra; QUERY: 1, ANSWER: 2, AUTHORITY: 2, ADDITIONAL: 2

= ;; QUERY SECTION:

;; www.nostarch.com, type = A, class = IN

;; ANSWER SECTION:

www.nostarch.com. 2h13m2s IN CNAME nostarch.com.

nostarch.com. 2h13m2s IN A 68.60.21

;; AUTHORITY SECTION:

nostarch.com. 7h48m5s IN NS NS1.MEGAPH.NET.

nostarch.com. 7h48m5s IN NS NS2.MEGAPH.NET.

;; ADDITIONAL SECTION:

NS1.MEGAPH.NET. 7h48m5s IN A 216.000.176.4

NS2.MEGAPH.NET. 7h48m5s IN A 216.343.237.2

;; Total query time: 11 msec

;; FROM collectors.org TO SERVER: 127.0.0.1

;; WHEN Apr 12:24

;; MSG SIZE sent: rcvd: 144
```

哇，这么多信息！（当你使用`dig`时，你可能正在尝试调试某些东西。信息多比没有信息要好。）

我们学到了什么？首先，任何以`;`开头的内容都是注释，要么列出了`dig`使用的选项，要么将答案分为不同的章节。第一行列出了你正在使用的`dig`版本和命令行。第二行列出了`dig`正在使用的选项（因为你没有在命令行中指定任何选项）。第三行告诉`dig`得到了答案。接的一行包含一个重要的单词`NOERROR`，告诉我们`dig`找到了答案。如果你没有得到`NOERROR`，说明出了问题（常见错误如`NXDOMAIN`表示域名不存在，或`SERVFAIL`表示服务器配置错误）。接下来的几行代码除非你深入研究DNS或正在进行某些奇怪的操作，否则没用。让我们跳转到后续章节：query、authority和additional。

### Query Section（查询部分）

在查询部分，我们看到`dig`如何处理查询的。在我们的示例中，我们看到：

```text
;; www.nostarch.com, type = A, class = IN
```

让我们从简单的`class`部分开始。虽然DNS可以管理不同的命名系统，我们关注的是域名。`type`是我们要查找的记录类型。默认情况下，`dig`查找`A`（地址）记录，这意味着我们有名称；但`PTR`（指针）请求意味着我们有IP地址和关联名称。

### Answer Section（答案部分）

接下来是答案部分。第一项包含了我们要查找的主机(`http://nostarch.com/`)。数字`2h13m2s`是该信息的生存时间（TTL），即本地名称服务器缓存该信息的时间。`2h13m2s`表示它将在2小时13分钟2秒后过期。`IN`再次表示这是Internet数据。最后，`CNAME`表示后面是规范名称，告诉我们我们要查找的实际上是另一个东西的别名。`dig`的输出确认`www.nostarch.com`实际上是另一个名称的别名。答案的第二行与第一行几乎相同，只是它使用的是`A`而不是`CNAME`。这告诉我们后面是IP地址。

### Authority Section（权威部分）

为了获取`http://nostarch.com/`的IP地址，我们必须遵循权威名称服务器的链。权威部分列出了负责该域名的服务器、生存时间以及它们的数据类型。在这种情况下，名称服务器是`ns1.megapath.net`和`ns2.megapath.net`。`http://nostarch.com/`的数据缓存时间为7小时48分钟45秒，这些是（再次）Internet（IN）记录。`NS`意味着这些是名称服务器。

### Additional Section（附加部分）

最后，在附加部分，`dig`列出了我们需要的所有主机的IP地址。我们的示例列出了`http://nostarch.com/`的名称服务器`ns1.megapath.net`和`ns2.megapath.net`。这里有趣的地方是生存时间为7小时48分钟35秒。在这种情况下，生存时间不是本地名称服务器保留`http://nostarch.com/`名称服务器信息的时间。一旦时间过去，你的名称服务器将丢弃信息并从互联网的根名称服务器之一获取名称服务器列表。这不一定是好是坏，但如果你试图解决问题，了解它是很有用的。

对几个域名运行`dig`，熟悉输出应该的样子。

## 使用 Dig 查找主机名

假设你有一个IP地址并想识别关联的主机名；例如，你可能想知道某个号码的所有者。这是互联网上的一个常见问题——你可能会看到一个地址每五秒访问一次你的网站，你想知道是谁以及他们想做什么。

要查找名称，使用`dig -x`选项进行反向查询。由于大部分结果与正向查询看到的完全相同，我们只看不同的部分：答案。

```bash
dig -x 66.80.60.21
```

输出示例：

```text
;; ANSWER SECTION:

21.60.80.66-in-addr.arpa. 24h IN PTR www.megapath.net...
```

虽然我们知道至少有`www.nostarch.com`和`nostarch.com`位于这个IP地址，但这个反向查询向我们展示了主机的正确名称。

## 更多 Dig 选项

`dig`程序采用各种命令行来控制它如何检查信息。查看`dig(1)`获取这些选项的完整列表。我们在这里只讨论服务器名称和递归选项，因为它们是最常用的。

### Server Name

第一个选项是服务器名称。默认情况下，`dig`查询`/etc/resolv.conf`中列出的第一个名称服务器。然而，如果你正在调试问题，你想询问不同的名称服务器。你可以在命令行上通过`@`选项来实现这一点。例如，要询问`dns1.yahoo.com`关于`AbsoluteBSD/`的已知信息，请输入：

```bash
dig @ns1.yahoo.com AbsoluteBSD.
```

### 控制 Dig 如何查询

`dig`还有另外两种选项：控制`dig`如何运行的选项以及控制`dig`如何查询的选项。控制`dig`如何运行的选项以减号(`--`)为开头；控制`dig`如何查询的选项以加号(`+`)为开头。虽然`dig`可以做很多巧妙的技巧，但它们超出了本章的范围。然而，控制它如何查询是非常有用的。

默认情况下，名称服务器查询是为了返回答案。虽然当你向名称服务器询问域名时这很有用，但在调试时你并不想要挖掘答案；相反，你想轮流检查名称服务器。你可以使用`norecursion`选项来实现这一点。

```bash
dig AbsoluteBSD.com +norecurse
```

现在尝试这个命令，使用一个你非常确定本地名称服务器从未查询过的域名。我最喜欢的DNS测试站点是`http://www.moo.com/`，仅仅因为它很酷、冷门、可爱、基本无害，而且从来没有人看它。你几乎可以保证，你的名称服务器上的没有人最近没有访问过`http://moo.com/`。

如果你的名称服务器没有缓存这些信息，或者这些信息已从缓存中过期，你的第一个部分看起来将和我们之前的示例一样。然而，权威部分（authority section）看起来会完全不同：

```text
; AUTHORITY SECTION:

18h9m9s IN NS A.GTLD-SERVERS.NET.
18h9m9s IN NS G.GTLD-SERVERS.NET.
18h9m9s IN NS H.GTLD-SERVERS.NET.
18h9m9s IN NS C.GTLD-SERVERS.NET.
18h9m9s IN NS I.GTLD-SERVERS.NET.
18h9m9s IN NS B.GTLD-SERVERS.NET.
18h9m9s IN NS D.GTLD-SERVERS.NET.
18h9m9s IN NS A.GTLD-SERVERS.NET.
18h9m9s IN NS F.GTLD-SERVERS.NET.
18h9m9s IN NS J.GTLD-SERVERS.NET.
18h9m9s IN NS K.GTLD-SERVERS.NET.
18h9m9s IN NS E.GTLD-SERVERS.NET.
18h9m9s IN NS M.GTLD-SERVERS.NET.
```

要查询根名称服务器，请结合`norecurse`选项和服务器名称`dig`命令并尝试你的查询：
