
Script done, file is `typescript`

$

$ `cat typescript`          # 显示捕获的信息

Script started on Mon Nov 27 14:12:14 2000

$ `ps`

PID TTY       S       TIME CMD

725 console    I +       0:00.02 `/usr/bin/getty console console vt100`

775 pts/1      S       0:00.10 `-ksh (ksh)`

2729 pts/1    S       0:00.00 `script`

2730 pts/1    S +       0:00.00 `script`

2731 pts/2    S       0:00.00 `sh -is`

2732 pts/2    R +       0:00.01 `ps`

$

$ `date`

```
Mon Nov 27 14:12:23 EST 2000
```

$ `exit`

```
script done on Mon Nov 27 14:12:26 2000
```

$

# `script -a` # 附加到现有文件

Script started, file is `typescript`

$

$ `print '############'`

################

$ `date`

Mon Nov 27 14:13:10 EST 2000

$ `exit`

Script done, file is `typescript`

$

$ `cat typescript` # 显示内容

Script started on Mon Nov 27 14:12:14 2000

$ `ps`

| PID | TTY | S | TIME | CMD |
| :--- | :--- | :--- | :--- | :--- |
| 725 | console | I + | 0:00.02 | `/usr/bin/getty console console vt100` |
| 775 | pts/1 | S | 0:00.10 | `-ksh (ksh)` |
| 2729 | pts/1 | S | 0:00.00 | `script` |
| 2730 | pts/1 | S + | 0:00.00 | `script` |
| 2731 | pts/2 | S | 0:00.00 | `sh -is` |
| 2732 | pts/2 | R + | 0:00.01 | `ps` |

$ `date`

```
Mon Nov 27 14:12:23 EST 2000
```

## `select`

### 官方描述
生成带有数字的单词菜单。

### 语法
```
select identifier [word...] ; do
```

### 选项
无

### 奇特性
将菜单写入到 stderr。

### 示例
```bash
$ `select item in b*` # 设置包含文件名的菜单
> `do`
> `print $item` # 打印选择的文件
> `done`

1) buzz
2) buzz1
3) buzz2
4) buzz3
5) buzz4

#? 2 # 选择项目 2
buzz1
#? 6 # 选择项目 6
buzz4
#? 8 # 忽略不存在的项目
#? `Ctrl+D` 退出

$ `print $PS3`
#? PS3 变量内容（默认）
$
```

## `set`

### 官方描述
设置 shell 选项。

### 语法
```
set [-abCefhkmnopstx] [-o option ...] [-A name] [argument ...]
```

### 选项
- `-A name` 为数组赋值准备。
- `-f` 禁用文件名生成。
- `-h` 使命令在第一次遇到时被跟踪。
- `-o` 提供大量选项，包括 `emacs`, `vi`, `noclobber`, `xtrace`, `verbose`, `ignoreeof` 等。
- `-v` 打印读取的输入行。
- `-x` 打印执行命令及其参数。

### 奇特性
其他参数是位置参数，并按顺序分配给 `$1`, `$2` 等。

### 示例
```bash
$ `set den cheryl` # 使用设置位置参数
$ `print $1 $2`
den cheryl
$ `print $` # 显示当前设置的选项（interactive, Jobs complete with a message, sort parameters）
$
$ `set -v` # 设置另一个选项（verbose）
$
```

```bash
$ `print $` # 显示设置的选项（现在包含 v）
print $-
imsv
$
```

```bash
$ `set +v` # 关闭 verbose 选项
set +v
$
```

```bash
$ `print $` # 回到正常
ims
$
```

## `shift`

### 官方描述
将位置参数左移（`$2` 变成 `$1` 等）。

### 语法
```
shift [n]
```

### 选项
无

### 奇特性
移动后递减（参数计数）。
没有右移——只有左移。

