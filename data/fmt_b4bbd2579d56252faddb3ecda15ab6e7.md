
```
jdoe/home/jdoe/src/yencode-0.46 $ make install
Making install intl
make[1]: Entering directory /home/jdoe/src/yencode-0.46/int/
if test "yencode" = "gettext"
& & test = "int-comppa.o"; then \
  /bin/sh -case "*/mkinstallstallirs" in *) echo "../mkinstallstallirs"; ;; *) echo \
-> "../mkinstallstallirs"; ;; esac /home/jdoe/home/jdoe/include; \
  /usr/bin/install -c 64 libintl.h /home/jdoe/include/libintl.h; \
  $LIBTOOL@ -mode=install \
  /usr/bin/install -c 64 libintl.a /home/jdoe/libintl.a; \
else
  :;
  fi
if test 'no' = yes; then \
  /bin/sh -case "*/mkinstallstallirs" in *) echo "../mkinstallstallirs"; ;; echo \
-> "../mkinstallstallirs"; ;; esac /home/jdoe/lib; \
  temp=/home/jdoe/lib/t-charset.alias; \
/home/jdoe/man/ypostrc.5
  Manual page describing the ~/.ypostrc format.
  ...
```

```
make[2]: Leaving directory /home/jdoe/src/yencode-0.46'
make[1]: Leaving directory /home/jdoe/src/yencode-0.46'
jdoe/home/jdoe/src/yencode-0.46 $
```

代码列表 14.5 输入 `make install` 以完成安装过程。

# 第 15 章

# 安装你自己的软件

- 2. `make install`

输入 `make install` 完成该过程（参见代码列表 14.5）。

- 3. `~/bin/yencode`

尝试新软件！（（当然，请将 `yencode` 替换为安装的软件名称。）（参见代码列表 14.6）。

哇！它运行了！

- 4. `cd ; rm ~/src/yencode*`

在你确定一切运行良好后，对整个源码树进行 tar 和 gzip 压缩（如果需要，在主目录中进行）。或者，如果空间紧张，可以删除源码。

继续见下页

```
jdoe /home/doe/src/yencode-0.46 $ make
cd . \
& CONFIG_FILES=CONFIG_HEADERS=config.h \
/bin/sh ./config.status
config.status: creating config.h
config.status: config.h is unchanged
make all -recursive
make[1]: Entering directory `/home/doe/src/yencode-0.46'
Making all in intl
make[2]: Entering directory `/home/doe/src/yencode-0.46/intl`
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory `/home/doe/src/yencode-0.46/intl`
Making in po
make[2]: Entering directory `/home/doe/src/yencode-0.46/po`
```

```
gcc -DLOCALED_IR="/home/doe/src/local" -DSYSYYPE="i686-pc-linux-gnu" -I. -I.,\n-I. ./lib -Iintl \-Wall -Wno-unused -gO2 -c -f ydecode.c ilo echo ''' /../ydecode.c
gcc -Wall -Wno-unused -gO2 -o ydecode.o crc file.o o ../libmisc
make[3]: Leaving directory `/home/doe/src/yencode-0.46/src`
make[2]: Leaving directory `/home/doe/src/yencode-0.46/src`
make[2]: Entering directory `/home/doe/src/yencode-0.46`
make[2]: Leaving directory `/home/doe/src/yencode-0.46`
make[1]: Leaving directory `/home/doe/src/yencode-0.46`
```

代码列表 14.4 向你的屏幕输出了大量的垃圾（但希望没有错误信息）。

代码列表 14.5 输入 `make install` 以完成安装过程。

代码列表 14.6 它运行了！

# 第 14 章

## 提示

- ■ 遇到错误时，请耐心解决。

- ■ 编译失败后，输入 `makeclean` 清理源码。

- ■ 有时并不值得费力。

- ■ 特别注意路径。

- ■ 注意 `cal` 是符合千年虫标准的。

# 使用实用工具

当你认为 Unix 已经很棒了……它变得更棒了！Unix 提供了大量的实用工具——小型程序——可以让你的生活变得轻松。例如，你可能想使用日历、计算器或拼写检查器。

### 目录

* 使用日历工具

* 使用计算器工具

* 计算表达式

* 单位转换

* 交互式拼写检查

* 查找定义

* 打印你的工作

* 保存话记录

# 使用 cal 日历

Unix 最实用的工具之一是 `cal`，逻辑上它就是一个日历。查看今天是几、12 月 31 日是星期几，或者全年日历长什么样。正如代码列表 15.1 所示，你只需要输入 `cal` 以及任何你特定选项。

使用 `cal` 工具：

- 1. `cal`

在 shell 提示符下输入 `cal` 查看当前月份日历，如代码列表 15.1 所示。然后，按照接下来的几个步骤尝试不同的选项。

- 2. `cal -j`

使用 `cal -j` 查看儒略历，它显示从一年开始的每一天的编号。（此参数在所有系统上均有效）。

- 3. `cal 2004 | more`

将 `cal 2004` 传递至 `more` 以查看整年的日历。

- 4. `cal 12 1941`

输入 `cal` 加上特定日期以查看特定年份的日历。

```bash
[jdoe@frazz jdoe]$ cal
2003年1月
Su Mo Tu We Th Fr Sa
1 2 3 4
5 6 7 8 9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31
```

```bash
[jdoe@frazz jdoe]$ cal -j 2004
2004年3月
Sun Mon Tue Wed Thu Fri Sat
61 62 63 64 65 66
67 68 69 70 71 72 73
74 75 76 77 78 79 80
81 82 83 84 85 86 87
88 89 90 91
```
