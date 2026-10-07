
# 第 14 章 管理 DNS

我们还学习了一些解析器无法记忆或使用的内容。例如，我们可以从名称中推测，IBM 的 DNS 管理员已按照建议，将 DNS 服务委托给地理位置和网络上都具有分散性的服务器。我们看到 IBM 在同一网络上运行了四个 Web 服务器——也许是为了优雅地处理负载。我们知道 VSNL（一家大型 ISP）的 DNS 管理员没有他们能做到的那样尽职，因为他们整个域名只有两个名称服务器，并且没有修正反向映射。

DNS 是极尽迷人的，花几个小时玩玩 `dig` 是非常有回报的——这不仅可以学习到有趣的知识，而且因为熟悉 `dig` 的查询和响应对于调试你自己的 DNS 配置问题非常有帮助。

## 使用 BIND 配置名称服务器

BIND 是 Unix 上的事实标准 DNS 软件。它包含一个回答 DNS 查询的名称服务器守护进程（`named`）、一个允许程序进行此类查询的解析器库，以及一些实用程序程序。BIND 由 ISC（互联网软件协会）维护，网站地址为 http://www.isc.org/bind/。

目前常用的 BIND 有三个主要版本：4、8 和 9。现在强烈不建议使用 BIND 4（因为存在许多安全漏洞和其他错误），此处将不会讨论它。BIND 8 具有许多新功能和错误修复，现在已相当广泛部署。它正在积极维护，但仍然容易受到各种攻击；因此也强烈不建议使用。Red Hat 提供了 BIND 9。

> 注意：如果你正在将 BIND 8 升级到 BIND 9，请务必阅读 `/usr/share/doc/bind-9.2.1/misc/migration` 文件，以了解任何关于配置文件的问题（会导致 BIND 无法运行），并使用 shell 脚本。BIND 9 手册的 HTML 版本是 `/usr/share/doc/bind-9.2.1/arm` 目录下的 `B9ARM.html` 文件。

在本章中，我们将讨论随 Red Linux 附带的 BIND 9。BIND 9 是从头重写的，旨在使代码更加健壮，并抛弃旧代码固有的问题。它符合新的 DNS 标准，在功能、性能和安全性方面代表了巨大的改进。

RPM 包包含 `named` 守护进程和丰富的 BIND 文档。`bind-utils` RPM 包包含了其他工具，其中无无贵的 `dig(1)` 工具。如果你选择自己编译 BIND，可以从 ISC 网站下载源码分发并按照其中的构建说明进行操作。

> 注意：你还会在 `/usr/share/doc/bind-9.2.1/directory` 目录下的 `README` 文件找到构建说明。

## 使用 BIND 配置名称服务器

一旦安装了 RPM，以下目录特别值得关注，因为它们包含了 BIND 使用的文件，并包含列表所示所示的信息。

| 路径 | 描述 |
| :--- | :--- |
| /etc/ | 配置文件。 |
| /usr/bin/ | dig, host, nslookup, nsupdate。 |
| /usr/sbin/ | named, rndc, 以及各种支持性程序。 |
| /usr/share/doc/bind-9.2.0/ | BIND 文档。 |
| /usr/share/man/ | 手册页。 |
| /var/named/* | 区域文件 (Zone files)。 |

如果你从源码安装，文件将位于你在 `configure` 时指定的位置，默认目录在 `/usr/local/` 下。

此示例使用 BIND 配置名称服务器，然后根据需要扩展它以提供有 DNS 服务。要实现这一点，你必须配置 `named`（名称服务器守护进程）和 `rndc` 组件（一个允许与运行中的名称服务器进行各种交互的控制程序）。你可能还需要配置解析器软件，稍后会讨论这一点。

## rndc.conf

rndc 使用 TCP 连接（端口 9553）与 `named` 通信；对于身份验证，它在将命令通过网络发送到 `named` 之前，使用加密密钥对命令进行数字签名。配置文件默认为 `/etc/rndc.conf` 必须指定一个要通信的服务器，以及在通信时使用的相应密钥（该密钥必须被 `named` 识别）。

`named` 目前支持的唯一身份验证机制是使用 HMAC-MD5 算法加密的密钥，并在 `rndc` 和 `named` 之间共享。生成密钥最简单的方法是使用 `dnssec-keygen` 工具。在下面的示例中，你要求该工具生成一个名为 `rndc` 的 128 位 HMAC-MDS 用户密钥：

```
$ dnssec-keygen -a hmac-md5 -b 128 -n user rndc
Krndc.+157+14529

$ cat Krndc.+157+14529.private
Private-key-format: v1.2
Algorithm: 157 (HMAC_MD5)
Key: mkKd2FiHMe1Jqx1/z4cfw==
```

该工具分别创建两个带有 `.key` 和 `.private` 扩展的文件。`.private` 文件中的 `Key:` 行告诉我们 `rndc` 和 `named` 需要共享的密钥 (mKKd2fIHMFe1JqX/z4cfw=)。一旦有了它，我们可以设置非常简单的 `/etc/rndc.conf`：

/etc/rndc.conf

```
# 与名称服务器 "localhost" 通信时名为 "rndc" 的密钥。
server localhost {
    key rndc;
};

# 这里是名为 "rndc" 密钥的细节
key rndc {
    algorithm hmac-md5;
    secret mKKd2fIHMFe1JqX/z4cfw=;
};

# 与名称服务器 "localhost" 通信时名为 "rndc" 的密钥。
server localhost {
    key rndc;
};

# 这里是名为 "rndc" 密钥的细节
key rndc {
    algorithm hmac-md5;
    secret mKKd2fIHMFe1JqX/z4cfw=;
};
```

（注：由于原文中存在大量重复和 OCR 错误片段，译文已根据逻辑要求进行了清理和对齐。）
