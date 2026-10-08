

# zip, zipcloak, zipnote, zipsplit 1591

在 OS/2 上，zip 无法匹配某些名称，例如包含感叹号或井号。这是 OS/2 本身的问题：32 位的 DosFirst/Next 无法找到此类名称。GNU zip 等程序也受到此影响。

在 OS/2 下，DIR 显示的扩展属性（Extended Attributes）数量（为了兼容性）是 16 位版本的 `QueryPathInfo()` 返回的数量。否则，OS/2 1.2.0 在对文件使用该命令时会报告 EA 大小。32 位 `QueryPathInfo` 返回的结构布局略有不同；它使用了额外的填充和链接指针（这是一个链表），以确保在移植到未来的 RISC OS/2 版本时，所有边界都符合 4 字节对。因此，zip 返回的值（它使用这种 32 位模式的大小）与 OS/2 1.3 上的 16 位 MS-C 编译版本不同，即使是后者也显示的是 32 模式的大小。

Copyright (C) 1990-1997 Mark Adler, Richard B. Wales, Jeanel Gilly, Onno van der Linden. Kai Uwe Rome, Igor Mandrichenko, John Bush, and Paul Knitz.

允许任何个人或机构使用、复制或重新发布软件，前提是包含所有原始文件、非营利目的并保留此版权声明。

> 与任何其他免费软件一样，ZIP 及其相关工具按原样提供，不带任何形式的保证，无论是明示还是暗示的。版权持有者对使用本软件而导致的任何损害不承担责任。

请通过电子邮件向 zip-bugs@lists.wku.edu 发送错误报告和意见。对于错误报告，请包含 zip 的版本（见 `zip -h`）、编译时使用的选项（见 `zip -v`）、使用的机器和操作系统，以及尽可能多的额外信息。

# 感谢

感谢 R. P. Byrne 提供的 Shrink Pas 程序，该程序启发了本项目，且其 shrink 算法被借用了；感谢 Phil Katz 将 zip 文件、压缩格式和 .ZIP 文件扩展名投入公领域，并接受对格式的微调；感谢 Steve Berg 对 deflate 格式的说明；感谢村冈彦（Haruhiko Okamura）和 Leonid Brokhuis 为压缩算法提供的一些很有用想法；感谢 Keith Peterson、Rich Wales、Hunter Goat 和 Mark Adler 为 Info-ZIP 组提供供使用的邮件列表和 FTP 站点；最重要的是 Info-ZIP 组本身（列在文件 info 中），没有了他们不知疲倦的测试和错误修复工作，一个便携的 zip 工具将是不可能的。

最后，我们应该感谢（埋怪）第一位 Info-ZIP 协调员 David Kirschbaum，是他从一开始让我们陷入了这种困境。该手册页由 R. P. C. Rodgers 为 UNIX 重新编写过。

# 1592

# zipinfo

# zipinfo — 列出 Zip 归档的详细信息

# 概要

```
usr/bin/zipinfo [-12smlvhMTtz] file[.zip] [file(s)...] [-x xfile(s)...]
/usr/bin/unzip -Z [-12smlvhMTtz] file[.zip] [file(s)...]
-x xfile(s)
```

# 描述

注意，zipinfo 与 unzip 是同一个程序（在 UNIX 下是它的链接）；但在某些系统上，当编译 unzip 时可能会省略对 zipinfo 的支持。

zipinfo 列出 ZIP 归档中文件的技术信息。这些信息包括文件权限、加密状态、压缩类型、版本以及压缩程序所使用的操作系统或文件系统。默认行为（指定未带选项的文件）是为每个文件生成单行条目，头部和总计提供整个归档的摘要信息。该格式是 UNIX `ls -l` 和 `unzip -v` 输出的结合，如下例所示：

| castle%zipinfo.zip 106272 bytes 4 files |
| -rw-rw---- 1.9 76800 t-def 18-Aug-98 21:55 085X01.DOC |
| -rw-a-- 2.0 67072 b-def 22-Aug-98 01:39 085X042.DOC |
| -rw-a-- 2.0 95232 t-def 31-Aug-98 20:29 085X042.DOC |
| -rw-a-- 2.0 63488 t-def 4-Oct-98 20:24 085X0E.DOC |
| 4 files, 302592 bytes uncompressed, 105898 bytes compressed: 65.0% castle$ |

注意在允许的系统中你可能会为 zipinfo 定义一个别名。你可以复制并重命名执行文件、创建一个链接，或者创建一个名为 ii 的命令文件。ii 对应于 UNIX 中常用的长列表别名。这两个命令输出之间的相似性是有刻意的。

# 参数

file[.zip] ZIP 归档的路径。如果你对文件指定通配符，则按操作系统（或文件系统）决顺序列出每个匹配的文件。只有文件名可以

# 1593

# zipinfo 1594

# 详细描述

zipinfo 有许多种模式，如果你熟悉 `ls(1)` 命令，它的行为可能很难理解。默认行为是以所示的格式列出文件。

```
-rw-rw---- 1.9 2802 11-Aug-91 13:48 per.2660
```

此示例是一个在 UNIX 系统上生成的 ZIP 文件。它来自 UNIX，示例中文件开头的权限是以 UNIX 格式打印的。

第二和第三字段表示该文件是在 UNIX 下使用 1.9 版本的 zip 压缩的。第四字段显示了未压缩的大小（2802）

