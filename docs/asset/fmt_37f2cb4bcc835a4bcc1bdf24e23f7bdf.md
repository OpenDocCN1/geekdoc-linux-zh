
``` 
runtimes 1               # 单次 amanda 运行中使用的
                          # 磁带数量
tapedev "/dev/nrft0"      # 使用的不回带磁带设备
rawtaped "/dev/rft0"     # 使用的原始设备（仅 ftape）
```

``` 
tapetype HP-DAT       # 磁带类型
                          #（参见下文 tapetype）
                          # label constraint all
labelstr "^[0-9] [0-9]*$
                          # 磁带必须匹配
```

# 指定持有磁盘。这些用作 dump 写入磁带

# 之前的临时暂存区域，

# 建议大多数站点使用。

``` 
holdingdisk hdl {
  comment "main holding disk"
  directory "/home/amanda"  # 持有磁盘的位置
  use 290 Mb                  # 可以使用多大空间
  chunksize -1               # 块大小
}
```

# 注意，虽然下面的关键字是 infofile，但

# 只是历史原因如此，因为现在它被认为

# 是目录（除非你选择了除了默认'text'以外的

# 数据库格式）

``` 
infile "/var/lib/amanda/normal/curinfo"  # 数据库 目录
logdir "/var/lib/amanda/normal"  # 日志目录
indexdir "/var/lib/amanda/normal/index"  # 索引目录
```

## tapetype

# 在此处定义你使用的磁带类型，并在上面的 "tapetype"

# 中引用。这里包含了一些典型的磁带类型。

# tapetype 告诉 amanda MB 如何存放在磁带上，

# 文件标记有多大，以及磁带设备有多快。

``` 
define tapetype HP-DAT {
  comment "DAT 磁带驱动器"
  # 由 Rob Browning <rlb@cs.utexas.edu> 提供的数据
  length 1930 mbytes
  filemark 311 kbytes
  speed 468 kbytes
}
```

## dumptypes

#

# 这些由 dumplist 文件引用。

``` 
define dumptype global {
  comment "全局定义"
  # 这对于设置全局参数非常有用，这样你就
  # 不必到处都输入它们。
}
```

``` 
define dumptype always-full {
  global
  comment "始终对此文件系统进行完整 dump"
  compress none
priority high
dumpcycle 0
}
```

此 `amanda.conf` 示例文件是从 `/etc/amanda/DailySet1` 目录复制的较大示例中简化而来的。示例 `amanda.conf` 文件提供了可用配置选项的额外信息。此外，Amanda 的在线 man 页面应该很有帮助（输入 `man amanda` 读取它）。你可以在 `/usr/share/doc/amanda-server/` 目录中找到更多指令。通常，你必须执行以下操作：

- 修改报告的 org 名称。
- 更改 `tapedev` 和 `rawtaped` 的设备名称以匹配你的磁带设备。
- 选择适用于你的驱动器设备的磁带类型条目。
- 修改持有磁盘中指定的目录名称以匹配你的目录。

## 创建 disklist 文件

你还必须在 `/etc/amanda/normal` 目录下创建 `disklist` 文件。它仅包含要备份的系统和分区的列表。每个条目都包含 `always-full` 限定符，以告诉 Amanda 备份什么。为了方便解释，示例 `amanda.conf` 文件中嵌入了一些值：

（注：由于原文后半部分存在大量重复且逻辑混乱的文本，已根据“不要重复输出原文”的原则，仅对核心内容进行了翻译处理。）

## 第 13 章：文件的备份与恢复 573

`pax` 程序是一个 POSIX 标准实用程序，可以读取和写入多种归档格式。Fedora 和 RHEL 都自带了 `pax` 的 RPM 软件包。如果尚未安装，要获取最新版本的 `pax`（前提是您已连接互联网），请以 root 用户身份输入以下命令：

```bash
# yum install pax
```

如果你没有连接互联网，请挂载包含 Fedora 或 RHEL 发行版的 CD/DVD，切换到 RPMS 目录，然后使用 `rpm` 命令安装 `pax`。

```bash
# rpm -Uhv pax-*
```

