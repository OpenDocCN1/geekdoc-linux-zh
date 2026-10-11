

# RHEL 中的 named.conf 配置文件

在 RHEL 中，`named.conf` 和 `named.caching-nameserver.conf` 文件共同持有与前一节中描述的 `named.conf` 文件及包含的 `named.rfc1912.zones` 文件类似的区域。

# DNS 胶合记录 (GLUE RECORDS)

常见的做法是将提供某个区域服务的名称服务器放在该区域内部。例如，你可能将始于 `site1.example.com` 的区域的名称服务器（图 24-3，第 777 页）放置在 `ns.site1.example.com`。当 DNS 缓存尝试解析 `www.site1.example.com` 时，example.com 的权威服务器会返回指向 `ns.site1.example.com` 的 NS 记录。在尝试解析 `ns.site1.example.com` 时，DNS 缓存再次查询 example.com 的权威服务器，而该服务器又指向 `ns.site1.example.com`。这个循环导致无法解析 `ns.site1.example.com`。

解决此问题最简单的方案是不允许任何名称服务器驻留在其指向的区域内部。由于每个区域都是根区域的子域，这意味着每个域名将由根服务器提供服务，且完全无法扩展。更好的解决方案是*胶合记录*。胶合记录是一种 A 记录，当执行 NS 查询时，除了 NS 记录外还会返回该记录。由于 A 记录提供了名称服务器的 IP 地址，因此它不需要被解析，也不会产生有问题的循环。

redhat.com 的名称服务器设置说明了胶合记录的用法。当你查询 redhat.com 的 NS 记录时，DNS 返回三个 NS 记录。此外，它还返回三个 A 记录，提供 NS 记录指向的主机的 IP 地址：

```
$ dig -t NS redhat.com
...
;; QUESTION SECTION:
;redhat.com. IN NS
;; ANSWER SECTION:
redhat.com. 600 IN NS ns1.redhat.com.
redhat.com. 600 IN NS ns2.redhat.com.
redhat.com. 600 IN NS ns3.redhat.com.
```

```
;; ADDITIONAL SECTION:
ns1.redhat.com.        161952  IN    A       66.187.233.210
ns2.redhat.com.        77938   IN    A       209.132.183.2
ns3.redhat.com.        77938   IN    A       66.187.229.10
...
```

你可以通过在授权域的区域文件中为名称服务器提供 A 记录来创建胶合记录：

```
site1.example.com. IN    NS ns.site1.example.com
ns.site1.example.com. IN    A  1.2.3.4
```

# TSIG：事务签名 (TRANSACTION SIGNATURES)

DNS 组件之间的交互基于查询-响应模型：一部分向另一部分发出查询并接收回复。传统上，服务器根据 IP 客户端的地址来确定是否以及如何回复查询。*IP 欺骗*（第 1089 页）相对容易实施，使得这种情况不理想。BIND 的近期版本支持事务签名 (TSIG)，它允许两个系统通过使用共享密钥建立信任关系。

TSIG 为区域的 master 和 slave 服务器之间提供了额外的身份验证层。当 slave 服务器位于与 master 服务器不同的站点时（这是应该如此的情况），在站点之间操作路由器的恶意人员可能会伪造 master 服务器的 IP 地址并更改 slave 上的 DNS 数据（中间人攻击）。然而，如果使用 TSIG，此人需要知道密钥才能更改 slave 上的 DNS 数据。

# 创建密钥

密钥是一个编码字符串，最多为 512 位。随 BIND 附带的 *dnsssec-keygen* 实用程序生成此密钥。以下命令使用 MD5（一种*单向哈希函数*，第 1097 页）生成 512 位随机密钥：

```
$ /usr/sbin/dnsssec-keygen -a hmac-md5 -b 512 -n HOST keyname
Kkeyname.+157+47586
```

在上面的命令中，请将 *keyname* 替换为唯一且有意义的字符串。此命令在一个名称类似于 *Kkeyname.+157+47586.private* 的文件中创建密钥，其中 *keyname* 被替换为密钥的名称，+157 表示使用的算法，+47586 是密钥的哈希值。如果你再次运行相同的命令，哈希部分将不同。

密钥文件不直接使用。使用 cat 命令并带有私钥文件名作为参数，以显示你在下一步中所需的算法和密钥信息：

```
$ cat Kkeyname.+157+47586.private
Private-key-format: v1.2
Algorithm: 157 (HMAC_MD5)
Key: uNPDouqVwR7Vo/zyfYjkQbQhCtd6Prm...
BITS: AAA=
```

# 使用共享密钥

下一步是通过在两台服务器的 `/etc/named.conf` 文件中插入以下代码来告知名称服务器关于共享密钥。这是 `named.conf` 中的一个顶级部分；请在 Options 部分之后插入它：

