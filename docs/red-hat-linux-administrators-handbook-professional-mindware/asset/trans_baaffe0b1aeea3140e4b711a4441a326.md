

DNS 服务本身是由反向 DNS 服务提供的，这就是为什么你的 `/etc/named.conf` 文件中总需要一个特殊的区域声明，其形式如下：

```
zone "0.0.127.in-addr.arpa" {
type master;
file "named.local";
};
```

你还需要在名称服务器的工作目录中拥有 `named.local` 区域文件。该文件如清单 8-4 所示。

**清单 8-4** *named.local 文件*

```
@ IN SOA localhost. root.localhost. (
1999020100 ; Serial
7200 ; Refresh - 2 hours
3600 ; Retry - 1 hour
43200 ; Expire - 12 hours
3600 ) ; Minimum - 1 hour

IN NS localhost.
1 IN PTR localhost.
```

## 配置仅缓存/从属 DNS 服务器

从技术角度来看，所有的 DNS 服务器都具有缓存功能；换句话说，DNS 服务器默认使用缓存。然而，如果你不想为任何互联网域名提供 DNS 服务，而仅希望提高网络的 DNS 查询性能，你可以运行一个仅缓存的 DNS 服务器。这样的服务器将包含一个 `/etc/named.conf` 文件，如清单 8-5 所示。

**清单 8-5** *仅缓存 DNS 服务器的 /etc/named.conf 文件*

```
zone "" {
type hint;
file "named.ca";
};

zone "0.0.127.in-addr.arpa" {
    type master;
    file "named.local";
};
```

第一个区域声明指定名称服务器使用 `named.ca` 文件在启动时确定根名称服务器名称。第二个区域声明用于为本地回环网络提供反向名称服务。这就是创建仅缓存名称服务器所需的全部内容。

## 控制 DNS 服务器

`named` 发行版附带了一个名为 `ndc` 的实用程序，它提供了一种简单的命令行界面来控制名称服务器。

## 启动名称服务器

你的名称服务器应在启动时自动启动。如果它没有自动启动，请执行以下步骤：

1.  以 root 用户身份登录到你的名称服务器系统，并将目录更改为 `/etc/rc.d/init.d`。确保该目录下有一个名为 `named` 的脚本。如果你缺少此脚本，请从你的 Red Hat CD-ROM 重新安装 BIND 发行版 RPM，或从 RegHat 网站下载它。
2.  在确认你有 `/etc/rc.d/init.d/named` 脚本后，将目录更改为你的默认系统运行级别（参见 `/etc/inittab`）的 `rc` 目录。对于大多数系统，默认运行级别是 3；如果你的也是如此，请将目录更改为 `/etc/rc.d/rc3.d`。
3.  创建一个名为 `SXXnamed` 的符号链接，指向 `/etc/rc.d/init.d/named` 脚本。在 `SXXnamed` 中用一个大数字（例如 55 或 85）替换 `XX`，以确保系统不会在网卡正确设置之前尝试启动名称服务器。例如，要创建一个指向 `named` 脚本的名为 `S55named` 的符号链接，请运行以下内容：

创建此链接后，每次启动系统时，你的系统都会启动名称服务器。然而，如果你更喜欢手动运行名称服务器，请使用 `ndc` 程序，如下所示：

`ndc start`

## 重新加载新的名称服务器配置

在你修改任何区域文件或 `/etc/named.conf` 文件后，必须重启名称服务器才能使更改生效。你可以按以下方式强制名称服务器重新加载新配置：

`ndc reload`

别忘了修改你所修改的任何区域文件中 SOA 记录里的序列号，否则名称服务器将不会加载新配置。

若要先终止名称服务器再重启，请在上述行中使用 `restart` 代替 `reload`。

## 停止名称服务器

如果由于任何原因需要停止名称服务器，请运行 `ndc` 命令，如下所示：

`ndc stop`

## 查看名称服务器统计信息

你可以使用 `ndc` 程序在名称服务器的工作目录中生成各种名称服务器统计信息。运行以下内容以在名称服务器的工作目录中创建一个名为 `named.stats` 的文件：

`ndc stats`

此统计文件显示各种信息项，包括每个 RR 的查询数量。

每次修改 DNS 信息时，别忘了使用名称服务器查询工具测试配置。

## 测试你的 DNS 服务器

