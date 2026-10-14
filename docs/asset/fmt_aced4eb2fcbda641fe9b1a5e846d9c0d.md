
```
rsh = {
  renewable = true
  forwardable= true
  encrypt = true
}
```

```
rcp = {
```

# kinit 565

```
) encrypt = true
telnet = (
  autlogin = true
  renewable = true
  forwardable=
)
login = (
krb5_get_tickets = true
)
```

### 选项

- `-c cache_name` 使用 `cache_name` 作为凭证（票据）缓存名称和位置。如果你不指定此选项，`kinit` 将使用默认的缓存名称和位置。
- `-f` 请求可转发的票据。
- `-k [-t keytab_file]` 请求从本地主机 `keytab` 文件中的密钥获取主机。你可以使用 `-t keytab_file` 选项指定 `keytab` 文件的名称和位置。否则，`kinit` 将使用默认名称和位置。
- `-1 lifetime` 请求一个具有寿命 有期的票据。如果你不指定 `-1` 选项，将使用默认票据有效期（由每个站点配置）。指定比每个站点配置的最大有效期更长的票据有效期将导致获得最大有效期的票据。参见第 566 页的“时间格式”，了解你可以为有效期指定的有效时间持续格式。
- `-p` 请求可代理的票据。
- `-r renewable_life` 请求总有效期为 `renewable_life` 的可续期票据。参见第 566 页的“时间格式”，了解你可以为 `renewable_life` 指定有效时间持续格式。
- `-R` 请求刷新票据授予票据 (TGT)。请注意，即使票据仍在可续期范围内，你也无法刷新已过期的票据。
- `-s start_time` 请求从 `start_time` 开始有效的后期票据。后期票据发行时设置了无效标记，并且在此之前回传给 KDC。参见第 566 页的“时间格式”，了解你可以为 `start_time` 指定有效绝对时间或时间持续格式。`kinit` 会在尝试匹配时间持续时间之前尝试匹配绝对时间。

# 566 kinit

- `-S service_name`

在获取初始票据时指定一个备用服务名称。

- `-v`

请求将缓存中的票据授予票据（带有无效标记）传递给 KDC 进行验证。如果票据在请求的时间范围内，则缓存将被通过验证的票据替换。

### 新时间格式

以下绝对时间格式可用于 `-s start_time` 选项。示例基于 2002 年 7 月 2 日下午 1:35:30 的日期时间。

| 绝对时间格式 | 示例 |
|---|---|
| `ymmddhh[:ss]` | 020702133530 |
| `hhmm[:ss]` | 133530 |
| `yy:mm:dd:hh:mm:ss` | 02:07:02:13:35:30 |
| `hh:mm[:ss]` | 13:35:30 |
| `ldate:ltime` | 07-07-99:13:35:30 |
| `dd-month-yyyy:hh[:ss]` | 02-july-2002:13:35:30 |

| 变量 | 说明 |
|---|---|
| `dd` | 日。 |
| `hh` | 小时（24小时制）。 |
| `mm` | 分钟。 |
| `ss` | 秒。 |
| `yy` | 世纪内的年份（0-68 是 2000 年到 2068 年；69-99 是 1969 年到 1999 年） |
| `yyyy` | 包含世纪的年份。 |
| `month` | 区域设置的全称。 |
| `ldate` | 区域的日期表示。 |
| `ltime` | 区域设置的时间表示。 |

| 时间格式 | 示例 |
|---|---|
| `d` | 14d |
| `h` | 7h |
| `m` | 5m |

# 596 kinit

| 时间格式 | 示例 |
|---|---|
| `s` | 30s |
| `d` | 14d |
| `h` | 7h |
| `m` | 5m |

## 570

- `-s` 静默运行（产生输出），但仍会根据是否找到凭据缓存来设置退出状态。如果 `klist` 找到凭据缓存，则退出状态为 0，否则为 1。
- `-t` 显示 `keytab` 文件中每个 `keytab` 条目的持续时间戳。

