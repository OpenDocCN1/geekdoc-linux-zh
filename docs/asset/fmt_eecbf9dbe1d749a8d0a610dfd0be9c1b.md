
# Shellutils

`Shellutils` 包包含 `basename`, `chroot`, `date`, `dirname`, `echo`, `env`, `expr`, `factor`, `false`, `groups`, `hostid`, `hostname`, `id`, `logname`, `nice`, `nohup`, `pathchk`, `pinky`, `printenv`, `printf`, `pwd`, `seq`, `sleep`, `stty`, `su`, `tee`, `test`, `true`, `uname`, `uptime`, `users`, `who`, `whoami` 程序。

## 描述

`basename` 去掉文件名中的目录。
`chroot` 运行命令或交互式 shell。
`date` 以指定的格式显示当前时间。
`dirname` 去掉文件名中的目录部分。
`echo` 显示一行文本。
`env` 在修改的环境中运行程序。
`expr` 计算表达式。
`false` 总是以失败状态码退出。
`groups` 打印用户所属的组。
`hostid` 以十六进制打印当前主机的数字标识符。
`hostname` 设置或打印当前主机名。
`id` 打印用户的真实和有效 UID 和 GID。
`logname` 打印当前用户的登录名。
`nice` 以修改的调度优先级运行程序。
`nohup` 运行不受挂断信号影响的命令，输出到非终端。

### yes

`yes` 会不断输出字符串，直到被杀死。

# Shadow Password 套件内容

`Shadow Password Suite` 包含 `chage`, `chfn`, `chsh`, `expiry`, `faillog`, `gpasswd`, `lastlog`, `login`, `newgrp`, `passwd`, `sg`, `su`, `passwd`, `dpasswd`, `groupadd`, `groupdel`, `groupmod`, `grpck`, `grpconv`, `grpunconv`, `logout`, `mkpasswd`, `newusers`, `pwck`, `pwconv`, `pwunconv`, `useradd`, `userdel`, `usermod` 和 `vipw` 程序。

## 描述

### chage

`chage` 修改密码更改之间的天数以及最后一次密码更改的日期。

### chfn

`chfn` 修改用户账户的全名、办公室号码、办公室分机和家庭电话信息。

### chsh

`chsh` 更改用户的登录 shell。

### expiry

目前尚清楚该程序的用途。

### faillog

`faillog` 格式化失败日志 `/var/log/faillog` 的内容，并维护失败计数和限制。

### gpasswd

`gpasswd` 用于管理 `/etc/group` 文件。

### lastlog

`lastlog` 格式化并打印最后登录日志 `/var/log/lastlog` 的内容。将打印登录名、端口和最后登录时间。

### login

`login` 用于与系统建立新会话。

### newgrp

`newgrp` 用于在登录会话期间更改组 ID。

### passwd

`passwd` 修改用户和组账户的密码。

### sg

`sg` 以不同的组 ID 执行命令。

### su

将有效用户 ID 和组 ID 更改为用户的 ID 和组 ID。这替换了从 `Shellutils` 软件包安装的 `su` 程序。

### chpasswd

`chpasswd` 从标准输入读取用户名和密码对对的文件，并使用这些信息更新一组现有用户。

# dppasswd

`dppasswd` 为用户登录 shell 添加、删除和更新拨号密码。

### groupadd

`groupadd` 命令使用命令行上指定的值和系统默认值创建新组账户。

### groupdel

`groupdel` 命令修改系统账户文件，删除所有引用组的条目。

### groupmod

`groupmod` 命令修改系统账户文件以反映命令行上指定的更改。

### grpck

`grpck` 验证系统身份验证信息的完整性。

### grpconv

`grpconv` 将普通组文件转换为影子组文件。

### grpunconv

`grpunconv` 将影子组文件转换为普通组文件。

### logoutd

`logoutd` 强制执行 `/etc/porttime` 中指定的登录时间和端口限制。

### mkpasswd

`mkpasswd` 读取标志指定格式的文件并将其转换为相应的数据库文件格式。

### newusers

`newusers` 读取用户名和明文密码对的文件，并使用这些信息更新一组现有用户或创建新用户。

### pwck

`pwck` 验证系统身份验证信息的完整性。

### pwconv

