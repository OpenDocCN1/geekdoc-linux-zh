
# 如果 syslogger 无法写入内核记录拒绝操作的文件，调试 syslogger 可能会变得困难。在这种情况下，你可以执行以下操作：

```
watch -n 1 'dmesg | tail -5'
```

`/usr/bin/rsyslog`

```
#include <abstractions/base>
#include <abstractions/nameservice>
```

`capability sys_tty_config`, `capability dac_override`, `capability dac_read_search`, `capability`, `setgid`, `capability sys_nice`, `capability syslog`,

## syslog 配置

`/etc/rsyslog.conf` `r`, `/etc/rsyslog.d/` `r`, `/etc/rsyslog.d/**` `r`,

`/var/run/rsyslog.pid` `rw`, `/var/pool/rsyslog/` `r`, `/var/pool/rsyslog/**` `rw`.

`/usr/lib/(32,64)/rsyslog/*.so.so`

`/dev/tty*` `r`, `/dev/xconsole` `rw`, `rw,[PROC]kmsg`

`/dev/log` `wl`, `/var/lib*//dev/log` `wl`, `/var/pool/post-fix/log` `wl`,

## 使用 infile 时需要 'r'

`/var/log/**` `rw`,

## 添加这些 mysql

`#etc/mysql/my.cnf` `r`, `/(var/run/mysqld/mysqld.sock` `rw`,

## 添加这些 postgresql

```
#include <abstractions/openssl>
#include <abstractions/ssl_cert*>
```

`/(var/run/postgresql/s.PGASQL.*[0-9]` `rw`

## 站点特有的添加和覆盖

详情请参见 `local/README`。
```
#include <local/usr/bin.rsyslog>
```
