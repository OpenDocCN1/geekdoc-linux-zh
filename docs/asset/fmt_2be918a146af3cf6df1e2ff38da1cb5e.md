
```
root:sed-3.02# CPPFLAGS=-Dre_max_failures=re_max_failures2 \
  > ./configure --prefix=/usr --disable-nls
root:sed-3.02# make LDFLAGS--static
root:sed-3.02# make prefix=$LFS/usr install
root:sed-3.02# mv $LFS/usr/bin/sed $LFS/bin
```

## 目录

Sed 软件包包含 `sed` 程序。

### 描述

`sed` 是一个流编辑器。流编辑器用于对输入流（文件或来自管道的输入）执行基础文本转换。

### 安装 Shellutils

安装 Shellutils 命令：

运行以下命令来安装 Shellutils：

```
root:sh-utils-2.0# ./configure --prefix=/usr --disable-nls
root:sh-utils-2.0# make LDFLAGS=--static
root:sh-utils-2.0# make prefix=$LFS/usr install
root:sh-utils-2.0# cd $LFS/usr/bin
root:bin# mv date echo false pwd stty $LFS/bin
root:bin# mv stu true hostname $LFS/bin
```

## 目录

Shellutils 软件包包含 `basename`, `chroot`, `date`, `dirname`, `echo`, `env`, `expr`, `factor`, `false`, `groups`, `hostid`, `ids`, `logname`, `nice`, `nohup`, `pathchk`, `pinky`, `printenv`, `printf`, `pwd`, `seq`, `sleep`, `stty`, `su`, `tee`, `test`, `true`, `utny`, `uptime`, `users`, `who`, `whoami` 和 `yes` 程序。

### 描述

### basename

`basename` 从文件名中剥离目录和后缀。

### chroot

`chroot` 在特殊的根目录中运行命令或交互式 shell。

### date

`date` 以指定的格式显示当前时间，或设置系统日期。

### dirname

`dirname` 从文件名中剥离非目录后缀。

### echo

`echo` 显示一行文本。

### env

`env` 在修改后的环境中运行程序。

### expr

`expr` 评估表达式。

### factor

`factor` 打印所有指定整数的质因数。

### false

`false` 总是以指示失败的状态码退出。

### groups

`groups` 打印用户所属的组。

### hostid

`hostid` 打印当前主机的数字标识符（十六进制）。

### hostname

`hostname` 设置或打印当前主机系统的名称。

### id

`id` 打印用户或当前用户的真实和有效 UID 及 GID。

### logname

`logname` 打印当前用户的登录名。

### nice

`nice` 以修改后的调度优先级运行程序。

### nohup

`nohup` 运行忽略挂断信号的命令，并将输出到非 tty 设备。

### pathchk

`pathchk` 检查文件名是否有效或具有移植性。

### pinky

`pinky` 是一个轻量级的 finger 工具，用于检索有关特定用户的信息。

### printenv

`printenv` 打印所有或部分环境变量。

### printf

`printf` 格式化并打印数据（同 C 语言中的 `printf` 函数）。

### pwd

`pwd` 打印当前/工作目录的。

### seq

`seq` 按指定的增量打印范围内的数字。

### sleep

`sleep` 等待一段时间。

### stty

`stty` 修改并打印终端行设置。

### su

`su` 使用替换的用户和组 ID 运行 shell。

### tee

`tee` 从标准输入读取并写入标准输出和文件。

### test

`test` 检查文件类型并比较值。

### true

`true` 总是以指示成功的状态码退出。

### tty

`tty` 打印连接到标准的终端文件名。

### uname

`uname` 打印系统信息。

### uptime

`uptime` 告诉系统已运行多久。

### users

`users` 打印当前登录到主机的用户名。

### who

`who` 显示谁正在登录。

### whoami

`whoami` 打印你的有效 userid。

### yes

`yes` 重复输出字符串直到被杀死。

### 安装 Tar

安装 Tar

运行以下命令来安装 Tar：

```
root:tar-1.13# ./configure --prefix=/usr --disable-nls
root:tar-1.13# make LDFLAGS=--static
root:tar-1.13# make prefix=$LFS/usr install
root:tar-1.13# mv $LFS/usr/bin/tar $LFS/bin
```

## 目录

`tar` 软件包包含 `tar` 和 `rmt` 程序。

### 描述

### tar

`tar` 是一个归档程序，用于从名为 `tarfile` 的归档文件中存储和提取文件。

### rmt

`rmt` 是一个供远程使用的程序。

### 安装 Textutils

安装 Textutils

运行以下命令来安装 Textutils：

```
root:textutils-2.0# ./configure --prefix=/usr --disable-nls
root:textutils-2.0# make LDFLAGS=--static
root:textutils-2.0# make prefix=$LFS/usr install
```

## 目录

Textutils 软件包包含 `cut`, `cksum`, `comm`, `split`, `expand`, `fold`, `head`, `join`, `md5sum`, `nl`, `od`, `paste`, `pr`, `ptx`, `sort`, `sum`, `tac`, `tail`, `tr`, `tsort`, `unexpand`, `uniq` 和 `wc` 程序。

### 描述

### cut

`cut` 选择行的部分。

### cksum

`cksum` 计算校验和。

### comm 比较文件。

### split 分割文件。

### expand 扩展制表符。

### fold 折叠行。

### head 打印前几行。

### join 合并文件。

### md5sum 计算 MD5 散列值。

### nl 给行编号。

### od 以八进制显示。

### paste 合并文件行。

### pr 格式化打印。

### ptx 打印排列组合。

### sort 对行排序。

### sum 计算总和。

### tac 反序打印。

### tail 打印最后几行。

### tr 翻译字符。

### tsort 数值排序。

### unexpand 压缩制表符。

### uniq 去除重复行。

### wc 统计行、字和字节。

# 复制 `/proc/devices`

为了让 `MAKEDEV` 脚本在 `/dev` 中正确创建设备节点，它需要访问 `/proc/devices` 的权限。我们尚无法在 LFS 系统上挂载 proc 文件系统，因此我们将 `/proc/devices` 文件复制到 `$LSFS/proc`。这意味着当内核更新 `/proc/devices` 时，`$LSFS/proc/devices` 文件不会被更新，但我认为这样做没有害，因为它只在执行 `MAKEDEV` 脚本期间需要它。只需确保在继续阅读本书之前，不要在接下来的 3 分钟内通过加载或卸载内核模块或重启电脑来添加或删除任何硬件。

运行以下命令复制 `/proc/devices` 文件：

```
root:~# cp /proc/devices $LSFS/proc
```

## 第 6 章：安装基础系统软件

### 简介

所有软件的安装都非常简单，你可能会认为为每个软件包提供通用的安装说明要简单且快捷得多，并且只有当某个软件包需要备选安装方法时才解释如何安装。虽然我同意你的观点，但我选择为每一个软件包都提供完整的指令。这样做仅仅是为了避免任何可能的混淆和错误。

### 调试符号和编译器优化

大多数程序和库默认使用带有调试符号和 2 级优化级别（`gcc` 选项 `-g` 和 `-O2`）并针对特定 CPU 进行编译。在 Intel 平台上，软件默认是为 `i386` 处理器编译的。如果你不想在自己的机器以外的其他机器上运行软件，你可能希望更改默认编译器选项，以便它们以更高的优化级别编译、不带调试符号，并为你的特定架构生成代码。让我先解释一下什么是调试符号。
