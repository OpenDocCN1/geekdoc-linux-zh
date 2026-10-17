
下载文件后，用户尝试将 `joe` 移动到 `/usr/local/bin` 并收到错误，用户使用 `su` 命令变成超级用户并获得移动文件的权限。一旦文件移动，用户使用 `chmod` 建立访问权限，现在系统上的任何人都应该可以使用 `joe`。

## 获取、构建并安装软件？

无论你对你的 Linux 系统有多满意，早晚你都会想要安装或升级软件包。安装软件包的步骤由该软件包的创建者决定，不同软件包之间差异很大。参考第 918 页关于下载和安装 `joe` 编辑器的说明，这是一个相对简单的过程。虽然没有标准的软件包安装方法，但有一些常用的技术。第 922 到 926 页的讨论引导你安装特定的软件包——Shell——但其目的是向你展示如何安装任何使用类似过程的软件包。此外，还帮助。

安装一个新的软件包或现有软件的新版本需要获取软件的副本。获取 Linux 软件的一种方法是从互联网获取发行包。使用 `ftp` 工具连接到拥有发行包的远程站点并传输副本。

了解软件包的一种方法是通过新闻组的消息。如果你足够，读取器可以使用消息中的 HTML 链接为你下载软件。如果没有，读取器将定位软件包并自动使用 `ftp`。

示例中，Jenny 下载并安装了新发布的 Shell 版本 `3.0.0`。她的第一步连接到托管 `zsh` 的站点之一并使用 `ftp` 下载软件。大多数软件发行包由一个 `tar` 归档组成并用 `gzip` 压缩以节省磁盘空间和传输时间。此类文件通常具有 `.tar.gz` 或 `.tgz` 扩展名。

某些软件发行者提供源码版本和预编译版本。虽然编译发行包通常是一个复杂且耗时的过程，但如果你的 Linux 系统有二进制版本，安装会更容易。大多数软件包和少数免费软件包仅以二进制版本提供。

Jenny 必须连接 `uarchive.co.uuc.edu` 站点。她使用 `cd` 创建工作目录 `/usr/local/src/incoming`——下载软件的目录——并使用 `ftp` 命令连接远程站点。一旦作为匿名用户 `ftp` 登录，她使用电子邮件地址作为密码，进入存放 `zsh` 发版的目录并列出该目录的内容。

```
cd /usr/local/src/incoming

ftp uarchive.co.uuc.edu

连接到 uarchive.co.uuc.edu.

220 uarchive.co.uuc.edu FTP server (Version-2.0.4) 2004年6月15日 17:42:40 (UTC)

Name(uarchive.co.uuc.edu): ftp

Password:(uarchive.co.uuc.edu):

331 登录成功，请发送您的电子邮件地址作为密码。

230 登录成功，已应用访问限制。

远程系统是 Unix。

使用二进制模式传输文件。

ftp cd pub/packages/shells/zsh

530 OK

200 PORT 命令成功。

150 正在为 /bin/ls 打开 ASCII 模式数据连接。

共 8384

-rw-r--r 1 ftppadmin ftppadmin 59652 8月15日 22:23 zsh-3.0.0.tar.gz

-rw-r--r 1 ftppadmin ftppadmin 1466 8月15日 22:54 MDSSUM

-rw-r--r 1 ftppadmin ftppadmin 3139 8月23日 02:52 META-TAG

-rw-r--r 1 ftppadmin ftppadmin 4653 9月4日 00:06 META-TAG.html

-rw-r--r 1 ftppadmin ftppadmin 1195 8月15日 23:29 README

-rw-r--r 1 ftppadmin ftppadmin 628435 8月15日 22:43 zsh-3.0.0.tar.gz

-rw-r--r 1 ftppadmin ftppadmin 1327843 8月15日 22:44 zsh-RCS.tar.gz

-rw-r--r 1 ftppadmin ftppadmin 730962 8月15日 22:06 zsh-doc.tar.gz

-rw-r--r 1 ftppadmin ftppadmin 736 8月16日 12:38 zsh.tar.gz -> zsh-3.0.0.tar.gz
```

## 附录 B：帮助！

### 6. 如何从互联网下载软件？

要安装一个新的软件包或你已有的软件的新版本，需要获取软件的副本。获取 Linux 软件的一种方法是从互联网获取发行包。使用 `ftp` 工具连接到有发行包的远程站点并传输副本到你的机器。

## 如何安装软件代码？

文件 `zsh.tar.gz` 是 Jenny 感兴趣的文件 `zsh-3.0.0.tar.gz` 的符号链接。这是开发者通常提供的一种便利措施；它不仅为包提供了一个更短的名字，还允许在开发新版本时通过单一名称来识别该包。

