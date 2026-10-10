
19. 在命令提示符下，输入 `rm -f /root/test*` 并按下**Enter**键以删除在本实用项目中创建的 tar 归档文件。

20. 输入 `exit` 并按下**Enter**键以注销你的 shell。

# 项目 11-3

在本实用项目中，你将使用 cpio 和 dump 实用程序创建、查看和提取归档。

- 1. 在你的 Fedora Linux 虚拟机上，按**Ctrl+Alt+F2** 切换到命令行终端 (tty2)，并使用用户名 **root** 和密码 **LNXr0cks!** 登录终端。
- 2. 在命令提示符下，输入 `find /etc/samba | cpio -ovcBL -O test.cpio` 并按下**Enter**键，以在 test.cpio 文件中创建一个包含 /etc/samba 目录及其内容的归档。上述命令中的每个选项表示什么？
- 3. 在命令提示符下，输入 `cpio -ivtB -i test.cpio` 并按下**Enter**键。显示了什么内容？上述命令中的每个选项表示什么？
- 4. 在命令提示符下，输入 `cpio -ivcduBF -i test.cpio` 并按下**Enter**键，以提取 test.cpio 文件中归档的内容。文件被提取到了什么位置？是否有文件被覆盖？上述命令中的每个选项表示什么？
- 5. 在命令提示符下，输入 `yum install dump` 并按下**Enter**键。当被提示时按下**y**以完成 dump RPM 软件包（及其依赖的软件包）的安装。
- 6. 在命令提示符下，输入 `dump -0uf test.dump /dev/sda1` 并按下**Enter**键，以在归档文件 test.dump 中创建 /boot 文件系统的归档。执行了哪种类型的备份？/etc/dumpdates 文件会被更新吗？
- 7. 在命令提示符下，输入 `cat /etc/dumpdates` 并按下**Enter**键。该文件是否显示了你的完整备份和时间？
- 8. 在命令提示符下，输入 `mkdir /new` 并按下**Enter**键。接下来，在命令提示符下输入 `cd /new` 并按下**Enter**键，将当前目录更改为 /new 目录。
- 9. 在命令提示符下，输入 `restore -rf /root/test.dump` 并按下**Enter**键。显示了什么内容？使用的是绝对路径名还是相对路径名？
- 10. 在命令提示符下，输入 `ls -F` 并按下**Enter**键，以查看 /new 目录的内容。显示了什么内容？
- 11. 在命令提示符下，输入 `cd` 并按下**Enter**键，返回到你的主目录。
- 12. 在命令提示符下，输入 `rm -Rf /new` 并按下**Enter**键，以删除在本实用项目中创建的目录。
- 13. 在命令提示符下，输入 `rm -f /root/test*` 并按下**Enter**键，以删除在本实用项目中创建的归档。
- 14. 输入 `exit` 并按下**Enter**键，以注销你的 shell。

# 项目 11-4

在本实用项目中，你将从源代码编译和安装一个程序。

- 1. 在你的 Fedora Linux 虚拟机上，按 Ctrl+Alt+F1 切换到图形终端 (tty1)，并使用用户名 user1 和密码 LNXr0cks! 登录到 GNOME 桌面。
- 2. 打开 Firefox Web 浏览器，从 www.rdesktop.org 下载 rdesktop 1.8.2 的源代码 tarball (rdesktop-1.8.2.tar.gz)。将源代码 tarball 保存到默认位置 (/home/user1/Downloads)，完成后注销 GNOME 桌面。
- 3. 接下来，按 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用用户名 root 和密码 LNXr0cks! 登录终端。
- 4. 在命令提示符下，输入 `yum groupinstall "Development Tools"` 并按下 Enter 键，以从软件仓库安装编译工具。
- 5. 在命令提示符下，输入 `yum install libX11-devel openssl-devel` 并按下 Enter 键，以从软件仓库安装 X11 和 OpenSSL 开发库。
- 6. 在命令提示符下，输入 `cp /home/user1/Downloads/rdesktop-1.8.2.tar.gz ~` 并按下 Enter 键，以将 rdesktop 源代码 tarball 复制到你的主目录。
- 7. 在命令提示符下，输入 `tar -zxvf rdesktop-1.8.2.tar.gz` 并按下 Enter 键，以解压和提取 tarball 的内容。接下来，在命令提示符下输入 `ls -F` 并按下 Enter 键。创建了哪个目录？
- 8. 在命令提示符下，输入 `cd rdesktop-1.8.2` 并按下 Enter 键。接下来，在命令提示符下输入 `ls -F` 并按下 Enter 键。是否有可执行的 configure 程序？是否存在 README 和 INSTALL 文件？
- 9. 在命令提示符下，输入 `./configure --disable-dreadsd --disable-smartcard` 并按下 Enter 键，以运行 configure 脚本而不配置 cdesk 和 smartcard 支持。这个程序的作用是什么？在输出的底部，你能看到 Makefile 是否成功创建了吗？
- 10. 在命令提示符下，输入 `make` 并按下 Enter 键。make 程序的作用是什么？哪个程序编译了程序的不同部分？
- 11. 在命令提示符下，输入 `make install` 并按下 Enter 键。make install 命令的作用是什么？
- 12. 在命令提示符下，输入 `cd` 并按下 Enter 键，返回到你的主目录。接下来，输入 `rm -Rf rdesktop-1.8.2` 以删除 rdesktop 的源代码目录。
- 13. 在命令提示符下，输入 `which rdesktop` 并按下 Enter 键。哪个目录包含 rdesktop 可执行程序？中央数据库是否更新了此信息？
- 14. 在命令提示符下，输入 `man rdesktop` 并按下 Enter 键。查看 rdesktop 命令的可用选项，完成后按 q 退出。
- 15. 输入 `exit` 并按下 Enter 键，以注销你的 shell。

