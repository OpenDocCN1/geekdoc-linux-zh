
- `=`：同步设置权限
- `r`：读权限
- `w`：写权限
- `x`：执行权限
- `s`：Suid 位
- `t`：粘滞位 (Sticky bit)

来看几个用法：

`chmod +r <file_name>`（赋予所有人读权限）

`chmod +rwx <file_name>`（赋予所有者所有权限）

### Linux 命令基础

`chmod o-wx <file_name>`（移除其他用户的写和执行权限）

`chmod u+rw,g+r,o+r <file_name>`（赋予所有者读写权限、组读权限、其他用户读权限）

`chmod go-rwx <file_name>`（从组和其他用户处移除所有 权限）

`chmod +x <file_name>`（赋予所有人执行权限）

让我们看一个如何更改权限的简单示例。我们有一个名为 `users.txt` 的文件。通过 `ls -l users.txt` 查看文件权限。

```
root@kemal:~# ls -l users.txt
-rw-r---- 1 root 144 Eyl 18 02:09 users.txt
```

状态似乎是 `-rw-r--`。正如之前提到的，初始标记 `-` 表示这是一个文件。如果是 `d` 字，我们会认为这是一个目录。根据此允许状态，所有者拥有读和写权限。如果我们想赋予组和其他用户写访问，必须使用 `chmod go+w users.txt` 命令。

```
root@kemal:~# chmod go+w users.txt
root@kemal:~# ls -l users.txt
-rw-rw-rw- 1 root 144 Eyl 18 02:09 users.txt
```

例如，为了移除组的读权限并移除其他用户的写权限，我们使用 `chmod g-r,o-w users.txt` 命令。

```
root@kemal:-# ls -l users.txt
-rw-rw-rw-- 1 root root 144 Eyl 18 02:09 users.txt
root@kemal:-# chmod g-r,o-w users.txt
root@kemal:-# ls -l users.txt
-rw-rw-r-- 1 root root 144 Eyl 18 02:09 users.txt
```

我们使用 `chmod` 命令来编辑权限，可以使用更实用的格式。我们通过数字模式表示权限来完成此过程。显示情况的数字等效权限如下：

### 文件所有者、组、和其他用户

| 所有者 | 组 | 其他用户 |
|---|---|---|
| `r = 4` | `r = 4` | `r = 4` |
| `w = 2` | `w = 2` | `w = 2` |
| `x = 1` | `x = 1` | `x = 1` |

根据上述匹配关系，我们可以用 `7` (4+2+1) 代替 `rwx`。同样，我们可以用 `777` 代替 `rwxrwxrwx`，用 `700` 代替 `rwx------`，用 `755` 代替 `rwxr-xr-x`。（`r-x=4+0+1`, `rw-=4+2+0`, `r=-4+0+0`）

例如，我们有一个名为 `deneme` 的文件，让我们赋予该文件所有权限 (rwx)。对于此，我们使用 `chmod 777 deneme` 命令。

```
root@kemal:-# ls -l deneme
-rw-r-r-- 1 root root 144 Eyl 21 00:27 deneme
root@kemal:-# chmod 777 deneme
root@kemal:-# ls -l deneme
-rwxrwxwx 1 root root 0 Eyl 21 00:27 deneme
```

## 116 | Linux 命令精通

现在，让我们关闭名为 `deneme` 的文件对除所有者以外所有用户的所有权限。我们需要使用 `chmod 700 deneme` 命令来实现此目标。

```
root@kemal:~# su zeynep
zeyep@kemal:/$ ls
Belgeler Downloads Genel Müzik Şablonlar Videolar deneme dwhelper Masaüstü Resimler users.txt
zeyep@kemal:/root$ cat deneme
Linux Commands
zeyep@kemal:/root$ exit
root@kemal:~# chmod 700 deneme
root@kemal:~# su zeynep
zeyep@kemal:/root$ cat deneme
cat: deneme: Erişim engellendi
zeyep@kemal:~$ _
```

如果你想对目录、子目录以及在文件中找到权限（例如 755）进行设置，你必须使用如 `chmod -R 755 <directory>` 的命令。这里注意 `-R` 参数的使用。

### Suid 位

每个用户都可以在其系统权限范围内执行操作。有时，普通用户临时需要 root 用户权限可能是必要的。因此，通常 root 用户能够运行程序，如果设置了 suid 位，当其他用户想要使用此程序时，只要程序可以运行，它就会以所有者的权限运行。更清楚地说，想要使用程序但没有权限的用户将需要 suid 位来临时运行该程序。

要设置 SUID 位，使用 `chmod u+s <file_name>` 命令。要找到带有 suid 位的文件，我们使用 `find / -perm -4000` 命令。

```
root@kemal:~\# find /perm -4000
/bin/ntfs-3g
/bin/mount
/bin/fusermount
/bin/umount
/bin/su
/usr/bin/bin/chfn
/usr/bin/newgrp
/usr/bin/pkexec
/usr/bin/gpasswd
/usr/bin/chsh
/usr/bin/kismet_capture
/usr/bin/at
/usr/bin/procmail
/usr/bin/sudo
/usr/bin/passwd
```

让我们看看这些文件，例如 `sudo` 文件的访问权限。

```
root@kemal:~# ls -l /usr/bin/sudo
-rws-xr-x 1 root root 176400 Mar 12 2015 /usr/bin/sudo
root@kemal:~#
```

当我们检查访问权限时，我们看到 `rws` 表达式。`s` 表示 suid 位已激活。

### 查找所有用户都可以写入的文件

写权限的文件和目录会产生安全风险。要列出这些文件，我们可以使用 `find / -perm -2 ! -type l -ls` 命令。

```
root@kemal:~# find . -perm ! -type l -ls
15269 4 drw-xr-x 2 root 4096 Mar 7 2015 /var/tmp
15250 4 drw-xr-x 14 root 4096 Eyl 21 01:37 /var/tmp
39360 4 drw-xr-x 2 root 4096 Eyl 26 23:36 /var/tmp/syst
end-private-92705376c16942a9b8511053-bf72aa35a8-rtkit-daemon.service-cfda50/tmp
153919 4 drw-xr-x 2 root 4096 Aug 22 11:10 /var/tmp/syst
end-private-7e2f72d18b6c054e6ab2b2738032e5-rtkit-daemon.v1251/tmp
15265 4 drw-xr-x 2 root 4096 Aug 22 11:06 /var/tmp/syst
end-private-045073b0e4f7994a99015a5e6ba979-rtkit-daemon.service/tmp
27110 4 drw-xr-x 2 root 4096 Aug 27 22:17 /var/tmp/syst
end-private-08a1b47122e4f8516eeb0a99-rtkit-daemon/tmp
15233 4 drw-xr-x 2 root 4096 Aug 22 11:06 /var/tmp/syst
```

在正常操作期间，可能会存在无写的文件。其中可能包含符号链接。为了排除符号链接，我们使用命令 `-type l`。

### Umask

在 Linux 系统中，分配新创建的文件和目录的默认访问权限由 `umask` 决定。要确定 umask 值，我们使用 `umask` 命令。

```
root@kemal:~# umask
0022
root@kemal:~#
```

通常，这个值在所有 Linux 发行版中均为 `022`。当你创建一个文件或目录时，默认权限将根据 umask 如下：

- 目录：`rwx-xr-x` (755)
- 文件：`rw-r--` (644)
