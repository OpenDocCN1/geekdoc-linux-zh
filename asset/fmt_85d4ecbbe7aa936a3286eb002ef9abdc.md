
无论是对于个人使用还是工作，我都能从 Red Hat Linux 的标准安装开始，并在极少或无需更改的情况下提供所需服务。

然而，为了提供所有正在的服务，需要许多细小的更改和额外的服务。本地管理员应该注意以下内容：

- `/etc/rc.d/rc.local` 文件在启动时执行，包含了你添加到服务器的任何应在启动时执行的额外服务。

- 检查 `/etc` 下可能需要的特定站点更改。这些可能包括：

  - `/etc/inetd.conf`（你应该确保禁用不必要的服务如 fetch、echo；并添加或更改你需要的服务）。

  - `/etc/exports`（允许挂载 NFS 卷的主机列表；详情参见第 7.6 节）。

  - `/etc/nntpserver`

  - `/etc/lilo.conf`（包含 LILO 引导器的信息 —— 启动时加载 Linux 内核的过程；详情参见第 4.8 节）。

  - `/etc/sudoers`（赋予特殊权限的用户列表以及他们被允许执行的命令）。

  - `/etc/named.boot`（用于 DNS；详情参见第 7.2 节）。

`/usr/local/` 及其子目录中的任何内容都是是从压缩包等安装而非使用 RPM 安装时产生的额外包或对现有包的修改。（或者至少，你应该将它们安装在这里。）这些文件，特别是 `/usr/local/src/` 下的文件，应该保持更新。详情参见第 10 章。

# 第 7 章 自定义配置与管理问题

## 7.1. Web 服务器与 HTTP 缓存代理管理

> （警告：忽略此章节！）

6. 如果用户需要启用电子邮件转发，你可以创建一个 `.forward` 文件，只需将正确的电子邮件作为文件的第一行且唯一的行即可。

就是这样。用户可以使用 FTP 更新页面。

## 7.2. 域名服务器 (DNS) 配置与管理

在我们的工作单位，我们使用 Linux 作为 DNS 服务器。它的性能异常出色本节将介绍如何使用 Red Hat 发行版自带的 BIND 8.x 软件包为这些服务配置 DNS 表。

注意：Red Hat 5.1 及更早版本使用的是 BIND 4.x 软件包，其配置文件格式略有不同。BIND 8.x 提供的功能比 BIND 4.x 更多，由于 4.x 不再进行开发，你应该考虑将 BIND 包升级到最新版本。只需安装 BIND RPM 包（详细信息请参阅第 10.1 节使用 RPM 工具的说明），然后将你的配置文件转换为新格式即可。

幸运的是，将现有的 BIND 4.x 配置转换为符合 BIND 8.x 标准的文件非常简单！在 BIND 提供的文档中（例如，针对 BIND 8.1.2 的 `/usr/doc/bind-8.1.2/`），存在名为 `named-bootconf.pl` 的文件，这是一个可执行的 Perl 程序。假设你的系统中安装了 Perl，你可以使用该程序转换配置文件。操作时，请执行以下命令（以 root 身份）：

```bash
cd /usr/doc/bind-8.1.2/
./named-bootconf.pl < /etc/named.boot > /etc/named.conf
mv /etc/named.boot /etc/named.boot-obsolete
```

现在你应该有一个 `etc/named.conf` 文件，它看起来应该是 BIND 8.x 的“开箱即用”状态。现有的 DNS 表可以在新版本的 BIND 中直接工作，因为表的格式保持不变。

在 Linux 下配置 DNS 服务涉及以下步骤：

- 1. 要启用 DNS 服务，`etc/host.conf` 文件应如下所示：

```conf
# 首先通过 /etc/hosts 查找名称，然后按照 DNS 查询顺序查找
hosts, bind
# 我们没有具有多个地址的机器。检查是否存在 IP 地址欺骗
nospoof on
# 如果有人尝试欺骗则发出警告
alert on
```

额外的欺骗检测会给 DNS 查找带来轻微的性能影响（尽管忽略不计），所以如果你不太担心这一点，你可能希望禁用 `nospoof` 和 `alert` 条目。

