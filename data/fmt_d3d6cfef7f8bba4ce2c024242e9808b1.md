
| Availability CSI | SUNwscplo |

| CSI | 已启用 |

## 参见

`lp(1)`, `lpstat(1)`, `lpc(1B)`, `lpq(1B)`, `pr(1)`, `lpadmin(1M)`, `printers(4)`,

`inters.conf(4)`, `attributes(5)`, `standards(5)`

# lpstat — 显示状态信息

## 概要

```
/usr/bin/lpstat [-d] [-r] [-s] [-t] [-a] [-c] [-f] [-u]
```

## 描述

`lpstat` 显示打印队列当前状态。如果不指定选项，`lpstat` 输出所有请求的状态。任何非选项参数均被视为请求 ID（参见 `lp`）。`lpstat` 命令打印此类请求的状态。您可以按任意顺序指定选项并使用 `-u [login-ID-list]` 打印用户的状态。`login-ID-list` 参数可以包括以下两种形式：用逗号分隔的项目列表，或者引号内用空格分隔的项目列表。例如：

## 736

## lpstat

```
castle% lpstat -u "user1 user2 user3"
```

在任何字母后跟列表作为参数将打印与字母相关的信息。例如，以下命令打印所有请求的状态。

```
castle% lpstat -o
```

在此类字母后省略列表将打印与字母相关的信息。例如，以下命令打印所有请求的状态。

```
castle% lpstat -o
```

打印客户端按特定顺序查找打印机信息。详情参见 `printers.conf(4)` 和 `printers(4)`。

## 选项

- `-d` 打印输出请求的默认目标。
- `-o [list]` 打印请求的状态。`list` 是一个混合打印机名称、类名和请求 ID 的列表。您可以省略字母。使用原子性、POSIX 类型(`server:destination`)或联邦命名服务 (FNS)(`../service/printer/...`) 指定打印机和类名。关于原子和 FNS 名称命名规范的信息请参见 `printers.conf(4)`，以及标准。
- `-r` 打印 LP 调度器的状态。
- `-R` 打印每个请求在打印队列中的位置数字。
- `-s` 打印状态摘要，包括 LP 调度器的状态、默认目标、打印机及其关联设备列表、共享打印系统的列表、当前安装的所有格式列表，以及所有识别的字符集和打印轮列表。
- `-t` 打印所有状态信息。这包含了通过 `-s` 选项获得的所有信息，加上所有打印机的接受和空闲/忙碌状态。
- `-u [login-ID-list]` 打印用户输出请求的状态。`login-ID-list` 参数可以包括或或全部：
  - `login-ID` 任意系统上的用户。
  - `system-name!login-ID` `system-name` 上的任意用户。
  - `system-name!all` `system-name` 上的所有用户。
  - `all!login-ID` 所有系统上的用户。

## lpstat

- `-v [list]` 打印打印机名称以及与其关联的设备路径名称或打印打印系统名称。`list` 是打印机名称列表。

以下选项仅在从 Solaris 2.x LP 打印服务器发出时才会返回准确结果。

- `-a [list]` 报告打印目标是否接受请求。`list` 是打印机名称和类名混合的列表。
- `-c [list]` 打印所有类及其成员名称。`list` 是类名列表。
- `-f [list][-1]` 验证 `list` 中的表单是否被 LP 打印服务识别。`list` 是表单列表；默认值为所有。`-1` 选项列出表单描述。
- `-p [list][-D]` 打印打印机状态。`list` 是打印机名称列表。如果指定了 `-D` 选项，则为列表中的每个打印机打印简短描述。如果指定了 `-1` 选项且打印机在本地系统中，则返回每台打印机配置的完整描述，包括挂载的表单、允许的内容和打印机类型、打印机描述以及使用的接口。
- `-S [list][-1]` 验证字符集或打印轮是否被 LP 打印服务识别。`list` 中的项可以是字符集或打印轮；列表默认值为所有。如果指定了 `-1` 选项，则在每个项后附加处理该打印轮或字符集的打印机列表。此列表还显示打印轮或字符集是否已挂载，或指定其映射的内置字符集。
- `-d` 打印输出请求的目标。
- `-o [list]` 打印输出请求的状态。`list` 是打印机名称、类名和请求 ID 的混合列表。你可以省略键字母 `-o`。
- `-r` 打印 LP 请求调度器的状态。
- `-R` 打印显示每个请求在打印队列中位置的数字。
- `-s` 打印状态摘要，包括 LP 调度器状态、默认目标、打印机及其关联设备列表、共享打印服务的系统列表、当前挂载的所有表单列表，以及所有已识别的字符集和打印轮列表。

