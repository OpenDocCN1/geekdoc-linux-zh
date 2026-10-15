
`comment` = Temporary file space

`path` = `/tmp`

`read only` = no

`Public` = yes

## 6 与 Windows 机器共享 Linux 驱动器

如上述简单的 `smb.conf` 所示，与 Windows 用户共享 Linux 驱动器非常简单。然而，像 Samba 的其他一切一样，你可以在很大程度上进行控制。以下是一些示例：

### 与 Linux 机器共享 Windows 驱动器

要向公众共享驱动器，可以通过在 `smb.conf` 中添加如下内容来创建 `tmp` 部分的副本：

```
[public]

comment = Public Staff

path = /home/public

public = yes

writable = yes

printable = yes
```

要让上述目录对公众可读但仅允许 `staff` 组的人写入，请按如下方式修改条目：

```
[public]

comment = Public Staff

path = /home/public

public = yes

writable = yes

printable = no

write list = @staff
```

关于驱动器共享的其他技巧，请参考 Samba 文档或帮助页（`man pages`）。

## 7 与 Linux 共享 Windows 驱动器

Samba 发行版包含一个用于 UNIX 机器的 SMB 客户端程序。它提供了一个类似 `ftp` 的界面。你可以使用此工具在 Windows 服务器和 Linux 客户端之间传输文件。

要查看主机上可用的共享，请运行：

```
/usr/sbin/smbclient -L host
```

其中 `host` 是你想要查看的机器。这将返回 `service` 列表——即它可以共享的驱动器或打印机。除非 SMB 服务器没有配置安全，否则它会要求你输入 `guest` 账户或该机器上的个人密码。例如：

```
smbclient -L zimerman
```

该命令的输出如下：

```
Server time is Sat Aug 10 15:58 1996

Timezone is UTC-0

Domain=[WORKGROUP] OS=[Windows NT 3.51]

Server=[NT LAN Manager 3.51]
```

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| ADMIN$ | Disk | Remote Admin |
| public | Disk | Public |
| CS | Disk | Default share |
| IPC$ | IPC | Remote IPC |
| OReilly | Printer | OReilly |
| prints | Disk | Printer Drivers |

| Server | Comment |
| :--- | :--- |
| HOPPER | Samba 1.9.15 |
| KERNIGAN | Samba 1.9.15 |
| LOVELACE | Samba 1.9.15 |
| RITCHIE | Samba 1.9.15 |
| ZIMMERMAN | Samba 1.9.15 |

浏览列表显示了网络上共享资源的 SMB 服务器。要使用客户端，请运行：

```
/usr/bin/smbclient <service>
```

其中 `service` 是共享名称。例如，如果你尝试访问一个在 `zimerman` 机器上共享为 `public` 的目录，`service` 将是 `zimerman\public`。由于 shell 的限制，你需要转义反斜杠，结果如下：

```
/usr/bin/smbclient \\zimerman\\public mypasswd
```

其中 `mypass` 是你的密码字符串。你会得到 `smb` 提示：

```
Server time is Sat Aug 10 15:58 1996

Timezone is UTC-0

Domain=[WORKGROUP] OS=[Windows NT 3.51]

Server=[NT LAN Manager 3.51]

smb: \
```

输入 `h` 获取 `smbclient` 的帮助：

```
smb: dir cd pwd

get mget put rename

more mask del mkdir

mdir rm prompt recurse

translate lowercase printmode queue

cancel stat exit

newer archive blocks size mode

setmode help

amba: ftp > h
```

如果你使用 `ftp`，就不需要 `smbclient` 的帮助页。

## 8 与 Windows 机器共享 Linux 打印机

要与 Windows 机器共享打印机，你需要确保你的打印机可以在 Linux 下工作。设置打印机的 SMB 共享是简单的。参考本地打印的 HOWTO。

由于作者使用的是连接到 Windows 机器的打印机，此部分不应被视为标准，仅作为建议。任何拥有共享细节的人请发送到 `dwood@plugged.net`，以便完成此部分。在你的 `smb.conf` 中添加打印配置：

```
[global]

printing = bsd

printcap name = /etc/printcap

load printers = yes
```

### 与 Linux 机器共享 Windows 打印机

```
log file = /var/log/samba.log

lock directory = /var/lock/samba

[printers]

comment = All Printers

security = server

path = /var/spool/lpd/lp

browseable = no

printable = yes

public = yes

writable = no

create mode = 0700
```

