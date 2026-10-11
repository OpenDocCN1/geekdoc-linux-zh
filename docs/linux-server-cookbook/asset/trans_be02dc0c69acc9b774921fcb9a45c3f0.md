
agonzalez@ubuntu:~$ ls -l example.txt
-rw-rw-r-- 1 agonzalez agonzalez 37 Jul 3 19:27 example.txt
agonzalez@ubuntu:~$ groups
agonzalez adm cdrom sudo dip plugdev lxd
agonzalez@ubuntu:~$ chown :root example.txt
chown: changing group of 'example.txt': Operation not permitted
agonzalez@ubuntu:~$ chown -v :sudo example.txt
changed ownership of 'example.txt' from agonzalez:agonzalez to :sudo

![](img/863afa537de4eed7deb11978bfbfa90e_159_0.png)

- 以管理员身份递归地更改目录的用户和组所有者。

```
root@ubuntu:/tmp# chown -R -v agonzalez:agonzalez snap/
changed ownership of 'snap/lxd/22911' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd/22923' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd/common' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd/current' from root:root to agonzalez:agonzalez
changed ownership of 'snap/lxd' from root:root to agonzalez:agonzalez
changed ownership of 'snap/' from root:root to agonzalez:agonzalez
```

![](img/863afa537de4eed7deb11978bfbfa90e_159_1.png)

命令 **chgrp** 用于仅更改文件和目录的组所有者。其语法为 **chgrp [选项] 组 文件/目录**。选项与 **chown** 命令相同。

## 命令 chmod

该命令用于更改文件和目录的权限。它允许我们使用符号或八进制表示法来指定权限。正如前文关于权限的描述，符号表示法具有如下语法：**u=权限,g=权限,o=权限**，而八进制表示法可以包含三个数字，或者在需要指定特殊权限时包含四个数字。

命令 *chmod* 可以使用等号字符（=）替换当前权限，或使用加号（+）增加更多权限来操作当前权限，或使用减号字符（-）移除权限。该命令 *chmod* 允许使用加号（+）添加权限或使用减号（-）删除权限，而无需替换等号（=）。同样，*chmod* 允许仅指定要修改的权限，而不必指定所有组件。此外，可以使用字母 “*a*” 来设置、添加或删除所有组件的权限。

此命令的选项与命令 **chown** 的选项相同（参见 *表 5.11*）。**图 5.15、5.16** 和 **5.17** 展示了使用命令 **chmod** 的不同示例：

- 指定用户具有读写权限，组仅具有读权限，其他用户无任何权限。

```
agonzalez@ubuntu:~$ chmod -v u=rw,g=r,o= example.txt
mode of 'example.txt' changed from 0664 (rw-rw-r--) to 0640 (rw-r----);
```

![](img/863afa537de4eed7deb11978bfbfa90e_160_0.png)

- 移除组所有者的读权限：

```
agonzalez@ubuntu:~$ chmod -v g-r example.txt
mode of 'example.txt' changed from 0640 (rw-r-----) to 0600 (rw-------)
```

![](img/863afa537de4eed7deb11978bfbfa90e_160_1.png)

- 使用八进制表示法指定用户和组具有读写权限，其他用户具有读权限：

```
agonzalez@ubuntu:~$ chmod -v 644 example.txt
mode of 'example.txt' changed from 0600 (rw-------) to 0644 (rw-r--r--)
```

![](img/863afa537de4eed7deb11978bfbfa90e_160_2.png)

为了理解文件和目录的*执行*权限，*图 5.18* 和 *5.19* 展示了不同的示例：

- 为文件添加执行权限以便其能够被执行：

```
agonzalez@ubuntu:~$ stat -c "%a %A" appl
664 -rw-rw-r--
agonzalez@ubuntu:~$ ./appl
-bash: ./appl: Permission denied
agonzalez@ubuntu:~$ chmod -v u+x appl
mode of 'appl' changed from 0664 (rw-rw-r--) to 0764 (rwxrw-r--)
agonzalez@ubuntu:~$ ./appl
Example application
```

![](img/863afa537de4eed7deb11978bfbfa90e_160_3.png)

- 移除目录的执行权限以禁止访问内部文件：

```
agonzalez@ubuntu:~$ ls -ld regulardir/ regulardir/*
drwxr-xr-x 2 agonzalez adm      4096 Jul 30 19:53 regulardir/
-rw-rw-r-- 1 agonzalez agonzalez    0 Jul 30 19:53 regulardir/file
agonzalez@ubuntu:~$ chmod -v a+x regulardir/
mode of 'regulardir/' changed from 0755 (rwxr-xr-x) to 0644 (rw-r--r--)
agonzalez@ubuntu:~$ ls -ld regulardir/ regulardir/*
ls: cannot access 'regulardir/file': Permission denied
drw-r--r-- 2 agonzalez adm 4096 Jul 30 19:53 regulardir/
```

图 5.19：使用 chmod 移除执行权限的示例。

## 命令 cat

