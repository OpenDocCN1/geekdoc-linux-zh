
### 描述

使用 `SCCS help` 命令获取信息，用以进一步解释 `SCCS` 命令的错误、消息和警告。`help` 还提供了一些关于命令用法的信息。如果你未指定参数，`help` 将提示输入一个参数。参数可以是消息编号（通常出现在每个 `SCCS` 错误或警告消息后的括号内）或 `SCCS` 命令名。`help` 会响应消息的解释或命令的用法行。当所有其他方法都失败时，请尝试 `/usr/bin/help`。

`/usr/lib/help`
包含消息文本文件的目录。

### 属性
参阅 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNprot |

### 另见
`sccs(1)`, `sccs-admin(1)`, `sccs-cdc(1)`, `sccs-comb(1)`, `sccs-delta(1)`, `sccs-get(1)`, `sccs-prs(1)`, `sccs-prt(1)`, `sccs-rmdel(1)`, `sccs-sact(1)`, `sccs-scddiff(1)`, `sccs-unset(1)`, `sccs-val(1)`, `what(1)`, `sccsfile(4)`, `attributes`.

## sccs-prs, prs — 显示 SCCS 历史部分

### 概要
```
/usr/bin/prs [options] sfile
```

### 描述
使用 `prs` 命令获取 `SCCS` 历史信息。`prs` 还提供了一些关于命令用法的信息。如果你未指定参数，`prs` 将提示输入一个参数。参数可以是消息编号（通常出现在每个 `SCCS` 错误或警告消息后的括号内）或 `SCCS` 命令名。`prs` 会响应消息的解释或命令的用法行。当所有其他方法都失败时，请尝试 `/usr/bin/prs`。

`prs [options] sfile`

### 示例用法
使用 `prs` 命令显示 `sfile` 指定部分的 delta。

### 选项
在没有指定选项的情况下，`prs` 命令显示 `sfile` 中的每一行 delta。

- `-a` 显示所有 delta（见 `sccs-delta(1)`）。显示早于指定时间、并包含指定时间的所有 delta。
- `-e` 显示早于指定时间、并包含指定时间的所有 delta。
- `-date-time` 显示早于指定时间，并包含指定时间的所有 delta。
- `-c` 显示早于指定时间、并包含指定时间的所有 delta。
- `-1` 显示早于指定时间、并包含指定时间的所有 delta。
- `-dataspec` 显示早于指定时间、并包含指定时间的所有 delta。
- `-rs` 显示早于指定时间，并包含指定时间的所有 delta。

### 输出
`prs` 命令显示 `sfile` 中的每一行 delta。输出格式如下：`R`, `L`, `B`, `S`, `U`, `M`, `D`, `C`, `I`, `J` 出现在列中。数据关键字可能在输出中出现多次。

| 关键字 | 数据项 | 章节 |
| --- | --- | --- |
| A | Availability | SUNprot |
| B | 分支号 | nnnn |
| C | 注释 | text |
| D | 创建日期 | nn |
| Dm | 创建月份 | nn |
| Dn | 的 delta (序列号) | DS... |
| Dy | 创建日期 | nn |
| Dx | 排除的 delta (序列号) | DS... |
| I | sid | R::L::B::S |
| J | 联合编辑标志 | 是/否 |
| KF | 关键字错误/警告标志 | 是/否 |
| L | 级别 | nnnn |
| Ld | 删除的 delta | nnnnn |
| Li | 插入的 delta | nnnn |
| LK | 锁定版本 | R... |
| Lu | 未更改的 delta | nnnnn |
| M | 模块名称 | text |
| MF | 验证标志 | 是/否 |
| MP | 验证程序 | text |
| MR | delta 的数字 | text |
| ND | 空 delta 标志 | 是/否 |

| 关键字 | 数据项 | 文件章节 | 取值 |
| --- | --- | --- | --- |
| Dm | 创建月份 | nn | S |
| Dn | 的 delta (序列号) | DS... | S |
| DP | 前驱 delta 序列号 | nnnn | S |
| Ds | 默认 sid | F | S |
| DS | delta 序列号 | nnnn | S |
| Dt | delta 信息 | I::T:P :DS | S |
| DT | delta 类型 | D 或 R | S |
| Dx | 排除的 delta (序列号) | DS... | S |
| Dy | 创建年份 | nn | S |
| F | sfile | N/A | S |
| FB | 底部边界 | R: | S |
| FD | 文件描述性文本 | C | M |
| FL | 标志列表 | F | M |
| FT | 获取的正文 | B | M |

`sccs-prs`, `prs`

| 关键字 | 数据项 | 文件部分 | 值 | 格式 |
|---|---|---|---|---|
| :Q: | 用户定义的关键字 | F | text | S |
| :P: | 创建增量的用户 | D | username | S |
| :PN: | s. 文件路径名 | N/A | text | S |
| :R: | 版本号 | D | nnnn | S |
| :S: | 序列号 | D | nnnn | S |
| :T: | 创建的时间差 | D | :Th::Tm::Ts: | S |
| :Th: | 创建的小时差 | D | nn | S |
| :Tm: | 创建的分钟差 | D | nn | S |
| :Ts: | 秒差 | D | nn | S |
| :UN: | 用户名 | U | text | M |
| :W: | 某种字符串的形式 | N/A | :Z:M\t:I: | S |
| :Y: | 模块类型标记 | F | text | S |
| :Z: | 字符串分隔符 | N/A | @(#) | S |

### 示例

以下命令：

```
castle% /usr/ccs/bin/prs -e -d":I\t:P:" program.c
```

产生：

- 1.6 username
- 1.5 username
...

## 文件

```
/Temp/pr/?????
```

临时文件。

### 属性

参见 `attributes(5)` 以了解以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNwsprot |

## sccs-prt, prt

### 相关
`sccs(1)`, `sccs-cdc(1)`, `sccs-delta(1)`, `sccs-get(1)`, `sccs-help(1)`, `sccs-prt(1)`, `sccs-sact(1)`, `sccs-sccsdiff(1)`, `what(1)`, `sccsfile(4)`, `attributes(5)`

### 诊断

使用 `SCCS help` 命令解释（参见 `sccs-help(1)`）。

# sccs-prt, prt — 显示 SCCS 文件的增量表信息

### 概要

```
/usr/ccs/bin/prt [-abdefistu] [-c date-time] [-r date-time] [-y sid] s.filename...
```
