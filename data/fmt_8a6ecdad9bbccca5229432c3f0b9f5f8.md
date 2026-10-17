
清单 5.21 创建了一个供 `admintrans` 组成员共享的目录。用户 `silvied`、`marionb` 和 `markusk` 在该目录中具有读写权限。每个用户都能够读取、更改和删除由另一用户创建的文件；命令 `chmod g+w admintrans` 赋予了该组所有成员的权限。其他用户的全部权限已通过 `chmod o-r,o-x admintrans` 被撤销；只有 `admintrans` 组的成员才能使用该目录并列出其中的文件。

是否可以防止意外删除由另一用户创建的文件？每个 *NIX 系统上已经存在一种使用此类保护的目录，即 `/tmp` 目录。清单 5.22 显示了权限。

#### LISTING 5.22 /tmp 目录

```
root@unixhost# ls -ld /tmp

drwxrwxrwt 6 root sys 381 Sep 20 11:13 /tmp
```

所谓的粘滞位用于防止一个用户删除由另一用户创建的文件。设置的粘滞位在权限中以字母 `t` 表示。如果用户在目录中具有写权限，则该用户能够删除文件，即使该用户对文件没有写权限。如果在目录上设置了粘滞位，则只有所有者和 `root` 能够删除文件。设置粘滞位如清单 5.23 所示。

#### LISTING 5.23 设置粘滞位

```
root@unixhost# chmod +t admintrans

root@unixhost# ls -l

total 10

drwxrwx-T 2 root admintrans 512 Sep 20 13:31 admintrans

drwxr-xr-x 5 chrisk admintrans 512 Aug 23 15:33 chrisk

...
```

这次出现大写字母 `T` 的原因是在某些 *NIX 变体中没有为其他用户设置权限。命令 `chmod +t <directoryname>` 可以工作。

#### 使用 chmod 与 1770

命令 `chmod` 接受两种不同的参数类型来指示文件或目录的权限。

Symbolic: `chmod g+rwx <filename>` 表示组具有读、写和执行权限。

Octal: `chmod 770 <filename>` 表示所有者和组具有读、写和执行权限。其他人没有任何权限。

要使用符号表示法获得相同的结果，你必须使用以下命令：`chmod u=rwx,g=rwx,o= <filename>`。符号表示法可用于移除或添加组的写权限：`g-w`（移除），`g+w`（添加）。符号表示法更易读。八进制表示法（基数八）更快，工作原理如下：

| user | group | others | Modus |
|------|-------|--------|-------|
| 0400 | 0040 | 0004 | read (r) |
| 0200 | 0020 | 0002 | write (w) |
| 0100 | 0010 | 0001 | execute (x) |
| 0500 | 0050 | 0005 | read/execute (r-x) |
| 0600 | 0060 | 0006 | read/write (rw-) |
| 0700 | 0070 | 0007 | read/write/execute (rwx) |

4 = 读、2 = 写、1 = 执行 的值相加等于 7（读、写、执行）。如果你用二进制系统来写相同的数值，一切就变得显而易见了。

```
rwx

4  0100  read

2  0010  write

1  0001  execute
```

这意味着二进制 `0110` 等于 `rw-` 或 `6`。如果你想使用八进制表示法来管理文件或目录的权限，你只需将所需的权限相加即可得到正确的数字，`755` 代表 `rwxr-xr-x`。

虽然似乎没有空间设置粘滞位，但实际上是有空间的。快速浏览前两个示例会发现有四个

```
#
#    purpose:    read in a config file and create load
#                on the target system
#
#    author:      Erik Keller
#
#    parameters:  -d directory to write to
#                 -s size of the first file b|k|m|g
#                 -n number of copies
#
########################################################
use Getopt::Std;

# Variables
getopt('dsn');
$the_dir = $opt_d;
$the_size = $opt_s;
$the_files = $opt_n;

# use mkfile for Solaris, BSD and OS X
$mkfile = "/usr/sbin/mkfile";

# create the directory
@args = ( "mkdir", "$the_dir");
system(@args) == 0
    or die "$0: couldn't create dir: $!";

# create the file
@args_mkfile = ("$mkfile", "$the_size", "$the_dir/Testing.file");
system(@args_mkfile) == 0
    or die "$0: couldn't create file: $!";

# copy loop
for($the_count = 0; $the_count < $the_files; $the_count += 1)
{
@args_cp = ("cp", "$the_dir/Testing.file",
"$the_dir/descht$the_count.file");
system(@args_cp) == 0
    or die "$0: couldn't copy the file: $!";
}
```

```
# clean up afterwards
@args_rm = ('rm', '-r', "$the_dir");
system(@args_rm) == 0
    or die "$0: couldn't remove the dir: $!";
# EOF
```

先说一个警告：此脚本能够严重破坏系统的稳定性。请自行承担风险使用。它适用于所有 Solaris、BSD 或 OS X 系统。它使用 `mkfile` 命令，该命令是上述系统的一部分。此命令的原始用途是在文件系统中创建交换文件。大小单位指定为 `b` = 块，`k` = 千字节，`m` = 兆字节，或 `g` = 千兆字节。脚本通过使用 `-d` 选项提供的路径和文件名来创建目录。大小通过 `-s` 选项提供，文件将在目录内复制 `-n` 次。

要在 HP-UX 上使用脚本，你必须将 `mkfile` 替换为 `prealloc`。此命令不了解 `mkfile` 理解的选项。它接受一个文件名和一个数字（解释为字节）。另一种解决方案是使用 `/usr/local` 树的 `tar` 归档，例如，并将此 `tar` 归档用作要复制的文件。

接下来，查看列表 5.25。

#### 列表 5.25 使用 loadtest.pl

```
erikk@unixhost> ./loadtest.pl -d tests/ltest1 -s 2m -n 50
```

列表 5.25 中的命令会引发以下事件：它在 `/tests/test1` 中创建一个大小为 2 兆字节的文件。该文件将被复制 50 次。然后脚本再次删除创建的文件和目录。脚本不会检查是否有足够的空间执行操作；如果磁盘空间不足，它会以错误消息终止并且不会清理。要创建可用的负载情况，你必须确保待测试的磁盘或阵列被填满接近容量。脚本可用于测试磁盘和网络连接。要测试网络连接，你只需使用通过 NFS 挂载的目录即可。你绝不应在生产网络内部使用脚本来测试网络连接。列表 5.26 给出了一个示例。

#### 列表 5.26 通过网络使用 loadtest.pl

```
erikk@unixhost> mount linuxhost:/data1/tests /myount/test

erikk@unixhost> ./loadtest.pl -d /myount/test/ltest1 -s 2m -n 50
```