```
[ljet]

security = server

path = /var/spool/lpd/lp

printer name = lp

writable = yes

public = yes

printable = yes

command = lpr -r -h -P %p
```

确保打印机（在此情况下使用 `ljet`）与 `/etc/printcap` 中的池目录匹配！

注意：在带有 Samba 的 UNIX 盒上有一些共享打印机。一个问题是关于 NT 的共享打印机属性。要修复此问题，请查看 Samba 发行版 `docs/WinNTxt` 文件中的注释。另一个是密码问题。查看同一文件中的注释可以获得令人烦恼的理解并解决问题。

## 9 与 Linux 共享 Windows 打印机

要在 Windows 机器上共享打印机，你必须执行以下操作：

- 你必须拥有 `/etc/printcap` 中的条目，且它们必须与本地目录结构（用于池目录等）对应。
- 你必须拥有 `/usr/bin/smbprint` 脚本。这随 Samba 源码提供，但并不是所有的 Samba 二进制发行版都提供。下面讨论了一个稍微修改过的副本。
- 如果你想将 ASCII 文件转换为 Postscript，你必须拥有 `nscript` 或等等物。`nscript` 是一个 Postscript 转换器，通常安装在 `/usr/bin` 中。
- 你可能希望通过易用的前端实现 Samba 打印机打印。下面提供了一个处理 ASCII、Postscript 或生成的 Postscript 的简单脚本。

下面的 `/etc/printcap` 条目用于 Windows 主机上的 HP 5MP 打印机。条目如下：

```
lp - 输出设备名称

sd - 池目录（在本地机器上）

af - 计费文件

mx - 最大文件大小（0 为无限制）

if - 输入过滤器（脚本）名称
```

更多信息，请参阅打印 HOWTO 或 `printcap` 的帮助页。

```
# /etc/printcap

#

# //zimmerman/oreilly via smbprint
```

```
# 1486
```

```
# lp:cm=HP 5PI Postscript OReilly on zimmerman:
:lp=/dev/lpd/lp:
:sd=/var/spool/lpd/lp:
:af=/var/spool/lpd/lp/acct:
:mx#0:
:if=/usr/bin/smbprint:
```

确保输出池（spool）目录和计数目录是可写的。确保 `if` 行持有指向 `smbprint` 脚本（下所示）的正确路径，并确保指向了正确的设备（`/dev` 特殊文件）。

接下来是 `smbprint` 脚本本身。它通常放置在 `/usr/bin`，据我所知，它归属于创建 Samba 的 Andrew Tridge。在 Samba 源码发行版中，许多二进制发行版缺少该文件，因此我在这里重新创建了它。

你可能希望仔细查看一下。这里有一些微小的修改被证明是有用的。

```bash
#!/bin/sh -x

# 此脚本是 unix 机器上 printcap 打印的输入过滤器。

# 它使用 smclient 程序将文件打印到指定的基于 smb 的服务器和服务上。

# 例如，你可以有如下的 printcap 条目：

#

# smb:dev/null-sd=/var/spool/smb:

# sh=/usr/local/samba/smbprint

# 这将创建一个名为 'smb' 的 unix 打印机，它将通过

# 此脚本打印。你需要为你的系统创建具有适当权限和

# 所有权的输出池目录 /usr/spool/smb。

# 将这些项设置为你想要打印的服务器和服务。

# 在示例中，我有一台名为 'lapland' 的 WfWg PC，它有一个

# 导出的 'printer' 的打印机，无需密码。

# 由 hamiltonton@ecnz.co.nz 进一步修改脚本

# (Michael Hamilton)，以便服务器、服务

# 和密码可以从

# /usr/var/spool/lpd/PRINTNAME/.config 文件中读取。

# 为了使此生效，/etc/printcap 条目必须

# 包含一个计数文件 (af...):

# cdcolour:

:cm=CD IBM Colorjet on 6th:

:sd=/var/spool/lpd/cdcolour:

:af=/var/spool/lpd/cdcolour/acct:

:if=/usr/local/etc/smbprint:

:mx#0:

:lp=/dev/null:

# /usr/var/spool/lpd/PRINTNAME/.config 文件

# 应该包含：

# server=PC_SERVER

# service=PR_SHARENAME
```

```bash
# password="password"

# 例如

# server=PAULS_PC

# service=CJET_371

# password="*"
```

```bash
# 调试日志文件，如果喜欢可以更改为 /dev/null。

# logfile=/tmp/smb-print.log

# logfile=/dev/null
```

