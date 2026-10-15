
与 `Bash` `time` 一样，`Linux` `time` 也可以对结果进行格式化。格式可以存储在一个名为 `TIME`（而不是 `TIMEFORMAT`）的变量中，或者可以通过 `-format` (`-f`) 开关明确指定。

-   `$A`—字面量 `$`。
-   `$E`—实际时间；以“小时:分钟:秒”格式显示的经过时间。
-   `$e`—实际时间；以秒为单位的经过时间。
-   `$S`—以 CPU 秒为单位的系统时间。
-   `$U`—以 CPU 秒为单位的用户时间。
-   `$P`—程序使用的 CPU 百分比。
-   `$M`—程序在内存中的最大大小（以千字节为单位）。
-   `$t`—程序的平均常驻集大小（以千字节为单位）。
-   `$D`—非共享数据区的平均大小。
-   `$P`—非共享堆栈的平均大小（以千字节为单位）。
-   `$X`—共享文本区的平均大小。
-   `$Z`—系统页的大小，以字节为单位。
-   `$F`—主要缺页错误的数量。
-   `$R`—次要缺页错误的数量（即页面之前已加载且仍被 `Linux` 缓存的情况）。
-   `$W`—进程被换出的次数。
-   `$c`—时间片上下文切换的次数。
-   `$w`—自愿上下文切换的次数。
-   `$I`—文件系统输入的次数。
-   `$O`—文件系统输出的次数。
-   `$r`—接收套接字消息的次数。
-   `$s`—发送套接字消息的次数。
-   `$K`—接收到的信号数量。
-   `$C`—命令行。
-   `$x`—退出状态。

与您的硬件无关的统计数据显示为零。

```bash
$ command time grep ken /etc/aliases
Command exited with non-zero status 1
0.00user  0.00system  0:00.02elapsed  0%CPU  (0avgtext+0avgdata 0maxresident)k
0inputs+0outputs (142major+19minor)pagefaults 0swaps
$ command time --format "%P" grep ken /etc/aliases
Command exited with non-zero status 1
0%
$ command time --format "Major faults = %W" grep ken /etc/aliases
Command exited with non-zero status 1
Major faults = 141
```

`--portability` (`-p`) 开关强制 `time` 遵循 `POSIX` 标准，这与 `Bash` 的 `time -p` 相同，并关闭了许多扩展功能。

```bash
$ command time --portability grep ken /etc/aliases
Command exited with non-zero status 1
real  0.00
user  0.00
sys  0.00
```

结果可以通过 `--output` (`-o`) 重定向到文件，或者通过 `--append` (`-a`) 追加到文件。`--verbose` (`-v`) 选项会提供每个统计项的详细解释。

## 创建 Man 手册页

`Linux` 的 `man` 手册页是为 `groff` 程序（GNU run off）格式化的特殊文本文件。`groff` 基于较旧的 `Unix` 程序 `troff`（用于打印机）和 `nroff`（用于终端）。`Troff` 最初由 `Joseph E. Ossanna` 在 1973 年创建。通过为重要脚本创建简短的 `man` 手册页，可以为关于您项目的在线信息创建一个单一的访问点。

请将您自己项目的手册页放在手册的第 9 节中。最初，第 9 节用于记录 `Linux` 内核，但现在它遵循传统的 `Unix` 解释，允许个人使用。第 9 节的手册页通常存储在 `/usr/share/man/man9` 中。如果您无法访问此目录，请在主目录中创建一个 `man9` 目录，并将您的个人手册页存储在那里。通过在 `Bash` 配置文件中将 `$HOME` 添加到 `MANPATH` 环境变量中，`man` 将搜索存储在您 `man9` 目录中的页面。

```bash
$ mkdir ~/man9
$ declare -x MANPATH="$HOME:/usr/share/man"
```

`man` 手册页是包含嵌入文本中的 `groff` 标记代码（或宏）的文本文件。这些代码很像网页中的 `HTML` 标签，控制页面中使用的间距、布局和图形。您还可以定义自己的 `groff` 代码。这些代码总是出现在行首，并以句号开头。

以下是一些 `groff` 标记代码的示例：

```groff
.\$Id
.TH MAN 9 "25 July 1993" "Linux" "Nightlight Corporation Manual"
.SH NAME
ftp.sh \- script to FTP orders to suppliers
.SH SYNOPSIS
.B ftp.sh
.I file
```

`groff` 代码以单独的行开始，以句号 (`.`) 开头，后跟一个或两个字母的代码。例如，`.B` 代码表示随后的文本是粗体（类似于 `HTML` 的 `<b>` 标签）。

与手册页相关的 `groff` 预定义宏在第 7 节的手册页 `man`（`man 7 man`）中有记录。一些常用的 `groff` 代码如下：

-   `.B`—粗体
-   `.I`—斜体
-   `.PP`—开始新段落
-   `.RS i`—缩进 `i` 个字符
-   `.RE`—结束上一个 `RS` 缩进
-   `.UR u`—开始由 URL 链接的文本
-   `.UE`—结束由 `.UR` 开始的链接文本
-   `.\`—表示注释
-   `.TH`—页面标题
-   `.SH`—子标题

虽然对手册页没有严格的要求，但大多数 `man` 手册页包含以下一个或多个部分：`SYNOPSIS`（概要）、`DESCRIPTION`（描述）、`RETURN VALUES`（返回值）、`EXIT STATUS`（退出状态）、`OPTIONS`（选项）、`USAGE`（用法）、`FILES`（文件）、`ENVIRONMENT`（环境）、`DIAGNOSTICS`（诊断）、`SECURITY`（安全性）、`CONFORMING TO`（符合性）、`NOTES`（备注）、`BUGS`（缺陷）、`AUTHOR`（作者）和 `SEE ALSO`（另请参阅）。如果您正在使用 `CVS`，您可以在 `VERSION`（版本）部分中包含 `CVS` 关键字，例如 `$Id$`。

为您的程序创建简单 `man` 手册页的最简单方法是找到一个类似的手册页并制作一个修改后的副本。

### 列表 8.4 Man 手册页示例

```groff
./'man page supply_ftp.sh.9
.TH "SUPPLY_FTP.SH" 9 "25 May 2001" "Nightlight" "Nightlight Corporation Manual"
.SH NAME
supply_ftp.sh \- Bash script to FTP orders to suppliers
.SH SYNOPSIS
.B supply_ftp.sh
.I file
.I supplier
.SH DESCRIPTION
.B supply_ftp.sh
sends orders via FTP to suppliers.
.I file
is the name of the file to send.
.I supplier
is the name of the supplier. The suppliers and their FTP account information
are stored in the text file
.I supplier.txt
.SH RETURN VALUES
The script returns 0 on a successful FTP and 1 if the FTP failed.
.SH AUTHOR
Created by Ken O. Burtch.
.SH FILES
/home/data/supplier.txt
.SH VERSION
$Id$
```

此页面显示为
