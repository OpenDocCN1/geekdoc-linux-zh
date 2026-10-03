
检查清单
eeprom
所有任务已执行。某些后台任务可能仍在运行。
运行 /usr/aset/util/taskstat 以检查其状态：
    /usr/aset/util/taskstat      [aset_dir]
其中 aset_dir 是 ASET 的操作目录，当前为=/usr/aset。
任务完成后，报告可在以下位置找到：
    /usr/aset/reports/latest/*.rpt
您可以通过以下方式查看它们：
    more /usr/aset/reports/latest/*.rpt
#

## 常识性安全技术

系统管理员可以实施最佳的系统安全措施，但如果没有用户的配合，系统安全就会受到损害。系统管理员必须教授有关系统安全的常识性规则，例如以下内容：

- 使用适当的密码。无数站点为其 root 账户使用诸如“admin”或“supervisor”之类的密码。
- 不要把你的密码告诉任何人，无论他自称是谁。我们这个时代最优秀的系统破解者之一说，他只需冒充系统支持人员，向用户索要密码，就能自由访问系统。
- 如果你离开系统，请注销或锁定屏幕。想想如果有人走到你的工作站并发送一封尖锐的电子邮件给你的公司总裁——署上你的名字！会造成什么损害！
- 未经系统管理员批准，不要将调制解调器连接到你的系统。

## 章节摘要

本章讨论了系统安全中的基本概念。在考虑安全时，首先要将硬件安全地放置在安全的位置。请记住：任何拥有对计算机的物理访问权限的人都可以访问操作系统和数据，无论你对其他方面做得多么安全。

通过控制系统上的用户登录来保护你的数据安全。确保用户拥有安全的密码，并且不会公开他们的登录名和密码。在合适的地方实施密码老化和受限 shell。

设置文件和目录权限，以确保用户只能访问他们被授权查看的数据。利用安全的 umask 值，并在必要时使用 ACL。利用本章所述的 Solaris 实用程序监控所有用户活动。最后，除非绝对必要，否则不要设置 setuid 和 setgid 权限。

如果你的系统在网络上，请实施本章所述的网络安全措施。关闭不需要的服务。使用“先拒绝，后允许”的规则。换句话说，关闭尽可能多的服务和应用程序，然后有选择地打开那些必不可少的服务。谨慎使用受信任的系统。此外，保持你的操作系统安全补丁为最新状态。随着新威胁的发现，它们会通过安全补丁迅速得到修复。第 4 章，“Software Package Administration，”描述了获取和加载系统补丁的过程。

最后，保护超级用户密码。将其严格控制，并确保它永远不会提供给除授权人员之外的任何人。限制使用超级用户登录，除非要执行的任务需要 root 权限。

尽管系统破解者似乎总能找到新的入侵方式，但本章所述的概念为抵御攻击提供了强有力的防御。此外，请参阅第 5 章，了解在设置和管理用户账户时如何将这些概念付诸实践。

在下一章中，我们将稍微转换一下思路，我将描述系统进程背后的所有细节。作为系统管理员，你的主要职责是管理系统上运行的所有进程。

## 关键术语

- Password aging
- Password encryption
- Default shells
- Restricted shell
- File access permissions
- User mask
- Sticky bit
- Access control list
- Trojan horse
- Set-user identification permission
- Set-group identification permission
- Firewall
- Network service
- Trusted host
- Automated Security Enhancement Tool
- Low security (as it pertains to ASET)
- Medium security (as it pertains to ASET)
- High security (as it pertains to ASET)

## 应用你的知识

### 练习

### 8.1 监控用户

在此练习中，你将使用各种实用程序来监控访问系统的用户。

预计时间：5 分钟

1. 以 root 身份登录。
2. 在 /var/adm 目录中创建一个名为 loginlog 的文件：
```
cd /var/adm
touch loginlog
```
3. 注销并重新登录。不要使用 CDE 登录；使用命令行登录。
4. 在登录提示后输入 root，并提供错误的密码。重复此操作五次。第五次尝试后，使用正确的密码以 root 身份登录并按如下方式检查 /var/adm/loginlog 文件：
```
more /var/adm/loginlog
```
5. 使用 finger 命令按如下方式显示名为 user9 的用户的信息：
```
finger user9
finger -m user9
```
6. 使用 finger 命令按如下方式显示另一系统上用户的信息：
```
finger user9@<hostname>
finger -m user9@<hostname>
```
7. 使用 last 命令显示用户和重启活动。
8. 使用 logins 命令按如下方式获取有关 user9 登录账户的信息：
```
logins -x -l user9
```

### 8.2 文件访问

在此练习中，你将使用 UNIX 权限通过允许/禁止访问文件和目录来控制文件访问。

预计时间：20 分钟

1. 以 user9 身份登录。
2. 输入 umask 命令以确定当前的 umask 值：
```
umask
```
如果 umask 不是 002，请通过输入以下内容更改它：
```
umask 002
```
3. 按如下方式在你的主目录中创建一个文件：
```
cd $HOME
touch file1
```
4. 输入 ls -l 以查看分配给此文件的默认权限。
5. 按如下方式将你的 umask 设置为 022：
```
umask 022
```
6. 创建一个名为 file2 的文件，并查看默认权限值。
```
touch file2
ls -l
```
7. 按如下方式创建一个名为 newuser 的新用户：
```
useradd -u 3001 -g 10 -d /export/home/ user20 -m -s /bin/ksh -c "Temporary User" user20
```
将密码设置为 user20 如下：
```
passwd user20
```
8. 以 user9 身份注销并重新登录。你将被放置在你的主目录 /export/home/user9 中。

9. 创建一个名为 file10 的新文件，并列出权限：
```
touch file10
ls -l
```

10. 使用 chmod 在 file10 上设置 setuid 权限，并列出权限：
```
chmod 4555 file10
ls -l
```

11. 使用 chmod 在 file10 上设置 setuid 和 setgid 权限，然后显示权限：
```
chmod 6555 file10
ls -l
```
发生了什么变化？

12. 使用 chmod 删除 file10 的所有执行权限，然后显示新的权限：
```
chmod 6444 file10
ls -l
```

13. 按如下方式列出 /tmp 的目录权限：
```
ls -ld /tmp
```
注意 /tmp 上设置了粘滞位。

14. 以 user9 身份更改到 /tmp 目录并创建一个名为 file1 的文件。
```
cd /tmp
touch file1
ls -l
```
注意文件的权限。它们应为 644 (rw-r--r--)。

15. 切换到 user20。在 /tmp 目录中，删除名为 file1 的文件：
```
su user20
cd /tmp
rm file1
```
你收到了什么消息？

16. 退出当前 shell 以返回到 user9 ID。更改到 user9 主目录并设置 file10 上的 ACL，以便 user20 对文件具有读和写权限：
```
exit
cd $HOME
setfacl -m user:user20:6 file10
```

17. 现在，使用 ls -l 列出 file10 的文件权限。注意 + 号，表示文件上已设置 ACL。

18. 按如下方式列出 file10 上的 ACL 条目：
```
getfacl file10
```

19. 按如下方式删除 file10 上的 ACL：
```
setfacl -d u:user20 file10
```

### 8.3 限制 root 访问

在此练习中，你将对系统进行更改以限制 root 登录。

预计时间：10 分钟

1. 尝试从远程系统以 root 身份登录你的系统。如果 /etc/default/login 文件未从其默认设置中修改，你不应能够登录。

2. 从控制台以 root 身份登录你的系统。

3. 使用 vi 编辑名为 /etc/default/login 的文件，并在以下行的开头添加井号（#）：
```
#CONSOLE=/dev/console
```

4. 尝试从远程系统以 root 身份登录你的系统。它能工作吗？

5. 现在，尝试按如下方式从远程系统打开 FTP 连接：
```
ftp <hostname>
```
