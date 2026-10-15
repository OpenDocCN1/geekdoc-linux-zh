
```
zayedbalbahaith@M80007225/home/zayedbalbahaith
[root@M8007225 ~]$ xclock &
[2] 8390
[root@M8007225 ~]# Warning: Tried to connect to session manager,
None of the authentication protocols specified are supported
Warning: Missing charset in String to FontSet conversion
ls
Classes Documents Music Pictures
Desktop Downloads personal.txt Public Videos
[1]- Done xclock
[root@M8007225 ~]$
```

图 1.73：在另一个应用程序运行时同时执行要在后台运行的命令。

```
zayedbalbahaith@M80007225/home/zayedbalbahaith
File Edit View Search Terminal Help
[root@M80007225]# xclock &
[2] 8390
[root@M80007225]# Warning: Tried to connect to session manager,
None of the authentication protocols specified are supported
Warning: Missing charset in String to FontSet conversion
ls
Classes Documents Music Pictures
Desktop Downloads personal.txt Public Videos
[1]- Done xclock
[root@M80007225]# ps
PID TTY TIME CMD
7984 pts/0 00:00:00 su
7993 pts/0 00:00:00 bash
8390 pts/0 00:00:00 xclock
8411 pts/0 00:00:00 ps
[root@M80007225]# kill 8390
[2]+ Terminated
xclock
[root@M80007225]#
```

图 1.74：使用 `ps` 命令列出后台运行的进程

图 1.75：使用 `kill` 命令终止后台运行的 `xclock` 进程

## 成为超级用户

Linux 的多用户属性为系统提供了额外的保护和安全性；所有用户将拥有一有限的权限，而 `root` 用户将拥有最高权限的系统完全访问权限。在此部分中，实验涵盖了创建新用户，并通过 `cron` 命令作为测试用例修改了当前用户的权限和访问级别。

```
ituser@MB8007225:~
File Edit View Search Terminal Help
[ituser@MB8007225 -$ whoami
ituser
[ituser@MB8007225 -$]#
```

图 1.76：`whoami` 命令结果显示当前登录的用户是 `Ituser`

```
ituser@MB8007225:/home/ituser
File Edit View Search Terminal Help
[ituser@MB8007225 -$] su
Password:
[root@MB8007225 user]#
```

图 1.77：以 `root` 用户身份访问 shell

```
ituser@MB8007225:/home/ituser
File Edit View Search Terminal Help
[root@MB8007225 user]# whoami
root
[root@MB8007225 user]#
```

图 1.78：`whoami` 命令结果显示当前登录的用户是 `root` `root`

部分 "a" 中的 `whoami` 命令显示用户为控制 shell 的用户，且其文件被分配了有限权限；但在部分 "c" 中，`whoami` 命令显示的用户为 `root`，他拥有完全权限。

## `Ituser@M8000725:/home/ituser`

```
File Edit View Search Terminal Help
[root@M8000725 ituser]# # touch /etc/cron.deny
[root@M8000725 ituser]# #
```

图 1.79：在 `/etc/cron.deny` 创建创建一个新文件

## `Ituser@M8000725:/home/ituser`

```
File Edit View Search Terminal Help                               Modified
GNU nano 2.5.3                               File: /etc/cron.deny
ituser                                                                              


Read 0 lines
-Get Help Write Out Where Is Exec Next Justify
-M Read File Replace Uncut Text To Spell
-Exit Go To Line
```

图 1.80：将 `ituser` 添加到拒绝文件中

## `ituser@M8000725:~`

```
File Edit View Search Terminal Help
[root@M8000725#]# exit
[ituser@M8000725~ -] #
```

图 1.81：退出 `root` 登录

## `ituser@M8000725:~`

```
[root@M8000725 it]# exit
(ituser) are not allowed to use this program (crontab)
See crontab(1) for more information
[ituser@M8000725~ -] #
```

图 1.82：根据 `cron` 工具规则不允许运行 `crontab` 命令

由于文件在 "d" 部分使用 `cron` 工具被封锁，因此 shell 将不允许 `ituser` 运行 `crontab` 命令。

## `ituser@M8000725:~`

```
File Edit View Search Terminal Help
[ituser@M8000725~ -]# rm /etc/cron.deny
rm: remove write-protected regular file '/etc/cron.deny'? ? y
rm: remove '/etc/cron.deny': Permission denied
[ituser@M8000725~ -] #
```

图 1.83：由于 `ituser` 使用 `cron` 工具的权限被限制，导致无法删除文件 (`/etc/cron.deny`)

## `Ituser@M80007225:/home/ituser`

```
File Edit View Search Terminal Help
[root@MB8007225 ~]$ su
Password:
[root@MB8007225 #] /etc/cron.deny
rm: remove regular file '/etc/cron.deny'? y
[root@MB8007225 ituser]# #
```

图 1.84：使用 `root` 用户删除了文件 (`/etc/cron.deny`)

由于 (`/etc/cron.deny`) 文件是由 `root` 用户创建的，因此对 `ituser` 的任何修改都不会被其他用户采用，能够删除它的唯一用户是 `root` 用户。

使用提供的易用图形化用户界面工具创建并测试了一个新账户。

![](img/7be05572b414927ff78ba38f31a7ecfc_34_0.png)

图 1.85：通过图形工具创建 `shahrazad` 用户

![](img/7be05572b414927ff78ba38f31a7ecfc_34_1.png)

图 1.86：以 `shahrazad` 用户身份登录

![](img/7be05572b414927ff78ba38f31a7ecfc_35_0.png)

由于题目要求的密码是 "qw"，而 Fedora 工作站的密码长度策略规定至少为 8 个字符，我们在指定的密码末尾添加了两个额外数字，否则无法通过图形界面创建账户。

![](img/7be05572b414927ff78ba38f31a7ecfc_35_1.png)

## 使用 `ssh` 连接到

大多数服务器都配置了远程访问，`ssh` 提供了一种安全可靠的方式来执行此任务。本次 `ssh` 连接到地址为 `172.18.64.31` 的服务器，并执行了 "who"、`finger` 和 "w" 等多个命令。后续截图显示了该部分的细节。
