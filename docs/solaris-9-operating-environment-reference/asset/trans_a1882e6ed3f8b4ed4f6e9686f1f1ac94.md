

# 诊断信息

文件名：无差异

两个版本相同。

请使用 SCCS help 命令获取其他消息的解释（参见 sccs-help(1)）。

# sccs-unget, unget — 撤销对 SCCS 文件的之前的 Get 操作

# 概览

```
/usr/ccs/bin/unget [-ns] [-r sid] s.filename.
```

# 描述

使用 SCCS unget 命令撤销在创建待定增量（delta）之前执行的 `get -e` 效果。

如果你使用目录名代替 `s.filename` 参数，该命令适用于该目录下的所有 s 文件。不可读的文件会产生错误；程序将继续处理下一个文件（如果有）。使用连字符 (-) 作为 `s.filename` 参数表示从标准输入读取文件名，每行一个 s.file。

# 选项

- -n 留留原本会被删除的检索版本。
- -s 抑制显示 SCCS 增量 ID (sid)。
- -r sid 当同时检出多个版本时，指定要中止哪个待定增量。如果指定的 sid 具有歧义，或者在需要时你从命令行中省略了它，则会产生诊断结果。

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| 可用性 | Sunswprot |

# 参见

sccs(1), sccs-delta(1), sccs-get(1), sccs-help(1), sccs-prs(1),
sccs-prt(1), sccs-rmdel(1), sccs-sact(1), sccs-diff(1), what(1),
sccsfile(4), attributes(5)

# 诊断信息

使用 SCCS help 命令获取解释（参见 sccs-help(1)）。

# sccs-val, val - 验证 SCCS 文件

# 概览

```
/usr/ccs/bin/val [-s] [-m name] [-r sid]
/usr/ccs/bin/val [-y type] s.filename.
```

# 描述

使用 SCCS val（验证）命令来确定指定的 s.files 是否符合指定参数的特征。val 在单条命令行上最多可以处理 50 个文件。
val 有一个特殊的连字符 (-) 参数，会读取标准输入直到检测到文件结束代码。每行都会被独立处理，就像命令行参数列表一样。
val 会为处理的每条命令行向标准输出生成诊断消息，并在退出时返回一个指定的 8 位代码。
val 返回的 8 位代码是所有可能错误的析取，即它可以被解释为位字符串（从左到右），其中设置的位解释如下：

- 位 0 = 缺少文件参数。
- 位 1 = 未知或损坏的选项。
- 位 2 = 损坏的 s. file。
- 位 3 = 无法打开文件或不是 s. file 格式。
- 位 4 = SCCS 增量 ID (sid) 无效或存在歧义。
- 位 5 = sid 不存在。
- 位 6 = %Y 与 -y 参数不匹配。
- 位 7 = %M 与 -m 参数不匹配。

val 可以在一个命令行上处理两个或多个文件，并相应处理多条命令行（当读取标准输入时）。在这种情况下，将返回一个聚合代码，该代码是为每个处理的命令行和文件生成的代码的逻辑或结果。

# 选项

- -s 抑制正常的错误或警告消息。
- -m name 将 name 与 s. file 中的 %M ID 关键字进行比较。
- -r sid 检查指定的 sid 是否歧义、无效或不在 s. file 中。
- -y type 将 type 与 %Y ID 关键字进行比较。

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| 可用性 | SUNsprot |

# 1242

# scp

# 参见

sccs(1), sccs-admin(1), sccs-delta(1), sccs-get(1), sccs-help(1), what(1), sccsfile(4), attributes(5)

# 诊断信息

使用 SCCS help 命令获取解释（参见 sccs-help(1)）。

# scp - 安全复制（远程文件复制程序）

# 概览

```
/bin/scp [-BpqvrC46] [-S program] [-P port] [-c cipher]
[-i identity_file] [-o option] [user@host1:] file1 [user2@nhost2:] file2 [...]
```

# 描述

使用 Solaris 9 操作系统环境中新增的 scp 命令在网络上的主机之间复制文件。该命令使用 ssh(1) 进行数据传输，并使用与 ssh(1) 相同的身份验证方式和相同的安全性。与 rcp(1) 不同，scp 在需要身份验证时会提示输入密码或短语。

任何文件名都可以包含主机和用户规范，以指示文件将复制到该主机或从该主机复制。允许两个远程主机之间的复制。

# 选项

- -4 仅限 IPv4 地址。
- -6 仅限 IPv6 地址。
- -B 选择批模式。（防止询问密码或短语）。
- -c cipher 指定用于加密数据传输的密码算法。此选项直接传递给 ssh(1)。
- -C 启用压缩。-C 选项直接传递给 ssh(1)。
- -i identity_file 指定用于公共认证的身份文件。
- -o option 传递选项。
- -P port 指定端口。
- -q 禁用进度显示。
- -r 递归复制。
- -S program 指定要使用的程序。

