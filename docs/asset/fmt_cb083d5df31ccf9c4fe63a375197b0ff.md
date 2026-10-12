
- `lrwx-rw-x` 1 `root` `root` 7 Jul 28 12:56 `systty` -> `console`

*** 此从 `tty` 到 `console` 的符号链接是必须的

- `crw-rw--` 1 `root` `tty` 5, 0 Jul 18 1994 `tty5`

- `crw-w--y-` 1 `root` `tty` 4, 0 Jul 18 1994 `tty0`

- `crw-rw--` 1 `root` `tty` 4, 1 Jul 24 22:33 `tty1`

- `crw-rw--` 1 `root` `tty` 4, 2 Jul 24 22:34 `tty2`

- `crw-rw--` 1 `root` `root` 4, 3 Jul 24 21:49 `tty3`

- `crw-rw--` 1 `root` `root` 4, 4 Jul 24 21:49 `tty4`

- `crw-rw--` 1 `root` `root` 4, 5 Jul 24 21:49 `tty5`

- `crw-rw--` 1 `root` `root` 4, 6 Jul 24 21:49 `tty6`

- `crw-rw--` 1 `root` `tty` 4, 7 Jul 18 1994 `tty7`

- `crw-rw--` 1 `root` `tty` 4, 8 Jul 18 1994 `tty8`

- `crw-rw--` 1 `root` `tty` 4, 9 Jul 19 1994 `tty9`

- `crw-rw--` 1 `root` `sys` 1, 5 Jul 18 1994 `zero`

### `/etc`:

`total 20`

- `-rw--r--` 1 `root` `root` 2167 Jul 29 20:25 `DIR_COLORS`

- `-rw--r--` 1 `root` `root` 20 Jul 28 12:37 `HOSTNAME`

- `-rw-r--r--` `root` `root` 109 Jul 24 22:57 `fstab`

- `-rw-r--r--` `root` `root` 271 Jul 24 22:21 `group`

- `-rw-r--r--` `root` `root` 2353 Jul 24 22:27 `inittab`

- `-rw--r--r--` `root` `root` 0 Jul 24 21:02 `issue`

- `-rw--r--r--` `root` `root` 2881 Jul 28 19:38 `ld.so.cache`

*** 如果缺少 `ld.so.cache`，很多东西在启动时会出问题。

*** 确保包含了 `ldconfig` 并从 `rc.x` 运行它。

- `-rw--r--` 1 `root` `root` 12 Jul 24 22:22 `motd`

- `-rw--r----` 1 `root` `root` 606 Jul 28 19:25 `passwd`

- `-rw--r----` 1 `root` `root` 1065 Jul 24 22:21 `profile`

- `-drwxr-xr-x` 1 `root` `root` 1024 Jul 24 21:02 `rc.d/`

- `-drwxr-xr-x` 1 `root` `root` 18 Jul 24 22:21 `shells`

- `-drwxr-xr-x` 1 `root` `root` 774 Jul 28 13:43 `termcap`

- `-drwxr-xr-x` 1 `root` `root` 126 Jul 28 13:44 `tty`

- `-drwxr-xr-x` 1 `root` `root` 0 Jul 24 22:47 `utmp`

### `/etc/rc.d`:

`total 5`

*** 因为所有内容都运行在内存磁盘上，所以我没特意处理 `shutdown`。

- `-drwx-xr-x` 1 `root` `root` 1158 Jul 24 22:23 `rc.2`

- `-drwx-xr-x` 1 `root` `root` 1151 Jul 28 19:08 `rc.M`

- `-drwx-xr-x` 1 `root` `root` 13 Jul 24 23:36 `lib.so.5` -> `lib.so.0`

- `-drwx-xr-x` 1 `root` `root` 562683 May 19 1995 `lib.so.0`

*** `include termcap`

### `/lib`:

`total 588`

*** 我是 `ELF` 系统，所以如果你还在 `a.out`，那么你需要 `ld-linux.so`。使用该命令查看应该包含哪些库。

- `lrwxrwxrwx` 1 `root` `root` 17 Jul 24 23:36 `ld-linux.so` -> `ld-linux.so.1.7.3`

- `-drwx-xr-x` 1 `root` `root` 20722 Aug 15 1995 `ld-linux.so.1.7.3`

- `lrwxrwxrwx` 1 `root` `root` 13 Jul 24 23:36 `lib.so.5` -> `lib.so.0`

- `-drwx-xr-x` 1 `root` `root` 562683 May 19 1995 `lib.so.0`

- `lrwxrwxrwx` 1 `root` `root` 19 Jul 28 19:53 `termcap.so.2` -> `termcap.so.2.0`

- `-drwx-xr-x` 1 `root` `root` 11360 May 19 1995 `termcap.so.2.0`

### `/proc`:

`total 0`

### `/sbin`:

`total 191`

## `D.` `工具列出。`

*** 我使用的是 `agetty`。很多系统使用 `getty`。

*** 检查你的 `/etc/inittab` 查看使用的是哪一个。注意你需要 `(a)getty` 和 `login` 才能启动许多功能。

- `-drwxr-xr-x` 1 `root` `bin` 11309 Jul 24 22:54 `agetty*`

- `-drwxr-xr-x` 1 `root` `bin` 5204 Jul 24 22:19 `halt****` `启动需要这个`

- `-drwxr-xr-x` 1 `root` `bin` 20592 Jul 24 22:19 `init*`

- `-drwxr-xr-x` 1 `root` `root` 86020 Jul 28 19:07 `ldconfig`

- `-drwxr-xr-x` 1 `root` `root` 5329 Jul 27 14:10 `mkswap`

- `-drwxr-xr-x` 1 `root` `root` 5204 Jul 24 22:20 `reboot*`

- `-drwxr-xr-x` 1 `root` `root` 6024 Jul 24 22:20 `rdev*`

- `-drwxr-xr-x` 1 `root` `bin` 12340 Jul 24 22:20 `shutdown*`

- `-drwxr-xr-x` 1 `root` `root` 5029 Jul 24 22:20 `swapoff*`

- `-drwxr-xr-x` 1 `root` `bin` 5029 Jul 24 22:20 `spawn*`

- `-drwxr-xr-x` 1 `root` `root` 20592 Jul 28 17:18 `telnet*`

- `-drwxr-xr-x` 1 `root` `root` 7077 Jul 24 22:20 `update*`

### `/tmp`:

`total 0`

### `/usr`:

`total 2`

- `drwxr-xr-x` 2 `root` `root` `root` 1024 Jul 29 21:00 `adm/`

- `drwxr-xr-x` 2 `root` `root` `root` 1024 Jul 29 21:16 `lib/`

### `/usr/adm`:

`total 0`

### `/usr/lib`:

`total 0`

### `/var`:

`total 1`

*** 在我包含此项以及初始化 `/var/run/utmp` 的 `/etc/rc.s` 代码之前，有几个东西一直在抱怨，但这并不一定适用于你的系统。

- `drwxr-xr-x` 2 `root` `root` 1024 Jul 28 19:52

### `/var/run`:

`total 0`

`548`

# 目录

- `3.3.1` `'mem='` `参数` `.................................................................` `556`

- `3.3.2` `'swap='` `参数` `................................................................` `557`

- `3.3.3` `'buff='` `参数` `................................................................` `557`

- `3.4` `用于` `NFS` `根文件系统的启动参数` `..........................................` `558`

- `3.4.1` `'nfsroot='` `参数` `.......................................................` `558`

- `3.4.2` `'nfsaddrs='` `参数` `................................................` `558`

- `3.5` `其他杂内核启动参数` `..........................................` `559`
