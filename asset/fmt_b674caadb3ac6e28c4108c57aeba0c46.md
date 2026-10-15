
```
paul@RHEL52 ~~$ man password          # 打开找到的第一个
paul@RHEL52 ~~$ man 5 password          # 打开第 5 部分的页面
```

## 7.9. man db

如果你想了解更多关于 `man` 的信息，请阅读《终极手册》（The Fantastic Manual, RTFM）。

遗憾的是，手册页并没有无万能的答案……

```
paul@laika:~$ man woman
No manual entry for woman
```

## 7.10. mandb

如果你确信 `man page` 存在但无法访问它，可以尝试在 Debian/Mint 上运行 `mandb`。

```
root@laika:~# mandb
0 man subdirectories contained newer man pages.
0 manual pages were added.
0 stray cats were added.
0 old database entries were purged.
```

或者在 CentOS/Redhat 上运行 `makewhat`。

```
[root@centos65 ~#] apropos scsi
scsi: nothing
[root@centos65 ~#] apropos scsi
h (4) Smart Array
l (8) list SCSI devices (or hosts) and their attributes
d (4) Driver for SCSI Drives
sd (4) SCSI tape device
```

# 第 8 章 目录操作

本模块是对处理目录常用命令的简要概述：`pwd`、`cd`、`ls`、`mkdir` 和 `rmd`。这些命令在任何 Linux（或 Unix）系统上可用。本模块还讨论了绝对路径、相对路径以及 `bash` shell 中的路径自动补全。

## 8.1. pwd

可以使用 `pwd` 命令（打印目录）显示“你在这里”。试试看：打开一个命令行界面（也称为终端、控制或 xterm）并输入 `pwd`。该工具会显示你当前的目录。

```
paul@debian:~$ pwd
/home/paul
```

## 8.2. cd

你可以使用 `cd` 命令（切换目录）更改当前目录。

```
paul@debian:~$ cd /etc
paul@debian:~$ pwd
/etc
paul@debian:~$ cd /bin
paul@debian:~$ pwd
/bin
```

## 8.3. cd ~

可以使用 `cd ~` 命令切换到家目录。

```
paul@debian:~$ cd ~
paul@debian:~$ pwd
/home/paul
```

## 8.4. cd /

可以使用 `cd /` 命令切换到根目录。

```
paul@debian:~$ cd /
paul@debian:~$ pwd
/
```

## 8.5. cd .. (返回)

可以使用 `cd ..` 命令返回上级目录。

```
paul@debian:~$ cd ..
paul@debian:~$ pwd
/home
```

## 8.6. cd -

可以使用 `cd -` 命令切换到上一个目录。

```
paul@debian:~$ cd -
paul@debian:~$ pwd
/etc
```

## 8.7. pwd (绝对路径)

可以使用 `pwd` 命令显示你所在的绝对路径。

```
paul@debian:~$ cd /etc
paul@debian:~$ pwd
/etc
```

## 8.8. 相对路径 (相对路径)

```
paul@debian:~$ cd ..
paul@debian:~$ pwd
/home
```

## 8.9. ls (列出目录)

可以使用 `ls` 命令查看目录内容。

```
paul@debian:~$ ls
```

## 8.10. mkdir (创建目录)

可以使用 `mkdir` 命令创建新目录。

```
paul@debian:~$ mkdir testdir
```

## 8.11. rmdir (删除目录)

可以使用 `rmdir` 命令删除空目录。

```
paul@debian:~$ rmdir testdir
```

### 8.5.3. ls -lh

另一个常用的选项 `ls -h`。它以更易于人类阅读的格式显示数字（文件大小）。下面还展示了向 `ls` 提供选项的一些不同方式。我们将在本书的后部分解释输出的详细信息。

注意，我们在截图未使用字母 `L` 作为选项，而不是数字 `1`。

```
paul@debian:~$ ls -l -nhntotal 17M
-rw-r--r 1 paul 17M Sep 17 00:03 allfiles.txt
-rw-r--r 1 paul 95K Sep 17 00:03 dmesg.txt
-rw-r--r 1 paul 20K Sep 17 00:04 services
drwxr-xr-x 2 paul 4.0K Sep 17 00:04 stuff
-rw-r--r 1 paul 0 Sep 17 00:04 summer.txt
paul@debian:~$ ls -l -lh
total 17M
-rw-r--r 1 paul 17M Sep 17 00:03 allfiles.txt
-rw-r--r 1 paul 95K Sep 17 00:03 dmesg.txt
-rw-r--r 1 paul 20K Sep 17 00:04 services
drwxr-xr-x 2 paul 4.0K Sep 17 00:04 stuff
-rw-r--r 1 paul 0 Sep 17 00:04 summer.txt
paul@debian:~$ ls -l -1
total 17M
-rw-r--r 1 paul 17M Sep 17 00:03 allfiles.txt
-rw-r--r 1 paul 95K Sep 17 00:03 dmesg.txt
-rw-r--r 1 paul 20K Sep 17 00:04 services
drwxr-xr-x 2 paul 4.0K Sep 17 00:04 stuff
-rw-r--r 1 paul 0 Sep 17 00:04 summer.txt
paul@debian:~$
```

### 8.6. mkdir

在 Unix 树中漫游很有趣，但使用 `mkdir` 创建自己的目录更有趣。你必须给 `mkdir` 至少提供一个参数，即要创建的新目录名称。在输入开头的 `/` 之前请思考一下。

```
paul@debian:-$ mkdir mydir
paul@debian:~$ cd mydir
paul@debian:~/mydir ls -l
total 8
drwxr-xr-x 2 paul 4096 Sep 17 00:07
drwxr-xr-x 4 paul 4096 Sep 17 00:07 ..
paul@debian:~/mydir mkdir stuff
paul@debian:~/mydir otherstuff
paul@debian:~/mydir ls -l
total 8
drwxr-xr-x 2 paul 4096 Sep 17 00:07 otherstuff
drwxr-xr-x 2 paul 4096 Sep 17 00:07 stuff
paul@debian:~/mydir$ 
```

### 8.6.1 mkdir -p

该命令将失败，因为 `threirsdeep` 的父目录不存在。

```
paul@debian:-$ mkdir mydir2/mysubdir2/threedirsdeep
mkdir: cannot create directory 'mydir2/mysubdir2/threedirsdeep': No such file
or or directory
```

当给出选项 `-p` 时，`mkdir` 将根据需要创建父目录。
