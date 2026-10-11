

## 示例 5-21 /etc/security/access.conf 文件示例

```
# access.conf file
:-ALL:evil.com. spam.org
:-ALL EXCEPT root: tty1
:+ALL EXCEPT root:172.17.
:+wheel paul:leghorn
:-ALL:ALL
```

现在，只需将以下行

```
account required /lib/security/pam_access.so
```

按照需求添加到 /etc/pam.d 目录中的任意配置文件中。示例 5-22 展示了该条目在 /etc/pam.d/login 文件中的显示，其中新添加的部分以粗体显示。

## 示例 5-22 向 /etc/pam.d/login 文件添加 pam_access

| auth | required | /lib/security/pam_security.so |
| :--- | :--- | :--- |
| auth | required | /lib/security/pam_pwdb.so |
| auth | required | /lib/security/pam_nologin.so |
| account | required | /lib/security/pam_pwdb.so |
| **account** | **required** | **/lib/security/pam_access.so** |
| password | required | /lib/security/pam_cracklib.so minlen=20\* |
| password | required | retries=3 type=SECRET |
| password | required | /lib/security/pam_unix.so md5 use_authtok |
| session | required | /lib/security/pam_pwdb.so |

来自被拒绝位置的任何尝试访问都会导致权限拒绝错误信息，如示例 5-23 所示，其中 Paul 尝试在控制台登录。

## 示例 5-23 由于 pam_access 导致的登录失败尝试

```
pyramid login: paul
Password:
Permission denied
pyramid login:
```

所有因 pam_access 导致的失败尝试默认都记录在 /var/log/messages 中。有关日志文件的更多信息，请参阅第 8 章。

### 使用 pam_lastlog

该模块提供了显示上次登录时间信息以及“您有新邮件”信息的能力，分别作为模块类型 auth 和 session。前者比后者更为重要，因为它会泄露关于计算环境的信息。幸运的是，pam_lastlog 允许您控制显示的内容。

### 表 5.13 pam_lastlog 作为 auth 模块类型时的参数

| 参数 | 描述 |
| :--- | :--- |
| debug | 向 syslog 提供详细输出。 |
| nodate | 抑制显示该用户上次登录的日期。 |
| noterm | 抑制显示该用户上次登录时使用的终端名称。 |
| nohost | 抑制显示该用户上次登录的主机。利用此参数，您环境中的主机名将不会被披露。 |
| silent | 抑制整个 lastlog 消息。 |
| never | 如果用户以前从未登录过，这将导致显示欢迎消息。 |

用户登录。在此模式下，它接受表 5.13 中列出的参数。要使用此模块，只需在所有适当的 /etc/pam.d 配置文件中放入类似于以下行的记录（例如，login, rlogin, rsh）。

```
auth    optional    /lib/security/pam_lastlog.so nohost
```

注意 optional 控制标志。如果使用 required 代替，将没有人能够登录！您可能还希望将此行放在 auth 堆栈的最后。在此示例中，lastlog 消息将显示，但不会显示之前的主机信息。

作为 session 模块，pam_lastlog 告知用户关于电子邮件的信息。它不接受参数，并且同样必须使用 optional 控制标志。以下是一个示例条目：

```
session    optional    /lib/security/pam_lastlog.so
```

再次确认，此条目出现在每个适当的 /etc/pam.d 配置文件中。

> **注意**
> 
> 另一个应用程序可能在 PAM 认证步骤完成后显示 lastlog 或电子邮件信息。任何此类应用程序将使得配置 pam_lastlog 变得多余。

### 使用 pam_rhosts_auth

Berkeley r-命令的弊端在第 1 章中已有所阐述，其中我们检查了与这些工具相关的一些漏洞。在第 11 章中，我们将查看完全替换 Berkeley r-命令。

### 表 5.14 pam_rhosts_auth 的参数

