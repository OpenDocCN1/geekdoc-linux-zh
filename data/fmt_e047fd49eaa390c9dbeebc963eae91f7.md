
castle% `tip monet`

[connected]

...(假设我们正在与一个 UNIX 系统通信)...

`cubmon login:` `sam`

Password:

`monet%` `cat > sylvester.c`

-> Filename: `sylvester.c`

32 lines transferred in 1 minute 3 seconds

`monet%`

`monet%` - Filename: `reply.c`

List command for remote host: `cat reply.c`

65 lines transferred in 2 minutes

```
```

`monet%`

...(或者等价于)...

`monet%` `-p sylvester.c`

...(实际上显示为 ~[put] `sylvester.c`)...

32 lines transferred in 1 minute 3 seconds

`monet%`

`monet%` `-t reply.c`

...(实际上显示为 ~[take] `reply.c`)...

65 lines transferred in 2 minutes

`monet%`

...(为了在本地打印文件)...

`monet%` ~[Local command: `pr -h sylvester.c | lpr`

List command for remote host: `cat sylvester.c`

`monet%` ^-D

[EOT]

...(回到本地系统)...

```

## 环境变量

`tip` 会读取以下环境变量。

- `REMOTE` 远程文件的位置。
- `PHONES` 包含私有电话号码的文件位置。
- `HOST` 默认连接的主机。
- `HOME` 用户登录目录（用于 `chdirs`）。
- `SHELL` 在执行 `~` 转义时用于 `fork` 的 `shell`。

## 文件

```
/etc/phones

/etc/remote

/var/spool/locks/LCK ..*

/var/adm/aculog

~/.tiprc
```

> 用于避免与 UUOCP 冲突的锁文件。

用于记录拨出电话的文件。

初始化文件。

## 属性

后续属性的描述请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | `SUNWcsu` |

# 1350

# `tnfdump`

## 相关

`mail(1)`, `vi(1)`, `cu(1C)`, `uucp(1C)`, `ioctl(2)`, `attributes(5)`

# Bug

两个额外的变量 `chordelay` 和 `linedelay` 目前尚未实现。

# `tnfdump` — 将二进制跟踪范式 (TNF) 文件转换为 ASCII

# 概览

`/usr/bin/tnfdump [-r] tnf-file...`

## 描述

使用 `tnfdump` 命令将指定的二进制跟踪范式 (TNF) 跟踪文件转换为 ASCII。你可以用它进行性能分析。默认模式（不带 `-r` 选项）仅打印所有事件记录（由 `TNF_PROBE(3X)` 生成）和事件描述记录。它还会按时间排序事件。

## 选项

- `-r` 执行 TNF 到 ASCII 的原始转换。将输出视为二进制 TNF 文件的字面翻译，并包含文件中的所有记录。只有在你对 TNF 有良好理解时，此输出才有用。

## 示例

下面的示例将文件 `/tmp/trace-2130` 转换为 ASCII 以使用。输出使用了你的行；这些行被包含在这里。

```
cast tnfdump /tmp/trace-2130

probe tnf_name: "inloop" "keys cookie main loop;file

cookie2:c;line 50;swdewbeg in the loop

probe tnf_name: "end" tnf_string: "keys cookie main end;file

cookie2:c;line 41;swdewbeg exiting
```

| 已耗时间 (ms) | 增量 (ms) | PID LWPID | CPU 名称 | 数据 | 描述 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0.0000 | 0.0000 | 8792 | 1 | | inloop |
| 0.3300 | 0.3300 | 8792 | 1 | | inloop |
| 0.350500 | 0.011500 | 8792 | 1 | | inloop |

# 1351 # `tnump`

```
loop_count: 2

0.359500 0.009000 8792 | 1 | inloop

loop_count: 3

0.369500 0.010000 8792 | 1 | inloop

loop_count: 4

0.7759650 7775.6000 8792 | 1 | inloop

loop_count: 5

0.777601600 0.046500 8792 | 1 | inloop

loop_count: 6

0.777602500 0.009000 8792 | 1 | inloop

loop_count: 7

0.777603400 0.009000 8792 | 1 | inloop

loop_count: 8

0.777604300 0.009000 8792 | 1 | inloop

loop_count: 9

0.777605200 0.009000 8792 | 1 | inloop

loop_count: 10

0.777606100 0.009000 8792 | 1 | inloop

loop_count: 11

0.9475950 16.991800 8792 | 1 | end

node_struct: ( type: node_tnf_cur_sum: 12 )

max_cnt: 12
```

对于执行过程中遇到的所有 `probes` 都包含一个描述。描述以关键字 `tnf` 开头。`probe` 的名称位于关键字 `tnf_name` 之后并带有双引号。所有 `probes` 的描述都在双引号内。第一列显示自第一个事件以来的毫秒耗时间。第二列显示自上一个事件以来的毫秒时间。接下来的四列是 ID、LWP ID、线程 ID 和 CPU 编号。下一列是生成此事件的 `probe` 名称。你可以将 `probe` 与描述相匹配。最后一列是事件包含的数据，格式为 `arg_name_n`（参见 `TNF_PROBE(3X)`），随后是该参数的值。值的格式取决于其类型。`opaque` 参数以十六进制显示，所有其他整数以十进制显示，字符串用双引号显示，自定义记录包含在 `{}` 中。自定义记录的第一个字段指示其 TNF 类型（参见 `TNF_DECLARE_RECORD(3X)`），其余字段是记录的成员。

A - 表示该列没有数据。下面的示例将文件 `/tmp/trace-4000` 原始转换为 ASCII。

```
castle$ fndump -r /tmp/trace-4000

0x10e00 : (

tnf_tag 0x109c0 tnf_block_header

  generation 1

  bytes_valid 320

  A_lock 0

  B_block 0

  next_block 0x0

)

0x10e10 : (

tnf_tag 0x10100 probel

tnf_tag_arg 0x10e24 <tnf_sched_rec>

time_delta 128

test_ulong 4294967295

test_long -1

)

0x10e24 : (

tnf_tag 0x10cf4 tnf_sched_rec

tid 0

lwid 1

pid 13568

time_base 277077875828500

)

0x10e3c : (

probe2

tnf_tag 0x11010

tnf_tag_arg 0x10e24 <tnf_sched_rec>

time_delta 735500

test_str 0x10e48 "string1"

)

0x10e48 : (

tnf_tag 0x1072c tnf_string

tnf_self_size 16

chars "string1"

)

0x10e58 : (

tnf_tag 0x11ec probe3

tnf_tag_arg 0x10e24 <tnf_sched_rec>

time_delta 8680000

test_ulonglong 1844674403709551615

test_longlong -1

test_float 3.1428587

)

...

0x110ec : (

tnf_tag 0x10030 tnf_probe_type

tnf_tag_code 42

tnf_name 0x1101c "probe3"

tnf_properties <tnf_properties>
