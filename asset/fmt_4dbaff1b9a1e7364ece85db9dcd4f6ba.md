
### 1.3.5. 设置八进制权限

大多数 Unix 管理员使用传统的八进制系统来讨论和设置权限。按位元组来看，将 `r` 等于 4，`w` 等于 2，`x` 等于 1。

| 二进制 | 八进制 | 权限 |
|---|---|---|
| 000 | 0 | --- |
| 001 | 1 | --x |
| 010 | 2 | -w- |
| 011 | 3 | -wx |
| 100 | 4 | r-- |
| 101 | 5 | r-x |
| 110 | 6 | rw- |
| 111 | 7 | rwx |

这使得 777 等于 `rwxxrrwx`，根据同样的逻辑，654 代表 `rw-r--`。`chmod` 命令接受这些权限。

```
paul@laika:~$ chmod u=rw,ug+rw,o=r permissions.txt
paul@laika:~$ ls -l permissions.txt
-rwxr-xr-- 1 paul 2007-02-07 22:34 permissions.txt
```

### 1.3.6. umask

创建文件或目录时，会应用一组默认权限。这些默认权限由 `umask` 决定。`umask` 指定了你不不想默认设置的权限。你可以用 `umask` 命令显示 umask。

```
[Harry@RHEL4b ~]$ umask
0002
[Harry@RHEL4b ~]$ touch test
[Harry@RHEL4b ~]$ ls -l test
-rw-r--r-- 1 Harry 0 Jul 24 06:03 test
[Harry@RHEL4b ~]$
```

正如你所看到的，文件默认不可执行。这是 Unix 中的一项通用安全特性；新创建的文件永远永远可执行。你必须显式地执行 `chmod +x` 使文件变为可执行。这意味着 umask 中的 1 位是有意义的——`0022` 的 umask 等于 `033`。

### 1.3.7. mkdir -p

使用 `mkdir` 创建目录时，可以使用 `-m` 选项来设置**模式**。此截图对此进行了说明。

```
paul@debian5~$ mkdir -m 700 MyDir
paul@debian5~$ mkdir -m 777 Public
paul@debian5~$ ls -dl MyDir/ Public/
drwx-xr-x 2 paul 4096 2011-10-16 19:16 MyDir/
drwxrwxrwx 2 paul 4096 2011-10-16 19:16 Public/
```

### 1.3.8. cp -p

为了保留源文件的权限和时间戳，请使用 `cp -p`。

```
paul@laika:~/perms cp file* cp
paul@laika:~/perms cp -p file* cpp
paul@laika:~/perms ls -l
-rw-r--r-- 1 paul 0 2007-02-07 22:34 file33
-rwxr-xr-- 1 paul 0 2007-02-07 22:34 file42
```

## 1.4. 练习：标准文件权限

- 1. 作为普通用户，创建一个目录 `~/permissions`。在里面创建一个所有者为你的文件。
- 2. 从 `/etc/` 复制一个所有者为 root 的文件到你的 `permissions` 目录，现在这个文件的所有者是谁？
- 3. 以 root 身份，在用户的 `~/permissions` 目录下创建一个文件。
- 4. 作为普通用户，查看这个由 root 创建的文件的所有者是谁。
- 5. 将 `~/permissions` 中所有文件的所有者更改为你。
- 6. 确保你对这些文件拥有所有权限，而其他人只能读取。
- 7. 使用 `chmod`，770 等同于 `rwxwx---` 吗？
- 8. 使用 `chmod`，664 等同于 `r-xr-xr--` 吗？
- 9. 使用 `chmod`，400 等同于 `r-------` 吗？
- 10. 使用 `chmod`，734 等同于 `rwxr-xr-x` 吗？
- 11a. 以八进制和符号格式显示 `umask` 并对其进行设置。验证这是否有效。
- 11b. 将 `umask` 设置为 077，但使用符号格式进行设置。验证这是否有效。
- 12. 以 root 身份创建一个文件，只给其他人读取权限。普通用户可以读取这个文件吗？使用 `vi` 尝试向该文件写入。
- 13a. 以普通用户创建一个文件，只给其他人读取权限。另一个普通用户可以读取这个文件吗？使用 `vi` 尝试向该文件写入。
- 13b. root 可以用 `vi` 这个文件吗？
- 14. 创建一个属于某个组的目录，该组的每个成员都可以对文件进行读写并创建文件。确保人们只能删除他们自己的文件。

## 1.5. 解决方案：标准文件权限

- 1. 作为普通用户，创建一个目录 `~/permissions`。在里面创建一个所有者为你的文件。

`mkdir ~/permissions ; touch ~/permissions/myfile.txt`

- 2. 从 `/etc/` 复制一个所有者为 root 的文件到你的 `permissions` 目录，现在这个文件的所有者是谁？

`cp /etc/hosts ~/permissions/`

复制的文件所有者是你。

- 3. 以 root 身份，在用户的 `~/permissions` 目录下创建一个文件。

`(become root#) touch /home/username/permissions/rootfile`

- 4. 作为普通用户，查看这个由 root 创建的文件的所有者是谁。

`ls -l ~/permissions`

由 root 创建的文件所有者是 root。

- 5. 将 `~/permissions` 中所有文件的所有者更改为你。

`chown user ~/permissions/*`

你无法成为属于 root 的文件的所有者。

- 6. 确保你对这些文件拥有所有权限，而其他人只能读取。

`chmod 644 (on files)`

`chmod 755 (on directories)`

- 7. 使用 `chmod`，770 等同于 `rwxrwx---` 吗？

是的

- 8. 使用 `chmod`，664 等同于 `r-xr-xr-` 吗？

不是

- 9. 使用 `chmod`，400 等同于 `r-------` 吗？

是的

- 10. 使用 `chmod`，734 等同于 `rwxr-xr--` 吗？

不是

- 11a. 以八进制和符号格式显示 `umask`。

`umask ; umask -S`

- 11b. 将 `umask` 设置为 077，但使用符号格式进行设置。验证这是否有效。

`umask -S u=rw,go=`

- 12. 以 root 身份创建一个文件，只给其他人读取权限。普通用户可以读取这个文件吗？使用 `vi` 向该文件写入。

```
(become root)
echo hello > /home/username/root.txt
# chmod 744 /home/username/root.txt
```

```
(become user)
vi ~/root.txt
```

- 13a. 以普通用户创建一个文件，只给其他人读取权限。另一个普通用户可以读取这个文件吗？使用 `vi` 尝试向该文件写入。

```
echo hello > file ; chmod 744 file
```

是的，其他人可以读取这个文件

- 13b. root 可以读取这个文件吗？root 可以用 `vi` 写入这个文件吗？

是的，root 可以读取和写入这个文件。权限不适用于 root。

- 14. 创建一个属于某个组的目录，该组的每个成员都可以对文件进行读写并创建文件。确保人们只能删除他们自己的文件。