```
key keyname {
    algorithm "hmac-md5";
    secret "uNPDougWr7fvo/zFyjkjqkbQhcTd6Prm...";
};
```

`keyname` 是你创建的密钥名称。`algorithm` 是 `cat` 输出中括号内出现的字符串。`secret` 是前面输出中 `Key:` 后面的字符串。你必须用双引号括住每个字符串。复制密钥时要小心；虽然它很长，但不要将其分成多行。

由于密钥名称是唯一的，你可以将任意数量的密钥部分插入到 `named.conf` 中。为了保密，请确保除了 `root` 以外的用户无法读取它：要么授予 `named.conf` 权限，使得除 `root` 外没有人可以访问它，要么将密钥放在只有 `root` 才能读取的文件中，并使用 `include` 语句将其整合到 `named.conf` 中。

一旦两台服务器都知道了密钥，请在 `named.conf` 中使用 `server` 语句告知它们何时使用它：

```
server 1.2.3.4 {
    # 1.2.3.4 是使用此密钥的另一台服务器的 IP 地址
    keys {
        "keyname";
    };
};
```

每台服务器都必须有一个 server 部分，每个部分包含另一台服务器的 IP 地址。只有当它们首先使用共享密钥进行互相身份验证时，服务器才会相互通信。

# 在 chroot 监狱中运行 BIND

为了提高安全性，你可以在 chroot 监狱中运行 BIND。有关 chroot 监狱的安全优势及设置方式的信息，请参见第 448 页。另请参阅第 786 页关于 SELinux 的说明以及 `named` 手册页，以获取有关 BIND、SELinux 和 chroot 监狱的信息。`bind-chroot` 包设置 BIND 以在 chroot 监狱中运行，创建一个名为 `/var/named/chroot` 的目录，该目录取代了根目录 (`/`) 用于所有 BIND 文件。安装此包后，所有控制 BIND 的文件都位于此 chroot 监狱内，本章中使用的文件名是硬链接 (`REDORA`) 或指向 chroot 监狱中文件的符号链接 (`RHEL`)。如下例所示，在 Fedora 下，启动 named 时，`named` 脚本将 `/var/named/chroot/var/named` 链接到 /var/named（停止 named 时移除链接）。你可以通过比较两个目录的 inode 号来验证链接。

```
# ls /var/named/chroot/var/named
# ls -lL /var/named/chroot/var/named
139323 drwxr-x--- 2 root named 4096 2009-09-21 03:46 /var/named/chroot/var/named
# ls -lL /var/named
139302 drwxr-x--- 6 root named 4096 2009-11-24 11:42 /var/named
# service named start
Starting named:		[ OK ]
# ls -lL /var/named/chroot/var/named
139302 drwxr-x--- 6 root named 4096 2009-11-24 11:42 /var/named/chroot/var/named
```

安装了 bind-chroot 包后，你必须在 /etc/sysconfig/named 文件中将 ROOTDIR shell 变量设置为 /var/named/chroot，该文件被 named 初始化脚本引入。为此，请向 /etc/sysconfig/named 添加以下行：

```
ROOTDIR="/var/named/chroot"
```

# 故障排除

当你启动 DNS 缓存时，/var/log/messages 文件包含类似于下面的行。其他类型的 DNS 服务器显示类似的消息。

```
# cat /var/log/messages
...
named[134]: starting BIND 9.5.0b1 -u named -t /var/named/chroot
...
named[134]: found 1 CPU, using 1 worker thread
...
named[134]: loading configuration from '/etc/named.conf'
named[134]: listening on IPv6 interface lo, ::1#53
named[134]: listening on IPv4 interface lo, 127.0.0.1#53
named[134]: automatic empty zone: 127.IN-ADDR.ARPA
named[134]: automatic empty zone: 254.169.IN-ADDR.ARPA
named[134]: automatic empty zone: 2.0.192.IN-ADDR.ARPA
...
named[134]: automatic empty zone: B.E.F.IP6.ARPA
named[134]: command channel listening on 127.0.0.1#953
named[134]: command channel listening on ::1#953
named[134]: zone 0.in-addr.arpa/IN: NS '0.in-addr.arpa' has no address records (A or AAAA)
named[134]: zone 0.in-addr.arpa/IN: loaded serial 0
named[134]: zone 1.0.0.127.in-addr.arpa/IN: NS '1.0.0.127.in-addr.arpa' has no address records (A or AAAA)
named[134]: zone 1.0.0.127.in-addr.arpa/IN: loaded serial 0
named[134]: zone 1.0.0.0.ip6.arpa/IN: NS '1.0.0.0.ip6.arpa' has no address records (A or AAAA)
named[134]: zone 1.0.0.0.ip6.arpa/IN: loaded serial 0
named[134]: zone localhost.localdomain/IN: loaded serial 0
named[134]: zone localhost/IN: loaded serial 0
named[134]: running
```

