
# 概述

本章包含一组命令。这些命令用于执行基础系统功能和操作，例如管理命令历史、检查系统进程信息等。

你会发现 Linux 有一个非常强大的命令历史功能，具有许多快捷键和技巧可以方便访问以前使用的命令。

要查看你以前输入的命令列表，输入：`history`

注意：你输入的命令历史存储在文件中：`~/.bash_history`

要执行列表中的特定命令，输入：`!#` （将 `#` 替换为运行的命令编号（例如：`!100` ))

提示：如果你在命令前加一个空格，它将不会从 shell 历史记录中省略。

- 清除当前会话历史，输入：`history -r`
- 重新执行你输入的最后一个命令，输入：`!!`
- 以 root 权限重新运行上一个命令，输入：`sudo !!`
- 提示：重复上一个命令直到其执行成功，输入：`until !!; do :; done`
- 将上一个命令回显终端，输入：`!!:p`
- 在搜索历史中找到并执行匹配搜索字符串（即 `echo`）的最后一个命令，输入：`!?echo`
- 提示：要搜索并执行匹配字符串的最后一个命令，输入：`!?echo?:p`
- 重新执行上一个命令的选项，输入：`!$`
- 示例：列出一个目录文件夹，然后切换到该路径，输入：`ls /bin` (按回车) `cd !$` (按回车) 插入不带最后一个参数的最后一个命令，输入：`!:-`
- 按 `Ctrl+R` 反向搜索命令历史。
- 注意：这一次只能处理一个命令，按 `Ctrl+R` 下一个（按 `Ctrl+C` 取消）。
- 提示：从 `history` 命令获取更多信息（例如日期和时间），输入：`HISTTIMEFORMAT="%d/%m/%y %T " && history`
- 将运行过的最后一个长命令保存到脚本中：`echo "!!" > script_file.sh`
- 提示：按下 `ESC` 然后按 `*`（星号或 `TAB` 键）将插入自动补全的命令行结果，输入：`lsb_<ESC>\*`
- 注意：按下 `ESC` 然后按 `.`（点）将插入上一个命令的最后一个参数
- 查看 GB 为单位的空内存，输入：`free -g`
- 查看所有运行中的进程，输入：`ps -A`
- 如果有多个进程在运行，更实用的版本是输入：`ps -aux | less`
- 列出所有包含字符串（即 stuff）的运行进程：`ps aux | grep search_query`
- 查看当前日期和时间，输入：`date`
- 提示：显示美国西海岸下周三上午 10 点的本地时间，输入：`date --date='TZ="America/Los_Angeles" 09:00 next Fri'`
- 将你在 shell 中输入的任何内容（带时间戳）记录到名为 'typescript' 的文件中：`script -t 2> timing.txt -a session.txt`
- 在此处运行一些命令，完成后输入：`Ctrl+D` 或 `exit`。要回放记录的脚本，输入：`scriptreplay timing.txt session.txt`
- 显示你正在运行的发行版名称和版本，输入：`uname -a` OR— `lsb_release -a`
- 安装该命令，输入：`sudo apt-get install lsb` OR—`sudo yum install redhat-lsb-core`
- 检查发行版的另一种方法，输入：`cat /etc/issue`
- 查看你以什么用户名登录，输入：`whoami`
- 如果你不想学习 vi 或 vim 这样的文本编辑器，输入：`nano filename.txt`
- 注意：`nano` 是一个非常基础的文本编辑器，设计易于使用（它没有其他文本编辑器强大）。
- 创建一个可供脚本使用的变量，输入：`export test=HelloWorld` 显示变量内容，输入：`echo $test`
- 提示：要查看所有环境变量，输入：`env`
- 列出所有以字母 'S'（或任何其他字母）开头的定义变量，输入：`echo ${!S\*}` 
- 查看变量的内容，输入：`echo $SECONDS`
- 将文件从当前目录位置移动到之前所在的目录，输入：`mv file_name.ext $OLDPWD`
- 注意：`$OLDPWD` 是一个定义的变量，存储了你上次所在的目录。例如，输入：`cd /home` ，然后输入：`echo $OLDPWD` 。它将显示上一个目录的名称。
- 临时秒表（按 `Ctrl+D` 停止），输入：`time read`
- 需要帮助查找执行某操作的命令，输入：`apropos "directory"` OR— `apropos "file"`
- 查看当前年份或其他任何日期的日历，输入：`cal` OR- `cal -y` OR- `cal 2025`
- 显示系统运行时间（即操作系统启动以来的时间），输入：`uptime` OR— `uptime -p`
- 计时命令完成执行所需的时间，输入：`time ls -al /`
- 设置本地系统时间，输入：`sudo date --set="20:20:00"`
- 显示 ASCII 图表，输入：`man 7 ascii`

