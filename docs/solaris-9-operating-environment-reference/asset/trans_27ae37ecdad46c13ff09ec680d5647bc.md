
# 1062

# pkill

# 属性

查看 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUMMcsu |

# 另请

pkginfo(1), pkgmk(1), pkgparam(1), pkgproto(1), installf(1M), pkgadd(1M), pkgask(1M), pkgrm(1M), remove(1M), pkginfo(4), pkgmap(4), attributes(5)
应用封装开发者指南

# pkill — 查找或向进程信号

# 概要

```
/usr/bin/pkill [-signal] [-fnvx] [-P ppidlist] [-g pgrlist]
[-s sidlist] [-u euidlist] [-U uidlist] [-G gidlist] [-t termlist]
[pattern]
```

# 描述

查看 pgrep(1)。

# pidd — 进程工具

# 概要

```
/usr/bin/bin/pidd pid...
```

# 描述

查看 proc(1)。

# plimit — 获取或设置运行进程的资源限制

# 概要

```
/usr/bin/plimit [-km] pid...
/usr/bin/plimit -cdfnstv soft,hard... pid...
```

# 描述

在没有参数的情况下，plimit报告由 pid 标识的进程的资源限制。当你指定一个或多个 cdfnstv 选项时，plimit 会设置 pid 标识的进程中指定资源的软限制（当前限制）和/或硬限制（最大限制）。
只有进程的所有者或超级用户允许获取或设置进程的资源限制。只有超级用户可以增加硬限制。

# 选项

```
-k    以千字节（1,024 字节）而非 512 字节块显示文件大小。
-m    以兆字节（1,024*1,024 字节）显示文件和内存大小。
```

以下选项更改指定的资源限制。它们均接受以下格式的参数：
soft, hard
其中 soft 指定软限制（当前限制），hard 指定硬限制（最大限制）。如果你不指定硬限制，可以省略逗号。如果软限制为空字符串，则只设置硬限制。每个限制要么是字面字符串 unlimited，要么带有可选缩放因子的数字，如下：

```
-rk    千字节。
-rm    兆字节（CPU 时间为分钟）。
-rh    小时（仅限 CPU 时间）。
-mm:ss 分钟和秒（仅限 CPU 时间）。
```

软限制不能超过硬限制。
-c soft, hard
设置核心文件大小限制（默认单位为 512 字节块）。
-d soft, hard
设置数据段（堆）大小限制（默认单位为千字节）。
-f soft, hard
设置文件大小限制（默认单位为 512 字节块）。
-n soft, hard
设置文件描述符限制（无默认）。
-s soft, hard
设置栈段大小限制（默认单位为千字节）。
-t soft, hard
设置 CPU 时间限制（默认单位为秒）。
-v soft, hard
设置虚拟内存大小限制（默认单位为千字节）。

# 操作数

```
-pid    进程 ID 列表。
```

# 1064

# plot

# 示例

以下示例显示了卷管理守护进程 vold 的当前设置。

```
# plimit 213 /usr/sbin/vold
resource current maximum
time(seconds) unlimited unlimited
file(blocks) unlimited unlimited
data(kbytes) unlimited unlimited
stack(kbytes) 8192 2097148
coredump(blocks) unlimited unlimited
nofiles(descriptors) 1024 1024
vmemory(kbytes) unlimited unlimited
```

# 退出状态

- 0 成功。
- 非零 失败，例如无进程、权限被拒绝或无效选项。

# 文件

