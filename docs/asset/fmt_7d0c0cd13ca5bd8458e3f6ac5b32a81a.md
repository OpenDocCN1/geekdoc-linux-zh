
## 6.
在命令提示符下，输入 `mkdir compressed; cp /etc/hosts /etc/init` 并按回车创建子目录并复制 `hosts` 和 `init` 文件。

## 7.
在命令提示符下，输入 `compress -v compressed` 并按回车压缩 `Desktop` 目录的内容。接下来，输入 `ls -l` 查看目录内容。如果此目录中有符号链接，你是否能强制 `compress` 工具也压缩这些文件？

## 8.
在命令提示符下，输入 `uncompress -v Desktop` 并按回车解压 `Desktop` 子目录的内容。

## 9.
在命令提示符下，输入 `tar -ef | compress -v file.Z` 并按回车将内容输出到文件 `file.Z` 中。压缩率是多少？

## 10.
在命令提示符下，输入 `zless file.Z` 并按回车查看 `file.Z` 的内容。完成后，按 `q` 退出 `more` 工具。

## 11.
在命令提示符下，输入 `zip -v compressed` 并按回车将 `Desktop` 子目录的内容压缩成单个 `zip` 文件。你得到的压缩率是多少？

## 12.
在命令提示符下，输入 `unzip -v compressed.zip` 并按回车查看 `compressed.zip` 的内容。接下来，输入 `unzip compressed.zip` 并按回车提取内容。在解压过程中出现提示覆盖现有文件时，按 `A`。

## 13.
在命令提示符下，输入 `gzip -v services` 并按回车压缩 `services` 文件。此压缩率与步骤4中得到的压缩率相比如何？为什么？接下来，在命令提示符下输入 `ls -l services` 并按回车。`services` 文件的扩展名是什么？多大？

## 14.
在命令提示符下，输入 `gzip -v services.gz` 并按回车解压 `services` 文件。

## 15.
在命令提示符下，输入 `gzip -v -9 services` 并按回车压缩 `services` 文件。压缩率是多少？为什么？

## 16.
在命令提示符下，输入 `gzip -v services.gz` 并按回车解压 `services` 文件。

## 17.
在命令提示符下，输入 `gzip -v -1 services` 并按回车压缩 `services` 文件。压缩率是多少？为什么？

## 18.
在命令提示符下，输入 `gzip -v services.gz` 并按回车解压 `services` 文件。

## 19.
在命令提示符下，输入 `xz -v -9 services` 并按回车压缩 `services` 文件。压缩率是多少？为什么它比步骤13大？

## 20.
在命令提示符下，输入 `unxz -v services.xz` 并按回车解压 `services` 文件。

## 21.
在命令提示符下，输入 `bzip2 -v services` 并按回车压缩 `services` 文件。压缩率是多少？这与步骤4、步骤13和步骤19的压缩率相比如何？接下来，在命令提示符下输入 `ls -l` 并按回车。`services` 文件的扩展名是什么？多大？

## 22.
在命令提示符下，输入 `bzip2 -v services.bz2` 并按回车解压 `services` 文件。

## 23.
输入 `exit` 并按回车退出 `shell`。

# 项目 11-2

在本次实践项目中，你将使用 `tar` 工具创建、查看和提取归档。

## 1.
在你的 Fedora Linux 虚拟机上，通过 `Ctrl+Alt+F5` 切换到命令行终端 `tty5`，并使用用户名 `root` 和密码 `LINUXrocks!` 登录终端。

## 2.
在命令提示符下，输入 `tar -cvf test1.tar /etc/samba` 并按回车在当前目录下创建一个名为 `test1.tar` 的归档，包含 `/etc/samba` 目录及其内容。接下来，在命令提示符下输入 `ls -l test1.tar` 并按回车。`test1.tar` 有多大？

## 3.
在命令提示符下，输入 `tar -tvf test1.tar` 并按回车。显示了什么？

## 4.
在命令提示符下，输入 `mkdir /new1` 并按回车。接下来，在命令提示符下输入 `cd /new1` 并按回车将当前目录更改为 `/new1` 目录。

## 5.
在命令提示符下，输入 `tar -xvf /root/test1.tar` 并按回车提取 `test1.tar` 归档的内容。接下来，在命令提示符下输入 `ls -lRP` 并按回车查看 `/new1` 目录的内容。提取成功了吗？

