
我们使用的 Makefile 与这个一个之间的区别在于，我们修改了 `DESTBIN=""` `DESTEXEC=""` 和 `DESTRUN=""` 行，使其指向 BIND/DNS 的 chroot 目录。通过此修改，`ndc` 程序将知道去寻找 `named`。

```
CC=egcs -D GNU_SOURCE
CDEBUG=-O9 -froll-loops -ffast-math -align-double -mcpu=pentiumpro -march=pentium-
ofomit-frame-pointer -no-exceptions
DESTBIN=/usr/bin
DESTBIN=/chroot/named/usr/sbin
DESTEXEC=/chroot/named/usr/sbin
DESTMAN=/usr/man
DESTHELP=/usr/lib
DESTRUN=/chroot/named/var/run
DESTLIB=/usr/lib/bind/include/
LEX=flex -d
YACC=yacc -d
SYSLABS="-lffi"
INSTALL="-install"
MANDIR=manman
MANROFF=cat
CATEXT=$$
PS=ps -p
AR=ar -c
'at-crus'
RANLIB=
```

```
[root]# srcj make clean
[root]# srcj make
[root]# srcj cp bin/ndc/usr /usr/sbin/
[root]# srcj cp /usr/sbin/ndc? y
[root]# srcj strip /usr/sbin/ndc
```

我们构建二进制文件，然后将 `ndc` 程序的结果复制到 `/usr/sbin` 并覆盖旧文件。我们忘了使用我们的 `ndc` 二进制文件以获得更好的性能。

## 第 10

现在构建新的 `named` 和 `named-xfer` 二进制文件是一个好主意，以确保版本同时用于 `named` 和 `ndc`。

对于 `named` 程序：

```
[root]# cd /var/tmp/src
[root]# srcj cp port/linux/Makefile.set-orig port/linux/Makefile.set
[root]# srcj cp /port/linux/Makefile.set? y
```

编辑 `Makefile.set` 文件（`vi port/linux/Makefile.set`）以进行下方列出的更改：

```
CC=egcs -D GNU_SOURCE
CDEBUG=-O9 -froll-loops -ffast-math -align-double -mcpu=pentiumpro -march=pentium-
ofomit-frame-pointer -no-exceptions
DESTBIN=/usr/bin
DESTBIN=/chroot/named/usr/sbin
DESTEXEC=/chroot/named/usr/sbin
DESTMAN=/usr/man
DESTHELP=/usr/lib
DESTETC="/etc"
```

© Copyright 1999-2000 Gerhard Maurani and Open Network Architecture ®

```
'DESTRN=/var/run/
DESTLIB=usr/lib/bind/
DESTINC=usr/lib/bind/include/
LEX=flex -8 -f
YACC=yacc -d
SYSLBS=-I/usr
INSTALL=install
MANDIR=man
MANOFF=cat
CTATEXT=$$
PS=pg g
AR=ar crus
RANLIB="
```

```
[root@deep src] rm -f .settings

[root@deep src] make clean

[root@deep src] make

[root@deep src] cp bin/named/named /chroot/usr/sbin

[root@deep src] cp /chroot/usr/sbin/named? y

[root@deep src] cp bin/named-xfer /chroot/usr/sbin/named-xfer

[root@deep src] cp /chroot/usr/sbin/named-xfer? y

[root@deep src] strip /chroot/usr/sbin/named

[root@deep src] strip /chroot/usr/sbin/named-xfer
```

由于构建系统的变化，我们删除了 `named` 文件，并运行 `clean` 命令以确保没有过时的垃圾残留。在构建 `named` 二进制文件并将其复制到 chrooted 目录之后，我们还使用 `strip` 命令提高新二进制文件的性能。

## 第 11

移除不需要的文件和目录。

```
[root@deep] rm -f /usr/sbin/named

[root@deep] rm -f /usr/sbin/named-xfer

[root@deep] rm -f /etc/named.conf

[root@deep] rm -rf /var/named/
```

我们从 `/usr/sbin` 目录删除了 `named` 和 `named-xfer` 二进制文件，因为我们日常使用的版本位于 chroot 目录下。`named.conf` 和 `var/named` 也是如此。

## 第 12

我们必须测试新的 BIND/DNS 软件 chrooted 监狱。

- 第一件事是使用以下命令重启 syslog 守护进程：

```
[root@deep] # /etc/init.d/syslog restart

Shutting down kernel logger:

[ OK ]

Shutting down system logger:

[ OK ]

Starting system logger:

[ OK ]

Starting kernel logger:

[ OK ]
```
- 现在，使用以下命令启动新的 chrooted 监狱 BIND/DNS：

```
[root@deep] # /etc/init.d/named start

Starting named:

[ OK ]
```
启动 BIND/DNS 的新的 chrooted 监狱。

- 使用以下命令验证 BIND/DNS 运行：

```
[root@deep] # /etc/init.d/named start

Starting named:

[ OK ]
```
启动 BIND/DNS 的新的 chrooted 监狱。

- 使用以下命令重启 syslog 守护进程：

```
[root@deep] # /etc/init.d/syslog restart

Shutting down kernel logger:

[ OK ]

Shutting down system logger:

[ OK ]

Starting system logger:

[ OK ]

Starting kernel logger:

[ OK ]
```
- 使用以下命令验证 BIND/DNS 运行：

```
[root@deep] # /etc/init.d/named start

Starting named:

[ OK ]
```
启动 BIND/DNS 的新的 chrooted 监狱。

- 使用以下命令验证：

```
[root@deep] # ps | grep named
```
验证 BIND/DNS 运行状态。

- 使用以下命令重启 syslog 守护进程：

```
[root@deep] # /etc/init.d/syslog restart

Shutting down kernel logger:

[ OK ]

Shutting down system logger:

[ OK ]

Starting system logger:

[ OK ]

Starting kernel logger:

[ OK ]
```
- 现在，使用以下命令启动新的 chrooted 监狱 BIND/DNS：

```
[root@deep] # /etc/init.d/named start

Starting named:

[ OK ]
```
启动 BIND/DNS 的新的 chrooted 监狱。

- 使用以下命令验证：

```
[root@deep] # ps | grep named
```
验证 BIND/DNS 运行状态。

## 清理

```
[root@deep] rm -rf /var/tmp/src
```