Jenny 使用 `ftp` 二进制命令来确保文件以二进制模式下载。虽然某些远程系统会自动执行，但即使传输的仅是 ASCII 文件，使用二进制命令也无无处。

```
ftp> binary

200 Type set to I.

ft> get zsh.tar.gz

200 PORT command successful.

150 Opening BINARY mode connection for zsh.tar.gz (62843 bytes).

226 Transfer complete.

62843 bytes received in 2.9e+02 seconds (2.2 Kbytes/s)

ft> quit

221 Goodbye.
```

### 7. 如何安装软件源码？

下载完发行包——单个压缩的 tar 存档文件 `zsh.tar.gz` 后，Jenny `cd` 到 `/usr/local/src/zsh` 目录构建源码。她将 tar 存档移动到 `/usr/local/src/zsh` 并将文件提取到该目录。

```
$ cd /usr/local/src/zsh

$ mv ~/usr/src/incoming/zsh.tar.gz .

$ ls -l

-rw-r--r-- 1 Jenny group 62843 bytes Sep 6 19:48 zsh-3.0.0

$ tar -xpf zsh.tar.gz

$ ls -l

drwxr-xr-x 9 Jenny group 1024 Sep 6 19:52 zsh-3.0.0

-rw-r--r-- 1 Jenny group 62843 bytes Sep 6 19:48 zsh-3.0.0
```

此发行包在此处创建了 `zsh-3.0.0` 子目录以及所有提取出的文件：

| $ ls zsh-3.0.0 | META-FA | Startfiles | mkinstalldirs |
| --- | --- | --- | --- |
| Changel | Makefile.in | config.h | stamp-h.in |
| Doc | Util | config.sub | |
| Misc | aaconfig.h | configure | | |
| Etc | aclocal.md | configure.in | | |
| Functions | RE | | | |
| INSTALL | Src | config.guess | install-sh | |

#### 注意

某些包会将文件直接安装到工作目录，如果那里已存在这些文件，可能会导致问题。某些二进制发行版期望你在从包中提取后在根目录下运行。查看发行包前几个文件的路径将为你提供足够的信息来采取适当行动。

```
$ tar -xvf zsh.tar.gz | head -4

-rw-r--r-- hzl/operator 91864 Aug 15 10:30 1996 zsh-3.0.0/Changelog

-rw-r--r-- hzl/operator 4878 Jul 31 11:43 1996 Makefile.in

-rw-r--r-- hzl/operator 910 May 06:08 1996 ans12kr.man

-rw-r--r-- hzl/operator 85799 Jul 1 10:10 1996 zsh-3.0.0/doc/Intro.ms
```

### 8. 如何构建软件？

在开始构建软件之前，请阅读说明。人们在安装软件时遇到的大多数问题源于没有阅读所有说明或没有仔细遵守说明。大多数包都带有一个你应该先阅读的文件，通常命名为 `README`。之前 `zsh-3.0.0` 的列表显示有一个名为 `README` 的文件。该文件包含了关于 FAQ、`zsh`、文档等的有用信息。“Installing zsh”部分对此时的 Jenny 来说特别感兴趣。它的第一段指示 Jenny 阅读 `INSTALL` 和 `Etc/MACHINES` 行：

编译 `zsh` 的说明在 `INSTALL` 文件中。你还应该检查 `Etc` 子目录下的 `MACHINES` 文件，以查看是否有针对你特定架构的特殊说明。

Jenny 阅读了 `Etc/MACHINES` 文件中与 Linux 架构相关的信息，并学会了如果在配置软件期间报告系统列表不存在时该怎么办。她还了解到必须有一个指向 `/proc/self/fd` 的符号链接 `/dev/fd`。Jenny 给了以下命令来检查符号链接是否存在：

```
$ ls -l /dev/fd

lrwxrwxrwx 1 root 13 Sep 7 12:52 /dev/fd -> /proc/self/fd
```

像许多软件包一样，`zsh` 使用 GNU `configure` 来查看你的系统并确定那里发现的能力和特性。运行 `configure` 的说明在 `INSTALL` 文件中。接下来 Jenny 运行 `configure` 为编译 `zsh` 做准备。`INSTALL` 中的说明已经向 Jenny 展示了如何带上新的 `CFLAGS` 变量来调用 `configure`。

```
$ CFLAGS="-O3 -m486" ./configure

creating ..config.cache

configuring for zsh 3.0.0

checking host system... i486-unknown

checking for gcc ...

checking whether we using GNU C...

checking for traditional... no

checking how to run the C preprocessor... -E

checking for working... no

checking whether cross-compiling... no

checking for gcc

checking option to accept ANSI C...

checking for function prototypes... yes

checking size of long... 4

checking for lstat... yes

checking if echo in /bin/sh interprets sequences... no

updating ..config.cache

creating ..config.status

creating Makefile

creating Src/Makefile

creating Doc/Makefile

creating Misc/Makefile

creating Util/Makefile
```

