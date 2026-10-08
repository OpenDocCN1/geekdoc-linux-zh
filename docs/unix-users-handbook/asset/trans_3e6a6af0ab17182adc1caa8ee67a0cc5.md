

## Shell 程序

```bash
echo "PROG>>>> determining if make_recovery has been run by
            checking for /var/opt/ignite/arch.include."
if [ -f /var/opt/ignite/recovery/arch.include ]; then
    echo "make_recovery has been run."
else
    echo "make_recovery has not been run."
fi

echo "PROG>>>> determining if make_recovery was run with the
            -C (for check_recovery) option."
if [ -f /var/opt/ignite/recovery/makrec.last ]; then
    echo "make_recovery with -C has been run. We'll now
            run check_recovery."
    /opt/ignite/bin/check_recovery 2>&1
else
    echo "make_recovery with -C has not been run. We can't
            run check_recovery."
fi
} | tee -a /tmp/IMPORTANT/igtest.out
```

Shell 程序是您能够阅读和修改的文本，前提是确实拥有相应的权限。除了编程信息外，Shell 程序还包含以 # 开头的行所指示的注释。

## 链接

链接是指向存储在系统其他位置的文件指针。您不必在系统中保留两个或多个文件副本，而是可以链接到系统中已存在的文件。

在 UNIX 中，链接的一个特别有用的用途与操作系统的新版本有关。从一个版本升级到另一个版本时，文件的位置有时会发生变化，与其学习所有新位置，不如从旧位置创建指向新位置的链接。当您使用旧位置运行命令时，链接将指向新位置。

链接对于集中管理文件也很有用。如果一组相同的文件需要经常更新，链接到一个中心文件并更新它比在多个不同位置更新该文件的多个副本要容易得多。

## 设备文件

设备文件（有时称为设备特殊文件）包含有关连接到您系统的硬件的信息。由于设备特殊文件与系统管理功能相关联，因此在面向用户（而非系统管理员）的材料中通常很少涉及。我认为情况本应相反。如果用户想要向软盘或磁带写入文件，却不知道如何访问设备文件，这会非常令人沮丧。我将介绍一些设备文件的用途，以免您在这个领域完全处于黑暗之中。

您系统上的设备通常可以通过不同的设备文件来访问。例如，磁盘既可以通过块设备文件访问，也可以通过字符设备文件访问。大多数访问操作是系统管理员的责任；然而，当您尝试确定文件类型时，可能会遇到不同类型的特殊文件，例如字符设备和块设备。

您的系统上还有其他类型的文件，但对于初学 UNIX 而言，我将描述的文件类型提供了足够的背景知识来帮助您入门。

![](img/75f39fc91296b889c0653851accdfd46_89_0.png)

## file 命令

**file** 命令用于确定文件类型。此命令很有用，因为文件名并不总是指示其文件类型。以下示例执行文件的长列表以提供有关该文件的一些背景信息，然后运行 **file** 命令以显示文件类型。我在下一章才介绍用于列出文件的命令，但我在这些示例中包含了它。**ls** 命令提供文件列表。**ls** 将在下一章中详细介绍。我们在本章中只需要使用其基本形式。如果您需要查看，我已在本章末尾包含了 **ls** 的手册页。结合 “-l” 选项，您可以生成长列表，提供大量有关文件的信息。使用 **ls -l** 在以下示例中，您将看到每个文件的名称、文件类型、权限、硬链接数、所有者名称、组名称、字节大小和时间戳。您可能现在还不太清楚这些信息的大部分用途；然而，当查看 **file** 命令的输出时，其中一些信息可能会很有用。本章中关于 **file** 命令的示例表明，不同的 UNIX 变体可能产生略有不同的 **file** 命令输出。以下示例展示了 HP-UX 的“UNIX 示例”输出，以及可用时的 Linux 输出。

![](img/75f39fc91296b889c0653851accdfd46_90_0.png)

![](img/75f39fc91296b889c0653851accdfd46_90_1.png)

### 文本文件（UNIX 示例）

（由 **file** 命令描述为 *ascii text*。）

```text
# ls -l .mosaic-global-history
-rw-r--r--     1  201     users          587 Dec 22  1999 .mosaic-global-history
# file .mosaic-global-history
.mosaic-global-history: ascii text
#
```

### 文本文件（Linux 示例）

（由 **file** 命令描述为 *ASCII text*。）

```text
# ls -l *
-rw-r--r--     1  root    root         251367 Nov  5 07:11 debug
-rw-r--r--     1  root    root          2020 Nov  5 07:11 history
# file *
debug:        ASCII text
history:       ASCII text
```

