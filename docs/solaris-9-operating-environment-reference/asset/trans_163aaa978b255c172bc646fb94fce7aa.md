

# 环境变量

参阅 environ(5) 以了解以下影响 grep 执行的环境变量的描述：LC_COLLATE、LC_CTYPE、LC_MESSAGES 和 NLSPATH。

# 退出状态

- 0 找到一个或多个匹配项。
- 1 未找到任何匹配项。
- 2 语法错误或文件无法访问（即使找到了匹配项）。

# 属性

参阅 attributes(5) 以了解以下属性的描述：

# /usr/bin/grep

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNfac |

# /usr/xpg4/bin/grep

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNfac |

# 相关命令

egrep(1), fgrep(1), sed(1), sh(1), attributes(5), environ(5), largefile(5), regex(5), regexp(5), XPG4 (5)

# groups — 打印用户组组成

# 概要

```
/usr/bin/groups [user...]
```

# 描述

groups 命令在标准输出上打印你或可选指定的用户所属的组。每个用户属于 /etc/passwd 中指定的组，并可能属于 /etc/group 中指定的其他组。注意，/etc/passwd 指定了组的数值 ID (gid)。groups 命令在输出中将 gid 转换为组名。

# grpck

# 示例

以下示例显示了用户 winsor、ray 和 des 的组信息。
castle% groups winsor ray des
winsor : staff other sysadmin
ray : staff other sysadmin
des : staff sysadmin
castle%

# 文件

/etc/passwd 密码文件。
/etc/group 组文件。

# 属性

参阅 attributes(5) 以了解以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWcsu |

# 相关命令

group(4), passwd(4), attributes(5)

# grpck — 密码/组文件检查器

# 概要

/usr/bin/grpck [filename]

# 描述

参阅 pwck(1)。

# gunzip — 压缩或解压文件

# 概要

/bin/gunzip [-acfhlNnrtvV] [-S suffix] [name...]

# 描述

参阅 gzip(1)。

# gzcat — 压缩或解压文件

# 概要

```
/bin/gzcat [-fHLV] [name...]
```

# 描述

参阅 gzip(1)。

# gzcmp, gzdiff — 比较压缩文件新！

# 概要

```
/bin/gzcmp [cmp_options] file [file2]
/bin/gzdiff [diff_options] file [file2]
```

# 描述

gzcmp 和 gzdiff 是 Solaris 8 操作系统环境中新出的命令，用于在压缩文件上调用 cmp 或 diff 程序。所有指定的选项都直接传递给 cmp 或 diff。当你只指定一个文件时，比较的文件是该文件和一个未压缩的 file.gz。当你指定两个文件时，会在必要时对它们进行解压缩并送给 cmp 或 diff。cmp 或 diff 的退出状态将被保留。

# 属性

参阅 attributes(5) 以了解以下属性的描述。

| 属性类型 | 属性值 |
|---|---|
| 可用性 | Sunzip |

# 相关命令

cmp(1), diff(1), gzforce(1), gzip(1), gzmore(1), gznew(1), gzxexe(1)

# 错误

来自 cmp 或 diff 的信息指的是临时文件名，而不是指定的名称。

# gzdiff — 比较压缩文件新！

# 概要

```
/bin/gzdiff [diff_options] file [file2]
```

# gzexe

参阅 gzcmp(1)。

# gzexe — 原地压缩可执行文件

# 概要

```
/bin/gzexe [name...]
```

# 描述

使用 gzexe 命令原地压缩可执行文件，并在你运行它们时会自动解压（会有性能损失）。例如，执行 gzexe /bin/cat 会创建以下两个文件：
```
-r-xr-x 1 bin 964 Feb 11 /bin/cat
-r-xr-x 1 bin 24576 Nov 23 /bin/cat
```
/bin/cat 是原始文件，而 /bin/cat 是自解压文件。一旦确认 /bin/cat 工作正常，就可以删除它。此命令对于磁盘空间非常小的系统很有用。

# 选项

