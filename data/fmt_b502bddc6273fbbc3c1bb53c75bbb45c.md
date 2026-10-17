
# 为 `nsswitch.conf` 文件设置不可变位

`[root@deep] # cd /chroot/named/etc/`

`[root@deep] # chatter +nsswitch.conf`

带有 `"+i"` 属性的文件无法修改：它不能被删除或重命名，不能为此文件创建链接，无法向该文件写入数据。只有超级用户可以清除此属性。

## 步骤 3

告知 syslog chroot 环境：

通常，进程通过 `"dev/log"` 与 syslog 通信。由于 chroot 监狱的存在，这是不可能的，需要告知 syslog 指向 `"chroot/named/dev/log"`。要做到这一点，编辑 syslog 启动脚本以指定额外的位置：

编辑 syslog 行（`vi +24)/etc/rc.d/init.d/syslog`）来更改该行：

```
daemon syslog -m 0
daemon syslog -m 0 -a /chroot/named/dev/log
```

## 步骤 4

编辑 `named` 脚本（`vi /etc/rc.d/init.d/named`）来更改该行：

```
[-/usr/sbin/named] || exit 0
[-/chroot/named/usr/sbin/named ] || exit 0
[-/etc/named.conf] || exit 0
[-/chroot/named/etc/named.conf] || exit 0

daemon named
daemon/chroot/named/usr/sbin/named -t /chroot/named/ -g
```

- `-t` 告诉 `named` 启动新的 chroot 环境，
- `-u` 指定运行的用户，
- `-g` 指定运行的组。

Red Hat 的 init 脚本允许指定备用 PID 文件，这不会影响 `named` 的启动和停止操作，因为它们将在 chroot 外部调用。`BIND 8.2` 命令在此设置下无效。要修复它，必须从源码编译 `BIND`。如果你也映射新的 `named` 和 `named xfer`，应使用原始设置。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

要执行此，在 `BIND` 根目录下操作。

对于 `named`：

```
[root@deep]# cp bind-src.tar.gz /var/tmp
[root@deep]# cd /var/tmp/
[root@deep]# tar xpf bind-src.tar.gz
[root@deep]# cd src
[root@deep]# cp port/linux/Makefile.set port/linux/Makefile-orig
```

编辑 `Makefile.set`（`vi port/linux/Makefile.set`）进行以下更改：

```
-D_GNU_SOURCE
CDEBUG=-O9 -funroll-loops -ffast-math -multi-double -mcpu=pentium -march=pentium - 
omit-frame-pointer -no-exceptions
DESTIN=/usr/bin
DESTBIN=chroot/named/usr/sbin
DESTEXEC=chroot/named/usr/sbin
DESTMAN=/man
DESTHELP=/usr/lib
DESTETC=/etc
DESTRUN=/chroot/named/var/run
DESTLIB=/lib/bind/lib
DESTINC=/lib/bind/include/
LEX=flex -f
YACC=yacc -d
SYSLBS=-lff
INSTALL=make install
MANDIR=man
MANOFF=cat
CATEXT=$IN
AR=ar
RANLIB=-
```

我们之前使用的 `Makefile` 区别在于修改了 `DESTIN`、`DESTEXEC` 和 `DESTRUN` 行指向 `BIND` 的 chrooted 目录。通过此修改，`named` 程序现在知道哪里寻找 `"named"`。

```
[root@deep]# make clean
[root@deep]# make
[root@deep]# cp bin/named /chroot/named/usr/sbin/
[root@deep]# cp bin/named-xfer/xfer /chroot/named/usr/sbin/
[root@deep]# cp named-xfer /chroot/named/usr/sbin-named-xfer
[root@deep]# strip /chroot/named/usr/sbin/named
[root@deep]# strip /chroot/named/usr/sbin/named-xfer
```

我们编译二进制文件，将 `named` 的结果复制到 `"usr/sbin"` 并覆盖旧的。我们没有忘记 `strip` 我们新的 `"named"` 二进制文件以获得更好的性能。编译一个新的 `"named"` 二进制文件也是个好主意，确保 `named` 和 `named xfer` 使用相同的版本。

对于 `named`：

```
[root@deep]# cd /var/tmp/
[root@deep]# cp port/linux/Makefile.set-orig port/linux/Makefile.set
```

编辑 `Makefile.set`（`vi port/linux/Makefile.set`）进行列出的更改：

```
-D_GNU_SOURCE
```

© Copyright 1999 Open Network Architecture ® 209

```
CDEBUG=-O9 -funroll-loops -ffast-math -malign-double -mpu=pentiumpro -march=pentiumpro - 
omit-frame-pointer -no-exceptions
DESTBIN=/usr/bin
DESTBIN=/usr/sbin
DESTEXEC=/usr/sbin
DESTMAN=/man
DESTHELP=/usr/lib
DESTETC=/etc
DESTRUN=/var/run
DESTLIB=/lib/bind/lib
DESTINC=/lib/bind/include/
LEX=flex -f
YACC=yacc -d
SYSLBS=-lff
INSTALL=make install
MANDIR=man
MANOFF=cat
CATEXT=$IN
AR=ar
RANLIB=-
```

```
[root@deep]# rm -f
[root@deep]# make clean
[root@deep]# cp bin/named /chroot/named/usr/sbin
[root@deep]# cp bin/named-xfer/xfer /chroot/named/usr/sbin
[root@deep]# cp named-xfer /chroot/named/usr/sbin-named-xfer
[root@deep]# strip /chroot/named/usr/sbin/named
[root@deep]# strip /chroot/named/usr/sbin/named-xfer
```

我们移除了 `"settings"`，因为构建系统会缓存这些变量，并运行 `"make clean"` 命令以确保没有留下垃圾。在我们构建 `"named"` 二进制文件并用 `"named-xfer"` 将其复制到 chrooted 目录之后，我们还使用了 `"strip"` 命令提高新二进制文件的性能。

# 删除不需要的文件和目录

```
[root@deep]# rm -f /usr/sbin
[root@deep]# rm -f /usr/sbin/named-xfer
[root@deep]# rm -f /etc/named.conf
[root@deep]# rm -f /var/named/
```

## 步骤 5

测试新的 chroot 配置！重启 `syslogd`：

```
[root@deep]# /etc/rc.d/init.d/syslog restart
```

现在启动新的 BOUNDED 守护进程：

```
[root@deep]# /etc/rc.d/init.d/named start
```

确保它以 `named` 用户运行并带有新参数。

```
[root@deep]# ps aux grep named
```

关于本页面的意见和建议请邮寄至 `gmourani@videotron.ca`

`named 11466 0.0 1.2 2444 1850 ? 23:09:00/chroot/named/usr/bin/named -t/chroot/named -unnamed-named`