### 示例
```bash
$ `set den cheryl chris scott` # 设置四个位置参数
$ `print $1` # 包含 den
den$
$ `shift` # 向左移动 $1
$ `print $1` # $1 现在包含 cheryl
cheryl$
$ `print $#` # 参数计数现在是 3
3$
$ `shift 2` # 移动 2
$
$ `print $#` # 减少到一
1$
$ `print $1` # $1 现在包含 scott
scott$
```

## `sleep`

### 官方描述
暂停执行至少指定的时间。

### 语法
```
sleep seconds
```

### 选项
无

### 奇特性
根据系统活动，实际暂停时间可能会更长。

### 示例
```bash
$ `date`
Mon Nov 27 14:45:37 EST 2000
$ `sleep 15`          # 睡眠 15 秒
$ `print $?` # 15 秒后报告成功
0
$ `date`
Mon Nov 27 14:46:04 EST 2000
$
$ `sleep 15`          # 用 Ctrl+C 中断睡眠
$ `print $?` # 因中断导致非成功状态
258
$
```

## `sort`

### 官方描述
排序或合并文件。

### 语法
```
sort [-m] [-o output_file] [-Abdfinru] [-k keydef]...[-t character] [-T directory] [-y] [kilobytes] [-z record_size]... file...
```

### 选项
- `-m` 执行合并。
- `-b` 忽略空格和制表符。
- `-f` 将小写视为大写。
- `-k keydef` 指定一个或多个排序键（起始字节，结束字节）。
- `-n` 排序任何数字字符串。
- `-r` 反转顺序。
- `-u` 表示输出中没有重复项。

### 奇特性
没有独立的 merge 命令。

### 示例
```bash
$ `sort buzz` # 标准排序
! /bin/ksh
do
done
integer x=17
while :
x=17
$ `sort -r buzz` # 降序排序
x=17
while :
integer x=17
done
do
! /bin/ksh
$
$ `sort -k 3,1 buzz` # 跳过三个字节后找到的一个字节作为排序键
! /bin/ksh
do
done
integer x=17
while :
x=17
```

## `stop`

### 官方描述
停止后台作业。

### 语法
```
stop %job_number or pid
```

### 选项
无

### 奇特性
`stop` 命令是 `kill -STOP` 的别名。

### 示例
```bash
$ `buzz&` # 创建两个后台作业
[1] 1181
$ `buzz&`
[2] 1182
$

$ `jobs buzz&`
[2] - Running buzz&
[1] - Running buzz&
$

`stop %1` # Stop job #1
[1] + Stopped (SIGSTOP) buzz&
$

$ `jobs -l`
[1] + 1181 Stopped (SIGSTOP) buzz&
[2] - 1182 Running buzz&
$

