
# 破解 Linux 暴露：Linux 安全秘密与解决方案

当 TCP wrappers 使用 `-DPARANOID` 选项编译时，它们将拒绝来自任何正向和反向 DNS 记录不匹配的机器的连接。这让许多无法修复 DNS 记录的系统管理员感到恼恼。然而，匹配记录是你能够开始相信一个主机确实如其所称的那样的唯一方法。毕竟，如果一个管理员无法保持其记录同步，你还能信任其系统的安全性吗？

- 如果你自己编译 TCP wrappers，请指定 `-DPARANOID` 选项。大多数发行版默认都开启了。

## 信任网域内的攻击者

| 流行度 | 4 |
| :--- | :--- |
| 简单性 | 10 |
| 影响 | 9 |
| 风险评分 | 8 |

你怀疑一个 IP 为 `trouble.example.org` 的员工正准备离开公司。他有些心存不满，并一心想要破坏你 Linux 服务器上的重要信息。你想保护数据免受损坏或窃取，但你目前允许访问 `example.org` 网域内的所有机器。

## 使用 inetd 锁定网域内的特定主机

为了锁定该员工的机器，请在 `/etc/hosts.allow` 中使用 `EXCEPT` 操作符：

```
# /etc/hosts.allow

ALL: 127.0.0.1 trusted.machine.example.com \
      .example.org EXCEPT trouble.example.org

ipip3d: ALL

telnetd: server1.example.com
```

注意，我们不需要在一行中指定所有允许访问的机器。我们可以将它们放在单独的行中，如下：

```
# /etc/hosts.allow

ALL: 127.0.0.1

ALL: trusted.machine.example.com

ALL: .example.org EXCEPT trouble.example.org

ipip3d: ALL

telnetd: server1.example.com
```

## 第 13 章：访问控制与防火墙

锁定该用户机器的另一种方法是删除其反向 DNS 记录，在这种情况下，他的机器将不会映射到任何域名，纯基于主机名的规则将无法被匹配。

> 如果你删除了反向 DNS 记录，但存在与其 IP 地址的匹配项，他仍然可以访问被 TCP 封装的服务。

- 使用 `xinetd` 锁定网域内的特定主机：要锁定信任网络中的特定机器，请使用 `no_access`：

```
no_access = trouble.example.org
```

现在，即使我们允许访问 `.example.org`，也将拒绝访问 `trouble.example.org`。

## 针对非 inetd/xinetd 服务的攻击

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 6 |
| 风险评分 | 7 |

并不是所有的互联网服务都由 `inetd` 或 `xinetd` 启动。`Ssh` 就是其中一个例子。因此，我们无法使用 TCP wrappers 或 `xinetd` 来限制黑客的访问。即使我们通过 `telnet` 和 `FTP` 拒绝黑客访问我们的机器，她仍然能够通过 `Ssh` 连接。

- 编译 TCP Wrapper 支持：许多互联网程序允许在编译时加入 TCP wrappers，`Ssh` 就是这样一个例子。在配置 `SSH` 时，只需向配置程序传递 `--tcp-wrappers` 选项即可。然后你可以在 `/etc/hosts.allow` 中添加条目，例如：

```
sahd:example.com .trusted_network.org trusted_machine.example.org
```

- 请求程序维护者支持 TCP Wrappers：如果你想封装一个不支持 TCP wrappers 的程序，可以礼貌地请求维护者添加实现该功能所需的代码。遗憾的是，这并不总是成功的，但如果你确定了如何添加此功能并向维护者提供补丁，你的机会会大得多。

## 手动实现 TCP Wrappers

开源软件意味着源代码可用，因此我们可以根据需要对其进行修改。以下是一个为互联网服务程序添加 TCP wrappers 所需的代码示例。该示例来自 `tunnel` (`http://www.stunnel.org/`)，并假设使用 C 语言，且配置特定构建过程的程序定义了预处理器变量 `USE_LIBWRAP`。

需要以下头文件，它应该放在你的 C 程序的顶部：

```c
/* TCP wrapper */

#ifdef USE_LIBWRAP

#include <tcpd.h>

int allow_severity=LOG_NOTICE;

int deny_severity=LOG_WARNING;

#endif
```

在处理连接的函数中，在变量声明处包含以下内容：

```c
#ifdef USE_LIBWRAP

struct request_info request;

#endif
```

然后在建立连接后，在你进行任何操作之前，使用 TCP wrapper 库的 `hosts_access` 函数来判断你是否应该处理该连接或是否应该立即拒绝：

```c
#ifdef USE_LIBWRAP

request_init(&request, RQ_DAEMON.servername, RQ_FILE, local, 0);

fromhost(&request);

if (!hosts_access(&request)) {

    log(LOG_WARNING, "Connection from %s REFUSED by libwrap",

    inet_ntoa(addr.sin_addr), ntohs(addr.sin_port));

    log(LOG_DEBUG, "See hosts_access(5) for details");

    goto clean_local;

}

#endif
```

> 注意：你的代码可能与示例略有不同。也许你以不同的方式记录警告和调试语句。或者你订阅了需要避免的细节。

## 糟糕规则的滥用

| | |
| :--- | :--- |
| 流行度 | 4 |
| 简单性 | 6 |
| 影响 | 8 |
| 风险评分 | 7 |

你已经实现了 TCP wrappers 并向 `/etc/hosts.allow` 和 `/etc/hosts.deny` 添加了规则，但 TCP wrappers 似乎不起作用。TCP wrappers 无法正确拒绝访问通常由于其中一个文件的拼写错误。

## 检查 TCP Wrapper 规则有效性

`tcpchk` 和 `tcpmatch` 程序是验证 `/inetd.conf`、`/etc/hosts.allow` 和 `/etc/hosts.deny` 中定义的 TCP 规则的工具。

```
tcpchk [-a] [-d] [-i]
```
