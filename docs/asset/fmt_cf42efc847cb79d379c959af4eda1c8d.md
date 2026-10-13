
在本次练习中，一个名为 `permfile2` 的文件存在，所有者（`user1`）、所属组（`user1`）和其他用户具有读取权限，如下所示。如果权限有所不同，请在开始练习之前通过执行 `chmod 444 permfile2` 将其恢复到所需状态。

```
-r--r---- 1 user1 user1 0 Sep 6 21:12 permfile2
```

在此练习中，你将为所有者添加执行位，并为组和公共用户添加写位。然后你将取消公共用户的写位，并同时为三个用户类别分配读、写、执行权限。`chmod` 命令接受 `-v` 标志来显示其更改的内容。你也可以在每次命令执行后查看详细列表以进行验证。

### 1. 为所有者添加执行位：

```
[user1@server~$] chmod -v 544 permfile2
mode of 'permfile2' changed from 0444 (r--r----) to 0544 (r-xr--r--)
```

### 2. 为组和公共用户添加写位：

```
[user1@server~$] chmod -v 566 permfile2
mode of 'permfile2' changed from 0544 (r-xr--r--) to 0566 (r-xr-rw--)
```

### 3. 取消公共用户的写位：

```
[user1@server~$] chmod -v 564 permfile2
mode of 'permfile2' changed from 0566 (r-rw-rw--) to 0564 (r-xr--rw--)
```

### 4. 为所有三个用户类别分配读、写、执行权限：

```
[user1@server~$] chmod 777 -v permfile2
mode of 'permfile2' changed from 0564 (r-xr--rw--) to 0777 (rwxrwxrwx)
```

## 默认权限

Linux 在创建文件或目录时会为其分配默认权限。默认权限是根据 `umask`（用户掩码）权限值从预设的初始权限值中减得的。

`umask` 是一个三位八进制值（也用符号符号表示），引用所有者、组和公共用户的读、写、执行权限。它的目的是在新文件和目录上设置默认权限，而不影响现有文件和目录的权限。默认 `umask` 值对 `root` 用户设置为 `0022`，对普通用户设置为 `0002`。注意最左侧的 `0` 没有意义。运行不带选项的 `umask` 命令，将以八进制格式显示当前的 `umask` 值：

```
[user1@server1 ~] umask
0002
```

再次运行命令，但使用 `-S` 选项以符号形式显示 `umask`：

```
[user1@server1 ~] umask -S
u=rwx,g=rx,o=rx
```

预定义的初始权限值为文件为 `666` (`rw-rw-rw-`)，目录为 `777` (`rwxrwxrwx`)。即使 `umask` 设置为 `000`，新文件也将始终获得最高 `666` 权限；但是，如果需要，可以使用 `chmod` 命令显式地添加执行位。

### 计算默认权限

考虑以下示例来计算普通用户文件的权限值：

初始权限 `666`

`umask` - `002` (减法)

====================

默认权限 `664`

这意味着每个新文件都将为所有者和所属组分配读写权限，并为其他用户分配只读权限。

### 要计算普通用户的目录默认权限值：

| 初始权限 | 777 |
| :--- | :--- |
| `umask` | 002 (减法) |
| ================================ |  |
| 默认权限 | 775 |

这表示每个新文件将为所有者和所属组分配读写权限，其他用户分配只读权限。

如果你希望新文件和目录获得 `640` 和 `750`，可以通过运行以下命令设置 `umask` 为 `27`：

```
[user1@server1 ~] umask u=rwx,g=rx,o=
```

在命令行设置的 `umask` 值立即生效，并应用于随后创建的文件。现有文件和目录保持不变。现在作为 `user1` 创建 `tempfile` 和 `tempdir` 以测试 `umask` 的效果：

```
[user1@server1 ~] touch tempfile
[user1@server1 ~] ls -l tempfile
-rw-r-- 1 user1 user1 0 tempfile
[user1@server1 ~] mkdir tempdir
[user1@server1 ~] ls -ld tempdir
drwxr-xr- 2 user1 user1 0 tempdir
```