/proc/pid/* 进程信息和控制文件。

# 属性

查看 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | Sunmesa |

# 另请

proc(1), ulimit(1), getrlimit(2), setrlimit(2), proc(4), attributes(5)

# plot — 各种绘图仪的图形过滤器

# 概要

```
/usr/ucb/plot [-Terminal]
```

# 描述

plot 命令从标准输入读取绘图指令（参见 plot(4B)），并在标准输出产生适用于特定终端的绘图指令。

如果你不指定终端，将使用环境变量 TERM。默认终端是 tek。

# 环境变量

除 ver 之外，你可以配合 lpr -g（参见 lpr）使用以下终端类型产生输出。

- 2648 | 2648a | h8 | hp2648 | hp2648a
Hewlett-Packard 2648 图形终端。

- hp7221 | hp7 | h7
Hewlett-Packard 7221 绘图仪。

- 300
DASI 300 或 GSI 终端（Diablo 机制）。

- 300s | 300s
DASI 300s 终端（Diablo 机制）。

- 450
DASI Hyterm 450 终端（Diablo 机制）。

- 4013
Tektronix 4013 存储示波器。

- 4014 | tek
带有增强图形模块的 Tektronix 4014 和 4015 存储示波器。（对于没有增强图形模块的 Tektronix 4014 或 4015 使用 4013）。

- aed
AED 512 色图形终端。

- bgplot | bitgraph
BBN bitgraph 图形终端。

- crt
任何可以运行 vi(1) 的 CRT 终端。

- dumb | un
无光标寻址终端或行打印机。

- gigi | vt125
DEC vt125 终端。

- implot
Imagen 绘图仪。

- var
Benson Varian 打印机-绘图仪。

- var
Versatec D1200A 打印机-绘图仪。输出经过扫描转换，适用于 lpr -v 输入。

# 文件

```
/usr/ucb/aedplot
/usr/ucb/atoplot
/usr/ucb/bgplot
/usr/ucb/crtplot
/usr/ucb/dumbplot
/usr/ucb/gigiplot
/usr/ucb/hp7221plot
/usr/ucb/hpplot
```

```
/usr/ucb/implot
/usr/ucb/plot
/
/ucb/t300
///ucb/t01tek
/usr/ucb/vplot
```

# 属性

查看 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUMw |

# 另请

graph(1), tplot(1), vi(1), lpr(1), plot(4), attributes(5)

# pmap — 进程工具

# 概要

```
/proc/bin/pmap [-r] pid
```

# 描述

查看 proc(1)。

# popd — 更改工作目录

# 概要

```
/bin/cd [directory]
```

- sh
popd [+n]

# 描述

查看 cd(1)。

# postdaisy — 针式打字机 PostScript 转换器

# 概要

```
/lib/lp/postdaisy [-c num] [-f num] [-h num] [-m num] [-n num]
[-o list] [-p mode] [-r num] [-s num] [-v num] [-x num] [-y num]
[file...]
/lib/lp/postscript/postdaisy
```

# 描述

postdaisy 过滤器将针式打字机文件转换为 PostScript 并将结果写入标准输出。如果你未指定文件或 -，则从标准输入读取。

# 选项

- -c num 打印每页的副本。默认只打印一份。
- -f name 使用字体名称打印文件。
- -h num 设置初始水平索引。默认为 8。
- -m num 使用点大小代替初始索引设置的值。
- -n num 打印逗号分隔列表中的页码。
- -o list 打印逗号分隔范围列表中的页码。
- -p mode 以竖向（p）或横向（1）模式打印文件。模式的第一个字符有效。默认模式为竖向。
- -r num 选择回车和换行行为。如果 num 为 1，换行产生回车；如果 num 为 2，回车产生换行。将 num 设置为 3 开启模式。
- -s num 设置垂直移动索引。默认为 12。
- -v num 按因子放大每页。
- -x num 沿 x 轴移动 num 英。默认坐标系原点位于页面左上角，x 向右，y 向下。正 num 向右移动。默认偏移为 0.25 英寸。
- -y num 沿 y 轴移动 num 英。正 num 向上。默认偏移为 -0.25 英寸。

# 退出状态

- 0 成功。
- 非零 发生错误，例如无进程、权限被拒绝或无效选项。

# 文件

```
/lib/lp/postscript/forms.ps
/lib/lp/postscript/ps
```

# 属性

查看 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNpsf

# 另请

download(1), dpost(1), postdmd(1), postio(1), postmd(1), postprint(1), postreverse(1), posttekk(1), attributes(5)

# postdmd — 位图文件 PostScript 转换器
（根据概要内容修正为 postdaisy）

# 描述

postdaisy 过滤器将位图文件转换为 PostScript 并将结果写入标准输出。如果你未指定文件或 -，则从标准输入读取。

# 选项

- -c num 打印每页的副本。默认只打印一份。
- -f name 使用字体名称打印文件。
- -h num 设置初始水平索引。默认为 8。
- -m num 使用点大小代替初始索引设置的值。
- -n num 打印逗号分隔列表中的页码。
- -o list 打印逗号分隔范围列表中的页码。
- -p mode 以竖向（p）或横向（1）模式打印文件。模式的第一个字符有效。默认模式为竖向。
- -r num 选择回车和换行行为。如果 num 为 1，换行产生回车；如果 num 为 2，回车产生换行。将 num 设置为 3 开启两种模式。
- -s num 设置垂直移动索引。默认为 12。
- -v num 按因子放大每页。
- -x num 沿 x 轴移动 num 英。默认坐标系原点位于页面左上角，x 向右，y 向下。正 num 向右移动。默认偏移为 0.25 英寸。
- -y num 沿 y 轴移动 num 英。正 num 向上。默认偏移为 -0.25 英寸。

