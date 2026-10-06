

```bash
$ make -n credit
cc -c -o credit.c
cc -c -o accounts.c
cc -c -o credit credit.c accounts.c terms.
```

下一个示例使用了 `-t` 选项来更新名为 `credit` 的 tar 文件的修改时间。在你在使用 `-t` 选项后，make 会认为 `credit` 是最新的。

```bash
$ make -t credit
$ make credit
'credit' is up to date.
```

下一个示例展示了一个用于构建名为 `ff` 工具的简单 Makefile。由于构建 `ff` 需要的 `cc` 命令非常复杂，使用 Makefile 可以让你轻松地重新构建 `ff`，而无需尝试（更不用记住）`cc` 命令：

# $ cat Makefile

```makefile
# 从 fastfind.c 构建 ff 命令
SHELL=/bin/sh

ff:
	cc -traditional -o2 -g -DBIG=5120 -o ff fastfind.c myLib.a
```

# $ make ff

```bash
cc -traditional -o2 -g -DBIG=5120 -o ff fastfind.c myLib.
```

最后一个示例展示了一个更为复杂的 Makefile，它使用了在本节中未讨论的功能。请参阅第 1247 页引用的源码获取有关这些及其他高级功能的信息：

# $ cat Makefile

```makefile
############################################################
## 构建和维护缓冲区库
############################################################
SHELL=/bin/sh

############################################################
## 编译的标志和库。每当你使用该库构建程序时
# 都需要 XDLLIBS。CCFLAGS
# 提供最大优化。
cc=gcc
CCFLAGS=-O2 $(CCFLAGS)
XDLLIBS=-lXawd -lXt -lXnu -lXext -lX11 -lm
CFLAGS=-libbuff.a

############################################################
## 杂杂
INCLUDES=buf.h
INCLUDES=xtbuff.ad.h
OBJS=buff.o buf_print.o xtbuff.o

############################################################
## 运行 'make' 即可生成帮助信息
help Help:
	@echo "You can make the following:"
	@echo " "
	@echo "libbuf.a -- the buffer library"
	@echo "bufdisplay -- any-format buffer"
	@echo "buf2pm -- convert buffer to pixmap"
############################################################
# 主目标是库
libbuf.a: $(OBJS)
	@rm -f libbuf.a
	ar vr libbuf.a $(OBJS)
	ranlib libbuf.a
############################################################
# 次要目标 -- 从库构建的工具
bufdisplay: bufdisplay.c -o bufdisplay $(BUFLIB) $(XLDLIBS)
	$(CC) $(CFLAGS) bufdisplay.c -o bufdisplay
buf2pm: buf2pm.c libbuf.a
	$(CC) $(CFLAGS) buf2pm.c -o buf2pm $(BUFLIB)

############################################################
## 构建单个对象单元
buff.o: $(INCLUDES) buff.c
	$(CC) -c $(CFLAGS) buff.c

buff_print.o: $(INCLUDES) buff_print.c
	$(CC) -c $(CFLAGS) buff_print.c

xtbuff.o: $(INCLUDES) $(XINCLUDES) xtbuff.c
	$(CC) -c $(CFLAGS) xtbuff.c
```

`make` 工具可以用于编译代码以外的任务。作为一个最后的示例，假设你有一个数据库，其中包含两列 IP 地址和对应的主机名，该数据库将这些值导出到一个名为 `hosts.tab` 的文件中。你需要从该文件中提取主机名，并生成一个包含这些名称的名为 `hosts.html` 的 Web 页面。下面的 Makefile 是一个简单的报告生成：

```makefile
$ cat makefile
#
SHELL=/bin/sh

hosts.html: hosts.tab
	@echo "<html><<body>>" > hosts.html
	@awk '{print $2, "<br>"}' hosts.tab >> hosts.html
```

# man

显示命令的文档

man [options] [section] command
man -k keyword

man 工具为 GNU/Linux 命令提供在线文档。除了使用命令外，许多其他命令以及与 GNU/Linux 使用相关的详细信息也有文档可用。由于许多命令来自 GNU，GNU info 实用（第 45 页）经常提供额外信息。

每个 man 页面都关联有一个单行标题。该标题由命令名称、该命令所在的手册章节以及该命令功能的简要描述组成。这些标题存储在数据库中，以便你对与每个 man 页面相关的关键字进行快速搜索。

# Arguments

`section` 参数告诉 man 将搜索限制在手册的指定章节（手册章节列表请参见第 44 页）。如果没有此参数，man 将按数字顺序搜索章节直到找到 man 页面。在 man 命令的第二种形式中，`-k` 选项允许在标题数据库中搜索关键字；man 会显示包含指定关键字的标题列表。`man -k` 命令的功能与 `apropos`（第 79 页）相同。

# Options

- -a 显示所有章节的手册页。当你...时使用此选项。
- -k 在标题数据库中搜索关键字；man 会显示包含指定关键字的标题列表。
- -t 更新目标文件的修改时间。

# Discussion

除了使用命令外，许多其他命令以及与 GNU/Linux 使用相关的详细信息也有文档可用。由于许多命令来自 GNU，GNU info 实用（第 45 页）经常提供额外信息。

