

应用程序必须决定如何发送数据（这发生在传输层——在本例中为 TCP）。然后，一旦知道如何发送消息，应用程序就必须决定数据发往何处（这对应于网络层——在本例中为 IP 地址）。下一个至关重要的信息是机器的物理地址（即 MAC 地址，位于物理层）。当应用程序知道所有这些之后，它就发送数据包。导致这一事件的预备过程称为*封装*。当数据包被接收时，接收方会执行一整套复杂的逆向仪式，该过程称为*解封装*。

然而，在封装和解封装之间，通过 TCP/IP 连接的两个系统实际上必须互相“通信”。

## 理解网络地址

每个主机的网络地址，或*IP 地址*，由四组十进制数字组成。其格式如下：

aaa.bbb.ccc.ddd

每个三位数（此处用 `aaa` 到 `ddd` 表示）可以是 0 到 256 之间的值，总共各占 8 位。例如，我的 IP 地址可能是（但实际上并不是）12.3.45.6。只要您没有连接到互联网，您可以选择任何三位数。但在网络上，某些数字不被视为有效的寻址数字，因此不会使用。因此，在建立您的 IP 地址时，请确保事先清楚您需要多少网络以及多少主机。

## 网络类别

将网络指定为 A 类、B 类或 C 类反映了两个特征：(1) 初始八位组，以及 (2) 它如何分组对应于 `aaa`、`bbb`、`ccc` 和 `ddd` 的地址。表 11-3 比较了 IP 中的网络类别；并排来看，它们并不难区分。

![](img/8ad518fddafc7f5e73715a2604b61d50_365_0.png)

> 如果您有兴趣了解更多关于网络寻址和网络更详细领域的信息，请阅读 Fred Butzen 和 Christopher Hilton 著、IDG Books Worldwide 于 1998 年出版的《The LINUX Network》。

表 11-3 IP 中的网络类别
| 类别 | 初始八位组 | 网络地址 | 主机地址 |
| :--- | :--- | :--- | :--- |
| A | 1-126 | aaa | bbb.ccc.ddd |
| B | 128-191 | aaa.bbb | ccc.ddd |
| C | 192-224 | aaa.bbb.ccc | ddd |
| 保留 | 0, 127, 224-254* | 不适用 | 不适用 |

> *0 未被使用，127 用于回环地址。224-254 保留用于其他网络用途，包括广播。*

如表 11-3 所示，网络地址第一部分的数字（对应 aaa 的初始八位组）落在一个范围内，该范围能立即揭示网络的类别。（好吧，也许不是立即，但肯定经过练习后就能识别。）所以，快速测验：地址 124.228.8.4 属于哪类网络？（答案是 A 类。）坏消息是，这个话题很快就会变得更加复杂；好消息是，现在还不是时候。

## 使用 DNS 为网络命名

大多数用户不希望仅仅为了访问网络上的另一台主机就记住一堆数字——而且对某些人来说，输入数字几乎同样乏味。例如，您本可以输入 maple.circa.ufl.edu，而不是 128.227.8.4。当您打开 Web 浏览器时，此类地址名称使用的是域名服务（DNS）。例如，www.yahoo.com 是与几个不同 IP 地址关联的名称，具体取决于网络流量。

DNS 命名约定以类似于 UNIX 文件系统结构的方式工作。您从一个根名称服务器（.）开始，然后决定您发送到的地址是政府（.gov）、商业（.com）、非营利组织（.org）、网络服务提供商（.net），还是其他国家的一部分。所有这些指定都称为顶级域名。表 11-4 列出了各国的顶级域名。

表 11-4 各国的顶级域名

| 顶级域名 | 国家 |
| :--- | :--- |
| .au | 澳大利亚 |
| .ca | 加拿大 |
| .cn | 中国 |
| .de | 德国 |
| .dk | 丹麦 |
| .eg | 埃及 |
| .es | 西班牙 |
| .fr | 法国 |
| .it | 意大利 |
| .jp | 日本 |
| .kr | 韩国 |
| .mx | 墨西哥 |
| .ng | 尼日利亚 |
| .no | 挪威 |
| .nz | 新西兰 |
| .se | 瑞典 |
| .uk | 英国 |
| .us | 美国（使用不多） |
| .za | 南非 |