# 描述

任何文件名都可以包含主机和用户规范，以指示文件将复制到该主机或从该主机复制。允许两个远程主机之间的复制。

# 选项

- -4 仅限 IPv4 地址。
- -6 仅限 IPv6 地址。
- -B 选择批模式。（防止询问密码或短语）。
- -c cipher 指定用于加密数据传输的密码算法。此选项直接传递给 ssh(1)。
- -C 启用压缩。-C 选项直接传递给 ssh(1)。
- -i identity_file 指定用于公共认证的身份文件。
- -o option 传递选项。
- -P port 指定连接的端口。
- -q 禁用进度显示。
- -r 递归复制。
- -S program 指定要使用的程序。

# 参数

任何文件名都可以包含主机和用户规范，以指示文件将复制到该主机或从该主机复制。允许两个远程主机之间的复制。

# 描述

任何文件名都可以包含主机和用户规范，以指示文件将复制到该主机或从该主机复制。允许两个远程主机之间的复制。

# 选项

- -4 仅限 IPv4 地址。
- -6 仅限 IPv6 地址。
- -B 选择批模式。（防止询问密码或短语）。
- -c cipher 指定用于加密数据传输的密码算法。此选项直接传递给 ssh(1)。
- -C 启用压缩。-C 选项直接传递给 ssh(1)。
- -i identity_file 指定用于公共认证的身份文件。
- -o option 传递选项。
- -P port 指定连接的端口。
- -q 禁用进度显示。
- -r 递归复制。
- -S program 指定要使用的程序。

# 操作数

任何文件名都可以包含主机和用户规范，以指示文件将复制到该主机或从该主机复制。允许两个远程主机之间的复制。

# 描述

任何文件名都可以包含主机和用户规范，以指示文件将复制到该主机或从该主机复制。允许两个远程主机之间的复制。

# 选项

- -4 仅限 IPv4 地址。
- -6 仅限 IPv6 地址。
- -B 选择批模式。（防止询问密码或短语）。
- -c cipher 指定用于加密数据传输的密码算法。此选项直接传递给 ssh(1)。

# 状态

val 返回的 8 位代码是所有可能错误的析取，即它可以被解释为位字符串（从左到右），其中设置的位解释如下：

- 位 0 = 缺少文件参数。
- 位 1 = 未知或损坏的选项。
- 位 2 = 损坏的 s. file。
- 位 3 = 无法打开文件或不是 s. file 格式。
- 位 4 = SCCS 增量 ID (sid) 无效或存在歧义。
- 位 5 = sid 不存在。
- 位 6 = %Y 与 -y 参数不匹配。
- 位 7 = %M 与 -m 参数不匹配。

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| 可用性 | Sunsprot |

# script — 记录会话

# 概览

/usr/bin/script [-a] file

# 描述 

使用 script 命令记录在终端上显示的所有内容。如果未指定文件名，记录将保存在当前目录下的 `typescript` 中。

# 选项

- -a 将会话追加到文件而不是覆盖它。

# 示例 

以下示例通过默认启动 `script` 然后显示注释：

```
castle script
Script started on Thu Apr 01 16:34:25 1999
castle# who
winsor console Apr 01 07:53 (:0)
winsor pts/3 Apr 01 07:54 (:0.0)
winsor pts/4 Apr 01 07:54 (:0.0)
winsor pts/5 Apr 01 07:54 (:0.0)
winsor pts/6 Apr 01 07:54 (:0.0)
castle# ps -ef | grep script
winsor 491 408 0 16:34:25 pts/6 0:00 script
winsor 492 491 0 16:34:25 pts/6 0:00 script
winsor 497 493 0 16:34:36 pts/7 0:00 grep script
castle# ^D script, file is typescript
castle# more typescript
Script started on Thu Apr 01 16:34:25 1999
castle# who
winsor console Apr 01 07:53 (:0)
winsor pts/3 Apr 01 07:54 (:0.0)
winsor pts/4 Apr 01 07:54 (:0.0)
winsor pts/5 Apr 01 07:54 (:0.0)
winsor pts/6 Apr 01 07:54 (:0.0)
castle# ps -ef | grep script
winsor 491 408 0 16:34:25 pts/6 0:00 script
winsor 492 491 0 16:34:25 pts/6 0:00 script
winsor 497 493 0 16:34:36 pts/7 0:00 grep script
castle# ^D script done on Thu Apr 01 16:34:38 1999
castle# tami*
```
