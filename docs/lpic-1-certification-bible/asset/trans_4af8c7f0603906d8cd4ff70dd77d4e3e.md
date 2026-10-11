

- Linux 打印 HOWTO——本 HOWTO 提供了有关配置 Linux 打印的信息。
- Linux 安全 HOWTO——本 HOWTO 提供了有关为 Linux 系统提供安全防护的信息。
- SMB HOWTO——本 HOWTO 提供了有关配置 SMB 的信息。
- Linux 声音 HOWTO——本 HOWTO 提供了有关配置 Linux 系统上声卡设备的信息。
- 用户身份验证 HOWTO——本 HOWTO 提供了有关 Linux 系统上用户身份验证流程的信息。
- Windows 局域网服务器 HOW-TO——本 HOWTO 提供了有关配置 Linux 以在包含 Microsoft 客户端的网络上提供服务器服务的详细信息。
- Winmodems 与 Linux HOWTO——本 HOWTO 提供了有关在 Linux 系统上配置 Winmodem 的信息。
- Linux WWW HOWTO——本 HOWTO 提供了有关将 Linux 配置为 Web 服务器和客户端的信息。
- Linux XDMCP HOWTO——本 HOWTO 提供了有关配置 X 显示管理器控制协议的信息。
- Linux XFree86 HOWTO——本 HOWTO 提供了有关配置 X Window 的信息。
- XFree86 视频时序 HOWTO——本 HOWTO 提供了有关配置 X Window 视频设置的信息。
- X Window 用户 HOWTO——本 HOWTO 提供了有关为用户配置 X Window 的信息。

## 故障排除

如果在安装或使用 CD-ROM 程序时遇到困难，请尝试以下解决方案：

- 关闭可能正在运行的任何防病毒软件。安装程序有时会模拟病毒活动，这可能会让计算机错误地认为其受到了病毒感染。（请确保稍后重新开启防病毒软件。）
- 关闭所有正在运行的程序。运行的程序越多，可用于其他程序的内存就越少。安装程序通常还会更新文件和程序；如果保持其他程序运行，安装可能无法正常工作。

如果 CD 仍然存在问题，请致电 Hungry Minds Worldwide 客户服务电话号码：(800) 762-2974。美国以外地区请致电 (317) 572-3993。Hungry Minds, Inc. 仅提供安装及其他一般质量控制项目的技术支持；如需针对应用程序本身的技术支持，请咨询该程序的销售商或作者。

# 模拟考试

本附录中的模拟考试将通过类似真实考试的测试来检验您的知识。在完成学习后使用这些考试来找出您的薄弱环节。

## 考试 101

1. 下列哪项会使 `cmd2` 独立于 `cmd1` 运行？
   - A. `cmd1 ; cmd2`
   - B. `cmd1 | cmd2`
   - C. `cmd1 >> cmd2`
   - D. `cmd1 > cmd2`

2. __________ 是 `kill` 命令使用的默认信号编号。

3. `updatedb` 命令用于更新哪个命令搜索的信息？
   - A. `grep`
   - B. `find`
   - C. `locate`
   - D. `whois`

4. 哪个命令用于在命令运行期间更改其优先级？
   - A. `job`
   - B. `nice`
   - C. `renice`
   - D. `top`

5. 哪个命令用于生成以下权限？
   ```
   -rw-rw-r--  myfile
   ```
   - A. `chown myfile`
   - B. `chmod 661 myfile`
   - C. `chmod 331 myfile`
   - D. `chmod 664 myfile`

6. 哪个文件用于指定用户的家目录？
   - A. /etc/passwd
   - B. /etc/skel
   - C. /etc/profile
   - D. /etc/bashrc

7. ___________ 用于查看安排在定期运行的作业。

8. 哪个命令将搜索 *editorial* 文件中所有 *lady* 的出现，并将它们替换为 *Lady*？
   - A. `sed -a s/lady/Lady/ editorial`
   - B. `tr l,L editorial`
   - C. `sed 's/lady/Lady/' editorial`
   - D. `grep 'lady' editorial | tr Lady`

