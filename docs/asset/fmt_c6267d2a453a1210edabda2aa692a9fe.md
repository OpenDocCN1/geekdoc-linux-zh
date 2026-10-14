
ttos2val.h

`-rm -f ttmkfdir.tar.gz`

`tar zcvf ttmkfdir.tar.gz ^`

```make
ttmkfdir: ttmkfdir.o

$(CC) -o $@ $^ $< $(LDFLAGS)
```

```make
ttmkfdir.o: ttmkfdir.c panose.ttos2val.h
```

```make
clean:
-rm -f ttmkfdir *.o core ~ ttmkfdir.tar.gz
```

你需要编辑变量 `FREETYPE_BASE`、`FREETYPE_INCL` 和 `FREETYPE_LIB`。在以前的示例中，我用 `#` 字符注释掉了默认值。在注释掉的值下方，我放置了新值。这些值应该与你安装的 FreeType RPM 匹配。

## 第 19 章 + 配置 X 窗口系统

6. 最后，在 Makefile 所在的输入命令 `make` 来创建 `tmkfddir` 程序：

```bash
[root@lemur tmkfddir#] make

gcc -Wall -pedantic -I/usr/include/freetype -c -o tmkfddir.o tmkfddir.o

gcc -o tmkfddir tmkfddir.o /usr/lib/libtttf.a

[root@lemur tmkfddir#] ls
```

Makefile README tmkfddir tmkfddir.o
Makefile~ panose.h tmkfddir.c ttos2val.h

从目录列表可以看出，`tmkfddir` 可执行文件已生成。如果你在执行 `make` 命令时收到任何错误，它们可能与设置 `FREETYPE` 变量不有关。请双击路径是否存在以及 `libtttf.a` 是否存在：`$(FREETYPE_BASE)/libtttf.a`。

7. 将 `tmkfddir` 工具安装到一个易于访问的目录——例如 `/usr/local/sbin`：

```bash
[root@lemur tmkfddir#] cp tmkfddir /usr/local/sbin/
```

8. 切换到 TrueType 字体目录并执行以下命令创建 `fonts.dir`：

```bash
cd /usr/share/fonts/StarOffice/TrueType

/usr/sbin/tmkfddir > fonts.dir
```

9. 现在尝试将 TrueType 字体路径添加到 X 路径中。

```bash
xset +fp /usr/local/fonts/StarOffice/TrueType

xset fp refresh
```

如果你得到类似下面的错误：

```bash
[root@lemur test]# xset +fp

/usr/share/fonts/StarOffice/TrueType

xset: bad font path element (#38), possible causes are:
```

目录不存在或权限错误

目录缺少 fonts.dir

错误的字体服务器地址或语法

请确保该目录存在，并且对所有人均可读。这可能不是真正的问题。我发现服务器会拒绝带有大写 .TT 扩展名的字体。如果你将字体文件重命名为小写的 `.ttf` 扩展名，它应该就能工作。要确认你的字体已添加到 X 服务器字体路径，你可以执行之前的任何一种字体检查。检查可用字体的另一种方法是使用 `xlsfont` 工具：

```bash
xlsfont | grep <font search string> | more
```

如果你看到了你的字体，可以按照“转换为 Type1”章节中的描述，将它们添加到 `/etc/X11/XBF6Config` 中的 X 服务器字体列表中。

## 提供字体（Type1 和 TrueType）

也可以向本地机器上的 X 服务器以及网络上的其他机器提供字体。这样做，你可以集中维护 X 中字体这项相当繁琐的工作。TurboLinux 带有 `xfs` 字体服务器。它同时支持 Type1 和 TrueType 字体。要配置 `xfs` 提供字体，你必须像列表 19-1 所示编辑 `/etc/X11/fs/config` 文件。

### 列表 19-1: /etc/X11/fs/config

```config
# 字体服务器配置文件

# $XConsortium: config.cpp,v 17.1 91/08/22 11:39:59 rws Exp $

clone-self = on

use-syslog = off

catalog = /usr/X11R6/lib/X11/fonts/misc/

/usr/X11R6/lib/X11/fonts/Speedo/

/usr/X11R6/lib/X11/fonts/Type1/

/usr/X11R6/lib/X11/fonts/75dpi/

/usr/X11R6/share/fonts/default/Type1/

/usr/X11R6/lib/X11/fonts/75dpi

error-file = /var/log/xfs.errlog

# 单位为点

default-point-size = 120

default-resolutions = 75,75,100,100

deferglyphs=all

# 字体缓存控制。以 KB 为单位

cache-hi-mark = 2048

cache-low-mark = 1433
```

该配置文件的关键条目是 `catalog` 行。在这里你将添加希望 `xfs` 提供的字体。这是一个用逗号分隔的字体列表——类似于 `X86Config` 文件的 Files 部分。`catalog` 条目可以跨行。确保最后一行不以逗号结尾。查看 `xfs` 的手册页可以了解更多选项。默认选项应该满足你的需求。请注意，我略微修改了 `/etc/X11/fs/config` 文件，使得 `catalog` 行是可读的且有一个有效的路径。要启动 `xfs`，可以使用类似下面的命令：

```bash
xfs -config /etc/X11/fs/config -port 7101
```

## 第19 章 - 配置 X 窗口系统

这告诉 `xfs` 使用正确的配置文件和端口 7101。要使用 `xfs` 提供的字体，你需要在字体路径中添加以下行：

```
tcp/<xfs host>:<port>
```

其中 `<xfs host>` 是运行 `xfs` 的机器的主名，如下：

```bash
xfs -config /etc/X11/fs/config -port 7101
```