`pwconv` 将普通 `passwd` 文件转换为影子文件。

### pwunconv

`pwunconv` 将影子 `passwd` 文件转换为普通文件。

### useradd

`useradd` 创建新用户或更新默认新用户信息。

### userdel

`userdel` 修改系统账户文件，删除所有引用指定登录名的条目。

### usermod

`usermod` 修改系统账户文件以反映命令行上指定的更改。

# vipw 和 vigr

`vipw` 和 `vigr` 分别编辑 `/etc/passwd` 和 `/etc/group` 文件。带有 `~s` 标志，它们将分别编辑这些文件的影子版本，即 `/etc/shadow` 和 `/etc/gshadow`。

# Modutils

## 内容

`Modutils` 软件包包含 `depmod`, `genksyms`, `insmod`, `insmod_ksymops_clean`, `kerneld`, `kernelversion`, `ksyms`, `lsmod`, `modinfo`, `modprobe` 和 `rmmod` 程序。

## 描述

### depmod

`depmod` 处理可加载内核模块的依赖描述。

### genksyms

`genksyms` 读取（标准输入） `gcc -E source.c` 的输出并生成包含版本信息的文件。

### insmod

`insmod` 在运行的内核中安装可加载模块。

### insmod_ksymops_clean

`insmod_ksymops_clean` 删除 2 天未访问的保存 `ksyms` 和模块。

### kerneld

`kerneld` 在用户空间执行内核操作（例如按需加载模块）。

### kernelversion

`kernelversion` 报告运行内核的主版本。

### ksyms

`ksyms` 显示导出的内核符号。

### lsmod

`lsmod` 显示所有加载模块的信息。

### modinfo

`modinfo` 检查与内核模块关联的对象并显示它可以获取的任何信息。

### modprobe

`modprobe` 使用 `depmod` 创建的类似 Makefile 的依赖文件，从预定义目录树中可用的模块集中自动加载相关模块。

### rmmod

`rmmod` 从运行的内核中卸载可加载模块。

# Procinfo

## 内容

`Procinfo` 软件包包含 `procinfo` 程序。

## 描述

`procinfo` 从 `/proc` 目录收集一些系统数据并以良好的格式打印到标准输出设备上。

# Procps

## 内容

`Procps` 软件包包含 `free`, `kill`, `ps`, `skill`, `snice`, `sysctl`, `tload`, `top`, `uptime`, `vmstat`, `w` 和 `watch`。

## 描述

`free` 显示空闲和使用的交换内存量。
`kill` 向进程发送信号。
`ps` 提供进程的快照。
`skill` 向进程发送信号。
`snice` 进程调度优先级。
`sysctl` 在运行时修改内核参数。
`tload` 输出系统负载图（如果未指定）。
`top` 提供处理器状态的实时查看。
`uptime` 一行显示当前时间、系统运行时间、登录用户数以及过去 1、5、15 分钟的系统平均负载。
`vmstat` 报告进程、分页、块 IO 和 CPU 活动的信息。
`w` 显示当前登录机器的用户。
`watch` 重复运行命令并全屏显示其输出。

# Vim

## 内容

`Vim` 软件包包含 `ctags`, `etags`, `ex`, `gview`, `gvim`, `rgview`, `rgvim`, `rview`, `rvim`, `view`, `vimtutor` 和 `xxd`。

## 描述

`ctags` 为源代码生成标签文件。
`etags` 与 `ctags` 相同，但它可以生成交叉引用文件，列出文件中各种源对象的信息。
`ex` 以 Ex 模式启动 vim。
`gview` 是 `view` 的 GUI 版本。
`gvim` 是 `vim` 的 GUI 版本。
`rgview` 是 `rview` 的 GUI 版本。
`rgvim` 是 `rvim` 的 GUI 版本。
`rview` 是 `view` 的限制版本。无法启动 shell且 Vim 不能挂起。
`rvim` 是 `vim` 的限制版本。无法启动 shell且 Vim 不能挂起。
`view` 以只读模式启动 vim。
`vim` 以常规方式启动 vim。
`vimtutor` 启动 Vim 教程。
`xxd` 创建十六进制转储或反之。

# Psmisc

## 内容

`Psmisc` 软件包包含 `fuser`, `killall` 和 `pstree`。
