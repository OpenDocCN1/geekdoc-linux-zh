
# Task 1:

- `man 5 updatedb.conf`

`updatedb.conf` 文件应包含一条指令，用于修剪类似 `/tmp/` 和 `/media` 等路径。鉴于你对 FHS 的了解：你认为从 `locate` 数据库中修剪这些路径有什么好处？为什么修剪 `nfs` 和 `proc` 等文件系统类型是个好主意？

# Task 2:

现在运行：

- `which which`
- `which locate`
- `whereis locate`
- `whereis updatedb`
- `whereis whereis`

`which` 显示给定（相对）命令的绝对位置，而 `whereis` 在此基础上扩展，显示其他相关文件，如配置文件、数据库和手册页。

# Notes:

许多常见的 Linux 工具是相当复杂的 C 程序；`which` 是一个例外。它是一个简短的 shell 脚本，稍加练习，你就可以完全理解它。查看 `/bin/which` 文件，看看其中有多少内容对你有意义！
