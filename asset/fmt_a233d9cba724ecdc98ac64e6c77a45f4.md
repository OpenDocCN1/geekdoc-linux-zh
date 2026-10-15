
按照约定，所有区域文件都以 `db.` 开头，然后是跟一些名称或数字以标识特定区域。当区域包含传统的 DNS 记录（名称映射到 IP，IP 反向映射到名称）时，通常使用名称；数字通常用于反向 DNS 记录（映射回名称的记录）。例如，默认情况下，Ubuntu 的 BIND 会包含几个区域文件，如 `db.root`（互联网上根服务器的信息）、`db.local`（localhost 区域信息）和 `db.127`（localhost 的反向 DNS 记录）。

- `/var/cache/bind`

这是 BIND 的工作目录，它将在此处存储从区域文件。如果你的服务器将作为特定区域的从服务器，请配置它以存储其文件。

- `/etc/init.d/bind9`

这是 BIND 的初始化脚本。一旦安装了 `bind9` 包，它将自动设置为在系统启动时启动，但你可以通过 `/etc/init.d/bind9` 手动运行初始化脚本，或者运行 `sudo service bind9`。

- `/var/log/syslog`

这是 BIND 的默认日志文件。许多不同的服务都会记录到此文件中，但 BIND 的日志条目将以关键字 `named-` 开头，因此如果你只想查看 BIND 的日志条目，可以运行 `sudo grep /var/log/syslog`。

## 缓存名称服务器

默认的 BIND 配置开箱即用即可缓存名称服务器。本质上，缓存名称服务器充当 DNS 查询的中间。一旦你配置了缓存名称服务器，当一个主机请求特定记录时，缓存名称服务器会连接互联网，检索记录并将其存储在本地。如果第二个主机请求相同的记录，且该记录未从缓存中过期，缓存名称服务器将直接返回缓存结果。这可以极地提高主机网络的的响应时间，特别是对于 Web 浏览，因为经常有相同的记录（例如 `www.google.com`）被多个主机请求。

## DNS 主服务器

缓存名称服务器非常有用，但当大多数人安装 BIND 时，他们的打算是托管一些自己的区域文件。当名称服务器在本地托管区域文件而不需要从任何其他源检索它们时，它被称为主服务器（master）。当你向 DNS 服务器添加区域时，基本上有三步：创建区域文件、在 `named.conf` 中添加该区域文件的引用，并告诉 BIND 重新加载其配置。

对于我的示例，假设我在网络内部有一个位于 `192.168.0.5` 的名称服务器，并注册了 `example.net`。我希望这个名称服务器具有以下条目：

- `ns1.example.net` 指向 `192.168.0.5`（名称服务器本身）。

- `example.net` 也指向 `192.168.0.7`。

- `www.example.net` 指向 `192.168.0.7`。

- `gateway.example.net` 指向 `192.168.0.1`。

创建新区域文件最简单的方法是复制一个你已有的并进行修改。在这种情况下，最好的候选文件是 `/etc/bind/db.local` 文件，所以我将其复制到 `db.example.net`。

```
$ sudo cp /etc/bind/db.local /etc/bind/db.example-net
```

当我用文本编辑器打开 `db.example.net` 时，我将看到以下配置：

```
: BIND data file for local loopback interface
:$TTL 604800
@ IN SOA localhost.root.localhost. (
      2 : Serial
      604800 : Refresh
      86400 : Retry
      241920 : Expire
      604800 : Negative Cache TTL)
@ IN NS localhost.
@ IN A 127.0.0.1
@ IN AAAA ::1
```

因为这并不打算成为 BIND 的完整指南，我将不会介绍该文件中的每一个选项，但默认情况下，它被配置的 TTL（生存时间，即名称服务器请求记录后我们认为该记录有效的时间）为 `604800` 秒，即七天。接下来，它列出了 `localhost` 作为 SOA（起始起点，应被视为信息最佳源的服务器），而 `root@localhost` 是该主机的电子邮件地址（通过 `root.localhost` 引用）。在更后的部分，文件列出 `localhost` 为该区域的名称服务器并带有一个 NS 记录，然后将 `localhost` 的 IP 地址设置为 `127.0.0.1`，甚至为 `localhost` 添加了带有 AAAA 记录的 IPv6 地址。

我更改了此记录以适应我的需求，这就是生成的区域文件：

```
: BIND data file for local loopback interface
:$TTL 604800
```

```
: BIND data file for example.net

:$TTL 1d

@ IN SOA ns1.example.net. root.example.net. (

      2 : Serial

      604800 : Refresh

      86400 : Retry

      241920 : Expire

      604800 ) : Negative Cache TTL

:

@ IN NS ns1.example.net.

@ IN A 192.168.0.6

ns1 IN A 192.168.0.5

www IN A 192.168.0.7

gateway IN A 192.168.0.1
```

