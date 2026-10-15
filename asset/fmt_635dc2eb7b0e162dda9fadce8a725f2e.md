
genksyms 读取（标准输入）来自 `gcc -E source.c` 的输出并生成包含版本信息的文件。

### `insmod`
`insmod` 在运行的内核中安装可加载模块。

### `insmod_ops_clean`
`insmod_ops_clean` 删除 2 天内未访问的保存符号和模块。

### `kerneld`
`kerneld` 在用户空间执行内核操作（例如按需加载模块）。

### `kernelversion`
`kernelversion` 报告运行内核的主版本号。

### `ksyms`
`ksyms` 显示导出的内核符号。

### `lsmod`
`lsmod` 显示所有已加载模块的信息。

### `modinfo`
`modinfo` 检查与模块关联的对象文件并显示它可以获取的任何信息。

### `modprobe`
`modprobe` 使用 `depmod` 创建的类似 Makefile 的文件，从预定义目录树可用模块集中自动加载相关模块。

### `rmmod`
`rmmod` 从运行的内核中卸载可加载模块。

# 安装 Procinfo

安装 Procinfo

如果你想为此软件包添加编译器优化，请编辑 `Makefile` 文件并编辑 `CFLAGS` 变量。

运行以下命令安装 Procinfo：

```
root:procinfo-17# sed "s/-ltermcap/-lncurses/" Makefile
>Makefile2
root:procinfo-17# mv Makefile2 Makefile
root:procinfo-17# make
root:procinfo-17# make install
```

## 目录

Procinfo 软件包包含 `procinfo` 程序。

### 描述

`procinfo` 从 `/proc` 目录收集一些系统数据并格式化地打印到标准输出设备。

# 安装 Procps

安装 Procps

如果你想为此软件包添加编译器优化，请编辑 `Makefile` 文件并编辑 `CFLAGS` 变量。

运行以下命令安装 Procps：

```
root:procps-2.0.7# sed "s/XConsole/#XConsole/" Makefile
>Makefile2
root:procps-2.0.7# mv Makefile2 Makefile
root:procps-2.0.7# make
root:procps-2.0.7# mv /usr/bin/kill /bin
```

# 目录

Procps 软件包包含 `free`, `kill`, `oldps`, `ps`, `skill`, `snice`, `sysctl`, `tload`, `top`, `uptime`, `vmstat`, `w` 和 `watch` 程序。

### 描述

`free` 显示系统中物理内存和交换内存的总量和可用，以及内核使用的共享内存和缓冲区。

### `kill`
`kill` 向进程发送信号。

# `oldps` 和 `ps`
`ps` 提供当前进程的快照。

### `skill`
`skill` 发送信号以处理匹配特定标准的进程。

### `snice`
`snice` 更改匹配特定标准的进程调度优先级。

### `sysctl`
`sysctl` 在运行时修改内核参数。

# `tload`
`tload` 将当前系统负载平均图表打印到指定的 tty（如果未指定，则打印到负载进程的 tty）。

### `top`
`top` 实时持续查看处理器的活动。

### `uptime`
`uptime` 以单行形式显示以下信息：当前时间、系统运行时间、当前登录的用户数以及过去 1、5 和 15 分钟的系统负载平均值。

### `vmstat`
`vmstat` 报告关于进程、内存、分页、块 IO、陷阱（traps）和 CPU 活动的信息。

# `w`
`w` 显示当前在机器上的用户及其进程。

### `watch`
`watch` 重复运行命令，并显示其输出（第一个屏幕的内容）。

# 安装 Psmisc

安装 Psmisc

如果你想向此包添加编译器优化，请编辑 `Makefile` 文件并修改 `CFLAGS` 变量。

运行以下命令安装 Psmisc：

```
root:psmisc# sed "s/-ltermcap/-lcurses/" Makefile >Makefile2
root:psmisc# mv Makefile2 Makefile
root:psmisc# make
root:psmisc# make install
```

