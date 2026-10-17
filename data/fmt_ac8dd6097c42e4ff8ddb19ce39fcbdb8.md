
系统的 FQDN（完全域名）是解析器(3) 返回的主机名，例如，`ursula.example.com`。它通常是主机名后接 DNS 域名（第一个点之后的部分）。你可以检查 FQDN

使用 `hostname --fqdn` 或使用 `dnsdomainname` 的域名。

你无法通过 `hostname` 或 `dnsdomainname` 修改 FQDN。

设置 FQDN 的推荐方法是通过 `/etc/hosts`、DNS 或 NIS 将 hostname 设为完全限定域名（FQDN）的别名。例如，如果 hostname 为“ursula”，在 `/etc/hosts` 中可能有这样一行：

```
127.0.1.1 ursula.example.com ursula
```

从技术上讲：FQDN 是 `getaddrinfo(3)` 为 `gethostname(2)` 返回的主机返回的名称。DNS 域名是第一个点之后的部分。

因此，如何更改它取决于解析器的配置（通常在 `/etc/host.conf` 中）。通常 `hosts` 文件在 DNS 或 NIS 之前被解析，因此最常见的方法是在 `/etc/hosts` 中更改 FQDN。

如果一台机器具有多个网络接口/地址，或者在移动环境中使用，它可能有多个 FQDN/域名，或者一个都没有。因此，请避免使用 `hostname --fqdn`、`hostname --domain` 和 `dnsdomainname`。`hostname --address` 也存在同样的限制，因此也应避免。

# OPTIONS

- `-a`, `--alias`

显示主机的别名（如果已使用）。此选项已弃用，不应再次使用。

- `-A`, `--all-fqdns`

显示机器的所有 FQDN。此选项会列出所有配置的网络接口上的所有配置的地址，并将它们转换为 DNS 域名。无法转换的地址（例如，因为它们没有适当的反向 IP 条目）将被跳过。注意不同的地址可能解析为相同的名称，因此输出可能包含重复项。不要对输出的顺序做任何假设。

- `-b`, `--boot`

始终设置 hostname；如果 `-F` 指定的文件不存在或为空，则在未设置时将使用默认的 hostname `localhost`。

- `-d`, `--domain`

显示 DNS 域名的名称。不要使用 `domainname` 命令来获取 DNS 域名，而不是 DNS 域名。请改用 `dnsdomainname`。请查看上文“THE FQDN”章节中的警告，并使用此选项。

- `-f`, `--fqdn`, `--long`

显示 FQDN（完全限定域名）。一个 FQDN 由短主机名和 DNS 域名组成。除非你为主机查找绑定了 NIS，否则你可以在 `/etc/hosts` 文件中更改 FQDN 和 DNS 域名（它是 FQDN 的一部分）。请查看上文“THE FQDN”章节中的警告，并尽可能使用 `hostname--all-fqdns`。

- `-F`, `--filename`

从指定文件中读取名称。忽略注释（以 `#` 开头的行）。

- `-i`, `--ip-address`

显示主机名的网络地址。注意，这仅在主机名可以解析时才有效。请避免使用此选项；请改用 `hostname--all-ip-addresses`。

- `-I`, `--all-ip-addresses`

显示主机的所有网络地址。此选项列出所有网络接口上的所有配置的地址。跳过回环接口和 IPv6 链路地址。与 `-i` 不同，此选项不依赖名称解析。不要对输出的顺序做任何假设。

- `-s`, `--short`

显示短主机名。这是在第一个点处截断的主机名。

- `-V`, `--version`

在标准输出上打印版本信息并成功退出。

- `-y`, `--yp`, `--nis`

显示 NIS 域名。如果给出了参数（或 `--file`），则 root 也可以设置新的 NIS 域。

- `-h`, `--help`

打印用法信息并退出。

# NOTES

`hostname` 在查找主机的 FQDN、别名和网络地址时尝试的地址族由你的解析器配置决定。例如，在 GNU Libc 系统上，可以通过使用 `/etc/resolv.conf` 中的 `inet6` 选项指示解析器优先尝试 IPv6 查询。

# FILES

`/etc/hostname`: 历史上，此文件本应只包含 hostname 而不是完整的规范 FQDN。现在，大多数软件都能处理完整的 FQDN。系统初始化脚本在启动时会读取此文件以设置 hostname。

`/etc/hosts`: 通常，在此处通过将 hostname 别名为 FQDN 来设置域名。

# AUTHORSORS

- Peter Tobias, <tobias@debian.de>

- Bernd Eckenfels, <nettools@debian.de>

- Michael Meskes, <meskes@debian.org>

# dos2unix

# NAME

`dos2unix` - DOS/Mac 转 Unix 文本文件转换

# SYNOPSIS

```
dos2unix [options] [FILE...]
unix2dos [options] [FILE...] [-n OUTFILE...]
```

# DESCRIPTION
