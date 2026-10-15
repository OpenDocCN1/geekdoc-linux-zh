
```bash
matthew@seymour~:$ sudo ufw enable
```

```bash
matthew@seymour~:$ sudo ufw logging on
```

```bash
matthew@seymour~\$ sudo ufw allow 80
```

```bash
matthew@seymour:-$ sudo ufw delete allow 80
```

```bash
matthew@seymour~:$ sudo ufw allow ssh
```

```bash
matthew@seymour~$ sudo ufw allow from 192.168.0.1
```

```bash
matthew@seymour~$ sudo ufw delete allow from 192.168.0.1
```

```text
# 最后修改时间：2011年9月25日 08:58:35

#include <tunables/global>

# 如果 syslog无法写入内核记录拒绝操作的文件，那么

# 调试 syslog可能会变得困难。在这种情况下，你可以执行

# 以下操作：watch -n 1

`dmesg` | tail-5

/usr/bin/rsyslog { #include <abstractions/base> #include <abstractions/
nameservice

    capability sys_tty_config, capability dac_override, capability dac_read_search,
    capability setuid, capability setgid, capability sys_nice, capability syslog,

# rsyslog 配置 /etc/rsyslog.conf r, /etc/rsyslog.d/ r, /etc/
rsyslog/** r, /(var,)/run/rsyslog.pid rwk, /var/spool/rsyslog/ r, /var/spool/
rsyslog/** rw.

/usr/lib/(32,64)/rsyslog/*.so mr, @{PROC)/

/dev/tty* r, /dev/xconsole rw,

ksmag

/dev/log r, /var/lib/*/dev/log wl, /var/spool/
postfix/dev/log wl,

# 使用 infile /var/log** 时需要 'r'

# 为支持 mysql 添加这些内容 
#/etc/mysql/my.cnf r, #/(var,)/run/mysqld/mysqld.
sock rw,

# 为支持 postgresql 添加这些内容 ##include <abstractions/openssl> #include
<abstractions/ssl_certs> #/(var,)/run/postgresql/.s.PGSQL.*[0-9] rw,

# 站点特定的添加和覆盖。详情参见 local/README。
#include<local>/usr/sbin.rsyslog>

- r - 
- w - 写
- ux - 无限制执行
- Ux - 环境无限制执行
- px - 离散配置文件执行
- Px - 环境离散配置文件执行执行
- ix - 继承执行
- m - 允许 PROT_EXEC 调用 mmap(2)
- l - 链接
```

```bash
matthew@seymour~:$ sudo genprof google-chrome
```

```bash
start:
matthew@seymour~ sudo service apparmor

stop:
matthew@seymour~ sudo service apparmor

reload:
matthew@seymour~ sudo service apparmor (or restart)

show status:
matthew@seymour~ sudo service apparmor
```

```bash
matthew@seymour~~$ apparmor device
```

```bash
matthew@seymour~~$ apparmor -t /dev/sda
```

```bash
matthew@seymour~~$ apparmor -m -l /dev/sda
```

```bash
matthew@seymour~~$ apparmor -m -l /dev/sda
```

```bash
matthew@seymour~~$ apparmor -t device
```

```bash
matthew@seymour~~$ sync
```

```bash
matthew@seymour~~$ chattr -R /path/to/directory
```

```bash
matthew@seymour~~$ sysctl -a
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_rfc1337 = 0
net.ipv4.tcp_std = 0
net.ipv4.tcp_abort_on_overflow = 0
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_sync = 0
net.ipv4.tcp_fin_timeout = 60
net.ipv4.tcp_retries = 15
net.ipv4.tcp_retries = 3
net.ipv4.tcp_keepalive_intvl = 75
net.ipv4.tcp_keepalive_probes = 9
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.ipfrag_time = 30
```

```bash
matthew@seymour~~$ sysctl -w net.ipv4.tcp_retries=20
```

```bash
matthew@seymour~~(reads / requests) = 100
```

```sql
[mysqld]
key_buffer_size=16M
datadir=/var/lib/mysql
```

```sql
mysql> SHOW STATUS LIKE 'Qcache%';
+----------------------+
| Variable_name           | Value                |
+----------------------+
| Qcache_free_blocks      | 1                    |
| Qcache_free_memory     | 169544               |
| Qcache_hits            | 698                  |
| Qcache_inserts         | 38                   |
| Qcache_low_prunes      | 20                   |
| Qcache_not_cached      | 0                    |
| Qcache_queries_in_cache | 18                   |
| Qcache_total_blocks    | 57                   |
+----------------------+
8 rows in (0.00 sec)
```

```sql
query_cache_size=32M.
```

```bash
matthew@seymour~~$ sudo modprobe -t net
```

```text
alias char-major-89 i2c-dev
options eeprom ignore=2,0x50,2,0x51,2,0x52
```

```bash
matthew@seymour~~$ sudo lsmod | less
Module          Size Used by
parport_pc      19392 1
lp              8236 0
joydev          17377 0
parport         29640 2 parport_pc,lp
autofs4         10624 0
sunrpc          101064 1
```

```bash
matthew@seymour:-$ sudo rmmod joydev
```

```bash
matthew@seymour~ sudo modprobe -r joydev
```

```bash
matthew@seymour:~$ sudo modprobe joydev
```
