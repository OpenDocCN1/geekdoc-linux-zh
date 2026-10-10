
注意，通过为这些区域创建不同的视图（`views`），将根据查询的来源向查询返回不同的信息。例如，当有人从互联网请求 DNS 服务器的地址（`ns1.yourdomain.com`）时，他们将获得地址 `123.45.67.89`。然而，当来自局域网内部的查询请求 `ns1.yourdomain.com` 时，返回的地址是 `10.0.0.1`。此外，任何来自互联网的私有计算机（`red.yourdomain.com`, `blue.yourdomain.com` 等）拒绝。

## 编辑 named.conf

首先，你在主 DNS 服务器上配置 `/var/named/chroot/etc/named.conf` 文件，以代表你的示例 `yourdomain.com` 域名。此示例从 Fedora 和 RHEL 中 `caching-nameserver` 软件包自带的 `/etc/named.conf` 文件开始（在继续之前，请确保已安装了 `caching-nameserver` 和 `bind` 包，并对任何配置文件制作备份副本）。以下是关于编辑 `named.conf` 文件的一些提示：

- 如果一个语句包含语句，请确保最后一个语句以分号结尾。
- 注释可以以流行编程语言相同的格式出现。这些语言使用 C（以 `/*` 开头并以 `/*` 结束）、C++（以 `//` 开始并到物理行的末尾）以及 shell 或 Perl 风格（从 `#` 开始并到物理行的末尾）。
- 前导感叹号（`!`）否定一个元素。在语句中放入 `!123.45.67.89` 会导致 IP 地址 `123.45.67.89` 不匹配该元素。（只需确保否定发生在正向匹配之前，或者正向匹配具有优先。）

编辑后的 `/var/named/chroot/etc/named.conf` 文件如下：

```
options {
  directory "/var/named";
  dump-file "/var/named/data/cache_dump.db";
  statistics-file "/var/named/data/named_stats.txt";
}
acl "mylan" {
  127/8; 10.0.0.0/24;
}
controls {
  inet 127.0.0.1 allow { localhost; } keys { rndckey };
}
view "inside" {
  match-clients { "mylan"; };
  recursion yes;
}
zone "." IN {
  type hint;
  file "named.ca";
};

zone "0.0.10.in-addr.arpa" IN {
  type master;
  file "yourlan.db";
};
zone "yourdomain.com" {
  type master;
  file "db.yourdomain.com.inside";
  allow-transfer { 10.0.0.2 };
};

view "outside" {
  match-clients { any };
  recursion no;

zone "." IN {
  type hint;
  file "named.ca";
};

zone "yourdomain.com" {
  type master;
  file "db.yourdomain.com.outside";
};

include "/etc/bind/rnd.key";
```

# 第 25 章：通过 DNS 使服务器公开

## 设置区域文件（内部）

`/var/named/chroot/var/named` 目录包含了 `/var/named/chroot/etc/named.conf` 文件指向的区域文件。对于本示例，你只需要从头开始创建三个区域文件。你可以（也应该）保持 `named.ca` 文件不变。

域名服务器的大部分实际工作发生在区域文件中。在示例中，`db.yourdomain.com.inside` 包含了 `yourdomain.com` 的基础记录，包括所有私有名称和地址。以下是一个示例：

```
TTL      86400               hostmaster.yourdomain.com.
@        IN  SOA  yourdomain.com.
                        2008042701 ; Serial
                        28800               ; Refresh
                        14400               ; Retry
                        360000              ; Expire
                        86400 )             ; Minimum

; Name servers
         IN  NS  ns1.yourdomain.com.
         IN  NS  ns2.yourdomain.com.

; Mail server for domain
         IN  MX 10  mail.yourdomain.com.

; Public servers
ns1       IN  A  10.0.0.1
ns2       IN  A  10.0.0.2
mail      IN  A  123.45.67.2
www       IN  A  123.45.67.3
ftp       IN  A  123.45.67.4

; Private clients on the LAN
red       IN  A  10.0.0.2
blue      IN  A  10.0.0.3
green     IN  A  10.0.0.4
yellow    IN  A  10.0.0.5
```

; EOF

你“内部”的 `yourdomain.com` 区域文件包含了有关该区域信息的资源记录。你的 DNS 服务器使用 `TTL`（生存时间）来告诉存储你为此域名提供的信息的名称服务器，它们在丢弃这些信息并获取新信息之前可以保留这些信息。第一个值是整个区域的默认值，时间单位为秒。因此，`86400` 的值表示客户端使用信息应每 24 小时获取一次该域名的最新记录。

## 第四部分：Fedora RHEL 网络和服务器设置

`SOA` 行标识了域名的权威机构。`at (@)` 符号代表 `yourdomain.com` 名称 ——点（`.`）必须出现在域名的末尾。点代表互联网的根。如果你漏掉了点，你的 DNS 服务器将附加域名，因此 DNS 服务器将使用名为 `yourdomain.comyourdomain.com` 的名称。`hostmaster@yourdomain.com` 字符串表示接收与域名相关邮件的人的电子邮件地址。（点变为 `@` 符号，结果为 `hostmaster@yourdomain.com`）。关于 `SOA` 记录的其他信息如下：

- 以任意数字开始。如果区域记录发生更改，通过序列号来提醒其他服务器，它们可以获取关于你域名的最新数据。

**注意：** 如果你在更改区域记录后忘记增加序列号，缓存这些数据的其他服务器将永远不会获取你的更改。为了帮助记忆，请在序列号中使用日期。数字 `2008042701` 代表 2008 年 4 月 27 日。`01` 代表该当天进行的第一次更改。

- `Refresh`（刷新）——定义了该区域的从 DNS 服务器检查更改的方式。

名称服务器（`NS`）记录定义了代表此区域的名称服务器。假设 `NS` 记录定义了 `yourdomain.com` 中名为 `ns1` 和 `ns2` 的主机。`MX` 记录指示了该域名的主服务器的位置，以便 DNS 服务器将电子邮件重定向到 `yourdomain.com` 中的用户。文件的其余部分定义了与域名相关的私有客户端和公共服务器的 IP 地址。请注意，地址为 `10.0.0.2` 的服务器既是局域网上的客户端也是 DNS 服务器。

## 设置区域文件（外部）

对于“外部”，你使用来自“内部”的文件创建了 `db.yourdomain.comoutside`，但有以下例外：

- 删除了所有对局域网内私有客户端的引用。这样，在互联网上徘荡的人就无法获取关于你计算机的信息。
- 将主、从 DNS 服务器（`ns1` 和 `ns2`）的地址更改为 `123.45.67.1` 和 `123.45.67.2`。通过这种，公众只能看到名称服务器的公共地址。（当然，你需要使用自己的 IP 地址来代替 `123.45.67.1` 和 `123.45.67.2`）。

## 设置区域文件（反向查找）

示例中的另一个新文件是 `yourlan.db` 文件，它包含了对局域网内计算机执行反向 IP 查询所需的信息。以下是一个示例：
