
`BIND 8` `controls` 语句定义了 `rndc` 使用的控制通道。`rndc` 可以使用 `Unix socket` 或网络 `socket` 作为控制通道。`controls` 语句定义了这些 `socket`。`BIND 8` `controls` 语句见列表 B.12。

### 列表 B.12: `BIND 8` `controls` 语句语法

```
controls {
  inet ip_addr
  port ip_port
  allow { address_match_list };
  unix pathname
  perm file_permissions
  owner uid
  group gid;
};
```

前三个选项（`inet`, `port` 和 `allow`）定义了网络 `socket` 的 `IP` 地址、端口号以及允许通过该通道进行控制的系统访问控制列表。由于 `BIND 8` 的认证机制较弱，创建一个可以从网络访问的控制通道是一项冒险操作。任何获得该通道访问权限都可以控制命名服务器进程。

最后四个选项（`unix`, `perm`, `owner` 和 `group`）定义了 `Unix socket`。`Unix socket` 以文件形式出现在文件系统中。它通过普通文件路径进行标识（例如 `/var/run/rndc`）。与任何文件一样，`unix socket` 分配了其所有者的 `uid` 和组 `ID` (`gid`)。它受标准文件权限保护。`file_permissions` 值必须以 `0` 开头。例如，要设置读写、组读和无其他权限，数值值应为 `0640`。

大多数 `BIND 8` 配置不包含 `controls` 语句，因为默认配置不需要更改。`rndc` 无法在网络上安全地使用，因此未使用 `inet`、`port` 和 `allow` 选项来配置网络 `socket`。`rndc` 在对 `UNIX socket` 进行任何修改的情况下在本地工作。对于 `BIND 8`，默认配置就是所有需要的。

`BIND 9` `controls` 语句定义了 `rndc` 使用的控制通道。`rndc` 执行的功能与旧的 `ndc` 程序相同，但可以在网络上可靠地使用。`BIND 9` `controls` 语句见列表 B.13。

### 列表 B.13: `The BIND 9 controls` 语句语法

```
controls {
  inet ip_addr|*
  port ip_port
};
```

```bind
allow address_match_list {
  keys key_list; 
}
```

`inet`、`port` 和 `allow` 选项在定义 `BIND 9` 网络套字时执行的功能与 `BIND 8` 相同，但现在它们是真正有用的，因为 `rndc` 可以可靠地通过网络套字运行。除了这些选项外，`BIND 9` 还增加了一个 `keys` 选项，用于定义为 `rndc` 客户端和服务器提供强认证的加密密钥。

在 `BIND 9` 中，`controls` 语句定义了一个网络 `socket`。它没有定义 `Unix socket` 的选项。即使 `rndc` 是从名称服务器控制台本地运行的，也会使用网络 `socket`。请参第 4 章有关在服务器上本地运行 `rndc` 所需的 `controls` 语句示例。

## `BIND 9 View` 语句

`view` 语句允许不同的客户端以不同的方式查看同一个区域。这使得为组织内部客户端提供内部视图，并为外部客户端提供更受限的视图成为可能。`view` 命令的语法所示列表 B.14。

### 列表 B.14: `view` 语句语法

```bind
view-name {
  match-clients { address_match_list };
  view-option; ...
  zone-statement; ...
};
```

- `view-name`: 配置内部用于用于标识此视图的任意名称。为了防止与关键字冲突，`view-name` 应该包含在引号中，例如 `"internal"`。

- `match-clients`: 定义通过此视图访问区域的客户端列表。

- `view-option`: 任何标准的 `BIND 9` 选项。在 `view` 语句内部定义的任何选项仅适用于此视图。这允许根据所使用的区域视图，对同一区域应用不同的选项。

- `zone-statement`: 标准的 `BIND 9` 区域语句。一个完整的区域语句嵌入在 `view` 语句内部，以定义通过此视图访问的区域。

`view` 语句仅在 `BIND 9` 中可用。`BIND 8` 不支持视图（`views`）。

## 附录 C：`sendmail` 的 `m4` 宏

### 概述

本附录是用于可能构建 `sendmail` 配置文件的 `m4` 宏的快速参考指南。（有关如何使用 `m4` 宏的教程，请参阅第 5 章“配置邮件服务器”。）本附录描述了宏的语法和功能；信息截至发布日期是准确的。有关宏的最新、准确描述，请参阅随 `sendmail` 发行版提供的文档以及 `sendmail/cf` 目录下的 `README`。