有许多工具可用于手动查询名称服务器。如果你想拥有几个常用的查询工具，请从你的 Red Hat CD-ROM 安装 `bind-utils` RPM 发行版。`bind-utils` 发行版包含 `dig`、`dnsquery`、`host`、`nslookup` 等。我最喜欢的，也是使用最广泛的，是 `nslookup` 实用程序，因此本节使用它来测试 DNS 配置。

假设你刚刚在一个域名注册网站注册了一个全新的域名，并且已经在名称服务器上设置了必要的 DNS 配置。在重启名称服务器后，你想通过 `nslookup` 测试配置。

当你从命令行运行 `nslookup` 时，它会显示默认使用的名称服务器的主机名和 IP 地址。如果你正在名称服务器系统上运行 `nslookup`，你应该看到名称服务器的名称和 IP。如果你没有看到名称服务器的信息，请确保你的 `/etc/resolv.conf` 文件已正确配置。

另一方面，如果你在一台非名称服务器的计算机上运行 `nslookup`，你必须告诉程序使用你想要测试的名称服务器。只有当域名注册网站尚未向根名称服务器发布新域名的名称服务器信息时，你才需要这样做。要告诉 `nslookup` 使用不同于默认的名称服务器，请在 `nslookup` 命令提示符下输入 `server host_name`（其中 `host_name` 是你想要测试的服务器的 hostname）。输入此命令后，`nslookup` 将对所有查询使用指定的名称服务器主机。

`nslookup` 实用程序允许你使用简单的语法执行任何类型的 DNS 查询。例如，要查找域的名称服务器，请在 `nslookup` 程序内运行以下命令：

```
set query=ns
domain.tld
```

第一行告诉 `nslookup` 为下一个域（`domain.tld`）执行 NS（名称服务器 RR）查询。类似地，你可以执行 A、MX、CNAME 等查询。如果你得到的响应看起来不对，请回到区域文件，确保没有拼写错误。一个常见的错误是省略完整主机名末尾的句点。

## 管理虚拟域名的 DNS

单个名称服务器可以为许多域名提供名称服务。此功能允许单个系统托管许多互联网域名。事实上，大多数 ISP 就是这样为客户提供商网站服务的。由于这些域名托管在另一个域（例如，ISP 自己的域）上，它们被称为*虚拟域名*，这在如今非常常见。如果你需要日常为客户创建大量虚拟域名，你可能希望尽可能自动化此过程。清单 8-6 显示了一个名为 *makesite* 的 Perl 脚本，你经常可以使用它来创建虚拟域名。

**清单 8-6** *makesite 脚本*

```
#!/usr/local/bin/perl -w

use strict;

# Purpose: makesite creates virtual sites.
# It uses a set of templates to create DNS and HTTPD
# configuration files.
#
# Note: this is a very *simple* script.
#
########################################

use Time::localtime;

my $site		= $ARGV[0] or &syntax;
my $MAKESITE_DIR	= '/scratch/dns/makesite/';
my $USER		= 'httpd';
my $GROUP		= 'httpd';
my $PERMISSION	= '2770';
my $BASE_DIR		= '/tmp/';
my $HTTPDIR		= 'htdocs';
my $SCGIBIN		= 'cgi-bin';
my $NAMED_PATH        = '/var/named';
my $NAMED_FILE_EXT    = '.db';
my $NAMED_TEMPLATE    = "$MAKESITE_DIR/named.template";
my $NAMED_CONF        = '/etc/named.conf';
my $HTTPD_CONF        = '/usr/local/apache/etc/httpd.conf';
my $VHOST_TEMPLATE    = "$MAKESITE_DIR/httpd.template";
my $LOG_FILE          = "$BASE_DIR/makesite.log";

my $dir = $site;
my @domain_types = qw(com net org edu);
my ($domain_ext, $thesite_dir, $public_dir,
    $htdocs_dir, $cgbind_dir, $named_file,
    $dir_len, $temp_len);

my $tm = localtime(time);
my $date = sprintf("%s-%02s-%02s-%02d", $tm->year+1900,
                   $tm->mon+1,
                   $tm->mday,
                   $tm->hour,
                   $tm->min);
my $serial = sprintf("%s%02d%02d000", $tm->year+1900,
                    $tm->mon+1,
                    $tm->mday);

$site =~ y/[A-Z]/[a-z]/;

# Get the length with the EXT
$dir_len = length($dir);
```

*续*