上述示例显示了新文件和

## 特殊权限

Linux 提供了三种特殊的二进制文件或目录特殊权限位，对非 `root` 用户响应不同。这些权限位是用户标识位（通常称为 `setuid` 或 `suid`）、组标识位（又称 `setgid` 或 `sgid`）以及 `sticky` 位。

`setuid` 和 `setgid` 位可以定义在二进制执行文件上，允许非所有者和非组成员以所有者或所属组的权限运行它们。`setgid` 位也可以设置在共享目录上供小组协作。`sticky` 位可以设置在公共目录上以防止非所有者删除文件。

![](img/5a7f7913ea400cb401f185f6d1870b_190_0.png)

> `setuid` 和 `sticky` 位可以设置在目录和文件上；但没有效果。

特殊位的用法应受到监管和监控，以避免对系统操作和应用程序产生安全风险。

### 二进制执行文件上的 setuid 位

`setuid` 标志在文件所有者级别设置在二进制执行文件上。有了此位，非所有者执行文件时具有与文件所有者相同的权限。一个常见的例子是属于 `root` 用户的 `su` 命令。该命令默认启用了 `setuid` 位。查看下方所有者权限类中带划线的“s”：

```
[root@server1 ~]# ls -l /usr/bin/su
-rws-xr-x 1 root 52784 Dec 11 2018 /usr/bin/su
```

`su`（切换用户）命令允许用户使用目标用户的密码切换到另一个用户账户。然而，`root` 用户可以切换到任何用户账户而无需提示。当普通用户执行此命令时，它将像 `root`（所有者）身份一样运行

运行它，因此用户能够成功运行它并获得所需的结果。

## 练习 4-3：测试 setuid 位对可执行文件的影响

此练习应在 `server1` 上以 `root` 和 `user1` 的身份完成。

在本次练习中，你需要两个终端窗口：一个运行着 `root` 会话，另一个运行着 `user1`。作为 `user1`，你将切换到 `root` 并观察会发生什么。作为 `root`，你将撤销 `/usr/bin/su` 文件的 `setuid` 位，并再次尝试切换到 `root`。完成练习后，你将恢复 `/usr/bin/su` 的 `setuid` 位。

### 1. 以 root 身份登录并打开一个终端窗口（我们将其命名为 Terminal 1）。打开另一个终端（我们将其命名为 Terminal 2）并运行以下命令切换到 user1：

```
[root@server1 ~]# su - user1
```

### 2. 在 Terminal 2 上，运行 `su` 命令切换到 `root`：

```
[user@server1 ~]$ su - root
Password:
[root@server1 ~]#
```

输出确认了切换。

### 3. 在 Terminal 1 上，撤销 `/usr/bin/su` 的 `setuid` 位：

```
[root@server1 ~]# chmod -u-s /usr/bin/su
mode of '/usr/bin/su' changed from 4755 (rwxr-xr-x) to 0755 (rwxr-xr-x)
```

如执行位所示，该文件仍可所有人执行；然而，它将阻止普通非所有者切换账户，因为他们丢失了那种特殊的提权权限。

### 4. 在 Terminal 2 上，按 Ctrl+d 退出 root 登录。

### 5. 在 Terminal 2 上，切换回 root 并观察会发生什么：

```
[user1@server1 ~]# su -
Password:
su: Authentication failure
```

即使 `user1` 输入了正确的密码，仍收到了“身份验证失败”的消息。

### 6. 在 Terminal 1 上，恢复 `/usr/bin/su` 的 `setuid`：

```
[root@server1 ~]# chmod -v +4000 /usr/bin/su
mode of '/usr/bin/su' changed from 0755 (rwxr-xr-x) to 4755 (rwsr-xr-x)
```

使用参数 `+4000`，`chmod` 命令可以在不更改任何现有底层权限的情况下启用指定文件的 `setuid`。或者，你也可以使用如下符号表示法：

```
[root@server1 ~]# chmod u+s /usr/bin/su
```
