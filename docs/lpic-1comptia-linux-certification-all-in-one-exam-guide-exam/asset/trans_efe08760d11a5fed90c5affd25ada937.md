
+   C. search samba | man

+   D. which samba

26. 你需要查找与 PAM 服务相关的 man 手册页。哪个命令可以执行此操作？

- A. which pam
- B. man -s pam
- C. search pam | man
- D. apropos pam

27. 你需要使用 info 查看有关使用 smbpasswd 实用程序的信息。哪个命令可以执行此操作？

- A. info /smbpasswd
- B. info "smbpasswd"
- C. show info smbpasswd
- D. info smbpasswd

28. 在查看 info 节点时，哪个按键可用于导航到下一个节点？

- A. /next
- B. P
- C. N
- D. L

29. 在查看 info 节点时，哪个按键可用于导航到上一个节点？

- A. P
- B. /prev
- C. N
- D. /up

30. 在查看 info 节点时，哪个按键可用于导航到节点的开始位置？

- A. B
- B. /top
- C. HOME
- D. T

31. 你想将 `/tmp` 目录添加到系统的 `PATH` 环境变量中。你希望确保不要覆盖路径中现有的目录，因此在 shell 提示符下输入了 `PATH=PATH:~/temp`。你这样做正确吗？

- A. 是的，该命令将正确工作。
- B. 不，你必须先导出变量，然后再设置它。
- C. 不，你必须使用 $ 在每个 PATH 变量名之前。
- D. 不，你必须使用 $ 在第二个 PATH 变量名之前。

32. 你可以使用哪些命令来查看当前分配给你的环境变量的值？（选择两项。）

- A. set
- B. display
- C. var
- D. show
- E. env

33. 你想查看当前在 Linux 系统上定义的别名列表。你在 shell 提示符下可以发出什么命令来执行此操作？

- A. alias
- B. alias --l
- C. alias --a
- D. env alias

34. 哪个文件描述符指代命令处理完成后在屏幕上显示的文本？（选择两项。）

- A. stdin
- B. stdout
- C. stdisplay
- D. stdoutput
- E. stderr

35. 你想将 `tail /var/log/firewall` 命令的标准输出和标准错误发送到当前目录中名为 `lastevents` 的文件。哪个命令可以执行此操作？

- A. `tail /var/log/firewall 1> lastevents 2> lastevents`
- B. `tail /var/log/firewall > lastevents`
- C. `tail /var/log/firewall 1> lastevents 2>&1`
- D. `tail /var/log/firewall 1>&2> lastevents`

36. 你想将当前目录中 `logfile.txt` 文件的内容发送到 `sort` 命令进行按字母排序，并将其显示在屏幕上。哪个命令可以执行此操作？

- A. `sort < ./logfile.txt`
- B. `sort -i /logfile.txt`
- C. `sort < ./logfile.txt -d "screen"`
- D. `sort < ./logfile.txt > screen`

### 答案

1. C. bash 是大多数 Linux 发行版使用的默认 shell。

2. C. 按下 ALT-F2 将打开另一个控制台。你可以使用此控制台执行其他任务，而无需停止在第一个控制台屏幕上运行的程序。你可以通过按下 ALT-F1 切换回来。

3. B. 在文件名前添加 `./` 告诉 shell 该文件位于当前目录中。

4. A 和 D. 这两个命令都会将 PATH 环境变量打印在屏幕上。

5. A. Linux 是区分大小写的。题目中的命令使用了大写字母 U。

6. D. `top` 实用程序显示正在运行的进程。

7. C. `ifconfig` 命令用于查看和修改你的网卡配置。

8. D. `su` 命令可用于在 shell 提示符下切换到不同的用户账户。语法是 `su username`。如果你省略用户名，`su` 命令假定你想切换到 root 超级用户账户。

9. A. 非登录 shell 读取 `.bashrc` 文件以定义用户的 shell 环境。

10. E. 当 bash 登录 shell 首次打开时，会读取 `/etc/profile` 文件。

11. B. `.bash_history` 文件包含你最近的 shell 命令列表。

