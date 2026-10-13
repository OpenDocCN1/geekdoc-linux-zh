
# atoplot — 各种绘图器的图形过滤器

### 概要

```
/usr/ucb/plot [-Tterminal]
```

## 描述

参阅 `plot(1)`。

# atq — 显示在指定时间运行的任务

### 概要

```
/usr/bin/atq [-n] [username...]
```

## 描述

使用 `atq` 命令显示当前用户由 `at(1)` 命令创建的 at 任务。如果你以超级用户身份运行该命令，`atq` 将显示队列中的所有任务。

如果不使用任何选项，任务将按执行的时间顺序显示。

当超级用户在不指定用户名的情况下使用 `atq` 命令时，将显示整个查询结果；当你指定用户名时，则只显示属于该用户的任务。

## 选项

- `-c` 按照任务创建的顺序（即调用 `atq` 命令的时间）显示队列任务。
- `-n` 仅显示当前队列中的任务总数。

## 示例

以下示例显示了不带参数的 `atq` 命令的输出。列表仅显示当前用户 winsor 的任务。

```
castle$ atq
Rank Execution Date Owner Job Queue Job Name
1st Aug 28, 1998 17:00 winsor 90429800.a a try
2nd Aug 29, 1998 01:00 winsor 90432600.a a try
3rd Aug 29, 1998 07:30 winsor 90434700.a a stdin
4th Aug 30, 1998 15:00 winsor 90446040.a a try
```

作为对比，以下示例显示了 `at` 命令的输出，它也列出了队列中的 at 和 batch 任务。

```
castle$ -1
90437000.a Sat Aug 29 07:30:00 1998
90429800.a Fri Aug 28 17:00:00 1998
90432600.a Sat Aug 29 01:00:00 1998
90446040.a Sun Aug 30 15:00:00 1998
```

以下示例显示了以超级用户身份执行 `atq` 命令时的输出。

```
castle$ su
Password:
castle$ atq Execution Date Owner Job Queue Job Name
1st Aug 28, 1998 16:00 root 90429120.a a try
2nd Aug 28, 1998 17:00 winsor 90429840.a a try
3rd Aug 28, 1998 18:00 winsor 90429840.a a try
4th Aug 28, 1998 19:00 ray 90430200.a a try
5th Aug 28, 1998 21:00 ray 90430920.a a try
6th Aug 29, 1998 01:00 winsor 90432600.a a try
7th Aug 29, 1998 07:30 winsor 90434700.a a stdin
8th Aug 30, 1998 15:00 winsor 90446040.a a try
```

以下示例按创建时间排序了相同的内容。

```
castle$ -c
Rank Execution Date Owner Job Job Name
1st Aug 29, 1998 07:30 winsor 90434700.a a stdin
2nd Aug 28, 1998 17:00 winsor 90429840.a a try
3rd Aug 29, 1998 01:00 winsor 90432600.a a try
4th Aug 30, 1998 15:00 winsor 90446040.a a try
5th Aug 28, 1998 16:00 root 90429120.a a try
6th Aug 28, 1998 18:00 root 90429840.a a try
7th Aug 28, 1998 19:00 ray 90430200.a a try
8th Aug 28, 1998 21:00 ray 90430920.a a try
```

以下示例显示了 `atq -n` 返回的值。它仅列出队列中的数量。

```
castle# atq -n
8
castle#
```

以下示例显示了仅由 ray 队列的任务。

```
Rank Execution Date Owner Job Job Name
1st Aug 28, 1998 19:00 ray 90430200.a a try
2nd Aug 28, 1998 21:00 ray 90430920.a a try
castle#
```

## 文件

```
/var/spool/cron/atjobs
```

任务池区域。

## 属性

参阅 `attributes(5)` 了解以下属性的描述。

| 属性类型 | 属性值 |
|---|---|
| Availability | SUNWcsu |

## 另见

`at(1)`, `atrm(1)`, `cron(1)`, `attributes(5)`

# atrm — 删除 at 或 batch 缓存的任务

### 概要

```
/usr/bin/atrm [-afi] [[-job] [user] ...]
```

## 描述

使用 `atrm` 命令删除由 `at(1)` 命令创建尚未执行的延迟执行任务。你可以使用 `atq(1)` 显示这些任务和相关的任务号。

`atrm` 删除你指定的每个任务以及属于指定用户的所有，前提是你拥有这些任务或具有超级用户权限。

## 选项

- `-a` 删除当前用户创建的所有未执行任务。
- `-f` 强制抑制有关指定任务删除的信息。如果由超级用户调用，则清空整个队列。
- `-i` 交互式询问是否删除任务。如果你响应 y，则删除该任务。

## 示例

以下示例首先使用 `atq` 命令列出队列中的任务，然后以超级用户身份删除用户 ray 队列的任务。

| Rank | Execution Date | Owner | Job | Queue | Job Name |
|---|---|---|---|---|---|
| 1st | Aug 28, 1998 16:00 | root | 90429120.0 | a | try |
| 2nd | Aug 28, 1998 17:00 | winsor | 90429480.0 | a | try |
| 3rd | Aug 28, 1998 18:00 | root | 90429840.0 | a | try |
| 4th | Aug 28, 1998 19:00 | | 90430200.0 | a | try |
| 5th | Aug 28, 1998 21:00 | ray | 90430920.0 | a | try |
| 6th | Aug 29, 1998 01:00 | winsor | 90432600.0 | a | try |
| 7th | Aug 29, 1998 07:30 | winsor | 90434700.0 | a | stdin |
| 8th | Aug 30, 1998 15:00 | winsor | 90446040.a | a | try |

如果你想抑制删除任务列表列表，请使用 `atrm -f` 选项。

以下示例通过指定 at 任务删除任务。

```
castle$ atrm 90429120.a
90429120.a: removed
castle$
```

在以下示例中，超级用户使用 `atrm -i` 选项来交互式删除 winsor 队列的任务。

```
castle# atrm -i winsor
9043700.a: (owned by winsor) remove it? y
90429480.a: (owned by winsor) remove it? y
90432600.a: (owned by winsor) remove it? y
90446040.a: (owned by winsor) remove it? y
cast#
```

# audioconvert — 转换音频格式

### 概要

```
/usr/bin/audioconvert [-pF] [-f outfmt] [-o outfile] [[-i nfmt] [file...]] ...
```

## 描述

`audioconvert` 在一组支持的音频编码和文件格式之间转换音频数据。你可以用它压缩和解压缩音频数据，为原始音频文件添加音频头，并在标准数据编码（如 ulaw 和线性 PCM）之间进行转换。

如果没有文件名，`audioconvert` 从标准输入流读取数据并将音频文件写入标准输出。否则，输入文件将按顺序处理、合并并写入输出文件。

输入文件应包含识别音频数据格式的音频文件头。如果音频数据不包含可识别的头，你必须

## audioconvert 73