此命令用于查看一个或多个文件的内容。该内容将在标准输出中显示，并且如前所述，可以重定向到另一个文件或通过*管道*传递给另一个命令。此命令的常用选项如表 5.12 所示：

| 选项 | 描述 |
| :--- | :--- |
| -b, --number-nonblank | 对非空行进行编号 |
| -n, --number | 对非空行和空行进行编号 |

表 5.12：命令 cat 的常用选项

图 5.20 展示了如何查看文件内容以及如何对行进行编号：

```
agonzalez@ubuntu:~$ cat /etc/legal
The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

agonzalez@ubuntu:~$ cat -n /etc/legal
     1
     2  The programs included with the Ubuntu system are free software;
     3  the exact distribution terms for each program are described in the
     4  individual files in /usr/share/doc/*/copyright.
     5
     6  Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
     7  applicable law.
     8
```

图 5.20：使用命令 cat 的示例

## 命令 head 和 tail

命令 *head* 用于查看文件的开头部分，而命令 *tail* 用于查看文件的末尾部分。默认情况下，它显示前 10 行或后 10 行。可以使用 -*X*（例如，-20）或 -*n X*（例如 -*n 20*）来指定不同的行数。

命令 *tail* 有一个常用且实用的选项，用于继续跟踪文件中新追加的数据。此选项用于跟踪日志文件以检查*实时*状态。

*图 5.21* 和 *5.22* 展示了不同的示例：

- 查看文件 */etc/passwd* 的前五行：

```
root@ubuntu:~# head -n5 /etc/passwd
root::x:0:0:root:/root:/bin/bash
daemon::x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync::x:4:65534:sync:/bin:/bin/sync
```

*图 5.21：使用命令 head 的示例*

- 查看文件 */var/log/syslog* 的最后五行并等待追加的数据：

```
root@ubuntu:~# tail -n5 -f /var/log/syslog
Jul 31 07:57:53 ubuntu systemd[1]: Finished Daily apt upgrade and clean activities.
Jul 31 07:57:53 ubuntu systemd[1]: apt-daily-upgrade.service: Consumed 1.408s CPU time.
Jul 31 08:06:11 ubuntu rsyslogd: [origin software="rsyslogd" swVersion="8.2112.0" x-pid="666" x-info="https://www.rsyslog.com"] rsyslogd was HUPed
Jul 31 08:17:01 ubuntu CRON[6872]: (root) CMD (   cd / && run-parts --report /etc/cron.hourly)
Jul 31 09:17:01 ubuntu CRON[6321]: (root) CMD (   cd / && run-parts --report /etc/cron.hourly)
```

*图 5.22：使用命令 tail 的示例*

# 特殊字符

在 Linux 控制台中使用命令涉及使用一些对*shell*具有特定含义的特殊字符。前文已描述了一些特殊字符，例如波浪号 (*~*) 代表主目录，大于号 (*&gt;*) 和小于号 (*&lt;*) 代表*标准输入和输出*，以及竖线 (*|*) 代表数据*管道*。其他间接展示的特殊字符包括用于指定选项的连字符 (*-*)，用于指定或分隔目录的斜杠 (\/)，以及用于分隔命令、选项和参数的空格符号。*表 5.13* 展示了在*shell*中操作时其余的特殊字符：

| 特殊字符 | 描述 |
|---|---|
| \\ | 转义特殊字符 |
| $ (美元符号) | 用于访问变量数据 |
| “ * (双引号) | 保护双引号之间的所有内容不被视为特殊字符，并允许评估变量。 |
| ' * (单引号) | 与双引号类似，但不允许评估变量。 |
| # (井号) | 在 shell 中以井号开头的行被标记为注释。 |
| & (and) | 用于在后台执行进程。将在本章稍后描述。 |
| ? (问号) | 仅匹配一个字符 |
| * (星号) | 匹配一个或多个字符。 |
| [ ] (方括号) | 字符范围 |
| { } (花括号) | 指定不同的选项 |
| ( ) (圆括号) | 启动一个 *子 shell* |
| ; (分号) | 在一行中分隔多个命令。 |

*表 5.13：* 特殊字符列表及描述

*图 5.23* 到 *5.24* 通过实际示例展示了这些特殊字符的使用：

- 使用双引号和转义字符 (\) 来访问名称中包含空格的文件：

```
agonzalez@ubuntu:~$ ls filename with spaces
ls: cannot access 'filename': No such file or directory
ls: cannot access 'with': No such file or directory
ls: cannot access 'spaces': No such file or directory
agonzalez@ubuntu:~$ ls -l "filename with spaces"
-rw-rw-r-- 1 agonzalez agonzalez 0 Jul 31 10:29 'filename with spaces'
agonzalez@ubuntu:~$ ls -l filename\ with\ spaces
-rw-rw-r-- 1 agonzalez agonzalez 0 Jul 31 10:29 'filename with spaces'
```

*图 5.23：* 使用特殊字符的示例。

- 使用双引号和单引号处理变量时的区别：