## 6.
在命令提示符下，输入 `cd` 并按回车返回主目录。

## 7.
在命令提示符下，输入 `tar -zcf test2.tar.gz /etc/samba` 并按回车在当前目录下创建一个名为 `test2.tar.gz` 的 `gzip` 压缩归档，包含 `/etc/samba` 及其内容。接下来，在命令提示符下输入 `ls -l test2.tar.gz` 并按回车。`test2.tar.gz` 文件有多大？这与步骤2中得到的 `test1.tar` 大相比如何？为什么？

## 8.
在命令提示符下，输入 `tar -ztvf test2.tar.gz` 并按回车。显示了什么？

## 9.
在命令提示符下，输入 `mkdir /new2` 并按回车。接下来，在命令提示符下输入 `cd /new2` 并按回车。

## 10.
在命令提示符下，输入 `tar -zxf /root/test2.tar.gz` 并按回车解压并提取 `test2.gz` 归档。接下来，在命令提示符下输入 `ls -lRF` 并按回车查看 `/new2` 目录的内容。提取成功了吗？

## 11.
在命令提示符下，输入 `cd` 并按回车返回主目录。

## 12.
在命令提示符下，输入 `rm -Rf /new` 并按回车删除项目中创建的目录。

## 13.
在命令提示符下，输入 `rm -f test*` 并按回车删除项目中创建的归档。

## 14.
输入 `exit` 并按回车退出 `shell`。

# 项目 11-3

在本次实践项目中，你将使用 `cpio`、`dump` 和 `dd` 创建、查看和提取归档。

## 1.
在 Fedora Linux 虚拟机上，通过 `Ctrl+Alt+F5` 切换到命令行终端 `tty5`，并使用用户名 `root` 和密码 `LINUXrocks!` 登录终端。

## 2.
在命令提示符下，输入 `find /etc/samba | cpio -ov -O` 并按回车创建 `/etc/samba` 目录及其内容的归档。每个选项代表什么？

## 3.
在命令提示符下，输入 `cpio -ivtb test.pio` 并按回车。显示了什么？每个选项代表什么？

## 4.
在命令提示符下，输入 `cpio -ivdmM -T test.pio` 并按回车提取归档。文件提取到了哪里？是否有文件被覆盖？每个选项代表什么？

## 5.
在命令提示符下，输入 `dnf install dump` 并按回车安装 `dump` 包（以及依赖项）。

## 6.
在命令提示符下，输入 `dump -f test.dump /dev/sda` 并按回车创建 `/boot` 文件系统的归档。执行的是什么类型的备份？`/etc/dumpdate` 文件会更新吗？

## 7.
在命令提示符下，输入 `cat /etc/dumpdate` 并按回车。该文件显示了你的备份和时间吗？

## 8.
在命令提示符下，输入 `mkdir /new` 并按回车。接下来，在命令提示符下输入 `cd /new` 并按回车将当前目录进入 `/new` 目录。

## 9.
在命令提示符下，输入 `restore -rf /root/test.dump` 并按回车。

## 10.
在命令提示符下，输入 `ls -F` 并按回车查看 `/new` 目录的内容。显示了什么？恢复过程中使用的是绝对路径还是相对路径？

## 11.
在命令提示符下，输入 `cd` 并按回车返回主目录。

## 12.
在命令提示符下，输入 `dd if=/dev/sda of=test.img` 并按回车创建 `/boot` 文件系统的镜像备份。

## 13.
在命令提示符下，输入 `ls -l test.img test.dump` 并按回车。尽管两者都用于备份 `/boot` 文件系统，为什么 `test.img` 文件比 `test.dump` 大得多？

## 14.
在命令提示符下，输入 `rm -Rf /new` 并按回车删除项目中创建的目录。

## 15.
在命令提示符下，输入 `rm -f /root/test*` 并按回车删除项目中创建的归档。

## 16.
输入 `exit` 退出 `shell`。

# 项目 11-4

在本次实践项目中，你从源码编译并安装 `conky` 程序。

## 1.
在 Fedora Linux 虚拟机上，通过 `Ctrl+Alt+F1` 切换到 `tty1`，使用用户名 `user1` 和密码 `LINUXrocks!` 登录 GNOME 桌面。
