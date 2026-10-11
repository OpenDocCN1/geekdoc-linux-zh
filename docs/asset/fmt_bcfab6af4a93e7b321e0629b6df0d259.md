
你可以使用 DNS 实用程序——`dig` 和 `host`——从 shell 提示符交互式地试用 DNS。这些实用程序是 DNS 客户端。你可以使用它们查询 DNS 数据库并调试你在系统上设置的任何名称服务器。默认情况下，这些程序查询系统 `/etc/resolv.conf` 文件中列出的名称服务器。

你可以使用 `dig`（Domain Internet Groper 程序）查找域名或 IP 地址。例如，要查找 `ftp.redhat.com` 的 IP 地址，请输入

```text
dig ftp.redhat.com
```

`dig` 会详细打印 DNS 查询的结果。在输出中标记为 `ANSWER SECTION` 的部分查找结果。例如，对于此示例查询，该部分看起来像这样：

```text
;; ANSWER SECTION:
ftp.redhat.com.        300 IN A 66.187.224.30
```

此输出意味着名称 `ftp.redhat.com` 指的是 IP 地址 66.187.224.30。

使用 `dig` 进行*反向查找*（查找 IP 地址的主机名）也很简单。例如，要查找与 IP 地址 209.132.176.30 对应的主机名，请输入以下内容：

```text
dig -x 66.187.224.30
```

同样，答案出现在输出的 ANSWER SECTION 中，对于这个例子，看起来像这样：

```text
;; ANSWER SECTION:
30.224.187.66.in-addr.arpa. 600 IN PTR ftp.redhat.com.
```

在这种情况下，与 IP 地址 66.187.224.30 对应的主机名恰好是 `ftp.redhat.com`。

你还可以通过使用 `host` 程序来查询 DNS。`host` 程序产生紧凑格式的输出。例如，这是使用 `host` 查找主机名的 IP 地址的典型用法：

```text
host www.gao.gov
```

此命令生成以下输出：

```text
www.gao.gov has address 161.203.16.2
www.gao.gov mail is handled by 5 listserv.gao.gov.
```

默认情况下，`host` 打印 IP 地址和任何 *MX 记录*（这些记录列出了主机邮件处理器的名称）。

要进行反向查找，请使用 `-t ptr` 选项，并将 IP 地址作为参数，如下所示：

```text
host -t ptr 161.203.16.2
```

以下是 `host` 的结果：

```text
2.16.203.161.in-addr.arpa domain name pointer www.gao.gov.
```

在这种情况下，`host` 打印 *PTR 记录*（来自 DNS 数据库），该记录显示了与 IP 地址对应的主机名。(*PTR 指*指针*，且* PTR *记录指定与地址对应的名称。)*

你也可以尝试其他类型的记录，例如 *CNAME*（规范名称），如下所示：

```text
host -t cname www.ee.umd.edu
```

`host` 的响应如下：

```text
www.ee.umd.edu is an alias for edison.eng.umd.edu.
```

此输出表明 `www.ee.umd.edu` 的*规范名称*（或别名）是 `edison.eng.umd.edu`。

## 配置 DNS

你通过使用多个配置文件来配置 DNS。具体的文件集取决于你是否正在运行名称服务器，如果是，则是名称服务器的类型——缓存型或主型。无论你运行名称服务器与否，都需要一些配置文件。

### 配置解析器

要使用 DNS 客户端（`dig` 和 `host`），你的系统上不需要运行名称服务器。你可以使用它们查询你所在域的名称服务器。通常，你的 ISP 会提供此信息。你必须在 `/etc/resolv.conf` 文件中列出这些名称服务器的 IP 地址——解析器库读取此文件以确定如何解析主机名。此文件的格式如下

```text
domain your-domain.com
search your-domain.com
nameserver A.B.C.D
nameserver X.Y.Z.W
```

其中 `A.B.C.D` 和 `X.Y.Z.W` 是主要和次要名称服务器的 IP 地址（点分十进制地址，例如 192.168.0.1），由你的 ISP 提供。

`domain` 行列出本地域名。`search` 行指定首先搜索的主机名所属的域（通常，你将自己的域放在 `search` 行中）。`search` 行列出的域会在解析器库尝试解析之前附加到任何主机名后面。例如，如果你查找名为 `mailhost` 的主机，解析器库会先尝试 `mailhost.your-domain.com`；如果失败，它会尝试 `mailhost`。`search` 行适用于你尝试访问的任何主机名。例如，如果你试图访问 `www.redhat.com`，解析器会先尝试 `www.redhat.com.your-domain.com`，然后尝试 `www.redhat.com`。

另一个重要的配置文件是 `/etc/host.conf` —— 此文件告诉解析器在尝试解析主机名时该怎么做。典型的 `/etc/host.conf` 文件包含以下行：

```text
order hosts,bind
```

此命令告诉解析器首先查阅 `/etc/hosts` 文件，如果失败，则查询 `/etc/resolv.conf` 文件中列出的名称服务器。`/etc/hosts` 文件通常列出任何本地主机名及其 IP 地址。以下是 `/etc/hosts` 文件中的一行典型示例：

```text
127.0.0.1    hnpb200    localhost.localdomain    localhost
```

这一行表示 IP 地址 `127.0.0.1` 被分配给主机名 `lnbp200`、`localhost.localdomain` 和 `localhost`。

在最新的 Linux 内核版本中——即使用 GNU C 库（`glibc`）2 或更高版本的版本——名称服务切换（NSS）文件 `/etc/nsswitch.conf` 控制着解析器库、NIS、NIS+ 以及诸如 `/etc/hosts` 和 `/etc/shadow` 等本地文件等服务之间的交互方式。例如，`/etc/nsswitch.conf` 文件中的以下 `hosts` 条目指定解析器库首先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts: files nisplus dns
```

要了解更多关于 `/etc/nsswitch.conf` 文件及其功能的信息，请在终端窗口中输入 `man nsswitch.conf`。

### 配置缓存名称服务器

一种简单但有用的名称服务器是能够通过使用其他名称服务器找到主机名查询的答案，并记住该答案（通过将其保存在缓存中）以供下次使用。这种缓存名称服务器可以缩短访问最近访问过的主机所需的时间；因为答案已经存在于缓存中。

当您安装 BIND 时，缓存名称服务器的配置文件也会随之安装。这意味着您可以毫不费力地开始运行缓存名称服务器。本节介绍了配置文件以及启动缓存名称服务器所需执行的操作。

## /etc/named.conf 文件

您需要第一个配置文件是 `/etc/named.conf`。（实际上，这是 Fedora Core 和 SUSE 中的名称；在 Debian、MEPIS、Ubuntu 和 Xandros 中，BIND 配置文件称为 `/etc/bind/named.conf`。）`named` 服务器启动时会读取此配置文件。如果您安装了 BIND，则已经拥有此文件。以下是一个来自 Fedora Core 的 `/etc/named.conf` 文件：

```
options {
  directory "/var/named";
  dump-file "/var/named/data/cache_dump.db";
  statistics-file "/var/named/data/named_stats.txt";
  /
  * If there is a firewall between you and nameservers you want
  * to talk to, you might need to uncomment the query-source
  * directive below. Previous versions of BIND always asked
  * questions using port 53, but BIND 8.1 uses an unprivileged
  * port by default.
  */
  // query-source address * port 53;
};
```

//
// a caching only nameserver config
//

controls {
