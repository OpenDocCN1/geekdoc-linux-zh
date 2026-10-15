
## mkswap

描述

设置交换区域。

语法

`mkswap [-c] device`

重要标志和选项

- `-c`：在格式化前检查坏块。

## mlabel

描述

为 MS-DOS 软盘打标签。

语法

`mlabel _drive:`

重要标志和选项

- `-c`：显示当前信息。
- `-s`：提示用户标签。

## mmd

描述

移动或更多目录。

语法

`mmd osdirectory`

重要标志和选项

无

## mmove

描述

移动（也重命名）文件。

语法

`mmove sourcefile targetfile`

重要标志和选项

无

## modprobe

描述

根据类型加载更多模块。

语法

`modprobe -t pattern`

重要标志和选项

- `-a`：加载所有模块而不是第一个。
- `-c`：显示配置。
- `-l`：列出所有类型的模块。
- `-r`：卸载指定的模块。
- `-t`：只加载某种类型的模块。

## more

逐屏显示一个或多个文件，允许搜索并跳转到任意位置。

语法

`more [-dlfs] [-number] [file ...]`

重要标志和选项

- `-number`：设置每屏行数。
- `+number`：指定起始行。
- `-d`：提示用户。
- `-f`：导致行不折叠并被视为单行。
- `-1`：防止 Ctrl+L 被视为分页符。
- `-s`：将多个空行压缩为单行。

注意

关于查看文件时使用的命令详情，请参考 `more` 页面。

## mount

将文件系统挂载到指定的目录。

语法

`mount -a [rw] [-t vfst] device|dir`

`mount [-rw] [-o options, ...]] device|dir`

`mount [-rw] [-t vfst] [-o options] device dir`

重要标志和选项

- `-a`：挂载 `/etc/fstab` 中的所有文件系统。如果使用 `-t` 指定类型，则只加载 `/etc/fstab` 中指定类型的文件系统。
- `-o`：见下注。
- `-r`：以只读模式挂载文件系统。相当于 `-o ro`。
- `-t`：指定文件系统类型。
- `-w`：以读写模式挂载文件系统。相当于 `-o rw`。

注意

`-t` 参数可能的文件系统类型包括：

| Minix | vfat | ufs |
| ext | proc | romfs |
| ext2 | nfs | sysv |
| xiafs | iso9660 | xenon |
| hpfs | smbfs | coherent |
| msdos | ncpfs | |
| umsdos | affs | |

关于 `-o` 参数的选项列表，请参考 `mount` 页面，该页面提供了各种可用选项的详细描述。

## mrd

删除一个或多个 MS-DOS 目录。

语法

`mrd mdsosdirectory [msdosdirectory ... ]`

重要标志和选项

无

## mren

描述

重命名 MS-DOS 文件。与 DOS REN 命令类似，不同之处在于它也可以重命名目录。

语法

`mren oldname newname`

重要标志和选项

无

## mtype

描述

显示一个或多个 MS-DOS 文件的内容。与 DOS TYPE 命令类似。

语法

`mtype [-ts] mdsosfile [msdosfile ...]`

重要标志和选项

- `-s`：移除数据中的高位。
- `-t`：在显示之前将 DOS 文本文件转换为 Unix 文本文件。

## mv

描述

重命名并移动文件。当目录是最后一个参数时，将所有其他文件移动到该目录。

语法

`mv [-bfiu] [--backup] [--force] [--interactive] [--update] [source destination][source ... directory]`

重要标志和选项

- `-b --backup`：对正在移动的文件进行备份。
- `-f --force`：在不提示的情况下删除即将被移动操作覆盖的现有文件。
- `-i --interactive`：在覆盖任何现有文件之前进行提示。
- `-u --update`：如果现有文件的修改时间相同或更新，则不覆盖该文件。

## netstat

描述

显示网络状态信息，包括连接、路由表和接口统计。在未提供选项时，将显示活动套字的列表。

语法

`netstat [-Mnrs] [-c] [-i interface] [--interface interface] [--masquerade] [--route] [--statistics]`

重要标志和选项

- `-c`：每秒显示一次选择信息，直到按 Ctrl+C 中断。
- `-i [interface] / --interface [interface]`：显示指定接口的信息，如果未指定则显示所有接口的信息。
- `-M --masquerade`：显示伪装会话列表。
- `-n`：显示数值地址而不是其主机、端口或用户名。
- `-r --route`：显示内核路由表。
- `-s --statistics`：显示网络统计。

## newgrp

描述

将用户登录到一个新组，更改用户的组 ID。如果未指定组，则将组 ID 更改为登录组 ID。

语法

`newgrp [group]`

重要标志和选项

无

## newusers

描述

读取包含新用户列表的文件并创建这些用户。如果未指定文件，则应从标准输入提供用户信息。

语法

`newusers [file]`

重要标志和选项

无

注意事项

`newusers` 命令读取的文件格式与 `/etc/passwd` 文件相同，但有以下例外：
- 密码不应加密。它们在创建用户账户时会被加密。
- 如果指定的组不存在，则将创建新组。
- 如果用户的家目录不存在，将创建一个新的；如果已存在同名的目录，则将其所有权更改为新用户。
- 因为此文件将包含解密后的密码，因此务必始终保持其安全。

## nisdomainname

描述

显示当前的 NIS 域名。

语法

`nisdomainname`

重要标志和选项

无

## nslookup

描述

查询 DNS 服务器名称。可以在交互模式下运行。如果没有提供主机名，程序将进入交互模式。默认情况下，使用 `/etc/resolv.conf` 中指定的 DNS 服务器，除非指定了另一个。如果您想指定服务器但不查询指定的主机，则必须提供 `-` 代替主机名。

语法

```
nslookup [host|[-server]]
```

重要标志和选项

无

注意事项

有关交互模式下可用命令的说明，请参阅 `nslookup` 手页。

## passwd

描述

更改用户密码。当由 root 用户运行时运行时，可以通过提供用户名作为参数来更改特定用户的密码。

语法

```
passwd [username]
```

重要标志和选项

无

## paste

描述

合并一个或多个文件中对应的行。在同一行上顺序打印对应的行，用制表符分隔，并以换行符结束文件。如果未提供文件名，则从标准输入读取。

语法

```
paste [-s] [-d delim-list] [--serial] [--delimiters list] [file ...]
```

重要标志和选项

- `--delim-list`：指定使用的分隔符代替默认的制表符。如果列表中有多个字符，将连续使用这些字符，在使用最后一个字符后返回到列表中的第一个字符。
- `-s,--serial`：顺序粘贴一个文件的行，紧接着是下一个文件的行，从*第一个文件到最后一个文件*，每个文件占一行。

## pathchk

描述

检查文件名的有效性和移植性。具体来说，检查文件路径中的所有目录是否具有适当的执行权限，并且路径和文件名的每个组件的长度都不超过文件名组件的最大长度。

语法

```
pathchk [-p] [--portability] file ...
```

重要标志和选项

- `-p/--portability`：根据 POSIX 1 标准测试每个文件名的长度，而不是实际文件系统的长度限制。还会检查文件名中使用字符的移植性。

## pidof

描述

发送一个或多个命名程序的进程 ID 并显示这些 PID。

语法

```
pidof [-s] [-x] [-o pid] program [program ...]
```

重要标志和选项

- `-o pid`：从返回中省略进程 ID。
- `-s`：仅返回单个 PID。
- `-x`：返回 shell 以及命名程序的 ID。

## ping

描述

向网络主机发送回回显请求包，以查看其在网络是否可用。

语法
```
