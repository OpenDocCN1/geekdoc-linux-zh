
为主机名查找 IP 地址被称为“解析主机名”。感知网络的应用程序（如 Web 浏览器或 FTP 客户端）使用解析器库执行从名称到 IP 地址的转换。根据 `/etc/host.conf` 文件中的设置，解析器库会查询 `/etc/hosts` 文件或进行 DNS 查询来解析主机名。解析器库查询 `/etc/resolv.conf` 文件中的名称服务器。

![](img/fb03f7f944c69a481f34f490e877a2b9_634_0.png)

## 608 理解域名系统 (DNS)

除非你正在编写网络感知应用程序，否则不需要过多了解解析器库。为了运行 Internet 服务，你必须知道如何配置解析器。在本章后面，我将向你展示如何配置服务器以及 DNS 其他方面。

你可以使用 DNS 工具程序 —— `dig` 和 `host` —— 在 shell 提示符下交互地尝试 DNS。这些工具程序是 DNS 客户端。你可以使用它们查询 DNS 数据库以及你在系统中设置的任何名称服务器。默认情况下，这些程序查询你系统 `/etc/resolv.conf` 文件中的名称。

你可以使用 `dig`（Domain Internet Groper）程序查询域名的 IP 地址，反之亦然。例如，要查找 `ftphot.com` 的 IP 地址，输入：

```
dig ftphot.com
```

`dig` 会详细打印 DNS 查询结果。查看输出中标记为 `ANSWER SECTION` 的部分。例如，此查询的结果如下：

```
:: ANSWER SECTION:
ftphot.com      2  A       66.187.224.30
ftphot.com      2  A       209.132.76
```

这意味着名称 `ftphot.com` 指向两个 IP 地址 —— `66.187.224.30` 和 `209.132.76`。使用 `dig` 反向查找 IP 地址 地址也非常容易。例如，查找 IP 地址 `209.132.76` 对应的主机名，输入：

```
dig -x 209.132.76
```

答案再次出现在 `ANSWER SECTION` 中，这个示例看起来像这样：

```
:: ANSWER SECTION:
209.132.76.in-addr.arpa PTR ftphot.com.
```

在这种情况下，IP 地址 `209.132.76` 对应的主机名正好是 `ftphot.com`。

你也可以通过 `host` 程序查询 DNS。`host` 程序产生紧凑格式的输出。例如，使用 `host` 查找主机的 IP 地址的典型用法：

```
host google.com
```

## 609 配置 DNS

此命令生成如下：

`google.com has address 142.250.190.46`

默认情况下，`host` 打印 IP 地址和任何 MX 记录（这些记录列出了主机）。对于反向查找，使用 `-t` 选项并将 IP 地址作为参数，如下：

```
host -t ptr 142.250.190.46
```

这里是 `host` 的回复：

```
142.250.190.46.in-addr.arpa domain google.com.
```

在这种情况下，`host` 打印 PTR 记录（来自 DNS 数据库），显示与 IP 地址对应的主机名（PTR 指的是“指针”，PTR 记录指定了对应的名称）。

你也可以尝试其他类型的记录，例如 CNAME（用于规范名称），如下：

```
host -t cname www.umd.edu
```

`host` 的响应说是：

```
www.umd.edu is an alias for edu.umd.edu.
```

此输出表明 `www.umd.edu` 的规范名称（或别名）是 `edu.umd.edu`。

### 配置 DNS

你使用若干配置文件配置 DNS。具体的文件集取决于你是否运行名称服务器以及名称服务器的类型——缓存或代理。无论你是否运行名称服务器，都需要某些配置文件。

### 配置解析器

使用 DNS 客户端（`dig` 和 `host`）时，你的系统中不需要运行名称服务器。你可以使用它们查询域的名称服务器。通常，你的 ISP 会为你提供这些信息。你必须在 `/etc/resolv.conf` 文件中列出名称服务器的 IP 地址 —— 解析器库读取此文件来确定如何解析主机名。该文件的格式为：