文件中有很多需要注意。首先，我将 TTL 从七天改为一天。虽然可以使用秒表示，但 BIND 支持缩写，因此我可以使用 `1d` 表示一天，或 `4h` 表示四小时。我将 `ns.example.net` 设置为 SOA，并将 `root@example.net` 设置为联系电子邮件地址。我注意到 NS 记录引用了该区域使用的主机名称，但注意，由于此名称服务器在同一个域名 `example.net` 中，我需要确保在这里为它添加列出其 IP 地址的记录。还要注意，我不需要在任何 A 记录中添加 `.example.net`。

注意 请确保保存区域文件时，其权限和所有权与目录中的其他区域文件相同——这是避免以后重载 BIND 时出现任何权限问题的最佳方法。

我已经创建了区域文件，现在需要在 `named.conf` 中对其添加引用。当我用文本编辑器打开它时，可以看到许多类似的示例，类似于 `db.local` 文件的那个：

```
zone "localhost" {

  type master;

  file "/etc/bind/db.local";

}
```

所以我只需要在文件末尾添加一个类似的条目：

```
zone "example.net" {

  type master;

  file "/etc/bind/db.example.net";

}
```

# 第5章 ■ 普通 Ubuntu 服务器指南

一旦我保存了更改，我只需要告诉 BIND 重新加载配置，然后我就可以查询其中一个新记录的服务器了：

```
$ sudo service bind9 reload
+ Reload domain name server... bind [OK]
$ nslookup www.example.net localhost
Server: localhost
Address: 127.0.0.1#53
```

如果 BIND 重新加载失败，它会在命令行中提示。如果该命令行输出没有告诉你 BIND 拒绝重载，你可以查看 `/var/log/syslog` 以寻找线索。

## DNS 服务器

DNS 从服务器（slave）从另一个称为主服务器（master）的 DNS 区域获取其区域信息。事实上，一个 BIND 服务器可以作为一个区域的主服务器，同时作为另一个区域的从服务器。拥有一个主服务器和多个从服务器极大地简化了你的 DNS 管理，因为你只需要在主服务器上更新区域信息，它会自动传播到所有从服务器。当你在主服务器上更新区域并增加该区域内的序列号（`serial number`）时，一旦 BIND 重新加载，所有从服务器都会获取到区域已发生更改，并将自动下载更新。

由于 DNS 从服务器从主服务器获取区域信息，其配置要简单得多。只要主服务器配置为允许从服务器进行区域传输，你只需要在从服务器上向 `/etc/bind/named.conf` 添加一个条目即可。对于我们的示例，假设我想添加第二个名称服务器 `ns2.example.net`，其 IP 为 `192.168.0.10`。

### 配置主服务器

在我的主服务器 `192.168.0.5` 上，我需要编辑 `db.example.net` 文件并添加对 `ns2.example.net` 的引用。

```
; BIND data file for example.net
; TTL 1d SOA ns1.example.net.root.example.net. (

@ IN A : Serial
      3
604800 : Refresh
86400 : Retry
2419200 : Expire
604800 : Negative Cache TTL
:

@ IN NS ns1.example.net.
@ IN NS ns2.example.net.
@ IN A 192.168.0.6
snl IN A 192.168.0.5
s2 IN A 192.168.0.10
www IN A 192.168.0.1
gateway
```

现在，我需要在 `named.conf` 的 `example.net` 配置中添加一行，以便它允许来自 `192.168.0.10` 的区域传输，因此 `example.net` 在 `named.conf` 中的条目变为：

```
"example.net" {
type master;
file "/etc/bind/db.example.net";
allow-transfer { 192.168.0.10 };
}
```

### 配置从服务器

在从服务器上，通过 `tasksel` 或 `apt-get` 安装 `bind9` 包，然后我只需要在 `/etc/named.conf` 的底部为 `example.net` 添加一个从服务器条目。

```
"example.net" {
type slave;
file "/var/cache/bind/db.example.net";
masters { 192.168.0.5 };
}
```

使用 `sudo bind9 reload` 重新加载 BIND。一旦 BIND 重新加载，它会立即尝试从 `192.168.0.5` 执行 `example.net` 的区域传输。当区域传输完成后，如果我检查 `/var/cache/bind/` 目录，将看到生成的 `db.example.net` 区域文件。现在，下次我想对 `db.example.net` 进行更改时，只需更改主服务器上的文件，更新序列号，然后在主服务器上重新加载 BIND。从服务器会自动获取更新。

### 使用 rndc 管理 BIND

到目前为止，我通过 `bind9` 初始化脚本重新加载了 BIND。Ubuntu 还包含了另一个名为 `rndc` 的工具，可以帮助你管理 BIND。例如，使用 `rndc` 重新加载 BIND 配置，我会输入：

```
$ sudo rndc reload
```

