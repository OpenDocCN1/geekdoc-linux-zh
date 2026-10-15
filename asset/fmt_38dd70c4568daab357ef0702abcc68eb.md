
`-r-------- root root 1260 Jan 21 07:49 /etc/shadow`

更改密码需要更新此文件，那么非 `root` 用户如何做到这一点？让我们看看`/usr/bin/passwd`的权限。

```
root@RHELv4:~# ls -l /usr/bin/passwd
-r-s----x root root 21200 Jun 17 2005 /usr/bin/passwd
```

运行`passwd`程序时，你是在使用`root`凭据执行它。

你可以使用`find`命令找到所有 setuid 程序。

```
paul@laika:~~$ find /usr/bin -type f -perm -4000
/usr/bin/arping
/usr/bin/chch
/usr/bin/newgrp
/usr/bin/mount
/usr/bin/sudo
/usr/bin/ping
/usr/bin/passwd
/usr/bin/gpasswd
..
```

在大多数情况下，为可执行文件设置 setuid 就足够了。设置 setgid 会导致这些程序以其组所有者的凭据运行。

### 33.4. `sudo` 的 setuid

`sudo`二进制文件设置了 setuid 位，因此任何用户都可以以`root`用户身份运行它。

```
paul@rhel6:~~$ ls -l $(which sudo)
-rwsws-xr-x 1 root root 123832 Oct 7 2013 /usr/bin/sudo
paul@rhel6:~~$
```

### 33.5. 练习：粘位、setuid 和 setgid 位

- 1a. 设置一个属于`sports`组的目录。
- 1b. `sports`组的成员能够在该目录下创建文件。
- 1c. 该目录下创建的所有文件都应该属于`sports`组。
- 1d. 用户只能删除属于自己的用户文件。
- 1e. 测试这是否有效！
- 2. 验证`/usr/bin/passwd`的权限。移除 setuid，然后尝试作为普通用户更改密码。恢复权限并再次尝试。
- 3. 如果时间允许（或者如果你正在等待其他学生完成此练习），在`chattr`和`lsattr`的帮助页中阅读文件属性。在文件上设置`i`属性并测试其是否有效。

## 33.6. 解决方案：sticky、setuid 和 setgid 位

1a. 创建一个目录，其所有组为`sports`组。

```
groupadd sports
mkdir /home/sports
chown root:sports /home/sports
```

1b. `sports`组的成员应该能够在该目录下创建文件。

```
chmod 770 /home/sports
```

1c. 在此目录下创建的所有文件都应该属于`sports`组。

```
chmod 2770 /home/sports
```

1d. 用户应该只能删除由其用户所有拥的文件。

```
chmod +t /home/sports
```

1e. 测试该功能是否有效！

以不同的用户（组内成员和其他用户）身份登录，创建文件并观察权限。尝试修改和删除文件……

2. 验证`/usr/bin/passwd`的权限。移除`setuid`，然后作为普通用户更改密码。重置权限并重试。

```
root@deb503:~# ls -l /usr/bin/passwd
-rwxr-xr-x 1 root 31704 2009-11-14 14:51 /usr/bin/passwd
root@deb503:~# chmod 755 /usr/bin/passwd
root@deb503:~# ls -l /usr/bin/passwd
-rwxr-xr-x 1 root 31704 2009-11-14 14:51 /usr/bin/passwd
```

普通用户无法更改密码。

```
root@deb503:~# chmod 4755 /usr/bin/passwd
root@deb503:~# ls -l /usr/bin/passwd
-rwsrxr-x 1 root 31704 2009-11-14 14:51 /usr/bin/passwd
```

3. 如果时间允许（或者如果你正在等待其他学生完成此过程），请阅读`chattr`页面中的文件属性介绍。尝试在文件上设置属性并测试是否有效。

```
paul@laika:~# sudo su -
[sudo] password for paul:
root@laika:~# mdir attr
root@laika:~# cd attr
root@laika://attr# touch file42
root@laika://attr# lsattr
----------------------.file42
root@laika://attr# chattr +i file42
```

```
root@laika:~/attr# lsattr
----i---------- ./file42
root@laika:~/attr# rm -rf file42
rm: cannot remove file42: Operation not permitted
root@laika:~/attr# chattr -i file42
root@laika:~/attr# rm -rf file42
root@laika:~/attr#
```

## 第 34 章 访问控制列表

标准的 Unix 权限可能无法满足某些组织。本章介绍了访问控制列表（`acl`），以进一步保护文件和目录。

### 34.1. `/etc/fstab` 中的 `acl`

支持访问控制列表（`acl`）的文件系统必须在`/etc/fstab`中使用`acl`选项进行挂载。在下面的示例中，你可以看到根文件系统支持`acl`，而`/home/data`则不支持。

```
root@laika:~# tail -4 /etc/fstab
/dev/sda               / acl,relatime 0 1
/dev/sd2              /home/data auto noacl,defaults 0 0
pasha:/home/r          /home/pasha nfs defaults 0 0
wolf:/srv/data         /home/wolf nfs defaults 0 0
```

### 34.2. `getfacl`

可以使用`/usr/bin/getfacl`读取`acl`。此截图显示了如何使用`getfacl`读取文件`file33`。

```
paul@laika:~$ test getfacl file33
# file: file33
# owner: paul
# group: paul
user::rw-
group::-
mask:rwx
other::r--
```

### 34.3. `setfacl`

可以使用`/usr/bin/setfacl`或更改`acl`。这些截图显示了如何使用`setfacl`更改`file33`的`acl`。

首先，我们向`acl`中添加八进制权限为`7`的用户`sandra`。

然后，我们向同一文件的`acl`中添加八进制权限为`6`的组`tennis`。

```
paul@laika:~$ test setfacl -m g:tennis:6 file33
```

结果可以通过`getfacl`看到。

```
paul@laika:~$ test getfacl file33
# file: file33
# owner: paul
# group: paul
user::rw-
user:sandra:rwx
group::-
group:tennis:r--
mask:rwx
other::r--
```

### 34.4. 删除 `acl` 条目

`setfacl`命令的`-x`选项将从目标文件中删除`acl`条目。

```
paul@laika:/~/test$ setfacl -m u:sandra:7 file33
paul@laika:/~/test$ setfacl file33 | grep sandra
user:rwx
paul@laika:~/test$ setfacl -x sandra file33
paul@laika:~/test$ setfacl file33 | grep sandra
```

注意，在定义`acl`时省略`-u`或`-g`将将其默认为用户。

### 34.5. 删除完整的 `acl`

`setfacl`命令的`-b`选项将从目标文件中删除`acl`。

```
paul@laika:~/test$ setfacl -b file33
paul@laika:~/test$ lsattr file33
# file:file33
```