| 参数 | 描述 |
| :--- | :--- |
| debug | 生成更多的 syslog 输出。 |
| no_hosts_equiv | 禁用 `/etc/hosts.equivalent` 功能。 |
| no_rhosts | 忽略 `~/.rhosts` 文件。 |
| no_warn | 抑制向用户发出的警告消息。截至本书撰写时，该模块本来就不生成任何警告消息！ |
| privategroup | 通常，如果 `~/.rhosts` 文件可被除所有者以外的其他人写入，该模块将假设文件已被破坏并返回失败。如果所有者的组是 UPG，此参数将允许 `~/.rhosts` 文件可被所有者和所有者的组写入。如果 UID 和 GID 相同且大于 500，则此条件为真。 |
| promiscuous | 该模块的默认行为是忽略 `~/.rhosts` 和 `/etc/hosts.equivalent` 文件中的 `*` 通配符。此参数将允许此类通配符。不建议使用此参数。参见第 3 章。 |
| suppress | 抑制向 syslog 发出的错误消息。 |

> 有关 UPG 的讨论，请参阅第 4 章第 69 页的**组账户管理**。

在这里，我们将查看如何使用 `pam_rhosts_auth` 来限制或完全消除受信任主机。

此模块仅为 auth 类型模块。它接受表 5.14 中列出的参数。此模块的配置高度依赖于特定系统和站点。在内部允许此功能可能是可接受的，并且在您的用户眼中也是必要的。在某些系统上，如受限服务器、边界网络内的系统和防火墙，如果不完全禁止，应严格管制 `~/.rhosts` 和 `/etc/hosts.equivalent` 文件。您可能希望将此模块的条目放在 `/etc/pam.d/rsh` 和 `/etc/pam.d/rlogind` 以及任何其他使用这些文件的 PAM 感知服务中。为了影响传统实现（允许受信任主机），使用如下的条目

```
auth sufficient /lib/security/pam_rhosts_auth.so
```

在 auth 堆栈的顶部（至少，此模块必须出现在堆栈中向用户提示输入密码的模块之前）的 `/etc/pam.conf` 中。

- 边界网络（或 DMZ）通常由可供外部访问的系统组成。有关进一步信息，请参阅第 16 章第 488 页的*通用防火墙参考*中列出的参考资料。

/etc/pam.d/rsh 和 /etc/pam.d/rlogin。在敏感系统上的这些相同文件中可以放置更严格的条目。例如，形式为

```
auth        required      /lib/security/pam_rhosts_auth.so     no_rhosts
```

在 auth 堆栈的顶部（或者，再次，在生成密码提示的模块之前）的条目将完全禁用 $HOME/.rhosts 文件的使用，但将保留 /etc/hosts.equiv 的使用（这不适用于 root）。

### 一次性密码支持

pam_opie 和 pam_skey 都支持 OTP。这些在第 6 章中进行了讨论。

### PAM 与其他配置文件

到目前为止，您已经讨论了离散的 PAM 感知应用程序以及如何通过 PAM 授予或限制对这些应用程序的访问。事实证明，如果 PAM 感知应用程序没有自己的配置文件，Linux-PAM 将从 /etc/pam.d/other 文件中提供一组特殊的模块。此文件通常用于拒绝所有其他请求，并且默认情况下可能如示例 5-24 所示。例如，如果您下载了一个 PAM 感知应用程序，如 ssh 1.2.27（参见第 11 章），并且未提供 /etc/pam.d 中的 ssh 配置文件，则使用 other 文件，如果它如示例 5-24 所示，则 ssh 连接将始终失败。此外，pam_deny 根本不生成任何消息！不幸的是，这意味着您可能会花大量时间试图弄清楚为什么某些东西不起作用。正如名称所示，pam_deny 所做的是拒绝任何可用模块类型的所有请求。

#### 示例 5-24 常见的 /etc/pam.d/other 文件

| auth | required | /lib/security/pam_deny.so |
| :--- | :--- | :--- |
| account | required | /lib/security/pam_deny.so |
| password | required | /lib/security/pam_deny.so |
| session | required | /lib/security/pam_deny.so |

但有个好消息！有另一个模块，即 pam_warn 模块，它向日志记录信息消息，包括请求的服务、终端名称、用户名、远程用户名和远程主机名。pam_warn 模块仅针对模块类型 auth 和 password 操作。因此，您可能希望如示例 5-25 那样修改您的 /etc/pam.d/other 文件。这样，所有其他发出 auth 或 password 请求的服务都将生成日志条目。pam_warn 模块不仅限于与 pam_deny 一起使用。它可以用于任何 auth 或 password 堆栈以生成额外的日志消息。

#### 示例 5-25 对管理员友好的 /etc/pam.d/other 文件

```
auth       required       /lib/security/pam_warn.so
auth       required       /lib/security/pam_deny.so
```