请记住，使用 `rpm` 命令安装软件时，您需要以 root 身份登录。`pax` 的最后一个参数通常是要归档的文件或目录。`Pax` 接受多种命令行选项。你可以使用诸如 `*` 或 `?` 等通配符来指定多个文件或目录。使用的选项通常必须包含 `-r` 和 `-w` 参数，用于指定你是在读取还是写入归档。这些参数通常与 `-f` 参数配合使用，用于指定归档文件的名称。

通过以不同的组合使用 `pax` 参数，可以提取归档、列出归档内容或从一个位置复制整个目录层次结构。表 13-8 显示了 `pax` 命令的实际用法示例。

### 表 13-8：pax 使用示例

| Pax 命令 | 说明 |
|---|---|
| `pax -f myfiles` | 列出名为 `myfiles` 的归档内容。 |
| `pax -r -f myfiles` | 提取名为 `myfiles` 的归档内容。 |
| `pax -w -f myfiles /etc` | 创建一个名为 `myfiles` 的归档，包含 `/etc` 目录下的所有内容。 |
| `pax -w -f myfiles *.txt` | 归档当前目录下所有 `.txt` 扩展的文件。 |
| `pax -r -w /olddir /newdir` | 将 `/olddir` 目录的内容复制到新目录 `/newdir` 中。 |
| `pax -w -B 1440000 -f /dev/fd *` | 将当前目录的内容归档到多块软盘上。 |
| `pax -w -x cpio -f myfiles *` | 使用 `cpio` 格式将当前目录的内容归档到名为 `myfiles` 的归档文件中。 |
| `pax -r -U mary -f backups` | 从名为 `backups` 的归档中提取所有由用户 `mary` 拥有的文件。 |

注意，如果同时省略 `-r` 和 `-w` 选项，会导致 `pax` 仅列出归档的内容。如果你同时指定 `-r` 和 `-w` 选项，则应该省略 `-f` 选项并提供源和目的目录。这将导致源目录在指定的目的地被完全克隆。

你可以使用额外的参数来进一步修改 `pax` 命令的行为。例如，你可以结合 `-x` 选项和 `-w` 选项指定特定的归档类型，或使用 `-B` 选项指定写入每个多卷归档卷卷的字节数。

表 13-9 描述了 `pax` 命令的许多参数。

### 表 13-9：pax 选项

| Pax 选项 |  |
| --- | --- |
| `-r` | 从归档读取文件。 |
| `-w` | 将文件写入归档。 |
| `-a` | 将文件追加到以前创建的归档中。 |
| `-b blocksize` | 指定归档的数据块大小。它必须是 512 的倍数。 |
| `-c pattern` | 匹配所有除指定模式以外的文件。 |
| `-d` | 仅将文件名与文件或目录名匹配，不匹配完整路径。 |
| `-f archive` | 指定归档名称。 |
| `-i` | 在归档时交互式重命名文件。 |
| `-k` | 不覆盖现有文件。 |
| `-l` | 在复制模式 `-r -w` 下使用硬链接链接文件。 |
| `-n pattern` | 仅匹配提供模式的第一个文件。 |
| `-o options` | 特定于所用归档格式的额外选项。 |
| `-p string` | 指定归档或复制时保留的文件特性。有关此选项的更多信息请阅读 `pax` man 手页。 |
| `-s replstr` | 使用提供的正则表达式修改归档的文件名。 |
| `-t` | 保留归档文件的访问时间。 |
| `-u` | 不用旧版本覆盖文件。 |
| `-v` | 运行时提供详细输出。 |
| `-x format` | 指定归档格式。有效格式包括 `cpio`, `bcpio`, `sv4cpio`, `sv4crc`, `tar` 和 `ustar`。创建归档时默认使用 `ustar`。`Pax` 在读取归档时会自动确定正确的文件类型。 |
| `-z` | 表示应使用 `gzip` 压缩和解压归档。 |
| `-B bytes` | 指定每个归档卷的字节数。使用此选项在移动介质上创建多卷归档。 |
| `-D` | 不用修改时间较旧的文件覆盖现有文件。 |
| `-E limit` | 限制 `pax` 在遇到读取或写入错误时的重试次数。 |