国际顶级域名可能看似不直接相关，但请考虑一下：它们对用户可以是透明的。例如，Yahoo! 在您的屏幕上看起来可能只是一个网站，但实际上它是多个网站。Yahoo! 网站在美国是 www.yahoo.com；在法国，它是 www.yahoo.fr；在德国，它是 www.yahoo.de。这类幕后信息对管理员可能很有用。

当 DNS 客户端查找诸如 `corp.hp.com` 这样的名称时，其过程远比看起来的更曲折。首先，您的客户端会去查询当前的 DNS 表。例如，如果您的 DNS 地址是 `maple.circa.ufl.edu`，客户端会在表中查找 `circa.ufl.edu`。如果找不到任何内容，它就会向上查找 `ufl.edu` – 仍然没有任何结果。接下来，它向上查找 `.edu` 并在那里查找。再次没有任何结果。现在它前往根域 `.`，并在那里找到了 `.com`。既然找到了 `.com`，它就开始查找 `hp.com`。找到了。现在向下查找 `corp.hp.com`。因为客户端已经完成了所有这些工作，我们就知道 `corp.hp.com` 存在 – 因此我们不需要输入 IP 地址。

这些域可以包含其他域，或者直接指向主机（`www.ins.com` 是一个主机，而 `corp.sun.com` 是一个域）。这完全取决于域的结构方式。对于 `tigerlair.com`，情况比较简单。有两个被识别的主机：`www.tigerlair.com` 和 `ftp.tigerlair.com`。没有像 `corp.tigerlair.com`（用于功能划分）或 `florida.tigerlair.com`（用于区域划分）这样的子域。

## LINUX DNS 客户端

为了使您的 Linux 主机成为 DNS 客户端，您只需定义一个名称服务器并创建一个 `/etc/resolv.conf` 文件。该文件可能如下所示：

```text
domain best.com
nameserver 152.52.2.2
```

这定义了您的域名和名称服务器的 IP 地址。Linux 不再查看 `/etc/hosts` 文件，而是向名称服务器查询信息。您的 DNS 客户端配置是通过 `/sbin/netconfig` 完成的。如果您想测试名称服务器查询，请运行 `nslookup`。如果您使用 DNS，可以保留一个最小尺寸的 `/etc/hosts` 文件，其中包含一行 localhost 地址。

```text
Server: localhost
Address: 127.0.0.1

Non-authoritative answer:
Name: www9.yahoo.com
Address: 204.71.200.74
Aliases: www.yahoo.com
```

## LINUX 名称服务器

您还可以将您的 Linux 服务器设置为名称服务器。例如，我有域 `tigerlair.com`。如果我想设置像 `tchedn` 和 `kitchen` 这样的子域，或者像 `tiger` 或 `sharekahn` 这样的主机，我必须设置一个主机作为 `tigerlair.com` 域中实际存在哪些名称的权威来源。换句话说，名称服务器提供关于 `tigerlair.com` 中主机和子域的官方信息。

要将 Linux 设置为名称服务器，您需要安装软件包 `bind`，它是 DNS 的 UNIX 实现。当前版本的 BIND 是 8；请务必保持 BIND 更新，以获取错误修复和安全补丁。要配置名称服务器，您需要编辑 /etc/named.conf 文件以满足您的需求。以下是 tigerlair.com 的一个示例：

```text
/*
 * BIND 8 configuration for faux tigerlair.com
 * This shows a basic BIND 8 config file.
 */

options {
	directory "/var/named";
};
```

这将您的配置目录设置为如下定义的文件：

```text
logging {
	category lame-servers { null; };
	category cname { thelair; };
};
```

这启用了日志记录，包括该域的任何锥形名称（别名）。

```text
zone "tigerlair.com" in {
	type master;
	file "tigerlair.hosts";
};
```

上述列表将此名称服务器定义为主服务器。如果主服务器宕机，从服务器将接管请求。您不应将从服务器和主服务器定义为同一主机。

```text
zone "0.23.12.in-addr.arpa" in {
	type master;
	file "tigerlair.rev";
};
```

上述列表将此名称服务器定义为网络 12.23.0.0 的主服务器。这意味着它会将该网络上的任何名称转换为正确的地址。

```text
zone "tigerlair.com" in {
	type slave;
	file "tigerlair-slave.hosts";
	masters { 12.23.10.1; };
};
```

