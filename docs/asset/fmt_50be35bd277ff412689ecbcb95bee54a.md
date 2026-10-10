
- B. `-a`

- C. `-l`

- D. `-o`

# 第3章 GNU 和 Unix 命令 (领域 103)

7. `head` 和 `tail` 命令默认打印的行数分别是？

- A. `head` 为 10，`tail` 为 5

- B. `head` 为 5，`tail` 为 10

- C. 均为 10

- D. 均为 30

8. 你正尝试使用 `rm` 删除目录，但内部仍有文件和其他目录。假设你确定要删除该目录及其所有内容，需要什么命令和参数？

- A. `rm -f`

- B. `rm -rf`

- C. `rm -a`

- D. `rm -m`

9. 哪个命令将查找当前目录下以 2014 开头的目录？

- A. `find ./ -name "2014"`

- B. `find . -type d -name "2014"`

- C. `find / -type d -name "2014"`

- D. `find ./ -type d -name "2014*"`

10. 下列哪个命令可以从 `/etc/passwd` 获取排序后的用户名列表？

- A. `cat /etc/passwd | awk -F':' '{print $1}' | sort`

- B. `sort /etc/passwd | cut`

- C. `echo /etc/passwd`

- D. `cat /etc/passwd | awk '{print $1}' | sort`

11. `ls` 的哪些选项可以产生包含隐藏（点）文件的输出，并按最新文件在输出末尾进行排序？

- A. `-la`

- B. `-lat`

- C. `-ltr`

- D. `-altr`

12. 对已存在的文件执行 `touch` 命令，结果是什么？

- A. 文件的访问时间将在执行 `touch` 命令时更改为当前时间。

- B. 文件将被覆盖。

- C. 没有变化。

- D. 文件将被追加。

13. `mv` 和 `cp` 命令的哪个选项项会导致命令在覆盖已存在的文件之前进行提示？

- A. `-f`

- B. `-Z`

- C. `-r`

- D. `-i`

14. 下列哪个命令会将 `/etc/passwd` 的内容发送到标准输出（`stdout`）以及一个名为 `passwordfile` 的文件中？

- A. `cat /etc/passwd > passwordfile`

- B. `var /etc/passwd | tee passwordfile`

- C. `cat /etc/passwd | tee passwordfile`

- D. `echo /etc/passwd | stdout > passwordfile`

15. 服务器当前的层次结构包含一个名为 `/usr/local` 的目录。你需要在下方创建一个名为 `/usr/local/test/october` 的额外目录。哪个命令可以完成此任务？

- A. `mkdir -p /usr/local/test/october`

- B. `mkdir /usr/local/test/october`

- C. `mkdir -r /usr/local/test/october`

- D. `mkdir -f /usr/local/test/october`

16. `cp` 命令的哪个选项会以递归方式拷贝目录？

- A. `-v`

- B. `-R`

- C. `-Z`

- D. `-i`

17. 你收到了一个没有文件扩展名的文件。你可以运行哪个命令来帮助确定它可能是什么类型的文件？

- A. `grep`

- B. `telnet`

- C. `file`

- D. `export`

18. 哪个命令将创建 `/dev/sda` 磁盘分区的镜像并将该镜像放入名为 `output.img` 的文件中？

- A. `dd if=/sda of=/dev/sda`

- B. `dd if=output.img of=/dev/sda`

- C. `dd if=/dev/sda of=output.img`

- D. `echo /dev/sda > output.img`

# 第 3 章 • GNU 和 Unix 命令 (领域 103)

19. `cut` 命令默认使用的分分隔符是什么？

- A. 冒号 (Colon)

- B. 制表符 (Tab)

- C. 空格 (Space)

- D. 逗号 (Comma)

20. 下列哪项将解压并提取经过 `tar` 压缩和 `gzip` 压缩的文件内容？

- A. `tar -zxf <file.tgz>`

- B. `tar -xf <file.tgz>`

- C. `tar -vz <file.tgz>`

- D. `tar -fd <file.tgz>`

21. 在命令通过 `&` 放入后台运行后，使用哪个命令将其带前台处理？

- A. `bg`

- B. `fore`

