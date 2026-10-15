
24. __________ 是复制到每个用户家目录的文件位置。

25. `PS1` 环境变量用于定义以下哪项？

    - A. 命令路径

    - B. 家目录

    - C. shell 提示符

    - D. 签名文件

26. 以下哪项会将用户的 `pwd` 更改为其家目录，无论其当前 `pwd` 是什么？（选择所有适用项。）

    - A. `cd`

    - B. `cd ..`

    - C. `cd-`

    - D. `cd $HOME`

27. 以下哪个目录用于存储超级用户使用的系统实用程序？

    - A. `/etc`

    - B. `/root`

    - C. `/sbin`

    - D. `/usr/local`

28. 在哪里分配用户 shell？

    - A. `/etc/skel`

    - B. `/etc/passwd`

    - C. `/etc/profile`

    - D. `LILO`

29. 你最近在你的 Linux 系统中安装了一个新的磁盘驱动器。你希望在新磁盘驱动器上存储一个包含公司内部使用的许多数据文件的目录。以下哪项可用于使该变化对系统用户不可见？

    - A. `cp`

    - B. `mv`

    - C. 硬链接

    - D. 软链接

30. 哪个命令和选项用于删除用户的帐户和家目录？

    - A. `userdel -r`

    - B. `usermod -f`

    - C. `passwd -e`

    - D. `usermod -e`

31. ____________ 实用程序用于以十六进制格式显示文件。

32. 哪个命令可用于在文件内定位特定文本？

    - A. `grep`

    - B. `locate`

    - C. `find`

    - D. `where`

33. 以下哪项可用于挂起在前景中运行的进程？

    - A. `&`

    - B. `fg`

    - C. `bg`

    - D. `Ctrl+Z`

34. 你可以在哪里找到在 Linux 系统上安装和配置 Winmodem 的说明？

    - A. man pages

    - B. HOWTOs

    - C. `/usr/doc`

    - D. `dmesg`

35. 以下哪项将用于将名为 `mozilla_update` 的脚本作为后台进程运行？

    - A. `bg mozilla_update`

    - B. `mozilla_update&`

    - C. `mozilla_process`

    - D. `mozilla_process -bg`

### 考试 101

36. 如果想在不指定绝对路径的情况下运行文件，应使用哪个环境变量来指定文件的位置？

- A. `HOME`

- B. `PS1`

- C. `PATH`

- D. `TERM`

37. ____________________ 命令用于更改文件的所有者。

38. 在启动系统时，你注意到声音模块加载失败；但是，错误信息滚动得很快，转瞬即逝。你可以使用什么命令来查看这些错误？

- A. `dmesg`

- B. `messages`

- C. `errors`

- D. `lilo`

39. 使用哪个命令可以创建新的压缩归档文件？

- A. `gzip -t`

- B. `tar -cfz`

- C. `compress -tf`

- D. `bzip2 -tbz`

40. 使用哪个命令查看在后台运行的进程？

- A. `dmesg`

- B. `ls`

- C. `bg`

- D. `jobs`

41. 使用哪个实用程序查看文件的开头部分？

- A. `tac`

- B. `cat`

- C. `head`

- D. `top`

42. 哪种配额限制会阻止用户创建新文件？

- A. 停止限制

- B. 软限制

- C. 硬限制

- D. 最大限制

43. 哪个运行级（runlevel）用于执行本地管理任务，并禁止系统建立网络连接？

- A. 0

- B. 1

- C. 3

- D. 6

44. 用户配额保存在哪个文件中？

- A. `/etc/fstab`

- B. `/etc/passwd`

- C. `/quota.user`

- D. `/lilo`

45. 同事告诉你，关于 `syslog` 命令的信息可以在第 3 手册页（man page 3）中找到。你将如何查看这些信息？

- A. `man syslog 3`

- B. `man syslog -3`

- C. `man -3 syslog`

- D. `man 3 syslog`

46. 哪个命令不用于查看文件内容？

- A. `cat`

- B. `more`

- C. `less`

- D. `expand`

47. _______ 命令用于卸载文件系统。

48. _______ 命令将显示之前输入过的命令。

49. 使用 `www.deja.com` 你可能会找到哪类信息？

- A. 手册页

- B. Usenet 帖子

- C. 软件补丁

- D. 内核更新

50. 哪个目录不占用磁盘空间？

- A. `/proc`

- B. `/boot`

- C. `/root`

- D. `/local`

51. ______ 命令用于对文件系统执行一致性检查。

52. 哪个命令可以创建一个名为 `mydirlisting` 的文件，其中包含主目录中所有文件和目录的详细列表？

- A. `ls -aLR $HOME > mydirlisting`

- B. `ls -d > mydirlisting`

- C. `mydirlisting < ls -al $HOME`

- D. `ls -al | mydirlisting`

### 考试 102

1. ______ 命令用于创建 `ext2` 文件系统。

2. 你正在修复系统的主引导记录。你已通过启动盘启动系统，目前根卷已挂载到 `/recover`。你将如何重新安装 `LILO`？

- A. `lilo -r /recover/boot`

- B. `lilo -f /recover`

- C. `lilo -r /recover`

- D. `lilo -r /recover -b /recover/boot`

3. 添加新库时，需要更新哪个文件。

4. 哪个命令可以删除名为 `editor-2.0.i386.rpm` 的软件包？

- A. `rpm -i editor-2.0.i386.rpm`

- B. `rpm -e editor-2.0.i386.rpm`

- C. `dpkg -install editor-2.0.i386.rpm`

- D. `apt-get install editor-2.0.i386.rpm`

5. 要在编译前对内核配置进行单项修改，你会编辑哪个文件？

- A. `/usr/src/linux/Makefile`

- B. `/usr/src/linux/.config`

- C. `/usr/src/linux/config`

- D. `/usr/src/linux/configure`

6. 哪个命令可以告诉你哪个软件包拥有 `/etc/printcap` 文件？

- A. `dpkg -F /etc/printcap`

- B. `rpm -f /etc/printcap`

- C. `who /etc/printcap`

- D. `rpm -qf /etc/printcap`

7. __________ 文件会在所有非登录 `bash` 会话中执行。

8. 哪个命令显示你的主机与远程主机 `www.somedomain.org` 之间的路由？

- A. `traceroute -n www.somedomain.org`

- B. `route www.somedomain.org`

- C. `ping -r www.somedomain.org`

- D. `route -n www.somedomain.org`

9. 哪个命令最适合用于查找其他域名的联系人名称？

- A. `nslookup`

- B. `whois`

- C. `whois`

- D. `dig`

10. 更新 `inetd.conf` 文件后，必须运行哪个（些）命令？

- A. `/etc/rc.d/init.d/inetd restart`

- B. `kill -1 inetd`

- C. `kill -1 `cat /var/run/inetd.pid``

- D. 无需命令。

11. 可以创建 __________ 文件以防止非 `root` 用户登录到系统。

12. 哪个（些）命令用于启用影子密码？

- A. `shadow`

- B. `pwconv`

- C. `pwconv`

- D. `grpconv`

13. 哪个（些）命令用于解压文件 `mydoc.gz`？
