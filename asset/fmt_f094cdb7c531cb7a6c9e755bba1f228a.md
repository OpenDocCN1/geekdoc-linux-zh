
或者，您可以使用`passwd -L username`命令来锁定用户账户，并使用`passwd -U username`命令来解锁用户账户。

另一种常用于锁定用户账户的方法是改变`/etc/passwd`中指定给某用户账户的shell，从`/bin/bash`更改为无效的shell，例如`/bin/false`。如果没有有效的shell，用户就无法使用系统。要通过这种方式锁定用户账户，您可以编辑`/etc/passwd`文件并进行相应的更改。要解锁用户，只需输入`usermod`命令，或使用`chsh`命令。以下示例使用`chsh`命令将用户`bob`的shell更改为`/bin/false`：

```
[root@server1 root]# chsh -s /bin/false bob
Changing shell for bob.
Warning: "/bin/false" is not listed in /etc/shells
Shell changed.
[root@server1 root]# _
```

#### 删除用户账户

要删除用户账户，您可以使用`userdel`命令，并将用户名作为参数指定；这会移除`/etc/passwd`和`/etc/shadow`中与该用户账户对应的条目。此外，您可以为`userdel`命令指定`-r`选项，以删除该用户的家庭目录及其所有内容。

当删除一个用户账户时，之前属于该用户的任何文件都会变为由代表已删除用户UID的数字所有。未来任何被分配相同UID的用户账户将成为这些文件的所有者。

**管理用户和组**

假设，例如，用户`bobg`离开了公司。要删除`bobg`的用户账户并显示其旧文件的所有权，您可以使用以下命令：

```
[root@server1 root]# userdel bobg
[root@server1 root]# ls -la /home/bobg
total 52
drwx------   4 502      502      4096 Jul 17 15:37 .
drwxr-xr-x   5 root     root      4096 Jul 17 15:37 ..
-rw-r--r--    1 502      502        24 Jul 17 15:37 .bash_logout
-rw-r--r--    1 502      502       191 Jul 17 15:37 .bash_profile
-rw-r--r--    1 502      502       124 Jul 17 15:37 .bashrc
-rw-r--r--    1 502      502      5542 Jul 17 15:37 .canna
-rw-r--r--    1 502      502       820 Jul 17 15:37 .emacs
-rw-r--r--    1 502      502       118 Jul 17 15:37 .gtkrc
-rw-r--r--    3 502      502      4096 Jul 17 15:37 .kde
drwxr-xr-x   2 502      502      4096 Jul 17 15:37 .xemacs
-rw-r--r--    1 502      502      3511 Jul 17 15:37 .zshrc
[root@server1 root]#
```

从上述输出中，您可以看到`bobg`用户的UID为502。如果公司雇佣用户`sueb`来替代`bobg`，您可以将UID 502分配给她的用户账户，以便她可以拥有并`reuse`bobg的所有旧文件。

要创建一个UID为502的用户`sueb`并列出`bobg`家庭目录中文件的所有权，您可以使用以下命令：

```
[root@server1 root]# useradd -u 502 sueb
[root@server1 root]# ls -la /home/bobg
total 52
drwx------   4 sueb     sueb     4096 Jul 17 15:37 .
drwxr-xr-x   5 root     root     4096 Jul 17 18:56 ..
-rw-r--r--    1 sueb     sueb       24 Jul 17 15:37 .bash_logout
-rw-r--r--    1 sueb     sueb      191 Jul 17 15:37 .bash_profile
-rw-r--r--    1 sueb     sueb      124 Jul 17 15:37 .bashrc
-rw-r--r--    1 sueb     sueb     5542 Jul 17 15:37 .canna
-rw-r--r--    1 sueb     sueb      820 Jul 17 15:37 .emacs
-rw-r--r--    1 sueb     sueb      118 Jul 17 15:37 .gtkrc
-rw-r--r--    3 sueb     sueb     4096 Jul 17 15:37 .kde
drwxr-xr-x   2 sueb     sueb     4096 Jul 17 15:37 .xemacs
-rw-r--r--    1 sueb     sueb     3511 Jul 17 15:37 .zshrc
[root@server1 root]#
```

#### 管理组

迄今为止，向系统添加组的最简单方法是使用文本编辑器编辑`/etc/group`文件。另一种方法是使用`groupadd`命令。要向系统添加一个名为`group1`的组并将其GID设置为492，您可以使用以下命令：

```
[root@server1 root]# groupadd -g 492 group1
[root@server1 root]# _
```

然后，您可以使用`usermod`命令的`-G`选项向该组添加成员。要将用户`mary`添加到该组并查看添加结果，您可以使用以下`usermod`命令：

```
[root@server1 root]# usermod -G group1 mary
[root@server1 root]# tail -1 /etc/group
group1:x:492:mary
[root@server1 root]# _
```

还存在`groupmod`命令，可用于修改组名和GID，以及`groupdel`命令，可用于从系统中删除组。

要查看您所属的组列表，只需运行`groups`命令；要查看每个组的GID，只需运行`id`命令。每个命令都会首先列出主组。以下输出显示了`root`用户执行这些命令时的输出：

```
[root@server1 root]# groups
root bin daemon sys adm disk wheel
[root@server1 root]# id
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)
[root@server1 root]# _
```

从上述输出中，您可以看到`root`用户的主组是`root`组。该组作为由`root`用户创建的所有文件的组所有者附加，如下面的输出所示：

```
[root@server1 root]# touch samplefile1
[root@server1 root]# ls -1 samplefile1
-rw-r--r--    1 root     root       0 Jul 17 19:22 samplefile1
[root@server1 root]# _
```

要将主组临时更改为`groups`和`id`命令输出中列出的其他组，您可以使用`newgrp`命令。之后创建的任何新文件都将具有新的组所有者。以下输出演示了更改`root`用户的主组如何影响文件所有权：

```
[root@server1 root]# newgrp sys
[root@server1 root]# id
uid=0(root)  gid=3(sys)
groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)
[root@server1 root]# touch samplefile2
[root@server1 root]# ls -1 samplefile2
-rw-r--r--    1 root     sys        0 Jul 17 19:28 samplefile2
[root@server1 root]#
```

#### 注意
