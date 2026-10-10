
`dnl define(`LOCAL_MAILER_ARGS`, `procmail -a h -d $u`)\dnl`

`define(`STATUS_FILE`, `/var/log/sendmail.st`)\dnl`

> 注意：这些步骤仅在中央邮件枢纽配置需要。这将使 sendmail 使用 procgram 作为本地邮件传递代理，并定义状态文件 `sendmail.st` 位于 `/var/log` 目录下。

编辑 `linux.m4` 文件（`vi +16 /ostype/linux.m4`）并添加该行：

`define(`STATUS_FILE`, `/var/log/sendmail.st`)\dnl`

> 注意：这是本地服务器、客户端 sendmail 配置所需的步骤。它将定义状态文件 `sendmail.st` 位于 `/var/log` 目录下。

编辑 `header.m4` 文件（`vi +26 BuildTools/M4/header.m4`）并修改：

`define(`confLIBSEARCH`, `db bind resolv 44bsd`)\dnl`

修改为：

`define(`confLIBSEARCH`, `db1 bind resolv 44bsd`)\dnl`

此更改指定了安装在 Linux 上的 Berkeley 包。

编辑 `makemap.c` 文件（`vi +30 makemap/makemap.c`）并修改：

```c
# include <db.h>
```

修改为：

```c
# include <db_185.h>
```

编辑 `map.c` 文件（`vi +29 src/map.c`）并修改：

© Copyright 1999 Open Network Architecture ®

```c
# include <db.h>
```

修改为：
```c
# include <db_185.h>
```

编辑 `uds.c` 文件（`vi +28 src/uds.c`）并修改：

```c
# include <db.h>
```

修改为：
```c
# include <db_185.h>
```

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

`define(`OPTIMIZE`; `-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-family-pointer -fno-exceptions`)`
此选项定义了传递给 `CC` 的与特定 CPU 架构相关的优化标志。

`define(`LIBS`; `-lnsl`)`
此选项定义了传递给 `ld` 的 `-l` 标志。

`define(`LDOPTS`; `-s`)`
此选项定义了传递给 `ld` 的链接器选项。

`define(`MANOWN`; `root`)`
此选项定义了安装的手页（man pages）的所有者。

`define(`MANGRP`; `root`)`
此选项定义了安装的手页的所属组。

`define(`MANMODE`; `644`)`
此选项定义了安装的手页的模式。

`define(`MAN1SRC`; `1`)`
此选项定义了安装在 `confMAN1` 中的手页的源。

`define(`MAN5SRC`; `5`)`
此选项定义了安装在 `confMAN5` 中的手页的源。

`define(`MAN8SRC`; `8`)`
此选项定义了安装在 `confMAN8` 中的手页的源。

```
[root@$deep] cd /var/tmp/sendmail-version

[root@$deep] cd src

[root@$deep] sh Build -f ../Tools/siteconfig.m4

[root@$deep] cd

[root@$deep] cd mailalists

[root@$deep] sh Build -f ../Tools/siteconfig.m4

[root@$deep] cd

[root@$deep] cd makemap (Only for Mail Hub configuration)

[root@$deep] sh Build -f ../Tools/siteconfig.m4 (Only for Mail Hub configuration)

[root@$deep] cd praliliases (Only for Mail Hub configuration)

[root@$deep] sh Build -f ../Tools/siteconfig.m4 (Only for Mail Hub configuration)

[root@$deep] cd

[root@$deep] sh Build -f ../Tools/siteconfig.m4

[root@$deep] cd ..

```

注意：“`sh Build`” 脚本将创建新的目录
“`obj.yourOS,your.version,yourarchitecture`”，例如“`obj.Linux.2.2.13.i686`”
每个子目录程序可能会安装，然后在这些目录中创建指向
源文件和 Makefiles 的链接。

```
[root@$deep] make install -C obj.Linux.version.architecture

[root@$deep] make install -C mailalists/obj.Linux.version.architecture (Only for Mail Hub configuration)

[root@$deep] make install -C makemap/obj.Linux.version.architecture (Only for Mail Hub configuration)

[root@$deep] make install -C praliliases/obj.Linux.version.architecture (Only for Mail Hub configuration)

[root@$deep] make install -C smrs/obj.Linux.version.architecture

```

关于本页面的意见和建议请邮件至 `gmouriani@videotron.ca`

```
[root@debug#] ln -sf /usr/sbin/sendmail /usr/lib/sendmail

[root@debug#] strip /usr/sbin/mailmats

[root@debug#] strip /usr/sbin/makemap (Only for Mail Hub configuration)

[root@debug#] strip /usr/sbin/paliases (Only for Mail Hub configuration)

[root@debug#] strip /usr/sbin/smsh

[root@debug#] chown /usr/sbin/sendmail

[root@debug#] chown 0:0 /usr/sbin/mailmats

[root@debug#] chown 0:0 /usr/sbin/makemap (Only for Mail Hub configuration)

[root@debug#] chown 0:0 /usr/sbin/paliases (Only for Mail Hub configuration)

[root@debug#] chown 0:0 /usr/sbin/smsh

[root@debug#] chmod 515 /usr/sbin/smsh

[root@debug#] install -d -m755 /var/spool/mqueue

[root@debug#] mkdir root.mail /var/spool/mqueue

[root@debug#] mkdir etc/smsh

[root@debug#] mkdir etc/etc/mail (Only for Mail Hub configuration)
```