- -d 解压给定的可执行文件而不是压缩它们。

# 属性

参阅 attributes(5) 以了解以下属性的描述。

| 属性类型 | 属性值 |
| 可用性 | SUNzip |

# 相关命令

gzcmp(1), gzforce(1), gzip(1), gzmore(1), gznew(1)

# 注意事项

可执行文件是一个 shell 脚本。该脚本可能会产生某些安全漏洞。特别是，该可执行文件依赖 PATH 环境变量来查找 tail、ln 和 sleep 等其他命令。

# 错误

gzexe 尝试保留可执行文件的原始属性，但在某些情况下，你可能需要手动用 chmod 或 chown 修复它们。

# gzforce — 为所有文件强制添加 .gz 后缀

# 概要

/bin/gzforce [name...]

# 描述

使用 Solaris 8 操作系统环境中新出的 gzforce 命令强制为所有文件添加 .gz 后缀，以防止 gzip 不对它们进行二次压缩。此命令对于在文件传输后名称被截断的文件有用。在文件名限制为 14 个字符的系统上，原始名称会被截断以为 .gz 后缀留空间。例如，名为 foo 的名称将保持不变。

# 属性

参阅 attributes(5) 以了解以下属性的描述。

| 属性类型 | 属性值 |
| 可用性 | SUN |

# 相关命令

gzdiff(1), gzexe(1), gzgrep(1), gzip(1), gzmore(1), gznew(1)

# gzip, gunzip, gzcat — 压缩或解压文件

# 概要

```
/bin/gzip [-acfhlNrtvV] [-S suffix] [name...]
/bin/gunzip [-acfhlNrtvV] [-S suffix] [name...]
/bin/gzcat [-fhlV] [name...]
```

# 描述

使用 gzip 命令（SUN 包可用）缩小文件大小，使用 Lempel-Ziv 编码（LZ77）。

> 注意 — gzip 适用于文件。

在可能的情况下，每个文件将被替换为扩展名为 .gz 的文件，并保持相同的所有者、访问和修改时间。对于 VMS，默认扩展名为 -gz。对于 MS-DOS/OS FAT、Windows FAT 和 Atari，默认扩展名为 z。当你未指定文件或文件名为 - 时，标准输入被压缩到标准输出，gzip 尝试压缩普通文件。它忽略符号链接。如果压缩文件名对于文件系统过长，gzip 尝试对其进行截断。gzip 会截断超过 3 个字符的部分。如果名称由相同部分组成，长部分将被截断。例如，如果文件名限制为 14 个字符，mdos.exe 被压缩为 gzi.msexe。在没有文件名长度限制的系统上，名称不会被截断。

默认情况下，gzip 在压缩文件中保留原始文件名和时间戳。当使用 -N 选项解压时会使用这些。此功能对于文件名被截断或文件传输后时间戳丢失的情况有用。

你可以通过 gzip -d、gunzip 或 gzcat 将文件恢复原始格式。如果压缩文件中保存的原始名称不适用于文件系统，将根据原始名称构造一个新的合法的名称。

gzip 将命令行上的每个以 .gz、-gz、-z 或 .Z 结尾或以正确的魔数开头的文件替换为没有原始扩展名的未压缩文件。gzip 还识别特殊扩展 .tgz 和 .z 作为 .tar.gz 的缩写。

gzcat 等同于 gunzip -c。（在某些系统上，zcat 可能安装为 gzcat 以保留原始文件行。）

文件只有在使用 deflation 方法压缩的单个成员才能被 gzip 压缩。此功能有助于将 tar.zip 转换为 tar.gz。提取多个成员的文件请使用 unzip 代替 gunzip。

gunzip 可以通过 gzip、gunzip、compress -H 或 pack 解压缩文件。输入格式检测是自动的。对于两种格式，gunzip 检查 32 位 CRC。对于 pack，gunzip 检查未压缩长度。标准格式设计时并未允许一致性检查；然而，gunzip 有时会检查输入并在压缩损坏的 .z 文件时仍然产生垃圾输出。