- 2. 根据需要配置 `/etc/hosts` 文件。通常这里不需要包含任何内容，但为了提高性能，你可以添加任何你访问的主机（例如本地服务器），以避免对它们进行 DNS 查询。

- 3. `/etc/named.conf` 文件应根据下面的示例进行配置，以指向你的 DNS 表。

> （注意：所示的 IP 地址仅为示例，必须替换为你自己的类类地址！）

```conf
options {
// DNS 表位于 /var/named 目录下 "/var/named"

// 将任何未解析的请求转发到我们 ISP 的名称服务器
// （这只是示例 IP 地址 - 请勿使用！）
forwarders {
123.12.40.17;
}
/*
* 如果你与想要通信的名称服务器之间存在防火墙，
* 你可能需要取消注释下面的 query-source
* 指令。之前的 BIND 版本始终使用端口 53
* 进行提问，但 BIND 8.1 默认使用非特权
* 端口。
*/
// query-source address * port 53;
};

// 启用缓存并加载根服务器区域 "named.root" {
type hint;
file "";
};

// 所有 DNS 信息存储在 /var/named/mydomain_name.db 中
// （例如，如果 mydomain.name = foobar.com 则使用 foobar.db）
zone "mydomain.name" {
type master;
file "mydomain_name.db";
allow-transfer { 123.12.41.0 };
};

//  123.12.41.*, .42.*, .43.*, .44.* C 类的反向查找
// （这些是示例 C 类 - 请勿使用！）
zone "41.12.123.in-addr.arpa" {
type master;
file "123_12.rev";
allow-transfer { 123.12.41.0 };
};

// 126.27.18.*, .19.*, .20.* C 类的反向查找
// （这些是示例 C 类 - 请勿使用！）
zone "18.27.126.in-addr.arpa" {
type master;
file "126_27.rev";
allow-transfer { 123.12.41.0 };
};
```

提示：请注意上面的 `allow-transfer` 选项，它将区域传输限制给指定的 IP 地址。在我们的示例中，我们允许位于 123.12.41.0 的主机（可能是我们域中的一个从用 DNS 服务器）请求传输。如果你省略了此项，互联网上的任何人都将请求此类传输。由于这些信息经常被垃圾邮件发送者和欺骗者利用，我强烈建议你将区域传输限制在从用 DNS 服务器上，或者使用环回地址 `127.0.0.1`。

- 4. 你现在可以像 `/etc/named.conf` 文件所示，在 `/var/named/` 目录中设置你的 DNS 表。首次配置数据库文件是一项巨大的工程，并且超出了本文的范围。有几份指南应当参考。然而，下面提供了几个示例。

`/var/named/mydomain_name.db` 中的条目是正向查找文件：

```
; 这是起始记录 (SOA) 记录。包含有关名称服务器的联系和其他信息。每当文件更新时，必须更改序列号。
@ mydomain.name. postmaster.mydomain.name. (
1990811 ; 序列号
3600 ; 1 小时刷新
300 ; 5 分钟重试
172800 ; 2 天过期
43200 ) 12 小时最小

; 如正向查找表中的名称服务器
IN NS mydomain.name.
IN NS isp.name.

; MX 邮件交换器记录可以列出多个，优先级字段越小越优先。
IN MX mydomain.name.

; 提供有关机器类型和操作系统的信息
IN HINFO Pentium/350 LINUX NT

; 机器名称地址列表
spock.mydomain.name      IN A 123.12.41.40 ; Linux
mail.mydomain.name      IN A 123.12.41.41 ; Linux（主服务器）
kirk.mydomain.name      IN A 123.12.41.42 ; Windows

; 包括我们的其他类
twikel.mydomain.name    IN A 126.27.18.161 ; Linux 测试
one.mydomain.name      IN A 126.27.18.162 ; Linux 开发

; 别名（规范）
gopher CNAME myomain.name
ftp CNAME myomain.name
www CNAME myomain.name
```

`/var/named/123_12.rev` 中的条目是反向查找文件：