你可以向 `rndc` 传递其他参数以获取更多关于 BIND 服务的信息或向其提交命令。`rndc` 命令的一个有用方面点是，如果你希望管理员能够更新 DNS 但没有 root 权限，可以赋予该人员 `rndc` 命令的 `sudo` 权限。如果不带任何参数，你将得到一个列出可用命令的帮助页面。以下是最常用的几个：

- `reload`——重新加载所有配置文件和区域。如果你在 `reload` 命令后指定了特定区域，它将只重新加载该区域。
- `retransfer zone`——无论序列号是否已增加，都对区域进行重新传输。
- `reconfig`——类似于 `reload` 命令，但它只重新加载 `named.conf` 和任何新区域。
- `flush`——刷新服务器的所有缓存。这在缓存服务器上非常有用，如果它正持有一个不再有效的过时 IP 地址的话。
- `status`——输出关于 BIND 进程当前状态的某些统计信息，包括它正在管理的区域数量以及关于其当前负载的一些统计数据。

`rndc` 中还有许多其他命令，但这些是你会在管理 BIND 时会执行的最常见任务。

## Web 服务器

- `/etc/apache2/conf.d/`
  此目录被列为主 `apache2.conf` 文件中的包含目录，这意味着当 Apache 启动时，它将包含在此目录中找到的任何配置文件，并将它们添加到总体配置中。过去某些管理员（例如我本人）曾使用此目录来存储所有的虚拟主机，每个主机单独存储在一个文件中，但 Ubuntu 现在有了一个更好的解决方案，将在本章的稍后部分提到。该目录不再包含虚拟主机，而是用于存放 Apache 管理员（或软件包）可能想要从核心 `apache2` 之外单独添加的配置。

- `/etc/apache2/mods-available/`
  以前向 Apache 添加模块一直是一件痛苦事。一旦安装了模块本身，你就必须翻阅 `http.conf` 文件，找到可能被注释掉的某种 `mod_module` 逻辑引用，而且大多数时候为了加载它，还必须手动粘贴相关代码。Ubuntu 提供了一种更简单、更模块化的方法。系统中所有可用的模块都通过此目录下的 `.load` 和 `.conf` 文件表示。`.load` 文件包含了将模块加载到 Apache 所需的所有配置，而可选的 `.conf` 文件包含了 Apache 在加载文件后可能需要的任何额外配置。如果你想知道你的 Apache 安装中有哪些可用模块，只需查看此目录。

- `/etc/apache2/mods-enabled/`
  此目录的工作原理类似于 System V `init.d` 目录中不同的运行级别目录，因此如果说 `mods-available` 就像你的家 目录，那么这个目录就相当于 `rc.d`（如果你不明白我的意思，请查阅第 2 章对 System V init 的描述）。基本上，此目录包含指向 `mods-available` 中 `.load` 和 `.conf` 文件的软链接。当 Apache 启动时，它会看到此目录并加载其中引用的所有模块。例如，如果我想启用 CGI 模块，可以输入：

```bash
$ sudo ln -s /etc/apache2/mods-available/cgi.load \
/etc/apache2/mods-enabled/cgi.load
```

当然，Ubuntu 甚至提供了简化工具。要启用一个模块，只需运行 `a2enmod` 后跟你想要启用的模块名。要像我上面那样启用 CGI 模块，我只需运行：

```bash
$ sudo a2enmod cgi
```

同样，还有一个 `a2dismod` 程序可以为你禁用模块。它采用与 `a2enmod` 相同的语法，禁用 CGI 类型如下：

```bash
$ sudo a2dismod cgi
```

- `/etc/apache2/sites-available/`
  Ubuntu 组织 Apache 主机的方式与模块类似。在 Apache 创建之前，市面上的可用 Web 服务器软件每台物理服务器只能托管一个站点。Apache 引入了虚拟主机的概念，允许它在台物理服务器上托管多个站点。每个虚拟主机可以有完全不同的域名和完全不同的文档根。在 Ubuntu 下，这台机器上 Apache 可提供的每个虚拟主机（或站点）其配置都在一个独立的文件中，默认名为 `default`。该文件默认位于 apt 默认目录下，它定义了默认虚拟主机，如果配置了其他主机，或者没有其他站点的配置匹配请求的主机名，就会显示该主机。

- `/etc/apache2/sites-enabled/`
  与 `mods` 类似，此目录包含指向 `sites-available` 中配置文件的软链接。当你想要为 Apache 添加新的虚拟主机时，只需在 `sites-available` 下为该主机创建一个包含完整 `<VirtualHost>` 块的新配置，并将其软链接到此处：

```bash
$ sudo ln -s /etc/apache2/sites-available/mysite \
    /etc/apache2/sites-enabled/mysite
```

或者你可以使用 `a2ensite` 脚本，它的工作方式与 `a2enmod` 相同。只需运行 `a2ensite` 并将想要启用的站点作为参数即可。要启用 `mysite`，我会输入：

```bash
$ sudo a2ensite mysite
```

要禁用它，我可以使用 `a2dissite`：

```bash
$ sudo a2ddissite mysite
```
