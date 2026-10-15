
`ulimit -a` 限制用户资源<br>e.g. `ulimit -a` (-a: 显示系统的所有限制)

`umask` 显示或设置文件权限值<br>e.g. `umask 0022` (允许用户读写，其他用户读取)

`umask` 显示或设置文件权限值<br>e.g. `umask 0002` (允许用户组读写，其他用户读取)

`umask` 显示或设置文件权限值<br>e.g. `umask 077` (允许用户读写，其他用户权限)

`umount` 卸载设备或文件系统<br>e.g. `umount /dev` (卸载设备)

`unalias` 移除别名<br>e.g. `unalias alias` (删除别名)

`uname -a` 显示当前系统信息<br>e.g. `uname -a` (-a: 显示所有信息)

`uname -n` 显示当前系统信息<br>e.g. `uname -n` (-n: 显示主机名)

`unexpand` 将空格转换为制表符<br>e.g. `unexpand myfile.txt` (将 `myfile.txt` 转换为制表符)

`uniq` 过滤文件中的重复行<br>e.g. `uniq myfile.txt` (显示 `myfile.txt` 中的唯一行)

`unset` 移除 shell 变量或函数<br>e.g. `unset var` (删除变量)

`unzip` 从 zip 格式解压文件<br>e.g. `unzip archive.zip` (解压 `archive.zip`)

`uptime` 显示系统运行时间<br>e.g. `uptime` (显示系统运行时间)

`useradd` 添加新用户账户<br>e.g. `useradd username` (创建用户账户)

`useradd -d` 显示新用户的默认目录<br>e.g. `useradd -d` (显示默认目录)

`userdel` 删除现有用户账户<br>e.g. `userdel username` (删除用户账户)

`usermod -d` 修改主目录<br>e.g. `usermod -d /home/mydir` (-d: 指定主目录)

`usermod -l` 修改现有用户账户<br>e.g. `usermod -l username` (-l: 登录名)

`usermod -p` 修改现有用户账户<br>e.g. `usermod -p password` (-p: 修改密码)

`users` 显示当前登录的用户<br>e.g. `users` (列出所有登录的用户)

`vdir` 详细显示目录内容<br>e.g. `vdir` (`vdir` 类似于 `ls`，但更详细)

`vi` 打开文本编辑器<br>e.g. `vi filename` (用 编辑器打开文件)

`vmstat` 报告虚拟内存统计信息<br>e.g. `vmstat` (报告交换、磁盘 i/o 设备等)

`w` 列出每个用户的当前进程<br>e.g. `w username` (显示用户的进程)

`w -s` 以摘要形式列出当前进程<br>e.g. `w -s` (-s: 显示进程摘要)

`wait` 等待进程改变<br>e.g. `wait` (等待进程变化)

`watch` 定期执行命令<br>e.g. `watch -n 5` (-n5: 每 5 秒更新一次)

`wc` 显示字数、行数等<br>e.g. `wc myfile.txt` (列出 `myfile.txt` 的字数、行数等)

`wc -c` 显示字节数、行数等<br>e.g. `wc -c myfile.txt` (-c: 显示字节数)

`wget` 从网站下载网页<br>e.g. `wget http://www.example.com` (从上述 URL 下载网页)

`wget -c` 从网站下载网页<br>e.g. `wget -c http://www.example.com` (-c: 继续下载之前的)

`whatis` 显示命令的帮助页<br>e.g. `whatis ping` (显示 `ping` 的帮助页)

`whereis` 定位命令的源码、手册位置<br>e.g. `whereis ls` (显示 `ls` 的源码、手册位置)

`which` 显示可执行命令的路径<br>e.g. `which ftp` (显示 `ftp` 命令的完整路径)

`who` 显示当前登录的用户<br>e.g. `who` (列出所有登录用户、日期、时间...)

`who -a` 列出所有当前登录的用户<br>e.g. `who -a` (-a: 所有信息)

`whoami` 显示当前用户的登录名<br>e.g. `whoami` (显示你自己的用户名)

`whois` 显示域名所有者信息<br>e.g. `whois xvqix.com` (列出 `xvqix.com` 所有者信息)

`write` 向另一个用户写入消息<br>e.g. `write username` (然后写入你的消息...)

`xargs` 带参数执行命令<br>e.g. `find -name "a.*" | xargs rm` (找到名为 `a.*` 的文件并删除它们)

`xcalc` 启动图形化计算器<br>e.g. `xcalc` (打开科学计算器)

`xclock` 启动图形化时钟<br>e.g. `xclock -digital` (-digital: 指定数字钟)

`yes` 重复输出字符串直到停止<br>e.g. `yes "hello"` (重复输出 `hello` 直到停止)

`yum` 基于 `rpm` 的包管理器<br>e.g. `yum install update` (安装名为 `update` 的包)

`zcat` 输出压缩的文本<br>e.g. `zcat myfile.txt.gz | less` (解压文件并显示内容)

`zless` 显示未压缩/压缩的文件内容<br>e.g. `zless myfile.txt.gz` (`zless`: 按页显示内容)

`zmore` 显示未压缩/压缩的文件内容<br>e.g. `zmore myfile.txt.gz` (`zmore`: 按屏显示内容)

`zip` 将文件压缩为 zip 格式<br>e.g. `zip documents *` (为所有文件创建 `documents.zip`)

`unzip` 从 zip 格式解压文件<br>e.g. `unzip myfile.zip` (解压 `myfile.zip`.)

# 结语

我的朋友们：

这本书仅用于快速学习基础 Linux 命令。

感谢您的支持！

如果您愿意为这本书写一个积极的评价，我将不胜感激。

非常感谢！

顺颂商祺

诚挚地，

Ray Yao

我的朋友，我们下次见！

这本书是一本为初学者编写的指南，旨在快速学习 Linux 管理员或初学者频繁使用的 Linux 命令。书中涵盖了所有核心的 Linux 命令及其操作方法、示例和解释。它还包含了 Linux 帮助命令、符号、快捷键、运行级别（`run levels`）以及 `Vi` 命令。

书中有一张包含所有常用 Linux 命令的长表格，这对你的工作或学习将会有很大帮助。你可以快速学会所有核心的 Linux 命令。
