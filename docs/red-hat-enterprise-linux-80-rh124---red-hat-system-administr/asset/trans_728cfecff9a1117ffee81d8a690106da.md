

9. 使用 `:wq` 命令保存并退出文件。使用日期（秒）创建一个唯一的文件名进行备份。

![](img/59afb92e10b67a9cecc358a2c65e93b5_176_0.png)

```
[student@workstation ~]$ cp editing_final_lab.txt editing_final_lab_$(date +%F).txt
```

10. 在文件末尾添加一个横线。该横线应至少包含 12 个横杠。

```
[student@workstation ~]$ echo "------------------------------------------------" >> editing_final_lab.txt
```

11. 追加 Documents 目录的目录列表。在终端上显示目录列表并使用一条命令编辑该文件。

```
[student@workstation ~]$ ls Documents/ | tee -a editing_final_lab.txt lab_review.txt
```

```
[student@workstation ~]$ cat editing_final_lab.txt
-rw- 1 student 310 Jan 21 .bash_history
-rw- 1 student 18 Oct 12 .bash_logout
-rw- 1 student 141 Oct 12 .bash_profile
-rw- 1 student 312 Oct 12 .bashrc
drwx 0 student 201 Jan 14 .cache
drwx 10 student 203 Jan 14 .config
drwx 2 student 6 Jan 14 Documents
drwx 2 student 6 Jan 14 Downloads
-rw- 1 student 0 Jan 22 editing_final_lab.txt
-rw- 1 student 16 Jan 14 .sed_auth
-rw- 1 student 310 Jan 14 .ICEauthority
drwx 3 student 19 Jan 14 .local
drwx 2 student 6 Jan 14 Music
drwx 2 student 6 Jan 14 Pictures
```

12. 确认目录列表位于文件的底部。

```
drwx 3 student 19 Jan 14 .pki
drwx 2 student 73 Jan 14 .ssh
drwx 2 student 6 Jan 14 Templates
drwx 2 student 8 Jan 14 Videos
-rw- 1 student 1895 Jan 14 .viminfo
-----------------------------
lab_review.txt
```

## 评估

在工作站上，运行 `lab edit-review grade` 命令以确认本次练习成功。

```
[student@workstation ~]$ lab edit-review grade
```

## 结束

在工作站上，运行 `lab edit-review finish` 脚本完成本次练习。

```
[student@workstation ~]$ lab edit-review finish
```

本实验结束。

# 总结

在本章中，你学习了：

- 运行程序或进程三个三个通信通道：标准输入、标准输出和标准错误。
- 你可以使用 I/O 重定向从文件读取标准输入，或将进程的输出或错误写入文件。
- 管道可以将一个进程的标准输出连接到另一个进程的标准输入，并可用于格式化输出或构建复杂的命令。
- 你应该知道如何使用至少一种命令行文本编辑器，通常系统中安装了 Vim。
- Shell 变量可以帮助你运行命令，并且对于特定的 Shell 会话来说是唯一的。
- 环境变量可以帮助你配置 Shell 或其启动的进程的行为。

# 管理本地用户和组

# 目标

# 目标

创建、管理和删除本地用户和组，并管理本地密码策略。

- 描述 Linux 系统中用户和组的作用。
- 切换到超级用户账户管理 Linux 系统，并使用 `sudo` 命令授予其他用户超级用户权限。
- 创建、修改和删除本地定义的用户账户。
- 创建、修改和删除本地定义的组。
- 为用户设置密码管理策略，并手动锁定和解锁用户账户。

# 章节

- 描述用户和组的概念（及测）
- 获取超级用户权限（及引导练习）
- 管理本地用户账户（及引导练习）
- 管理本地组账户（及引导练习）
- 管理用户密码（及引导练习）

# 实验

管理本地 Linux 用户和组

# 描述用户和组的概念

# 目标

在完成本节后，你应该能够描述 Linux 系统中用户和组的作用。

# 什么是用户？

用户账户用于在不同的人和可以运行命令的程序之间提供安全边界。

用户拥有用户名，以便人类用户识别它们并使其易于操作。在内部，系统通过分配给它们的唯一标识数字（即 ID 或 UID）来区分用户账户。如果用户账户由人类使用，通常会分配一个密码，用户在登录时使用该密码证明他们是授权用户。

用户账户对于系统安全至关重要。每个文件都有特定的用户作为所有者。文件所有有助于系统对用户文件执行访问控制。与运行进程关联的用户决定了进程可以访问的文件和目录。

用户有三种类型：
- 超级用户：拥有系统的完全访问权限。
- 守护进程（Daemons）：在后台运行且不进行交互的进程。
- 普通用户：拥有有限权限。

要查看用户信息，使用 `id` 命令。

```
[user1@host ~]$ id
uid=1000(user1) gid=1000(user1) groups=1000(user1),27(sudo)
```

# 第 6 章

查看另一个用户的基本信息，使用 `id` 命令后接用户名。

```
[user2@host ~]$ id
uid=1002(user2) gid=1002(user2) groups=1002(user2)
```

上述命令的输出通过名称显示用户，但在内部用户名到 UID 的映射定义在账户数据库中。默认情况下，使用 `/etc/passwd` 文件存储信息。`/etc/passwd` 文件中的每行都包含一个用户的信息。它由冒号分隔的字段组成。这里有一个示例：user01:x:1000:1000:User One:/home/user01:/bin/bash

- 用户名 (user01)。
- 存储在此处的加密格式密码已移动到 `/etc/shadow` 文件，显示为 x。
- 用户的 UID (1000)。
- 用户主组的 GID (1000)。
- 用户的真实名称 (User One)。
  家目录 (/home/user01)。这是 Shell 启动时的初始工作目录。
- 该进程的默认 shell (//bin/bash)。

# 什么是组？

组是一组共享文件和其他系统资源的用户集合。组可以用于向一组用户授予文件访问权限，而不仅仅是单个用户。

和用户一样，组拥有用户名以便易于操作。在内部，系统通过分配给它们的唯一标识数字（即组 ID 或 G）来区分组。

组名到 GID 的映射定义在组账户数据库中。默认情况下，使用 `/etc/group` 文件存储本地组的信息。

`/etc/group` 中的示例：sudo:27:user01,user2

- 组名 (sudo)。
- 该组的 GID (27)。
- 属于该组的用户列表。

查看组信息，使用带 `a` 参数的 `ps` 命令。默认只显示当前 shell 中的进程。添加 `u` 参数以包含终端用户。

```
[student@workstation ~]$ ps -au
USER       PID %CPU %MEM    VSZ TTY START TIME COMMAND
root         1  0.0  0.1  16800 ?        Ss   09:00   /sbin/init
user01    1234  0.0  0.0  4500 pts/0    S    10:00 0:00 /bin/bash
user02    5678  0.0  0.0  4600 pts/1    S    10:01 0:00 /bin/bash
```
