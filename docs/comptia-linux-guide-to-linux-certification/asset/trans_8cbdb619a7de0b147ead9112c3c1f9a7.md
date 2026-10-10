

20. 以下哪个命令可用于在 RPM 软件仓库中搜索包含单词 "oobla" 的软件包？

- a. yum search oobla
- b. rpm -qS oobla
- c. yum list oobla
- d. rpm -qI oobla

## 动手项目

这些项目应按照给定的顺序完成。本章中介绍的动手项目总共需要三小时才能完成。此实验的要求包括：

- 一台安装了 Fedora Linux 的计算机（根据动手项目 2-1 的要求安装）和一台安装了 Ubuntu Server Linux 的计算机（根据动手项目 6-1 的要求安装）。

### 项目 11-1

在这个动手项目中，你将使用常见的压缩工具在 Fedora 20 上压缩和解压信息。

1. 启动你的 Fedora Linux 虚拟机。Linux 系统加载完成后，按 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用用户名 root 和密码 LNXrocks! 登录到终端。
2. 在命令提示符下，输入 `yum install ncompress` 并按 `Enter`。当被提示时按 `y` 以完成 `ncompress` RPM 软件包（以及任何软件包依赖项）的安装。
3. 在命令提示符下，输入 `cp /etc/services ~` 并按 `Enter`，以在你家目录中创建 `/etc/services` 文件的副本。接下来，在命令提示符下输入 `ls -l` 并按 `Enter`。services 文件有多大？
4. 在命令提示符下，输入 `compress -v services` 并按 `Enter` 以压缩 services 文件。压缩比是多少？接下来，在命令提示符下输入 `ls -l` 并按 `Enter`。services 文件有什么扩展名，它有多大？
5. 在命令提示符下，输入 `uncompress -v services.Z` 并按 `Enter` 以解压缩 services 文件。
6. 在命令提示符下，输入 `cp /etc/hosts /etc/inittab Desktop` 并按 `Enter`，以将 `hosts` 和 `inittab` 文件复制到你的 `Desktop` 子目录中。
7. 在命令提示符下，输入 `compress -vr Desktop` 并按 `Enter` 以压缩 `Desktop` 子目录的内容。接下来，在命令提示符下输入 `ls -lR Desktop` 并按 `Enter` 以查看 `Desktop` 目录的内容。哪些文件被压缩了？如果该目录中存在符号链接，你如何强制 compress 实用程序也压缩这些文件？
8. 在命令提示符下，输入 `uncompress -vR Desktop` 并按 `Enter` 以解压缩 `Desktop` 子目录的内容。接下来，在命令提示符下输入 `ls -lR Desktop` 并按 `Enter` 以验证这些文件已被解压缩。
9. 在命令提示符下，输入 `ps -ef | compress -v > psfile.Z` 并按 `Enter`，以将 `ps -ef` 命令的输出压缩到一个名为 `psfile.Z` 的文件中。压缩比是多少？
10. 在命令提示符下，输入 `zmore psfile.Z` 并按 `Enter` 以查看 `psfile.Z` 文件的压缩内容。完成后，按 `q` 退出 `more` 实用程序。
11. 在命令提示符下，输入 `gzip -v services` 并按 `Enter` 以压缩 services 文件。压缩比是多少？这个比率与第 4 步中获得的比率相比如何？为什么？接下来，在命令提示符下输入 `ls -l` 并按 `Enter`。services 文件有什么扩展名，它有多大？
12. 在命令提示符下，输入 `gunzip -v services.gz` 并按 `Enter` 以解压缩 services 文件。
13. 在命令提示符下，输入 `gzip -v -9 services` 并按 `Enter` 以压缩 services 文件。压缩比是多少？为什么？
14. 在命令提示符下，输入 `gunzip -v services.gz` 并按 `Enter` 以解压缩 services 文件。
15. 在命令提示符下，输入 `gzip -v -1 services` 并按 `Enter` 以压缩 services 文件。压缩比是多少？为什么？
16. 在命令提示符下，输入 `gunzip -v services.gz` 并按 `Enter` 以解压缩 services 文件。
17. 在命令提示符下，输入 `bzip2 -v services` 并按 `Enter` 以压缩 services 文件。压缩比是多少？这与第 4 步和第 11 步中的比率相比如何？为什么？接下来，在命令提示符下输入 `ls -l` 并按 `Enter`。services 文件有什么扩展名，它有多大？
18. 在命令提示符下，输入 `bunzip2 -v services.bz2` 并按 `Enter` 以解压缩 services 文件。
19. 输入 `exit` 并按 `Enter` 以注销你的 shell。