12. C. TAB 键用于命令补全。

13. A. `man` 实用程序用于查看 man 手册页。如果某个特定命令或实用程序没有可用的 info 节点，那么 `info` 实际上也可能显示 man 手册页。

14. D. MANPATH 环境变量存储大多数 Linux 发行版中 man 手册页的路径。

15. A. 你可以使用 `/etc/man_db.conf` 文件在某个 Linux 发行版上指定 man 文件的路径。

16. C. 手册的第 8 节包含 root 使用的实用程序和命令的 man 手册页。

17. B. 手册的第 1 节包含任何用户都可以使用的命令的 man 手册页。

18. D. `man mkdir` 命令将显示 mkdir 的 man 手册页。

19. C. `man chmod` 命令将显示 chmod 的 man 手册页。

20. B. man 手册页的 **SYNOPSIS** 部分提供了命令或实用程序所用语法的回顾。

21. C. man 手册页的 **SEE ALSO** 部分提供了相关资源列表。

22. D. 按下 *Q* 将退出 man。

23. C. 要在 man 手册页中搜索表达式“password”，你输入 `/password`。

24. C. 输入搜索词后，按下 *N* 将带你进入 man 手册页中该词的下一个实例。

25. B. 输入 `man -k samba` 将在 man 手册页中搜索术语“samba”。

26. D. 输入 `apropos pam` 将在 man 手册页中搜索术语“pam”。

27. D. 输入 `info smbpasswd` 将导致 `info` 显示有关 `smbpasswd` 实用程序的信息。

28. C. 按下 *N* 将跳转到下一个节点。

29. A. 按下 *P* 将跳转到上一个节点。

30. C. 按下 **HOME** 键将带你进入 info 节点的第一行。

31. D. 你必须在 = 号后使用 `$PATH` 来引用 **PATH** 变量。否则，**PATH** 将被解释为文本字面量字符串。

32. A 和 E. 你可以使用 `set` 命令或 `env` 命令来查看你的变量。

33. A. `alias` 命令用于查看你系统上的别名。

34. B 和 E. `stdout` 和 `stderr` 文件描述符代表大多数命令（默认）在屏幕上显示的输出。

35. C. `tail /var/log/firewall 1> lastevents 2>&1` 命令将把 `stdout` 和 `stderr` 都发送到同一个文件。

36. A. `sort < ./logfile.txt` 命令将把文件发送到 `sort` 命令的 `stdin`。

## 使用 vi 文本编辑器

在本章中，你将了解

- vi 文本编辑器的角色和功能
- 在 vi 中编辑文本文件

在使用任何 Linux 系统时（以及为了你的 Linux+ 和 LPIC-1 考试），你需要的一项关键技能是有效使用文本编辑器的能力。Linux 中的大多数系统配置任务都是使用文本编辑器编辑文本文件来完成的，无论是配置操作系统本身还是配置在系统上运行的服务。

这代表了 Linux 与其他操作系统（如 Windows）之间的重大差异。在 Windows 下，你的大多数配置设置都存储在一个名为 *Registry*（注册表）的数据库中。这些信息存储在一个称为 *keys*（键）的逻辑部分中。这些键存储在一个层次结构中；给定的键可以包含许多子键。这些键包含存储系统配置信息的值。例如，在图 3-1 中，Wallpaper 值被设置为 Wallpaper1.bmp 文件。此值设置用于 Windows 桌面背景的图片。

注册表是一个很好的概念，但它的一个主要问题是它不是为最终用户设计的。虽然 Windows 提供了名为 Regedit.exe 的注册表编辑器，但不建议你手动编辑注册表中的值。相反，你应该让操作系统以及安装在系统上的应用程序对注册表进行任何和所有更改。

另一方面，Linux 不使用像 Windows 注册表这样的中央数据库来存储所有系统配置信息。相反，你的所有配置信息都存储在文本文件中。这些文件中的大多数都存储在你的 Linux 系统的 /etc 目录中。例如，用于配置网络时间协议 (NTP) 的文本文件

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_114_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_114_1.png)

