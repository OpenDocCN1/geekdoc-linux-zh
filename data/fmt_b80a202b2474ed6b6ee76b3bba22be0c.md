
```
paul@debian7~$ head -c14 /etc/passwd
root:x:0:0:roopaul@debian7~$
```

## 10.2. tail

与`head`类似，`tail`命令将显示文件的最后几行。

```
paul@debian7~$ tail /etc/services
vboxd      20012/udp
binkp       24554/tcp
asp          27374/tcp
ast          27374/udp
csync2      30865/tcp
dircproc     57000/tcp
ffidos       60177/tcp
fido        60179/tcp
paul@debian7~$
```

你可以使用`tail -n`指定你想看到的行数。

```
paul@debian7~$ tail -3 /etc/services
fido        60179/tcp
paul@debian7~$
```

（注：原文 10.2 结尾处代码块似乎有断行，已按原样保留）

## 10.8. 解决方案：文件内容

1. 显示`/etc/services`的前12行。

```
head -12 /etc/services
```

2. 显示`/etc/passwd`的最后一行。

```
tail -1 /etc/passwd
```

3. 使用`cat`创建一个名为`count.txt`的文件，内容如下：

```
cat > count.txt
One
Two
Three
Four
Five (按下 Ctrl-d 结束)
```

4. 使用`cp`将该文件备份到`cnt.txt`。

```
cp count.txt cnt.txt
```

5. 使用`cat`将该文件备份到`catcnt.txt`。

```
cat count.txt > catcnt.txt
```

6. 反序显示`catcnt.txt`的所有行（最后一行在最）。

```
tac catcnt.txt
```

7. 使用`more`显示`/etc/services`。

```
more /etc/services
```

8. 显示`/usr/bin/passwd`命令中的可读字符字符串。

```
strings /usr/bin/passwd
```

9. 使用`ls`找到`/etc`目录中最大的文件。

```
ls -ls /etc
```

10. 打开两个终端窗口（或标签页），确保你处于同一个目录下。在第一个终端执行`echo This is the first line > tailing.txt`，然后在第二个终端中使用`tail -f tailing.txt`。现在回到第一个终端并执行`echo This is another line >> tailing.txt`（注意双大于`>>`），验证第二个终端的`tail -f`是否显示了两个行。按Ctrl-C停止`tail -f`。

11. 使用`cat`创建一个名为`tailing.txt`的文件，其中包含`tailing.txt`的内容，随后是`/etc/passwd`的内容。

```
cat /etc/passwd >> tailing.txt
```

12. 使用`cat`创建一个名为`tailing.txt`的文件，其中包含`/etc/passwd`的内容，在其后是`tailing.txt`的内容。

```
mv tailing.txt tmp.txt ; cat /etc/passwd tmp.txt > tailing.txt
```

## 第 11 章. Linux 文件树

本章将介绍Linux文件树中常见的目录。它还展示了在Unix系统中，一切皆文件。

## 11.1. 文件系统层次结构标准 (FHS)

许多Linux发行版部分地遵循文件系统层次结构标准（FHS）。FHS有助于未来更多Unix/Linux文件系统更好地符合标准。可以在`http://www.pathname.com/fhs`在线查看FHS，我们在那里看到：“文件系统层次结构被设计供Unix发行版开发者使用”。

## 11.2. man hier

不同的Linux发行版之间的文件系统存在一些差异。为了帮助你的机器，请输入`man hier`来查找有关文件系统层次结构的信息。该手册将解释你计算机上的目录结构。

## 11.3. 根目录 /

所有的Linux系统都有从根目录开始的目录结构。根目录由斜杠`/`表示，如下所示`/`。你Linux系统上存在的所有内容都可以在这个根目录之下找到。让我们简要查看根目录的内容。

```
[paul@RHEL4u3 ~]$ ls /
bin dev home media mnt sbin srv tftpboot usr
boot etc lib misc opt root selinux sys tmp var
```

## 11.4. 二进制目录

二进制文件是包含编译后的源文件（或机器码）的文件。二进制文件可以在计算机上执行。有时二进制文件也被称为可执行文件。

### 11.4.1. /bin

`/bin`目录包含所有用户使用的二进制文件。根据FHS，`/bin`目录应该包含`/bin/cat`和`/bin/date`（以及其他文件）。

在下方的图中，你看到了常见的Unix/Linux命令，如`cat`、`cpio`、`dd`、`dd`、`echo`、`grep`等。这些中的许多命令都将在本书中进行介绍。

```
paul@alika~$ ls /bin
archdetect      grep     mt               setupcon
autopartition false     mt-gnu           sh
bash           console mv               sh.distrib
bunzip2        fuser    nano              sleep
bcat            fusermount  nc.traditional stralign
bczmp          get_mountpoints netcat          tty
dbzdiff       grep      netstat         sync
bzgrep       grep      nfs-3g          sysfs
bzgrep       gzip      nfs-3g.probe    talf
bzgrep       gzip      parsed_devices tar
bzip2        hostname parted_server tempfile
bzip2ipecover  hw-detect               touch
bzless        ip        partman-commit true
cat            kbd_mode perform_recipe ulockmgr
              kill      pidof             umount
              ... 
```

### 11.4.2. 其他 bin 目录

你可以在许多其他目录中找到`/bin`子目录（注：原文为 /bin，此处意译为 bin 子目录）。一个名为`serena`的用户可以将她的程序放在`/home/serena/bin`中。

某些应用程序在直接从源码安装时会将它们存放在`/opt`中。`samba`服务器安装可以使用`/opt/samba/bin`来存储其二进制文件。

### 11.4.3. /sbin

`/sbin`包含配置操作系统的二进制文件。许多系统二进制文件需要`root`权限才能执行某些任务。

下方是一个包含更改IP地址、分区磁盘和创建`ext4`系统的系统二进制文件的截图。

```
paul@ubu10:~$ ls -l /sbin/mkfs.ext4
-rwxr-xr-x 1 root 9112 02-02
-rwxr-xr-x 1 root 6570 07-02 fdisk
-rwxr-xr-x 1 root 5514 08-18 ipconfig
```

# Linux 文件树结构
