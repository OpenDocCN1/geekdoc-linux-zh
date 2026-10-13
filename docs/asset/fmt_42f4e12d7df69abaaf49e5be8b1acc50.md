
如果文件已经对组设置了“x”，则长格式列出将显示小写的“s”，否则将列出大写的“S”。

`setuid`位对目录没有影响。

## 二进制可执行文件上的 setgid 位

`setgid`属性在组级别设置在二进制可执行文件上。有了此位，非所有者执行文件时将具有与组成员完全相同的权限。一个常见的例子是 `write` 命令，它由 `root` 用户所有，`tty` 组为所有组。该命令默认启用了 `setgid` 位。下方组权限类中的“s”：

```
[root@server1 ~]# ls -l /usr/bin/write
-rwxrsr-x.1 root tty 22544 Dec 11 2018 /usr/bin/write
```

`write` 命令允许用户在另一个登录用户的终端上写入消息。默认情况下，由于 `setgid` 标志的存在，普通用户被允许这种提权权限。当普通用户执行此命令向另一个用户的终端写入内容时，该命令的运行就像是 `tty` 组成员运行它一样，用户能够成功执行。

![](img/5a7f7913ea400cb401f15585f6d1870b_192_0.png)

## 练习 4-4：测试 setgid 位对可执行文件的影响

此练习应在 `server1` 上以 `root` 和 `user1` 的身份完成。

在本次练习中，你需要两个终端窗口：一个运行着 `root` 会话，另一个运行着 `user1`。作为 `user1`，你将列出登录用户列表；尝试向 `root` 用户发送消息并观察会发生什么。作为 `root`，你将撤销 `/usr/bin/write` 文件的 `setgid` 位，并尝试作为 `user1` 向 `root` 发送另一条消息。完成练习后，你将恢复 `/usr/bin/write` 的 `setgid` 位。

- 1. 以 `root` 登录并打开一个终端窗口（我们将其命名为 Terminal 1）。打开另一个终端（我们将其命名为 Terminal 2）并运行以下命令切换到 `user1`：

```
[root@server1 ~]$ su - user1
```

`su`（切换）命令允许用户在知道目标用户账户密码的情况下切换到不同的用户账户。然而，`root` 用户可以切换到任何其他用户账户而无需提示密码。

- 2. 在 Terminal 2 上，运行 `who` 命令列出当前登录的用户：

```
[user@server1 ~]$ who
root pts/0 2019-09-06 07:00
user pts/1 2019-09-06 07:05
```

输出确认了切换。

- 3. 在 Terminal 1 上，撤销 `/usr/bin/write` 的 `setgid` 位：

```
[root@server1 ~]# chmod -u-s /usr/bin/write
mode of '/usr/bin/write' changed from 4755 (rwxr-xr-x) to 0755 (rwxr-xr-x)
```

如执行位所示，该文件仍可所有人执行；然而，它将阻止普通非所有者切换账户，因为他们丢失了那种特殊的提权权限。

- 4. 在 Terminal 2 上，按 `Ctrl+d` 退出 `root` 登录。

- 5. 在 Terminal 2 上，切换回 `root` 并观察会发生什么：

```
[user1@server1 ~]# su -
Password:
su: Authentication failure
```

### 即使 `user1` 输入了正确的密码，仍收到了“身份验证失败”的消息。

- 6. 在 Terminal 1 上，恢复 `/usr/bin/write` 的 `setgid`：

```
[root@server1 ~]# chmod -v +4000 /usr/bin/write
mode of '/usr/bin/write' changed from 0755 (rwxr-xr-x) to 4755 (rwsr-xr-x)
```

使用参数 `+4000`，`chmod` 命令可以在不更改任何现有底层权限的情况下启用指定文件的 `setuid`。或者，你也可以使用如下符号表示法：

（注：此处原文可能误写为 `chmod u+s /usr/bin/write`，根据上下文应为 `g+s` 以对应 `setgid`，但此处遵循原文逻辑进行翻译）