### 内容

Psmisc 包包含 `fuser`、`killall` 和 `pstree` 程序。

### 描述

### `fuser`
`fuser` 显示使用指定文件或文件系统的进程 PID。

### `killall`
`killall` 向所有运行任何指定命令的进程发送信号。

### `pstree`
`pstree` 将运行中的进程显示为树状结构。

# 安装 Sed

安装 Sed

运行以下命令安装 Sed：

```
root:sed-3.02# ./configure --prefix=/usr
root:sed-3.02# make
root:sed-3.02# make install
root:sed-3.02# mv /usr/bin/sed /bin
```

### 内容

Sed 包包含 `sed` 程序。

### 描述

`sed` 是一个流编辑器。流编辑器用于对输入流（文件或管道的输入）执行基础文本转换。

# 安装 Shellutils

安装 Shell Utils

运行以下命令安装 Shellutils：

```
root:sh-utils-2.0# ./configure --prefix=/usr
root:sh-utils-2.0# make
root:sh-utils-2.0# make install
root:sh-utils-2.0# cd /usr/bin
root:bin# mv date echo false pwd stty /bin
root:bin# mv su true hostname /bin
```

### 内容

Shellutils 包包含 `basename`, `chroot`, `date`, `dirname`, `echo`, `env`, `expr`, `factor`, `false`, `groups`, `hostid`, `hostname`, `id`, `nice`, `nohup`, `pathchk`, `pinky`, `printenv`, `printf`, `pwd`, `seq`, `sleep`, `stty`, `su`, `tee`, `test`, `true`, `utny`, `uptime`, `users`, `who`, `whoami` 和 `yes` 程序。

### 描述

### `bas`
`basename` 从文件名中剥离目录和后缀。

### `chroot`
`chroot` 在特殊的根目录下运行命令或交互式 shell。

### `date`
`date` 以指定的格式显示当前时间，或设置系统日期。

### `dirname`
`dirname` 从文件名中剥离非目录后缀。

### `echo`
`echo` 显示一行文本。

### `env`
`env` 在修改后的环境中运行程序。

### `expr`
`expr` 评估表达式。

### `factor`
`factor` 打印所有指定整数的质因数。

### `false`
`false` 始终以表示失败的状态码退出。

### `groups`
`groups` 打印用户所属的组。

### `hostid`
`hostid` 打印当前主机的数字标识符（十六进制）。

### `hostname`
`hostname` 设置或打印当前主机系统的名称。

### `id`
`id` 打印用户或当前用户的真实有效 UID 和 GID。

### `logname`
`logname` 打印当前用户的登录名。

### `nice`
`nice` 以修改后的调度优先级运行程序。

### `nohup`
`nohup` 运行不受挂断影响的命令，并将输出到非 tty。

### `pathchk`
`pathchk` 检查文件名是否有效或可移植。

### `pinky`
`pinky` 是一个轻量级的 finger 工具，用于检索特定用户的信息。

### `printenv`
`printenv` 打印全部或部分环境变量。

### `printf`
`printf` 格式化并打印数据（同 C 语言 `printf` 函数）。

### `pwd`
`pwd` 打印当前/工作目录的。

### `seq`
`seq` 按指定的增量在特定范围内打印数字。

### `sleep`
`sleep` 延迟指定的时间。

### `stty`
`stty` 更改并打印终端行设置。

### `su`
`su` 使用替换的用户和组 ID 运行 shell。

### `tee`
`tee` 从标准输入读取并写入标准输出和文件。

### `test`
`test` 检查文件类型并比较值。

### `true`
`true` 始终以表示成功的状态码退出。

### `tty`
`tty` 打印连接到标准输入的终端文件名。

### `uname`
`uname` 打印系统信息。

### `uptime`
`uptime` 告诉系统运行了多久。

### `users`
`users` 打印当前的用户

### `who`
`who` 显示谁登录。

### `whoami`