`stop 1182` # Stop pid #1182
[2] + Stopped (SIGSTOP) buzz&
$
```

## `tail`

### 描述
显示文件的末尾。

### 语法
```
tail [-f | -r] [-c number | -n number] [file]
```

### 选项
- `-c number` 请求输出从指定的字符数开始显示。
- `-f` 请求 tail 函数在复制完最后一行后结束。可以监控文件内容的增长。
- `-n number` 请求输出从指定的行数开始显示。
- `-r` 反转显示顺序。

### 奇之处
默认显示文件的最后 10 行。

### 示例
```bash
$ `tail -n 3 buzz` # 显示文件的最后 3 行
do
x=17
done
$ `tail -c 3 buzz` # 显示文件的最后 3 个字符
ne$
```

## `tee`

### 描述
从标准输入读取并写入标准输出和文件。

### 语法
```
tee [-ai] file...
```

### 选项
- `-a` 向文件输出追加追加内容。
- `-i` 忽略 INT 信号。

### 奇之处
如果一个目标文件不可用，输出将继续写入其他文件。

### 示例
```bash
$ `ls -l b*`
-r-x-W-r-X 1 obrien obrien 47 Nov 26 12:19 buzz
-rwxxrwx-- 1 obrien obrien 90 Nov 26 12:45 buzz1
-r-x-W-r-X 1 obrien users 47 Nov 27 13:31 buzz10
-rwxxrwx-- 1 obrien obrien 152 Nov 26 12:48 buzz2
-rwxxrwx-- 1 obrien obrien 116 Nov 26 14:07 buzz3
-rwxxrwx-- 1 obrien obrien 165 Nov 26 14:08 buzz4
```

```bash
$ `ls -l b* | tee some_file` # 无法看到重定向输出
$ `ls -l b* | tee some_file` # 通过管道传给 tee，它会执行两个操作
# (重定向和显示)
```

```bash
-r-x-W-r-X 1 obrien obrien 47 Nov 26 12:19 buzz
-rwxxrwx-- 1 obrien obrien 90 Nov 26 12:45 buzz1
-r-x-W-r-X 1 obrien users 47 Nov 27 13:31 buzz10
-rwxxrwx-- 1 obrien obrien 152 Nov 26 12:48 buzz2
-rwxxrwx-- 1 obrien obrien 116 Nov 26 14:07 buzz3
-rwxxrwx-- 1 obrien obrien 165 Nov 26 14:08 buzz4
```

```bash
$ `cat some_file` # 显示重定向文件的内容
-r-x-W-r-X 1 obrien obrien 47 Nov 26 12:19 buzz
-rwxxrwx-- 1 obrien obrien 90 Nov 26 12:45 buzz1
-r-x-W-r-X 1 obrien users 47 Nov 27 13:31 buzz10
-rwxxrwx-- 1 obrien obrien 152 Nov 26 12:48 buzz2
-rwxxrwx-- 1 obrien obrien 116 Nov 26 14:07 buzz3
-rwxxrwx-- 1 obrien obrien 165 Nov 26 14:08 buzz4
```

## `test`

### 描述
评估条件表达式。

### 语法
```
test [expression]
```

### 选项
无

### 奇之处
它与 `[` 相同。

### 示例
```bash
$ `test -x buzz` # buzz 是可执行的吗？
$ `print $?` # 是
0
$ `test -b buzz` # buzz 是块特殊文件吗？
$ `print $?` # 不是
1
$
```

## `time`

### 描述
对命令的执行进行计时。

### 语法
```
time [-p] command [argument...]
```

### 选项
- `-p` 将计时输出写入标准错误（可能在所有 UNIX 变体中均不可用）。

### 奇之处
C shell 有该命令的自己的版本。

### 示例
```bash
$ `time ls -b*`
buss buzz1 buzz10 buzz2 buzz3 buzz4
real 0m.02s # 经过时间
user 0m.00s # 用户模式处理时间
sys 0m.02s # 内核（系统）模式处理时间
$
```

## `touch`

### 描述
更新文件的访问和修改时间。

### 语法
```
touch [-acfm] [-r reference_file | -t time]...
```

### 选项
- `-a` 仅更改访问时间。
- `-m` 仅更改修改时间。
- `-r reference_file` 使用指定的文件代替当前时间。
- `-t time` 指定要使用的时间。

### 奇之处
它可以用来创建一个空文件。

### 示例
```bash
$ `ls -l -d*` # 注意日期
-rw-rw-r-- 1 obrien priem 22 Nov 27 00:32 do_funcy
$
$ `date` # 当前日期
Mon Nov 27 15:52:30 EST 2000
$
$ `touch do_funcy` # 更改文件的日期
$
$ `ls -l -d*` # 注意日期
-rw-rw-r-- 1 obrien priem 22 Nov 27 15:32 do_funcy
$
$ `touch denfile` # 创建空文件
$
```

```bash
$ `ls -l d*` # 注意大小
-rw-rw-rw-- 1 obrien users  Nov 27 15:33 denfile
-rw-rw-rw-- 1 obrien obrien 22 Nov 27 15:32 denfile
```

## `tr`

### 描述
翻译字符。

### 语法
```
tr [-cd] string1 string2
```

### 选项
- `-c` 补全字符集。
- `-d` 删除指定字符的出现次数。
- `-s` 将重复字符压缩为单个。

### 示例
```bash
$ `tr 'a-z' 'A-Z' << EOF`
hello
EOF
HELLO
```

## `trap`

### 描述
捕获信号。

### 语法
```
trap command [signal ...]
```

### 奇之处
C shell 有该命令的自己的版本。

### 示例
```bash
$ `trap 'echo EXIT' EXIT`
$ `exit`
Exiting
$
```

## `true`

### 描述
评估条件表达式。

### 语法
```
test [expression]
```

### 选项
无

### 奇之处
它与 `[` 相同。

### 示例
```bash
$ `test -x buzz` # buzz 是可执行的吗？
$ `print $?` # 是
0
$ `test -b buzz` # buzz 是块特殊文件吗？
$ `print $?` # 不是
1
$
```

## `typeset`

### 示例
```bash
$ `typeset -AZ10 zfod` # 变量 zfod 是右对齐，
$ # 零填充，10字符宽。
$
$ `zfod=23` # 初始化为23
$
$ `print $zfod` # 注意零填充
0000000023
$
```

## `ulimit`

### 官方描述
设置或显示资源限制。

### 语法
```
ulimit [-HSacdfmnstvw] limit
```

### 选项
- `-a` 列出当前限制。
- `-c` 显示核心储文件的最大大小。
- `-d` 显示数据区域的最大大小。
- `-f` 显示最大文件大小。
- `-m` 显示物理内存使用的限制。
- `-n` 显示同时打开文件的最大数量。
- `-s` 显示最大栈大小。
- `-t` 显示以秒为单位的最大 CPU 时间。
- `-v` 显示最大虚拟内存 (kb)。
- `-w` 显示最大交换区 (kb)（并非所有 UNIX 变体上均可用）。

### 特殊之处
`H` 和 `S` 选项指定设置给给定资源的硬限制还是软限制。
硬限制设置后无法增加。
软限制可以增加到硬限制的值。当超过软限制时会发出警告。尝试超过硬限制时也会发出错误。

### 示例
```bash
$ `ulimit -a`
time(seconds) unlimited
file(blocks) unlimited
data(kbytes) unlimited
stack 8192
memory(kbytes) unlimited
coredump(blocks) 1000000
ofiles(descriptors) 1024
vmask(kbytes) unlimited
$
```

## `umask`

### 官方描述
显示或设置文件模式掩码。

### 语法
```
umask [-S] [mask]
```