```bash
# 器的最后一个参数是计数

# 文件名。

spool_dir=var/spool/lpd/lp

config_file=$spool_dir/.config
```

```bash
# 应该在配置文件读取以下变量：

# server

# service

# password

# user

eval 'cat $config_file'
```

```bash
# 一些调试帮助，如果你想保留相同的空间

# 将 >> 更改为 >

echo 'server $server, service $service' >> $logfile
```

```bash
# 注意，如果你想要自动进行 CR/LF 转换

# 可能需要添加行 'echo translate'

echo translate

echo 'print - '
```

```bash
! /usr/bin/smbclient \
\\\\server\\$service password -U $user -N -P \
>> $logfile
```

大多数 Linux 发行版都带有将 ASCII 文档转换为 Postscript 的功能。以下 Perl 脚本通过 `smbprint` 为 Linux 了一个了一个简单的接口，让生活变得更容易。

用法：`print [-a|-p] <filename>`
- `-a` 将 `<filename>` 打印为 ASCII
- `-c` 将 `<filename>` 格式化为源代码并打印
- `-p` 将 `<filename>` 打印为 Postscript
如果没有给出开关，`print` 将尝试猜测文件类型并进行适当的打印。

使用 `smbprint` 打印 ASCII 文件以截断长行。此脚本尽可能地在空白字符处折断长行（而不是在单词中间）。

源代码格式化是通过 `nscript` 完成的。它接受一个 ASCII 文件并将其格式化为两列，并带有漂亮的标题（日期、文件名等）。它还对行进行了编号。以此为例，可以实现其他类型的格式化。Postscript 文档格式化正确，因此它们直接通过。

```perl
#!/usr/bin/perl

# 脚本：print

# 作者：Brad Marshall, David Wood

#          Plugged In Communications

# 日期：960808

# 打印 oereilly 的脚本目前位于 zimmerman 上

# 用途：将各种类型的文件作为参数

# 进行适当处理，以管道到 Samba 脚本。

# 目前支持的文件类型：

# ASCII --   确保超过 $line_length 字符的行在空白

#           字符处折行。

# Postscript - 不采取任何操作。

# Code       以 Postscript 格式化（使用 nscript）以便正确

#             显示（横向、字体等）。

# 设置每行 ASCII 文本允许的最大长度。

$line_length = 76;

# 设置 Samba 打印的路径和名称

$print_prog = "/usr/bin/smbprint";

# 设置 nscript（ASCII 转换器）的路径和名称

$script = "/usr/bin/nscript";

unless ( -f $print_prog ) {

    die "找不到 $print_prog!";

}

unless ( -f $script ) {

    die "找不到 $script!";

}

&ParseCmdLine(@ARGV);

# 调试

print "文件类型为 $filetype";

if ($filetype == "ASCII") {

    &wrap($line_length);

} elsif ($filetype == "code") {

    &codeformat;

} elsif ($filetype == "ps") {

    &createarray;

} else {

    print "未知类型。";

    exit 0

# 与 Linux 机器共享 Windows 打印机
```

```bash
# 将数组管道到 smbprint
open(PRINTER, $print_prog) or die "无法打开 $print_prog: $!";
foreach (@newlines) {
    print PRINTER $line;
}

# 如果行不完整，发送额外的换行符。
print PRINTER "\n";
close(PRINTER);
print "完成";
exit 0;
```

# 以下是子程序

sub ParseCmdLine {

    # 解析命令行，确定文件类型

    # 获取 $arg 和 $file（如果存在）

    # 文件名

    if (# < 0) {

        usage;

    }

    # 调试

    foreach (@_) {

        print "$element \n";

    }

    $arg = shift(@_);

    if ($arg =~ /\*/) {

        $cmd = $arg;

    }

    # 调试

    print "找到了 $cmd。";

    $file = shift(@_);

    else {

        $file = $arg;

    }

    # 定义文件类型

    unless ($cmd) {

        # 没有参数

        if ($file =~ /\.ps$/) {

            $filetype = "ps";

        } elsif ($file =~ /\.c$/) {

            $filetype = "code";

        } elsif ($file =~ /\.a$/) {

            $filetype = "ASCII";

        }

    } else {

        # 我们有 $arg 中的类型

        if ($cmd =~ /\-p$/) {

            $filetype = "ps";

        } elsif ($cmd =~ /\-c$/) {