### 9. 如何安装编译好的软件？

许多包包含了你在安装之前可以运行的测试。进行这些测试的信息在随软件提供的说明中。如果你正在覆盖旧版本的程序，先备份旧版本是个好主意。在构建 `zsh` 时没有问题。

```
$ su

Password: # make install

cd src && make cc -gcc 'CPPFLAGS=-' DEFS='-DHAVE_CONFIG_H'

CFLAGS='-m486 -DCPPFLAGS=-' LIBS='-Llocal' prefix='/usr/local'

exec_prefix='/usr/local' bindir='/usr/local/bin'

infodir='/usr/local/info' mandir='/usr/local/man' manext='1' install.bin

make[1]: Entering directory /usr/local/src/zsh/zsh-3.0.0/Src

../instaldirs /usr/local/man

if [ -f /usr/local/bin/zsh ]; then mv /usr/local/bin/zsh /usr/local/bin/zsh

/usr/local/install -cp sh /usr/local/bin

if [ -f /usr/local/bin/zsh-3.0.0 ]; then rm -f

/usr/local/bin/zsh

make[1]: Leaving directory /usr/local/src/zsh/zsh-3.0.0/Src

cd doc && make cc -gcc 'CPPFLAGS=-' DEFS='-DHAVE_CONFIG_H'

CFLAGS='-m486 -DCPPFLAGS=-' LIBS='-Llocal' prefix='/usr/local'

exec_prefix='/usr/local' bindir='/usr/local/bin'

infodir='/usr/local/info' mandir='/usr/local/man' manext='1'

make[1]: Entering directory /usr/local/src/zsh/zsh-3.0.0/Doc

../instaldirs /usr/local/man

for f in zsh zcomp1.1 zshpen.1 zshmisc.1; do

/usr/bin/ginstall $f /usr/local/man \

done

make[1]: Leaving directory /usr/local/src/zsh/zsh-3.0.0/Doc

cd doc && make cc -gcc 'CPPFLAGS=-' DEFS='-DHAVE_CONFIG_H'

CFLAGS='-m486 -DCPPFLAGS=-' LIBS='-Llocal' prefix='/usr/local'

exec_prefix='/usr/local' bindir='/usr/local/bin'

infodir='/usr/local/info' mandir='/usr/local/man' manext='1'

make[1]: Entering directory /usr/local/src/zsh/zsh-3.0.0/Doc

../instaldirs /usr/local/info

for file in zsh.info zsh.info[-9]; do \

[ -f "$file" ] && /usr/bin/ginstall -c m 644 $file /usr/local/info ; \

done

make[1]: Leaving directory /usr/local/src/zsh/zsh-3.0.0/Doc
```

## 附录 B：帮助！

`configure` 工具报告此版本的 Linux 有系统调用，所以 Jenny 不想担心这个软件问题。X Window 系统的软件通常使用不同的源码配置方法发布。这些包没有提供 GNU `configure` 工具，而是使用 `make`。使用 `make` 的包的说明通常指示你使用 `make` 来配置软件。运行 `configure` 配置软件后，Jenny 可以通过运行 `make` 构建 `zsh`。再次，她遵循 `INSTALL` 文件中设置的程序。保存编译过程中 `make` 的输出是个好主意。Jenny 将标准输出和错误输出重定向到一个文件，然后重定向 `-f` 以查看编译进度。

```
$ make.out 2>&1

$ tail -f make.out

cd src && make CC='gcc' CPPFLAGS='' DEFS='-DHAVE_CONFIG_H'

CFLAGS='-m486' LDFLAGS='-L/termcap' prefix='/usr/local'

exec_prefix='/usr/local' bindir='/usr/local/bin'

indirir='/usr/local' mandir='/usr/local/man' manext='1'

make[1]: Entering directory /usr/local/src/zsh/zsh-3.0.0/Src

sed -n f /makepro.sed builtin.c > builtin.c
```
sed -n f /makepro.sed builtin.c > builtin.c
gawk -f /.signatures.as /usr/include/asm/signal.h > signatures.h
gcc -c -I. -I -DHAVE_CONFIG_H -03 -m486 builtin.c
```

make[1]: Entering directory /usr/local/src/zsh/zsh-3.0.0/Misc

make[1]: Nothing to be done for 'all'

make[1]: Leaving directory /usr/local/src/zsh/zsh-3.0.0/Misc
