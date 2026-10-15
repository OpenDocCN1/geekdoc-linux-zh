
`-rw-rw-rw-    1 root    sys      21507 Dec  7 07:20 ./opt/perf/status.rep.server`

`-rw-rw-rw-    1 root    sys      24570 Dec  7 07:20 /opt/perf/status.alertmen`

`-rw-rw-rw-    1 root    sys      160956 Dec  6 21:13 /opt/cmi1/log/inet.log`

`-rw-rw-rw-    1 root    sys      158796 Dec  7 07:17 .sam/log/samlog`

`-rw-rw-rw-    1 root    root        64730 Dec  7 07:17 .sam/boot.config`

`-rw-rw-rw-    1 root    sys       11906 Nov 24 14:27 .sam/poe.iout`

`-rw-rw-rw-    1 root    sys       11906 Nov 23 09:10 .sam/poe.iout.old`

`-rw-rw-rw-    1 root    sys           29 Nov 24 14:27 .sam/poe.dion`

你可以看到，该文件包含由空格分隔的几个字段。下一个示例评估第三个字段，以确定其是否等于 `"adm"`，如果是，则打印该行：

```
# awk '$3 == "adm" {print}' newfiles
-rw-rw-rw-    1 adm     adm      2750700 Dec  7 13:52 ./adm/wtmp
```

第三字段中恰好包含 `"adm"` 的只有一行。

下一个示例评估第三个字段，以确定其是否大致等于 `"adm"`，即第三个字段中包含嵌入的 `"adm"`，如果是，则打印该行：

```
# awk '$3 ~ "adm" {print}' newfiles
-rw-mw-rw-    1 adm     adm      2750700 Dec  7 13:52 ./adm/wtmp
-rw-------    1 sysadm  psoft          60 Dec  1 16:59 ./tmp/EAAa09057
```

此结果打印了上一个示例中的行（其第三个字段包含 `"adm"`），以及包含 `"sysadm"` 的一行。

下一个示例执行与上一个示例相同的搜索；不过，这次只打印第九个和第五个字段：

```
# awk '$3 ~ "adm" {print $9, $5}' newfiles
./adm/wtmp 2750700
./tmp/EAAa09057 60
```

这次只打印了文件名（第九个字段）和文件大小。

下一个示例评估第三个字段，以确定其是否不等于 `"root"`，如果是，则打印整行：

```
# awk '$3 != "root" {print}' newfiles
PROG>>> report of files not older than 14 days by find
the file system is /
-rw-rw-rw- 1 bin bin 8553 Dec 7 07:02 ./etc/shutdownlog
-rw-rw-rw- 1 autosys autosys 4052 Nov 25 14:08 /home/autosys/.sh history
-rw-rw-rw- 1 tsaxs users 2228 Dec 1 13:15 /home/tsaxs/.sh history
-rw-rw-rw- 1 tsfxo users 2862 Nov 24 10:08 /home/tsfxo/.sh history
PROG>>> report of files not older than 14 days by find
the file system is /usr
-rw-rw-rw- 1 oppof users 21 Dec 7 13:46 ./local/adm/etc/lmonitor.hst
-rw-rw-rw- 1 tsgjf users 1093 Dec 7 13:17
./local/flexim/licenses/license.log
PROG>>> report of files not older than 14 days by find
the file system is /opt
-rw-rw-rw- 1 bin bin 200 Dec 7 07:17 ./pred/bin/OPSDBFF
PROG>>> report of files not older than 14 days by find
the file system is /var
-rw-rw-rw- 1 adm 2750700 Dec 7 13:52 ./adm/wtmp
-rw-rw-rw- 1 lp lp 33 Dec 7 07:17 ./adm/lp/log
-rw-rw-rw- 1 lp lp 67 Dec 7 07:01 ./adm/lp/oldlog
-rw------- 1 sysadm psoft 60 Dec 1 16:59 /tmp/EAa09057
-rw-rw-rw- 1 tsgjf users 0 Dec 7 13:17 ./tmp/lpCHPCULPANGS
-rw-rw-rw- 1 tsgjf users 175 Dec 7 06:40 ./tmp.flexim/lmgrd.1507
-rw-rw-rw- 1 tsgjf users 175 Dec 7 13:28 ./tmp.flexim/lmgrd.1505
-rw-rw-rw- 1 lp lp 0 Dec 7 07:17 ./spool/lp/output
-rw-rw-rw- 1 lp lp 4 Dec 7 07:17 ./spool/lp/SCHEDLOCK
```

该命令的结果是打印了许多第三字段不包含 `"root"` 的行。

`newfiles` 使用空格来分隔字段。在 UNIX 世界中，我们并不经常享有这种便利。接下来的示例使用 `passwd.test`，它以冒号 `:` 作为字段分隔符。`passwd.test` 显示如下：

```
# cat passwd.test
root:PgYQCKVH65hyQ:0:0:root::/root:/bin/bash
bin::1:1:bin::/bin:
daemon::*:2:2:daemon::/sbin:
adm::*:3:4:adm::/var/adm:
lp::*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync::/bin:/bin/sync
shutdown:*:6:11:shutdown::/sbin:/sbin/shutdown
halt::17:0:halt::/sbin:/sbin/halt
mail::*:8:12:mail::/var/spool/mail:
news::*:9:13:news::/var/spool/news:
uucp::*:10:14:uucp:/var/spool/uucp:
operator:*:11:0:operator::/root:
games::*:12:100:games::/usr/games:
gopher::*:13:30:gopher::/usr/lib/gopher-data:
ftp::14:50:FTP User::/home/ftp:
man::*:15:15:Manuals Owner::/
nobody::*:65534:65534:Nobody::/:/bin/false
col:WHOyZFAYV2qm2Y:100:100:Caldera OpenLinux User::/home/col::/bin/bash
```

你可以使用 `-F` 选项后跟一个分隔符来指定字段分隔符，在 `passwd.test` 中该分隔符是冒号 `:`。以下示例指定了字段分隔符，然后评估第一个字段以判断其是否等于 `"root"`，如果相等，则打印整行：

![](img/75f39fc91296b889c0653851accdfd46_637_0.png)

```
# awk -F: '$1 == "root" {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
```

以下示例指定了字段分隔符，然后评估第四个字段以判断其是否等于 `"0"`，这意味着该用户属于与 root 相同的组；如果相等，则打印整行：

```
# awk -F: '$4 == "0" {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
sync:*:5:0:sync:/sbin/bin/sync
halt:*:7:0:halt:/sbin/sbin/halt
operator:*:11:0:operator:/root:
```
