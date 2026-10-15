

## 表 7.5 /etc/security/user 中的用户账户选项（AIX）

| 选项 | 类型 | 含义 |
|---|---|---|
| account_locked | Boolean | 如果为 true 则阻止登录 |
| admin | Boolean | 如果为 true 则授予管理员权限 |
| auth1 | Method list | 主要身份验证方法 |
| auth2 | Method list | 次要身份验证方法 |
| dictionary | Filenames | 密码必须排除的词典 |
| expires | Date | 用户账户的到期日期 |
| histexpire | Weeks | 用户不能重用密码的周期 |
| histsize | Number | 不能重用的以前密码的数量 |
| login | Boolean | 可以登录吗？对于 bin 之类的登录很有用 |
| loginretries | Number | 账户被锁定前的登录尝试次数 |
| logintimes | Time range | 限制用户可以登录的时间 |
| maxexpired | Weeks | 过期密码的宽限期 |
| maxrepeats | Number | 密码中字符可以出现的次数 |
| minage, maxage | Weeks | 密码的最小和最大年龄 |
| minalpha | Number | 密码中字母字符的最小数量 |
| mindiff | Chars | 新密码中允许的旧密码字符数 |
| minlen | Number | 密码的最小长度（不要设为 0） |
| minother | Number | 密码中非字母字符的最小数量 |
| pwdchecks | Filenames | 调用以检查密码是否安全的函数 |
| pwdwarntime | Days | 提醒用户更改密码的宽限期 |
| rlogin | Boolean | 用户可以 rlogin 或 telnet 到此账户吗？ |
| su | Boolean | 其他用户可以 su 到此账户吗？ |
| ttys | Device list | 此用户可以登录的终端 |
| umask | Octal | 用户创建文件的默认权限 |

哇，好长的列表！文件中的注释通常会给出默认值，对于低安全性安装来说这些默认值相当合理。我们建议更改其中几项：

- 将 umask 从 022 改为 077。
- 将 loginretries 从 0（无限制）改为一个较小的整数，比如 5。
- 将 minlen 从 0（允许无密码）改为至少 6 或 7。
- 将 expires 从 0（永不过期）改为一年（仅当你有工具可以定期刷新有效用户的到期日期时）。

> 有关 PAM 的更多信息，请参阅第 908 页。

不幸的是，这只是控制新用户登录的配置文件之一。文件 /etc/security/login.cfg 包含用于控制错误登录的参数（在提示登录名和密码之前插入的延迟、禁用账户前的允许错误登录次数、禁用账户的时长、何时重新启用它等）、允许登录的时间、请求用户密码时打印的提示符、有效 shell 的列表、同时登录的最大允许数量、等待用户密码的时间长度、要使用的登录授权类型（如果要使用它，这里就是指定 PAM10 的地方），以及密码加密算法（默认为 crypt）。无限地，也许病态地，可配置。更令人困惑的是，一些参数同时出现在两个文件中，有时名称相同（例如 logintimes），有时名称不同（loginretries 与 loginisable）。哎呀！杂乱和复杂无处不在！

## useradd 在 AIX 上不提供 -D 选项来显示新用户的默认值。

它将新用户放入单个组中，并且除非使用 -m 标志调用，否则不会创建其主目录（在这种情况下，它还会从 /etc/security 目录复制一个 .profile 文件）。

## useradd 示例

要在 Linux 系统上使用系统默认值创建新用户 "hilbert"，你可以简单地运行

```
$ sudo useradd hilbert
```

此命令将在 /etc/passwd 中创建以下条目：

```
hilbert:x:1005:20::/home/hilbert:/bin/sh
```

## useradd 通过在密码字段中放置一个 x 来禁用账户。你必须分配一个真实密码才能使账户可用。

下面显示了一个更现实的示例。我们指定 hilbert 的主组应为 "faculty"，并且他还应被添加到 "famous" 组。我们覆盖默认的主目录位置和 shell，并要求 useradd 在不存在时创建主目录：

```
$ sudo useradd -c "David Hilbert" -d /home/math/hilbert -g faculty -G famous -m -s /bin/tcsh hilbert
```

此命令创建以下 passwd 条目：

```
hilbert:x:1005:30:David Hilbert:/home/math/hilbert:/bin/tcsh
```

分配的 UID 比系统上最高的 UID 高一个，对应的 shadow 条目为

```
hilbert:!:14322:0:99999:7:0::
```

passwd 和 shadow 文件中密码占位符字符因操作系统而异。useradd 还会将 hilbert 添加到 /etc/group 中的相应组，创建目录 /home/math/hilbert，并从 /etc/skel 目录填充它。

## 7.6 使用 NEWUSERS 批量添加用户（LINUX）

Linux 的 newusers 可以从文本文件的内容一次性创建多个账户。它功能比较简陋，但在需要添加大量用户时可能很方便

![](img/14d78e3cecac4581d37024baf1e94cca_245_0.png)