注意：在 `Red Hat` 系统上，`sendmail/cf` 目录为 `/usr/share/sendmail-cf`。为了保持“发行版中立”，本附录引用 `sendmail/cf` 目录，但目录的实际位置取决于 `Linux` 发行版。

表 C.1 列出了 `sendmail m4` 宏，以及常见于 `sendmail` 配置的内置 `m4` 命令。在表表中，属于 `m4` 语言的命令以小写形式显示，而专门为 `sendmail` 开发的宏以大写显示。

### 表 C.1：`sendmail m4` 宏

| 命令 | 用法 |
| --- | --- |
| `CANONIFY_DOMAIN` | 列出应转换为规范名称格式的域名，即使选择了 `nocanonify` 特性。 |
| `CANONIFY_DOMAIN_FILE` | 标识一个文件，该文件列出了应转换为规范名称格式的域名，即使选择了 `nocanonify` 特性。 |
| `DAEMON_OPTIONS` | 为 `sendmail` 守护进程定义运行时选项。 |
| `define` | 为配置变量定义值。 |
| `divert` | 重定向 `m4` 进程的输出。 |
| `dnl` | 删除直到换行符（包括在）的所有字符。 |
| `DOMAIN` | 选择一个包含你特定域名属性的文件。 |
| `EXPOSED_USER` | 列出应跳过伪装的用户名。 |
| `FEATURE` | 标识包含在配置中的可选功能。 |
| `GENERICS_DOMAIN` | 列出应转换为通用名称格式的域名。 |
| `GENERICS_DOMAIN_FILE` | 标识一个文件，该文件列出了应转换为通用名称格式的域名。 |
| `HACKS` | 选择一个包含临时修复的文件。 |
| `INPUT_MAIL_FILTER` | 定义调用过滤器的变量。 |
| `LDAPROUTE_DOMAIN` | 根据 `LDAP` 目录路由的域名。 |
| `LDAPROUTE_DOMAIN_FILE` | 标识一个文件，该文件根据 `LDAP` 目录项路由。 |
| `LOCAL_DOMAIN` | 标记包含原始 `sendmail` 命令的语句开始。 |
| `LOCAL_CONFIG` | 定义邮件服务器的别机名。 |
| `LOCAL_NET_CONFIG` | 标记定义如何处理本地网络邮件的重写规则的开始。 |
| `LOCAL_RULE_n` | 标记重写规则部分。`n` 必须是 `0`、`1`、`2` 或 `3`，标识要添加的规则集。 |
| `LOCAL_RULESETS` | 标记要添加到配置中的规则集的开始。 |
| `LOCAL_USER` | 在转发本地邮件时应跳过的用户名列表。 |
| `MAIL_FILTER` | 标识包含在 `sendmail.cf` 中的一组过滤器。 |
| `MAILER_DEFINITIONS` | 标记包含原始 `sendmail` 命令的语句开始。 |
| `MASQUERADE_AS_DOMAIN` | 用于伪装外发邮件的域名。 |
| `MASQUERADE_DOMAIN_FILE` | 标识一个文件，该文件列出了应伪装的域名。 |
| `MASQUERADE_EXCEPTION` | 定义不伪装的主机。 |
| `MODIFY_MAILER_FLAGS` | 覆盖为邮件定义的标志。 |
| `OSTYPE` | 选择包含系统特定属性的文件。 |
| `RELAY_DOMAIN` | 定义应转发的域名。 |
| `RELAY_DOMAIN_FILE` | 标识一个文件，该文件列出了应转发的域名。 |
| `SITE` | 标识一个本地连接的 `UUCP` 主机。 |
| `SITECONFIG` | 标识列出所有本地连接 `UUCP` 站点的文件。 |
| `TRUST_AUTH_MECH` | 定义一组可信的认证机制。 |
| `undefine` | 清除为配置变量设置的值。 |
| `UUCPSMP` | 定义一组可信的认证机制。 |
| `VERSION` | 定义版本信息。 |

宏名称以美元符号 (`$`) 开头，类名以美元符号和等号 (`$`) 开头，选项以长选项名称（`SingleThreadDelivery`）表示。