### 项目 11-2

在这个动手项目中，你将使用 `tar` 实用程序创建、查看和提取存档。

1. 在你的 Fedora Linux 虚拟机上，按 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用用户名 root 和密码 LNXrocks! 登录到终端。
2. 在命令提示符下，输入 `tar -cvf test1.tar /etc/samba` 并按 `Enter`，以在当前目录中创建一个名为 `test1.tar` 的存档，其中包含 `/etc/samba` 目录及其内容。接下来，在命令提示符下输入 `ls -l` 并按 `Enter`。`test1.tar` 文件有多大？
3. 在命令提示符下，输入 `tar -tvf test1.tar` 并按 `Enter`。显示了什么？
4. 在命令提示符下，输入 `mkdir /new1` 并按 `Enter`。接下来，在命令提示符下输入 `cd /new1` 并按 `Enter`，以将当前目录更改为 `/new1` 目录。
5. 在命令提示符下，输入 `tar -xvf /root/test1.tar` 并按 `Enter` 以提取 `test1.tar` 存档的内容。接下来，在命令提示符下输入 `ls -RF` 并按 `Enter` 以查看 `/new1` 目录的内容。提取是否成功？
6. 在命令提示符下，输入 `cd` 并按 `Enter` 以返回你的家目录。
7. 在命令提示符下，输入 `tar -zcvf test2.tar.gz /etc/samba` 并按 `Enter`，以在当前目录中创建一个名为 `test2.tar.gz` 的 *gzip* 压缩存档，其中包含 `/etc/samba` 目录及其内容。接下来，在命令提示符下输入 `ls -l` 并按 `Enter`。`test2.tar.gz` 文件有多大？这与第 2 步中为 `test1.tar` 获得的尺寸相比如何？为什么？
8. 在命令提示符下，输入 `tar -ztvf test2.tar.gz` 并按 `Enter`。显示了什么？
9. 在命令提示符下，输入 `mkdir /new2` 并按 `Enter`。接下来，在命令提示符下输入 `cd /new2` 并按 `Enter`，以将当前目录更改为 `/new2` 目录。
10. 在命令提示符下，输入 `tar -zxfv /root/test2.tar.gz` 并按 `Enter` 以解压缩并提取 `test2.tar.gz` 存档的内容。接下来，在命令提示符下输入 `ls -RF` 并按 `Enter` 以查看 `/new2` 目录的内容。提取是否成功？
11. 在命令提示符下，输入 `cd` 并按 `Enter` 以返回你的家目录。
12. 在命令提示符下，输入 `modprobe floppy` 并按 `Enter`。这将加载软盘驱动器驱动程序。在软盘上创建和管理存档的过程与在磁带设备上创建和管理存档的过程相同。
13. 在命令提示符下，输入 `tar -cvf /dev/fd0 /etc/samba` 并按 `Enter`，以在设备 `/dev/fd0` 上创建一个存档，其中包含 `/etc/samba` 目录及其内容。
14. 在命令提示符下，输入 `tar -tvf /dev/fd0` 并按 `Enter`。显示了什么？
15. 在命令提示符下，输入 `mkdir /new3` 并按 `Enter`。接下来，在命令提示符下输入 `cd /new3` 并按 `Enter`，以将当前目录更改为 `/new3` 目录。
16. 在命令提示符下，输入 `tar -xvf /dev/fd0` 并按 `Enter` 以提取存储在第一个软盘上的存档内容。接下来，在命令提示符下输入 `ls -F` 并按 `Enter` 以查看 `/new3` 目录的内容。提取是否成功？
17. 在命令提示符下，输入 `mount /dev/fd0 /mnt` 并按 `Enter` 以将软盘挂载到 `/mnt` 目录。你收到什么错误信息，为什么？为什么文件系统类型没有自动检测？这个软盘可以挂载吗？
18. 在命令提示符下，输入 `rm -Rf /New [123]` 并按 `Enter` 以删除在此动手项目中创建的目录。