## 多用户系统管理

UNIX（以及后来的 Linux）从操作系统诞生之初就是多用户系统。Linux 有多个用于显示和管理登录用户的实用程序和命令。

- 显示当前登录用户的摘要，输入：`who` OR— `users`
- 显示用户最后一次登录系统的时间（包括真实用户 ID 和有效用户 ID），输入：`last user_name` OR— `last -ap`
- 显示系统上已知用户的信息，输入：`logins -u`

注意：`utmp`, `wtmp`, `btmp` 跟踪系统的所有登录和注销情况。这些文件被 `last` 和 `logins` 命令使用；`utmp` 维护当前状态的完整计数、系统启动时间（供 `uptime` 使用）、记录的终端、系统事件；`wtmp` 记录失败的登录尝试（包括它们上次运行的进程）；`btmp` 显示当前活动和登录用户的摘要。

## 文件系统命令

这些命令和工具执行基本功能，用于管理文件。Linux 拥有一套非常强大的用于管理设备、文件系统（包括分区和卷）以及相关文件的。关于文件系统的更多信息，请参阅“存储”章节。

| 格式 | 文件系统 | 已用 | 可用 |
| :--- | :--- | :--- | :--- |
| 常规 | root | 23701280 | 14417528 |
| 人类可读 | root | 227G | 138G | 89G |

- 以人类可读格式查看本地磁盘空间，输入：`df -h`
- 查看目录中的文件，输入：`ls` OR— `ls -al` 查看所有隐藏文件
- 注意：如果文件名开头有 '.'，则 '`ls`' 命令将无法显示它。
- 按大小排序文件（人类可读），输入：`ls -S`
- 提示：`ls -l`（详细格式列出目录）的快捷方式，输入：`ll`
- 切换路径到用户目录，输入：`cd ~` OR— 返回上一个目录，输入：`cd -`
- 注意：查看当前路径，输入：`pwd`
- 创建目录，输入：`mkdir folder_name`
- 复制文件，输入：`cp input_file output_file` 使用 `-r` 进行递归，输入：`cp -r dir1 dir2`
- 删除文件，输入：`rm file_name.ext`
- 警告：在使用破坏数据的命令配合通配符或其他递归功能时要格外小心，你可能会迅速删除大量无意删除的数据。
- 提示：删除所有非匹配字符串（即 `.txt`）的文件，输入：`rm !(.txt)`
- 删除文件夹，输入：`rmdir folder_name`
- 递归删除目录（例如子目录，`folder1/folder2/folder3`），输入：`rm -r folder_name`
- 提示：该命令是交互式的，在删除任何内容之前会询问权限，要使其不提示，输入：`rm -rf folder_name`
- 查找系统文件的位置，输入：`locate samba.conf`
- 查找文件所在位置，输入：`locate -i .bashrc`
- 注意：`locate` 命令通过搜索由 `updatedb` 命令维护的数据库工作。
- 查看文件内容，输入：`cat file_name.ext`

示例输出：
```
user@localhost:~$ cat text_file.txt Lorem ipsum dolor sit amet, consectetur adipiscing elit. In quis metus facilisis aliquam quis non nisl.
```
- 提示：要逐页查看文件内容，输入：`more file_name.ext`。 `less` 工具是 `more` 命令的高级版本，输入：`less file_name.ext`

要查找可执行文件的存储位置，请输入：`which mkdir`

提示：此命令的替代方案是，输入：`type -a mkdir`