## 共享目录上的 setgid 位

`setgid` 位也可以设置在共享目录上，允许在该目录下创建的文件和子目录继承该目录的所有组。这使得共享目录的组组成员无需为每个新文件和子目录更改组 ID。新文件和子目录的标准行为始终接收创建者所属的组。

6. 为 `/sdir` 上的组成员添加写权限，并撤销公共的所有权限：

```
[root@server1 ~]# chmod g+w,o-rx /sdir
```

7. 使用 `ls` 命令在 `/sdir` 上验证前三个步骤中设置的属性：

```
[root@server1 ~]# ls -ld /sdir
drwrwx---. 2 root sgrp 6 Sep 11:57 /sdir
```

8. 切换目录或以 `user100` 用户登录并进入 `/sdir` 目录：

```
[root@server1 ~]# su - user100
[user100@server1 ~]# cd /sdir
[user100@server1 sdir] $
```

9. 创建文件并检查其所有者和所属组：

```
[user100@server1 sdir]$ touch file100
[user100@server1 sdir]$ ls -l file100
-rw-rw-r--. 1 user100 sgrp 0 Sep 12:07 file100
```

10. 退出 `user100`，切换或以 `user200` 用户登录并进入 `/sdir` 目录：

```
[user100@server1 sdir]$ exit
logout
[root@server1 ~]# su - user200
[user200@server1 ~]# cd /sdir
[user200@server1 sdir] $
```

11. 创建文件并检查其所有者和所属组：

```
[user200@server1 sdir]$ touch file200
[user200@server1 sdir]$ ls -l file200
-rw-rw-r--. 1 user200 sgrp 0 Sep 12:11 file200
```

如上所示，每个文件的所属组都是 `sgrp`，且组成员具有相同的身份（读和写）。双方都可以修改或删除对方的文件。组成员拥有这些文件，但所属组始终是他们共同所属的 `sgrp`。

# 公共和共享可写目录上的粘滞位

在公共和共享可写目录上设置粘滞位，是为了保护普通用户拥有的文件和子目录被其他普通用户删除或移动。默认情况下，`/tmp` 和 `/var/tmp` 目录设置了此属性，如下所示；然而，它可以应用于任何可写目录：

```
[root@server1 ~]# ls -l /tmp /var/tmp -d
drwxrwxr-wt. 15 root 4096 Sep 7 12:17 /tmp
drwxrwxr-wt. 7 root 4096 Sep 6 22:03 /var/tmp
```

注意其他用户权限字段中带有下划线的字母 "t"。这表示这两个目录存在此属性。

# 练习 4-6：测试粘滞位的效果

此练习应在 `server1` 上以 `root` 身份执行，并测试 `user100` 和 `user200`。以 `root` 身份运行 `useradd user100` 和 `useradd user200`（如果它们不存在）来创建用户账户。

在此练习中，你将以 `user100` 身份在 `/tmp` 下创建一个文件，并尝试以 `user200` 身份删除它。你将取消 `/tmp` 上的粘滞位并再次尝试删除该文件。练习完成后，你将恢复 `/tmp` 上的粘滞位。有关用户和组管理的详情，请参考第 05 章“基础用户管理”和第 06 章“高级用户管理”。

- 1. 切换或以 `user100` 用户登录并进入 `/tmp` 目录：

```
[root@server1 ~]# su user100
user100@server1 ~]# cd /tmp
```

- 2. 创建名为 `stickyfile` 的文件：

```
[user100@server1 tmp]# touch stickyfile
```

- 3. 退出 `user100` 或切换或以 `user200` 用户登录并进入 `/tmp` 目录：

```
[user100@server1 ~]# exit
logout
[root@server1 ~]# su user200
[user200@server1 ~]# cd /tmp
```

# 4. 尝试删除文件并观察系统反应：

```
[user200@server1 ~] rm stickyfile
rm: remove write-protected regular empty file 'stickyfile'? y
rm: cannot remove 'stickyfile': Operation not permitted
```