9. 哪个命令允许您实时查看系统资源使用情况？
   - A. `nice`
   - B. `renice`
   - C. `ps -aux`
   - D. `top`

10. 哪个文件包含当前挂载的文件系统列表？
    - A. /etc/proc/
    - B. /mnt
    - C. /etc/fstab
    - D. /etc/mtab

11. 哪个选项允许环境变量声明在系统范围内使用？
    - A. `echo`
    - B. `export`
    - C. `cat`
    - D. `env`

12. 哪个命令会将 /ME 目录的文件和目录内容移动到 /YOU 目录？
    - A. `mv -a /ME /YOU`
    - B. `cp /ME/* /YOU/* ; rm -r /ME/*`
    - C. `mv /ME/* /YOU/*`
    - D. `cp -r /ME/* /YOU ; rm -r /ME`

13. 哪个命令将创建一个名为 `xmaclist` 的文件，使用列表文件的内容，按字母顺序排列内容并为每一行编号？
    - A. `fmt list > xmaclist`
    - B. `sort list | nl > xmaclist`
    - C. `ln list | sort | xmaclist`
    - D. `sort list | ln | xmaclist`

14. 以下哪个命令会终止进程 1234，而不给它优雅退出的机会？
    - A. `kill %1234`
    - B. `kill -now 1234`
    - C. `kill -9 1234`
    - D. `kill -12 1234`

15. 在 Linux 系统上创建用于数据存储的新分区时，会使用以下哪些工具？
    - A. `fdisk`
    - B. `format`
    - C. `mkfs`
    - D. `mount`

16. _______________ 实用程序提供 pwd 中已用磁盘空间的摘要。

17. 哪个命令用于编辑用户配额？
    - A. `quota`
    - B. `quotaon`
    - C. `edquota`
    - D. `vi`

18. umask 为 002 将生成什么默认文件权限？
    - A. `-rwxrwxrw-`
    - B. `-rw-rw-r--`
    - C. `--------`
    - D. `-rwxrw-rx`

19. /etc/shadow 文件需要什么访问权限？
    - A. `-r--------`
    - B. `-rw-rw-r--`
    - C. `-r-r-r-----`
    - D. `-rwxr--r--`

20. 哪个命令将立即关闭运行 Linux 的计算机？
    - A. `shutdown`
    - B. `telinit 6`
    - C. `shutdown now`
    - D. `telinit 0`

21. 新用户（Debbie）需要访问公司的 Linux 系统，必须做什么才能让她以用户 ID debbie 访问系统？（选择所有适用项。）
    - A. `useradd debbie`
    - B. `group debbie`
    - C. `shadow debbie`
    - D. `passwd debbie`

22. 哪个命令将授予我的文件的属主和组读取和执行的权限，而其他用户拥有读取权限？
    - A. `chmod 003 my file`
    - B. `chmod 554 my file`
    - C. `chmod 331 my file`
    - D. `chmod 662 my file`

23. 哪个命令用于查看 tar 实用程序的描述，包括可用的选项？
    - A. `more tar`
    - B. `grep tar`
    - C. `man tar`
    - D. `help tar`

24. __________ 是复制到每个用户家目录的文件位置。

25. PS1 环境变量用于定义以下哪项？
    - A. 命令路径
    - B. 家目录
    - C. shell 提示符
    - D. 签名文件

26. 以下哪项会将用户的 pwd 更改为其家目录，无论其当前 pwd 是什么？（选择所有适用项。）
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
    - D. LILO

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
    - C. /usr/doc
    - D. dmesg

35. 以下哪项将用于将名为 `mozilla_update` 的脚本作为后台进程运行？
    - A. `bg mozilla_update`
    - B. `mozilla_update&`
    - C. `mozilla_process`
    - D. `mozilla_process -bg`