- C. `4g`

- D. `fg`

22. 你需要编写一个脚本，收集系统中运行的所有 `Apache` 实例的进程 ID（PIDs）。下列哪个命令可以完成此任务？

- A. `ps auxw | grep apache`

- B. `pgrep apache`

- C. `processlist apache`

- D. `ls -p apache`

23. 下列哪个命令行会持续地监控一个名为 `nagios` 的单进程？

- A. `top -n 1`

- B. `ps -p 23`

- C. `top -nagios`

- D. `top -p pidof nagios`

24. 用户报告服务器上的各种程序正在崩溃。在检查日志时，你看到某些进程报告了内存溢出（out-of-memory）状况。你可以使用哪个命令查看整体内存使用情况，包括可用交换空间（`swap space`）？

- A. `tree`

- B. `pgrep`

- C. `uptime`

- D. `free`

25. 你正在使用 `vi` 编辑器修改文件并需要退出。你收到一条提示：“No write since last change.”假设你想保存工作，下列哪个命令将保存工作并退出？

- A. `:wq`

- B. `:ql`

- C. `dd`

- D. `x`

26. 使用哪个选项来更改 `head` 和 `tail` 命令的输出行数？

- A. `-l`

- B. `-f`

- C. `-g`

- D. `-n`

27. 哪个命令可以用于确定当前的负载平均值，以及自系统上次启动以来运行时间的信息？

- A. `uptime`

- B. `sysinfo`

- C. `bash`

- D. `-u`

28. 你需要启动一个需要终端和前台处理的长时间运行进程。但是，由于安全限制，你无法保持终端窗口打开。哪个命令将让你启动该进程并在稍后返回会话？

- A. `fg`

- B. `bg`

- C. `kill`

- D. `screen`

29. 你已尝试使用服务命令停止进程，并使用了 `kill` 命令。可以使用 `kill` 命令向进程发送什么种信号来强制进程结束？

- A. `-15`

- B. `-f`

- C. `-9`

- D. `-stop`

30. 在 `Bash shell` 中工作时，你需要重定向标准输出（`stdout`）和标准错误（`stderr`）。下列哪个命令会重定向标准输出和标准错误？

- A. `1>2`

- B. `>2`

- C. `2>&1`

- D. `>>`

31. 运行哪个命令可以确定当前用户创建进程的默认优先级？

- A. `prio`

- B. `nice`

- C. `renice`

- D. `defpriority`

32. 下列哪个 `egrep` 命令将检查 `/etc/passwd` 以寻找使用 `/bin/bash` 或 `/bin/zsh` 作为其 `shell` 的用户？

- A. `grep /etc/passwd`

- B. `egrep '*/sh$' /etc/passwd`

- C. `grep '*/*.sh$' /etc/passwd`

- D. `egrep '*/\.sh$' /etc/passwd`

33. `man` 命令的哪个选项可以访问不同级别的文档，例如，系统调用文档？

- A. `man 2 <argument>`

- B. `prog <argument>`

- C. `man --sys <argument>`

- D. `man --list`

34. 使用 `vi` 进行编辑时，哪个命令会切换到插入模式并在光标位置下方打开一个新行？

- A. `f`

- B. `a`

- C. `o`

- D. `i`

35. 可以发送哪个 `kill` 信号来重启进程？

- A. `-HUP`

- B. `-RESTART`

- C. `-9`

- D. `-SIG`

36. 下列哪个命令将显示你 `Bash` 历史记录的最后 50 行，包括当前会话的命令？

- A. `bash 50`

- B. `history 50`

- C. `cat .bash_history`

- D. `tail -f .bash_history`

# 第 4 章

# 设备、Linux 文件系统和文件标准 (领域 104)

以下 `CompTIA LINUX+/LPIC-1` 考试目标在本章中涵盖：

- 104.1 创建分区和文件系统

    - 管理 `MBR` 分区表
    - 使用各种 `mkfs` 命令创建各种文件系统，如
        - `ext2`
        - `ext3`
        - `ext4`
        - `XFS`
        - `VFAT`
    - 对 `ReiserFS` 和 `Btrfs` 的了解