### 示例

以下示例列出了用户 `ray` 的 Kerberos 票据。

`castle@ klist`

Ticket file: `/tmp/tkt8765`

Principal: `ray@Castle.Ab.COM`

| 发行时间 | 过期时间 | 主体 |
| --- | --- | --- |
| 10月10日 15:15:56 | 10月10日:16:15:56 | `krbtgt.Castle.Ab.COM@Castle.Ab` |

调用 `klist` 显示了主体 `gmarler/admin` 会话密钥的加密类型。

```
$ klist -e
Ticket cache: /tmp/krb5cc_1067
Default principal: gmarler/admin@GMARLER.COM
```

有效 起始时间 过期时间 服务 主体

Tue Feb 26 08:11:44 2002 Tue Feb 26 16:11:44 2002

krbtgt/GMARLER.COM@GMARLER.COM

new until Tue Mar 05 08:11:44 2002, Etype (skey, tkt):

DES-CBC-MD5, DES-CBC-CRC

$

调用 `klist` 显示了与主体 `gmarler/admin` 凭据相关的标志。

```
$ klist -f
Ticket cache: /tmp/krb5cc_1067
Default principal: gmarler/admin@GMARLER.COM
```

有效 起始时间 过期时间 服务 主体

Tue Feb 26 08:11:44 2002 Tue Feb 26 16:11:44 2002

krbtgt/GMARLER.COM@GMARLER.COM

renew until Tue Mar 05 08:11:44 2002, Flags: FRI

$

标志为 FRI，意味着这些凭据是可转发的（Forwardable）、可刷新的（Renewable），并且是该主体的初始（Initial）凭据。

## 环境变量

`KRB5CCNAME` 凭据（票据）缓存的位置。

## 文件

- `/etc/krb5/krb5.keytab`

本地主机 `keytab` 文件的默认位置。

- `/etc/krb5/krb5.conf`

Kerberos 配置文件。

- `/tmp/krb5cc_uid`

默认凭据缓存（`uid` 是用户的十进制 UID）。

### 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWcu |

## 参见

`kddestroy(1)`, `kinit(1)`, `attributes(5)`, `SEAM(5)`

# kpasswd — 修改用户的 Kerberos 密码

### 概要

`/usr/bin/kpasswd [principal]`

### 描述

使用 Solaris 8 操作系统环境中新出的 `kpasswd` 命令，`kpasswd` 会提示输入当前的 Kerberos 密码，该密码用于从 KDC 获取该用户 Kerberos 域的更改票据。如果 `kpasswd` 成功获取更改票据，用户将被提示两次输入新密码，并进行更改。

如果密码受指定新密码所需的长度和/或字符类数量的策略限制，则新密码必须符合该策略（五个字符类为：小写、大写、标点符号和其他所有）。

> 注意：本地机器必须安装 Kerberos 隐私支持，因为 `kpasswd` 需要在本地机器上安装带有隐私支持的 Kerberos GSS 插件模块。目前该模块仅在 Solaris 加密套件 CD 中可用（出于加密目的，DES 有导入/导出限制）。此支持由 `SUNW5pk` 和 `SUNW5ku` 包提供。

## 572

# kpasswd

# 缺陷

如果 `kpasswd` 被挂起，更改票据可能不会被销毁。

### 操作数

`principal`

更改 Kerberos 主体 `principal` 的密码。

否则，主体将从调用 `kpasswd` 命令的用户身份派生。

### 示例

在以下示例中，用户 `gmarler` 想要更改其拥有的 `gmarler/admin` 主体的密码。

```
$ kpasswd gmarler/admin
kpasswd: Changing password for gmarler/admin.
Old password: <enter original principal's password>
New password: <enter new password for this principal only>
New password (again): <repeat>
Kerberos password changed.
$
```

此命令仅更改 Kerberos 主体的密码，而不更改用户的密码。
