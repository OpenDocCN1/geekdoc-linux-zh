
```
$ ldd /usr/X11R6/bin/xbiff
libXaw.so.6 => /usr/X11R6/lib/libXaw.so.6 (0x40017000)
libXmu.so.6 => /usr/X11R6/lib/libXmu.so.6 (0x40051000)
libXt.so.6 => /usr/X11R6/lib/libXt.so.6 (0x40064000)
libSM.so.6 => /usr/X11R6/lib/libSM.so.6 (0x40080000)
libICE.so.6 => /usr/X11R6/lib/libICE.so.6 (0x400ba000)
libXext.so.6 => /usr/X11R6/lib/libXext.so.6 (0x400d2000)
libX11.so.6 => /usr/X11R6/lib/libX11.so.6 (0x400de000)
libm.so.6 => /lib/libm.so.6 (0x40187000)
libc.so.6 => /lib/libc.so.6 (0x40143000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

当系统中缺少库、运行时链接器使用了错误的库版本，或者共享库与操作系统的某些部分（如内核）不兼容时，就会出现问题。

## 问题 65

**症状：** 程序无法运行，并产生类似如下的错误消息

*progname: 无法加载库'libname'*

**问题：** 共享库缺失或不正确。

**修复：** 至少，运行时链接器默认会在 `/lib` 和 `/usr/lib` 中查找。如果你编译并链接的程序针对的是默认位置之外的共享库，则需要在（编译时）向链接器传递特殊选项，以告知运行时链接器库的位置。这些选项是 `-Ldir` 和 `-Wl,-rpath=dir`。6.4 节也会对它们进行说明。

文件 `/etc/ld.so.conf` 列出了运行时链接器除了 `/usr/lib` 和 `/lib` 之外要搜索的目录。如果你修改此文件，需要运行 `ldconfig -v` 使更改生效。

> **注意**
>
> 修改 `/etc/ld.so.conf` 时务必格外小心，不要添加不必要的条目（也就是说，除非你确实知道自己在做什么，否则不要添加任何东西）。多余的目录会降低系统性能。

## 6.3 典型的源代码发行版

源代码通常以压缩 tar 归档文件的形式发布，文件后缀如 `.tar.gz`、`.tar.bz2` 或 `.tgz`。用 gzip 创建的文件后缀为 `.gz`（有时极少数情况下为 `.z`）。`.bz2` 后缀来自 bzip2，一个较新的压缩程序。最后，任何带 `.Z` 后缀的文件来自老式的 Unix compress 程序；gzip 可以处理它。

## 问题 66

**症状：** 程序与问题 65 中一样无法运行，并且没有可用的源代码。

**问题：** 共享库缺失或不正确。

**修复：** 另一种修改运行时链接器行为的方法（应作为最后手段使用）是环境变量 `LD_LIBRARY_PATH`。你可以将其设置为冒号分隔的目录列表，运行时链接器会搜索这些目录以查找共享库。使用该变量会减慢程序启动时间，并可能导致严重的共享库不匹配，但有时这是唯一的选择。

## 警告

> 切勿在任何默认用户环境中设置 `LD_LIBRARY_PATH`，并且永远不要（在任何情况下）在设置了 `LD_LIBRARY_PATH` 时编译任何软件包。你的用户会抱怨程序找不到库，以及出现引用过时库版本的奇怪错误消息。

如果你确实需要使用 `LD_LIBRARY_PATH` 来运行一个没有源代码的程序——例如名为 `prog` 的程序——请将 `prog` 重命名为 `prog.bin`，并让 `prog` 成为像下面这样的包装脚本[其中 `libdir` 是共享库所在的目录]：

```
#!/bin/sh
LD_LIBRARY_PATH=libdir:$LD_LIBRARY_PATH
exec /usr/local/bin/prog.bin $@
```

相关手册页：`ldd` (1)、`ldconfig` (8)、`ld.so` (8)

### 如何处理那些 tar 压缩包

要解压压缩的 tar 文件（也称为 tarball），不要先将文件解压，然后通过两条单独的命令行运行 tar 来提取；而应在同一条管道中完成所有操作。GNU tar（你的系统上几乎肯定有）通过其 `-z` 选项简化了处理 gzip 文件的 tar 过程，该选项会告诉 GNU tar 先用 gzip 解压文件。

目前，还没有处理 `.bz2` 文件的标准方式，所以你需要在管道中完成。下面是一些示例。

要查看 `foo.tar.gz` 的内容，请使用：

```
$ tar -ztvf foo.tar.gz
```

要提取 `foo.tar.bz2` 的内容，请使用：

```
$ bunzip2 -dc foo.tar.bz2 | tar -xvf -
```