# Ipstat

- `-t` 打印所有状态信息，包括通过 `-s` 选项获得的所有信息，以及所有打印机的接受和空闲/忙碌状态。
- `-u [login-ID-list]` 打印用户的输出请求状态。`login-ID-list` 参数可以包含以下任何或所有构造：
    - `login-ID` 任意系统上的用户
    - `system-name!login-ID` 某系统上的用户
    - `system-name.!all` 某系统上的所有用户
    - `all!login-ID` 所有系统上的用户
    - `all` 所有系统上的所有用户
- `-v [list]` 打印打印机名称以及与其关联的设备路径名称或远程系统打印机。`list` 是网络打印机的打印机名称列表。

## Exit Status

- `0` 成功完成。
- 非零 发生错误。

## Files

```
/var/spool/print/*
```
LP 打印队列。
```
$HOME/.printers
```
用户可配置打印机数据库。
```
/etc/printers.conf
```
系统配置数据库。

## Attributes

有关以下属性的描述请参见 `attributes(5)`：

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNWpccu |

## See Also

`cancel(1)`, `lp(1)`, `lpq(1B)`, `lpr(1B)`, `lrm(1B)`, `printers(4)`, `printers.conf(4)`, `attributes(5)`, `standards(5)`

# Iptest

## Iptest — 生成行打印波纹图

### Synopsis

```
/usr/ucb/lptest [length [count]]
```

## Description

`lptest` 将传统的波纹测试模式写入标准输出。在 96 行中，波纹测试模式在每个位置打印所有 96 个可打印的 ASCII 字符。波纹测试模式最初用于测试打印机。它也用于测试终端、驱动终端端口、调试以及需要快速提供随机数据的任务。

> Note — 此命令已过时。

### Options

- `length` 指定输出行的字符长度。默认为 79 个字符。
- `count` 指定输出的行数。默认为 200 行。如果指定了 `count`，则必须也指定 `length`。

### Exit Status

- `0` 成功完成。
- 非零 发生错误。

### Attributes

有关以下属性的描述请参见 `attributes(5)`：

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNwscplp |

### See Also

`attributes(5)`

# ls — 列出目录内容

### Synopsis

```
/usr/bin/ls [-aAbCCdfFfgIlLmnopqrRstux1][file...]
/usr/xpg4/bin/ls [-aAbCCdfFfgIlLmnopqrRstux1][file...]
/usr/ucb/ls [-aAcCdfFfgIlLqrRstu1] file...
```

## Description

使用 `ls` 命令列出目录内容，并显示文件的权限、链接、所有者、组、大小（字节）、修改日期和时间以及文件名。

对于每个目录文件，`ls` 会列出目录的内容；对于每个普通文件，`ls` 会重复其名称和任何其他信息。

最后，连字符字母告诉您用户、组和其他人具有读取、写入和执行权限（见第2部分）。

**注意** — 文件名中的不可打印字符可能会导致列输出选项出现混淆。

如果列之间存在硬链接，则总块数是不的。

## 选项

- `-a` 列出所有项，包括以点（`.`）开头的项，这些项通常不会被列出。
- `-A` 列出所有项，包括以点（`.`）开头的项，但当前目录（`.`）和父目录（`..`）除外。
- `-b` 强制将不可打印字符以条进制 `\ddd` 符号打印。
- `-c` 使用 inode 的最后修改时间（文件创建、修改更改等）进行排序 (`-t`) 或打印 (`-l` 或 `-n`)。
- `-C` 显示多列输出，并按列向下对项进行排序。这种格式是默认格式。