```
domain domain.com
search your-domain.com
nameserver A.B.C.D
nameserver X.Y.Z.W
```

其中 `A.B.C.D` 和 `X.Y.Z.W` 是你的 ISP 提供的主、从名称服务器的 IP 地址（点分隔的数字地址，例如 `192.168.0.1`）。

`domain` 行列出本地域名。`search` 行指定了首先搜索主机名的域（通常，你将你的域名放在 `search` 行中）。在解析器库尝试解析主机名之前，会将列出的域名附加到任何主机名。例如，如果你寻找主机名 `mailhost`，解析器库首先尝试 `mailhost.your-domain.com`；如果失败，则尝试 `mailhost`。`search` 行适用于你尝试访问的任何主机名。例如，如果你正尝试访问 `www.redhat.com`，解析器首先尝试 `www.redhat.com.your-domain.com`，然后是 `www.redhat.com`。

你也可以通过 `host` 程序查询 DNS。`host` 程序产生紧凑格式的输出。例如，使用 `host` 查找主机的 IP 地址的典型用法：

```
host google.com
```

## 611 配置 DNS

### 配置缓存名称服务器

一个简单且实用的名称服务器是指通过其他名称服务器查找主机名查询的答案，并将答案记住（通过保存在缓存中），以供下次需要时使用。这种缓存名称服务器可以缩短最近访问宿机的时间；因为答案已经在缓存中了。

当你安装 BIND 时，缓存名称服务器的配置文件也会随之安装。这意味着你不需要花费太多精力就可以开始运行缓存名称服务器。本节将介绍这些文件以及你启动缓存名称服务器时需要执行的操作。

#### /etc/named.conf 文件

你需要的第一个配置文件是 `/etc/named.conf`。（实际上，这是 Fedora Core 和 SUSE 中的命名方式；在 Debian 和 Xandros 中，BIND 的配置称为 `/etc/bind/named.conf`。）`named` 服务器在启动时会读取此配置文件。如果你安装了 BIND，就已经拥有了这个文件。以下是一份来自 Fedora Core 的 `/etc/named.conf` 文件：

```
options [
  directory "/var/named";  /* 如果你和你想要通信的名称服务器之间有防火墙，
  * 你可能需要取消下面的 query-source
  * 指令的注释。
  */
  // query-source address * port 53;
];

// 仅缓存名称服务器配置
controls {
  inet 127.0.0.1 allow (localhost;) keys (rndckey);
};

zone ". IN {
  type hint;
  file "named.ca";
};

zone "localhost" IN {
  type master;
  file "localhost.zone";
  allow-update (none);
};

zone "0.0.127.in-addr.arpa" IN {
  type master;
  file "named.local";
  allow-update (none);
};

include "/etc/rndc.key";
```

## 612 配置 DNS

注释采用 C 风格（`/* ... */`）或 C++ 风格（以 `//` 开头）。该文件包含包含在大括号 `{...}` 中并以分号 `;` 结尾的块语句。块语句反过来包含其他语句，每个语句都以分号结尾。

`/etc/named.conf` 以一个 `options` 块语句开头，其中包含许多选项语句。`directory` 选项语句告诉 `named` 在哪里查找配置文件中行内出现的所有其他文件。在这种情况下，`named` 在 `/var/named` 目录中查找文件。

![](img/fb03f7f944c69a481f34f490e877a2b9_639_0.png)

在 SUSE 中，`/etc/named.conf` 中的 `directory` 选项指向 `/var/lib/named` 目录，这意味着所有的 BIND 配置文件都在 `/var/lib/named` 中。在 Debian 和 Xandros 中，明确指定配置文件位于 `/etc/bind/bind` 目录。

`/etc/named.conf` 中的 `controls` 语句包含安全信息，以便 `rndc` 命令能够连接到端口 953 上的 `named` 服务并与之交互。在这种情况下，`controls` 语句包含以下行：
