

# kinit

# 563

在指定的有效期之后，你必须再次运行 kinit 来刷新票据。kinit 会销毁缓存中的任何现有内容。在结束登录会话之前，可以使用 kdestroy(1) 命令销毁任何活跃的票据。

## 配置文件

你必须通过对 /etc/krb5/krb5.conf 文件进行适当修改，在你计划计划运行 kinit 的 Kerberos 客户端的系统上进行配置。默认的 krb5.conf 文件所示。

```
#
#pragma ident "(@)krb5.conf 1.2 99/07/20 SMI"
# Copyright (c) 1999, by Sun Microsystems, Inc.
# All rights reserved.
#
#krb5.conf template
# 为了完成此配置文件的
# 你将需要将 __name>__ 占位符替换
# 为适用于你网络的适当值。
#
[libdefaults]
  default_realm = __default_realm__

[realms]
  default_realm = (
    kdc = master_kdc_
    _slave_kdc_
    admin_server = master_kdc_
  )

[domain_realm]
  domain_mapping_

[logging]
  default = FILE:/var/krb5/kdc.log
  kdc = FILE:/var/krb5/kdc.log
krotate = {
# 多久滚动一次 kdc.log。日志滚动频率会比
# 该周期更频繁，如果 KDC 不被频繁使用
# 则频率更低。

  period = 1d

# 保留多少版本的 kdc.log (kdc.log.0, kdc.log.1, ...)

  versions = 10

[appdefaults]
  kinit = {
    renewable = true
```

# 564

# kinit

forwardable= true

```
)
gkadmin = {
  help_url = http://docs.sun.com:80/ab2/coll.384.1/SEAM/@AB2PageView/1195
}
```

以下示例显示了为 gmarler.domain 配置的文件。

- * Kerberos 5 客户端的配置文件
- 该客户端位于 gmarler.com DNS 域，且 Kerberos 5 域
- 以 DNS 域命名
- 因此，客户端的默认 Kerberos 域是 GMARLER.COM
[libdefaults/]

```
default_realm = GMARLER.COM
```

- * 对于 GMARLER.COM 域，我们有一个主和次要密钥
- 分发中心 (KDC): kdc.gmarler.com 和 kdc2.gmarler.com
- kdc.gmarler.com 同时兼任 Kerberos 管理服务器
[realms]

```
GMARLER.COM = {
  kdc = kdc.gmarler.com
  kdc = kdc2.gmarler.com
  admin_server = kdc.gmarler.com
}
```

- * 此节将 .gmarler.com DNS 域中的任何主机映射到
- GMARLER.COM Kerberos 域
[domain_realm]

.gmarler.com = GMARLER.COM

- * 此节为感知 Kerberos 的应用程序定义了默认值：请参阅有关 Kerberos
- 的 Sun 在蓝图：http://www.sun.com/blueprints/online.html
[appdefaults]

```
gkadmin = {
  help_url = http://localhost:8888/ab2/coll.384.2/SEAM
```

```
kinit = {
  renewable = true
  forwardable= true
  proxiable = false
}
```

```
rlogin = {
  renewable = true
  forwardable= true
  encrypt = true
}
```

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

# 选项

- -c cache_name 使用 cache_name 作为凭证（票据）缓存名称和位置。如果你不指定此选项，kinit 将使用默认的缓存名称和位置。
- -f 请求可转发的票据。
- -k [-t keytab_file] 请求从本地主机 keytab 文件中的密钥获取主机。你可以使用 -t keytab_file 选项指定 keytab 文件的名称和位置。否则，kinit 将使用默认名称和位置。

- -1 lifetime 请求一个具有寿命 有期的票据。如果你不指定 -1 选项，将使用默认票据有效期（由每个站点配置）。指定比每个站点配置的最大有效期更长的票据有效期将导致获得最大有效期的票据。参见第 566 页的“时间格式”，了解你可以为有效期指定的有效时间持续格式。

- -p 请求可代理的票据。

- -r renewable_life 请求总有效期为 renewable_life 的可续期票据。参见第 566 页的“时间格式”，了解你可以为 renewable_life 指定有效时间持续格式。
- -R 请求刷新票据授予票据 (TGT)。请注意，即使票据仍在可续期范围内，你也无法刷新已过期的票据。

- -s start_time 请求从 start_time 开始有效的后期票据。后期票据发行时设置了无效标记，并且在此之前回传给 KDC。参见第 566 页的“时间格式”，了解你可以为 start_time 指定有效绝对时间或时间持续格式。kinit 会在尝试匹配时间持续时间之前尝试匹配绝对时间。

# 566 kinit

- -S service_name
在获取初始票据时指定一个备用服务名称。

- -v
请求将缓存中的票据授予票据（带有无效标记）传递给 KDC 进行验证。如果票据在请求的时间范围内，则缓存将被通过验证的票据替换。

新时间格式
以下绝对时间格式可用于 -s start_time 选项。示例基于 2002 年 7 月 2 日下午 1:35:30 的日期时间。

| 绝对时间格式 | 示例 |
|---|---|
| ymmddhh[:ss] | 020702133530 |
| hhmm[:ss] | 133530 |
| yy:mm:dd:hh:mm:ss | 02:07:02:13:35:30 |
| hh:mm[:ss] | 13:35:30 |
| ldate:ltime | 07-07-99:13:35:30 |
| dd-month-yyyy:hh[:ss] | 02-july-2002:13:35:30 |

| 变量 | 说明 |
|---|---|
| dd | 日。 |
| hh | 小时（24小时制）。 |
| mm | 分钟。 |
| ss | 秒。 |
| yy | 世纪内的年份（0-68 是 2000 年到 2068 年；69-99 是 1969 年到 1999 年） |
| yyyy | 包含世纪的年份。 |
| month | 区域设置的全称。 |
| ldate | 区域的日期表示。 |
| ltime | 区域设置的时间表示。 |

| 时间格式 | 示例 |
|---|---|
| d | 14d |
| h | 7h |
| m | 5m |

# 596 kinit

| 时间格式 | 示例 |
|---|---|
| s | 30s |
| d | 14d |
| h | 7h |
| m | 5m |


