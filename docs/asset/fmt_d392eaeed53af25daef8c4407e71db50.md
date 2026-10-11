
Looking for matches...

Found(s) for `org.gnome.Solitaire` in `fedora` (system)

Use this method? [Y/n]: y

`org.gnome.Solitaire`:

[1] pulseaudio access

[2] dbus access

[1] xdg-run/dconf, ~/.config/dconf

[2] ca.edes.dconf, org.gnome.GConf

| ID | Arch | Branch | Remote |
|---|---|---|---|
| [✓] org.gnome.Solitaire | x86_64 | stable | fedora 8.4 MB / 8.4 MB |

```
Installation complete.
```

要检查安装是否成功，你可以再次使用 `flatpak list`：

```
$ flatpak list
```

| Name | Application ID | Version | Installation |
|---|---|---|---|
| Platform | org.flataproject.Platform | f32 | system |
| Solitaire | org.gnome.Solitaire | stable | system |

最后，要移除应用程序容器，使用 `flatpak uninstall` 命令：

```
$ sudo flatpak uninstall org.gnome.Solitaire
```

| ID | Arch | Branch |
|---|---|---|
| [-] org.gnome.Solitaire | x86_64 | stable |

```
Uninstall complete.
```

使用容器与使用包系统相似，但底层原理不同。然而，结果是在你的 Linux 系统上安装了一个易维护和升级的应用程序。

## 从源码安装

在包管理系统和应用程序容器之前，开源应用程序开发者需要分发源码，并允许用户在自己的系统中编译应用程序。源码包通常以 tar 包的形式发布。第4 章“更多 Bash Shell 命令”讨论过 tar 包——如何使用 `tar` 命令行创建它们以及如何解压它们。

如果你经常处理源码，很有可能仍然发现以 tar 包封装的软件。本节将带你完成解压和安装 tar 包软件软件包的过程。

在本例中，将使用软件软件包 `sysstat`。`sysstat` 实用是一个非常棒的软件包，提供了系统监控工具视图。

首先，你需要将 `sysstat` tar 包下载到你的 Linux 系统。虽然你可以在不同的 Linux 站点找到 `sysstat` 包，但最好直接去程序的源。在这种情况下，网站是 `sebastien.goddard.pagesperso-orange.fr`。

当你点击 `Download` 链接时，将进入包含下载文件的页面。本文目前的版本为 12.3.3，分发名为 `sysstat-12.3.3.tar`。

点击链接将文件下载到你的 Linux 系统。一旦下载完成，你可以使用以下命令进行解压：

要解压软件 tar 包，使用标准的 `tar` 命令：

```
$ tar -Jxvf sysstat-12.3.3.tar.xz

sysstat-12.3.3/

sysstat-12.3.3/pcp_stats.h

sysstat-12.3.3/rd_sensors.h

sysstat-12.3.3/xml/

sysstat-12.3.3/xml/sysstat.xsd

sysstat-12.3.3/xml/sysstat-3.9.dtd

sysstat-12.3.3/sa.h

sysstat-12.3.3/man/

sysstat-12.3.3/man/sadf.in

sysstat-12.3.3/man/mpstat.1

...

nsysstat-12.3.3/pcp_stats.c

sysstat-12.3.3/pr_stats.h

sysstat-12.3.3/rd_stats.c

sysstat-12.3.3/pr_stats.c

sysstat-12.3.3/travis.yml

sysstat-12.3.3/configure
```

# 第一部分：Linux 命令行

现在 tar 包和文件已经自动放置在一个名为 `sysstat-12.3.3` 的目录中，你可以进入该目录并继续。

首先，使用 `cd` 命令进入新目录并列出目录内容：

```
$ cd sysstat-12.3.3
$ ls
activity.c  images      pr_stats.h    sar.c
BUG_REPORT  INSTALL     raw_stats.c   sa_wrap.c
build       iocf.c    raw_stats.h   svg_stats.c
CHANGES     iocf.h     rd_sensors.c  svg_stats.c
cifiosat.c  iostat.c     sysconfig.in
cifiosat.h  iostat.h     rd_stats.c    sysstat-12.3.3.l
common.c    json_stats.c  rd_stats.h    sysstat-12.3.3.spec
common.h    json_stats.h  sysstat.in
configure   Makefile.in   rndr_stats.c  sysstat.iocnf
configure.in man       rndr_stats.h  sysstat.service.in
COPYING     mpstat.c    sa2.in        sysconfig.in
count.c     mpstat.h     sa_common.c  sysstat.h
CREDITS     pcp_def_metrics.c sa_conv.c  tapestat.h
cron        pcp_def_metrics.c sa_conv.h  tapestat.h
do_test     pcp_stats.c  sadc.c        tests
FAQ.md      pidstat.c    sadf.h        version.in
format.c    pidstat.c    sadf_misc.c  xml_stats.c
config      pr_stats.c   sa.h          xml_stats.c
$
```

在目录列表中，你通常应该看到一个 `INSTALL` 文件。阅读 `README` 文件是非常重要的。该文件中将包含你完成软件安装所需的指令。

遵循 `INSTALL` 文件包含的建议，下一步是为你的系统运行 `configure` 工具。该工具会检查你的 Linux 系统，以确保它拥有正确的库依赖，以及用于编译源代码的正确编译器：

```
./configure
```

### 检查程序：

- 正在检查 `gcc`... `gcc`
checking whether the C compiler works... yes
checking for C compiler default output file name... out
checking for suffix of executables...
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether `gcc` accepts `-g`... yes

## 第9 章：安装软件

...
config.status: creating man/cifsostat.1
config.status: creating tests/variables
config.status: creating Makefile

Sysstat version:          12.3.3.3

Installation prefix:      /usr/local

rc directory:               

directory:/etc

Init directory:               /etc/init.d

Systemd unit:             /lib/systemd/sysstat

Configuration file:       /etc/sysconfig/sysstat

Man pages directory:      $(datarootdir)/man

Compiler:                 gcc