# 项目 11-5

在本实用项目中，你使用 **rpm** 和 **yum** 命令查询、删除和安装 ncompress RPM 软件包。

- 1. 在你的 Fedora Linux 虚拟机上，按 **Ctrl+Alt+F2** 切换到命令行终端 (tty2)，并使用用户名 **root** 和密码 **LNXrocks!** 登录终端。
- 2. 在命令提示符下，输入 **rpm -qa | less** 并按下 **Enter** 键，以查看计算机上安装的 RPM 软件包。有很多吗？简要浏览列表，完成后按 **q** 退出 less 实用程序。
- 3. 在命令提示符下，输入 **rpm -q ncompress** 并按下 **Enter** 键。ncompress RPM 软件包安装在你的计算机上吗？你什么时候安装的？
- 4. 在命令提示符下，输入 **rpm -qi ncompress** 并按下 **Enter** 键，以查看关于 ncompress RPM 软件包的信息。此软件包使用什么许可证？
- 5. 在命令提示符下，输入 **rpm -ql ncompress** 并按下 **Enter** 键，以查看属于 ncompress 软件包的所有文件的位置。哪个目录包含 compress 和 uncompress 可执行文件？
- 6. 在命令提示符下，输入 **rpm -e ncompress** 并按下 **Enter** 键。此选项对 rpm 命令做什么？
- 7. 在命令提示符下，输入 **rpm -q ncompress** 并按下 **Enter** 键。ncompress RPM 软件包安装了吗？
- 8. 在命令提示符下，输入 **yum search compress | less** 并按下 **Enter** 键。ncompress RPM 软件包列出了吗？按 **q** 退出 less 实用程序。
- 9. 在命令提示符下，输入 **yum list available | grep compress** 并按下 **Enter** 键。ncompress RPM 软件包是否可以从软件仓库安装？
- 10. 在命令提示符下，输入 **yum install ncompress** 并按下 **Enter** 键。当被提示时按下 **y** 以完成安装。
- 11. 在命令提示符下，输入 **rpm -q ncompress** 并按下 **Enter** 键。ncompress RPM 软件包安装了吗？
- 12. 输入 **exit** 并按下 **Enter** 键，以注销你的 shell。

# 项目 11-6

在本实用项目中，你使用 **dpkg** 和 **apt-get** 命令安装、查询和删除 ncompress DPM 软件包。

- 1. 启动你的 Ubuntu Server Linux 虚拟机，并使用用户名 **root** 和密码 **LNXrocks!** 登录到 tty1。
- 2. 在命令提示符下，输入 **dpkg -l | less** 并按下 **Enter** 键，以查看计算机上安装的 DPM 软件包。有很多吗？简要浏览列表，完成后按 **q** 退出 less 实用程序。
- 3. 在命令提示符下，输入 **dpkg -L ncompress** 并按下 **Enter** 键，以列出组成 ncompress 软件包的文件。ncompress DPM 软件包安装在你的计算机上吗？
- 4. 在命令提示符下，输入 **apt-cache search compress | less** 并按下 **Enter** 键。ncompress 列出了吗？完成后按 **q** 退出 less 实用程序。
- 5. 在命令提示符下，输入 **apt-get install ncompress** 并按下 **Enter** 键，以从软件仓库安装 ncompress DPM 软件包。
- 6. 在命令提示符下，输入 **dpkg -l ncompress** 并按下 **Enter** 键，以列出组成 ncompress 软件包的文件。接下来，在命令提示符下输入 **dpkg -p ncompress** 并按下 **Enter** 键，以查看关于 ncompress 软件包的详细信息。
- 7. 在命令提示符下，输入 **apt-get purge ncompress** 并按下 **Enter** 键。当被提示时按下 **y**。purge 选项做什么？
- 8. 在命令提示符下，输入 **aptitude install ncompress** 并按下 **Enter** 键。此命令做什么？
- 9. 输入 **exit** 并按下 **Enter** 键，以注销你的 shell。

# 探索练习

- 1. 在你的 Fedora Linux 虚拟机上，打开 Firefox Web 浏览器并导航到 **www.sourceforge.net**。浏览可用软件，下载你选择的程序的源代码 tarball 并在你的系统上编译它。接下来，下载你选择的程序的 RPM 软件包并在你的系统上安装它。
- 2. 编写可用于执行以下操作的命令：
  - a. 使用 compress 实用程序压缩符号链接 /root/file 并显示压缩率。
  - b. 使用 gzip 实用程序压缩目录 /root/dir1 的内容并显示压缩率。
  - c. 解压文件 /root/letter.bz2。
  - d. 使用 gzip 快速压缩压缩文件 /root/letter。
  - e. 查找文件 /root/letter.gz 的压缩率。
  - f. 使用 bzip2 实用程序对文件 /root/sample 执行测试压缩。
  - g. 使用 bzip2 实用程序压缩文件 /root/sample，同时最小化压缩期间的内存使用量。
- 3. 编写可用于执行以下操作的命令：
  - a. 使用 tar 实用程序将 /var 目录（包含符号链接文件）的内容备份到系统上的第二个非回绕 SCSI 磁带设备。
  - b. 将文件 /etc/initab 追加到练习 3a 中创建的归档中。
  - c. 创建一个名为 /stuff/tar.gz 的 tarball，其中包含 /root/stuff 目录中的所有文件。