![](img/75f39fc91296b889c0653851accdfd46_91_0.png)

### 数据文件（UNIX 示例）

（由 **file** 命令描述为 *data*。）

![](img/75f39fc91296b889c0653851accdfd46_91_1.png)

```text
# ls -l Static.dat
-rw-r--r--    1    201        users     235874 Aug 26  1999 Static.dat
# file Static.dat
Static.dat:     data
#
```

### 源代码文件（UNIX 示例）

（由 **file** 命令描述为 *c program text*。）

```text
# ls -l krsort.c
-rwxrwxrw    1    201        users     3234 Nov 16  1999 krsort.c
# file krsort.c
krsort.c:      c program text
#
```

### 源代码文件（Linux 示例）

（由 **file** 命令描述为 *C program text*。）

```text
# ls -l *.c
-rw-r-r--    1 root        root     4521 Jul 12  1999 intl-bindtextdom.c
-rw-r-r--    1 root        root     6234 Jul 12  1999 intl-cat-compact.c
-rw-r-r--    1 root        root     14128 Jul 12  1999 intl-dgettext.c
-rw-r-r--    1 root        root     1750 Jul 12  1999 intl-dgettext.c
-rw-r-r--    1 root        root     12759 Jul 12  1999 intl-finddomain.c
-rw-r-r--    1 root        root     1907 Jul 12  1999 intl-gettext.c
-rw-r-r--    1 root        root     1646 Jul 12  1999 intl-intl-compact.c
-rw-r-r--    1 root        root     5361 Jul 12  1999 intl-loadmsgcat.c
-rw-r-r--    1 root        root     7271 Jul 12  1999 intl-localealias.c
-rw-r-r--    1 root        root     2914 Jul 12  1999 intl-textdomain.c
# file *.c
intl-bindtextdom.c:  C program text
intl-cat-compact.c:  C program text
intl-dgettext.c:     C program text
intl-finddomain.c:   C program text
intl-gettext.c:      C program text
intl-intl-compact.c: C program text
intl-loadmsgcat.c:   C program text
intl-localealias.c:  C program text
intl-textdomain.c:   C program text
#
```

### 可执行文件（UNIX 示例）

（由 file 命令描述为 shared executable。）

```text
# ls -l krsort
-rwxr-xr-x  1 201    users       34592 Nov 16  1999 krsort
# file krsort
krsort:		PA-RISC1.1 shared executable dynamically linked
-not stripped
#
```

### 可执行文件（Linux 示例）

（由 file 命令描述为 executable。）

```text
# ls -l a*
-rwxr-xr-x  1 root     root          3888 Jul 24  1999 activate
-rwxr-xr-x  1 root     root          4452 Feb 25  1999 adjtimex
# file a*
activate: ELF 32-bit LSB executable, Intel 80386, version 1,
stripped
adjtimex: ELF 32-bit LSB executable, Intel 80386, version 1,
stripped
#
```

### Shell 程序（UNIX 示例）

（由 file 命令描述为 commands text。）

```text
# ls -l llsum
-rwxrwxrwx  1 root     sys          1267 Feb 23  1999 llsum
# file llsum
llsum:		commands text
#
```

![](img/75f39fc91296b889c0653851accdfd46_93_0.png)

![](img/75f39fc91296b889c0653851accdfd46_93_1.png)

### Shell 程序（Linux 示例）

（由 **file** 命令描述为 *Bourne shell script text*。）

```text
# ls -l request-route
-rwx------ 1 root root 1046 Sep 19 1999 request-route
# file request-route
request-route: Bourne shell script text
#
```

### 链接（UNIX 示例）

（该链接未被 **file** 命令引用；此处显示为 *shared executable dynamically linked*。对 *dynamically linked* 的引用并不意味着这是一个链接。）

```text
# ls -l /usr/bin/ar
lr-xr-xr-xr 1 root sys 15 Mar 23 1999 ar -> /usr/ccs/bin/ar
# file /usr/bin/ar
/usr/bin/ar: s800 shared executable dynamically linked
#
```

### 链接（Linux 示例）

（该链接显示为 *symbolic link*。）

```text
# ls -l reboot
lrw xrwxrwx 1 root root 4 Nov 5 01:31 reboot -> halt
# file * | grep link
depmod: symbolic link to modprobe
ksyms: symbolic link to insmod
pidof: symbolic link to killall5
reboot: symbolic link to halt
rmmod: symbolic link to insmod
swapon: symbolic link to swapoff
telinit: symbolic link to init
udostctl: symbolic link to /sbin/umsync
umsetup: symbolic link to /sbin/umsync
#
```

