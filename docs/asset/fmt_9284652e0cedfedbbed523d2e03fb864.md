
## 设置 BIND 数据库文件

为了让你有足够的关于所有 DNS 记录类型的知识以开始工作，现在是时候创建为服务器提供数据的实际数据库了。数据库文件格式并不太严格，但随着时间的推移已经形成了一些惯例。遵循这些惯例会让你的生活更轻松，并为接手你工作的管理员铺平道路。

**提示** 记住在 BIND 配置文件中尽可能多地添加描述性的注释。

数据库文件是你最重要的配置文件。创建正向查找数据库很容易；但通常被遗漏的是对 IP 地址（即请求来源地址）执行的反向查找，因此提供这些信息是一种礼貌。

每个数据库文件都应该以一个 *TTL* 条目开始。该条目告诉 BIND，当显式指定时，每个单独记录的生存时间是多少。（SOA 记录中的生存时间，即 TTL，仅对 SOA 记录有效。）在 *TTL* 条目之后是 SOA 记录和至少一个 NS 记录。其所有内容都是可选的。（当然，“其他内容”才是让文件变得有用的关键！）你可能会发现以下通用格式很有帮助：

```
$TTL

SOA 记录

NS 记录

MX 记录

A 和 CNAME 记录
```

让我们从头到尾浏览为 DNS 服务器构建完整配置的过程，以及到目前为止的信息是如何整合在一起的。在这个示例中，我们将为 `example.org` 构建 DNS 服务器，实现以下目标：

- 建立两个名称服务器：`ns1.example.org` 和 `ns2.example.org`。
- 名称服务器能够对其已知的 IPv6 记录查询做出响应。
- 作为 `sales.example.org` 区域的从服务器，其中 `serverB.example.org` 将作为主服务器。
- 为 `serverA`、`serverB`、`smtp`、`ns1` 和 `ns2` 定义 A 记录。
- 为 `serverA-v6` 和 `serverB-v6` 定义 AAAA 记录（IPv6）。
- 将 `smtp.example.org` 定义为 `example.org` 域的邮件交换器（MX）。
- 将 `www.example.org` 定义为 `serverA.example.org` 的别名（CNAME），并将 `ftp.example.org` 定义为 `serverB.example.org` 的别名。
- 为 `serverA.example.org` 定义联系信息。

好了，邦德先生，你已经收到了指令。出发吧去完成任务。祝你好运！

## DNS 服务器流程详解

为了实现为 `example.org` 设置 DNS 服务器的目标，我们需要执行一系列步骤。让我们逐一个地过它们。

> 提示 如果不想不想打太多字，我们已经将你跟进所需的所有文件打包，并将它们保存在了以下 URL 中。你只需要下载、解压并将文件复制到步骤中指定的正确目录即可，如下：
```
# pwd
# wget http://linuxserverexperts.com/8e/chapter-17.tar.xz
# tar xvJf chapter-17.tar.xz
# cd chapter-17 && ls
```

1. 确保你已经按照本章较早描述的方法安装了 BIND DNS 服务器软件。根据你的发行版，使用 `rpm` 或 `dpkg` 命令来确认此项：
```
[master@fedora-server ~]$ rpm -q bind
```
对于基于 Debian 的发行版：
```
[master@ubuntu-server ~]$ dpkg -l bind9
```

> 注意 如果仅从源码编译并安装了 BIND，你的发行版包管理器将不会显示任何内容，因为 RPM 或 dpkg 数据库不会包含它的任何信息。你如何知道你安装了什么以及安装在哪里呢。

2. 使用任何你熟悉的文本编辑器创建主 DNS 服务器配置文件——`/etc/named.conf` 文件。在文件中输入以下文本：
```
options {

    listen port 53 { any };

    listen-v6 port 53 { any };

    directory "var/named";

    dump-file "var/named/data/cache_dump.db";

    statistics-file "var/named/data/named_stats.txt";

}
```
以下区域定义不需要任何修改。
第一个是根名称服务器的定义，并将我们的服务器设置为具有缓存能力的 DNS 服务器。第二个定义了 localhost。第三个区域定义定义了 localhost 的反向查找。
```
zone "." {

    type hint;

    file "root.hints";

}

zone "localhost" {

    type master;

    file "localhost.db";

}

zone "127.0.0.1-addr.arpa" {

    type master;

    file "127.0.0.rev";

}
```

3. 将上述文件保存为 `/etc/named.conf` 并退出文本编辑器。

4. 接下来，我们需要创建 `/etc/named.conf` 中引用的实际数据库。特别是我们要创建的文件是 `root.hints`、`localhost.db`、`127.0.0.1`、`example.org.db` 和 `example.org.rev`。所有文件都将存储在 BIND 的工作目录 `/var/named/` 中。我们将按照 `named.conf` 文件从顶部到底部的顺序创建它们。

5. 老实说，我们不需要手动创建 root hints。从互联网下载最新版本的 root hints。使用 `wget` 命令下载并复制到正确的目录：
```
# wget /var/named/root.hints http://www.internic.net/zones/root.hints
```

6. 使用任何你熟悉的编辑器创建主 DNS 服务器配置文件——`/etc/named.conf` 文件。在文件中输入以下文本：
7-16. 步骤涵盖了：保存 `/etc/named.conf`、创建各个区域数据库文件（`localhost.db`, `example.org.db` 等）、配置反向查找、启动 `named` 服务以及检查日志。

# 第 17 章 域名系统 (DNS)

> **提示** 如果你更改了 BIND 的配置文件（无论是主 `named.conf` 数据库文件），你需要通过向 `named` 进程发送 HUP 信号来让它重新读取。快速且简单的方法是使用系统的服务管理实用程序（如 `service`、`systemctl`、`rcnamed` 等）重新加载或重启守护进程。

17. 你可能想确保你的 DNS 服务器在下次重启时启动。使用 `systemctl` 命令：
```
[master@serverA named]$ sudo systemctl enable named.service
```

下一节将介绍介绍用于测试或查询 DNS 服务器的工具。

## DNS 工具箱

本节描述了你在处理 DNS 时需要熟悉的几个工具。它们将帮助你更快速地排排除故障。

## host

`host` 工具是一个非常实用的简单实用程序。当然，它的功能可以通过配合各种选项来扩展。其语法和一些常用选项如处所示：
```
host [-aclrTww] [-c class] [-n] [N dots] [-t type] [-W time]
```
