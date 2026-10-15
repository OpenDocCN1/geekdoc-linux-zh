
- Dan Nicholson <dnicholson@linuxfromscratch.org> – LFS 和 BLFS 编辑
- Alexander E. Patrakov – LFS 技术写作者、LFS 国际化编辑器、LFS Live CD 维护者
- Simon Perrault
- Scot McPherson <scot@linuxfromscratch.org> – LFS NNTP 网关维护者
- Douglas R. Reno <renodr@linuxfromscratch.org> – Systemd 编辑器
- Ryan Oliver <ryan@linuxfromscratch.org> – CLFS 项目共同负责人
- Greg Schaffer <gschafer@zip.com.au> – LFS 技术写作者和下一代64位启用构建方法
- Jesse Tie-Ten-Queue – LFS 技术写作者
- James Robertson <jwrober@linuxfromscratch.org> – Bugzilla 维护者
- Tushar Teredesai <tushar@linuxfromscratch.org> – BLFS 书编辑器、提示与补丁项目负责人
- Jeremy Utley <jeremy@linuxfromscratch.org> – LFS 技术写作者、Bugzilla 维护者、LFS-Bootscripts 维护者
- Zack Winkles <zwinkles@gmail.com> – LFS 技术写作者

# 附录 C 依赖关系

LFS 构建的每个软件包都依赖一个或多个软件包才能正确构建和安装。某些软件包存在循环依赖，即第一个包依赖第二个包，而第二个包又依赖第一个包。由于这些依赖关系，在 LFS 中构建软件包的顺序非常重要。本页面的目的是记录 LFS 中构建的每个软件包的依赖关系。

对于每个构建的软件包，下面列出了三种（有时多达五种）类型的依赖。第一类列出了编译和安装该软件包需要提供的其他软件包。第二类列出了在运行时使用该软件包的任何程序或库时必须提供的软件包。第三类列出了除第一类中的包外，运行测试套件还需要提供的软件包。最后一类依赖列表是指这些软件包在构建和安装之前，要求该软件包在其最终位置完成构建和安装。某些情况下，这是因为这些软件包将硬编码二进制文件的路径。如果不按照顺序构建，可能会导致安装到最终系统的脚本中包含 `/tools/bin/[binary]` 的路径。这显然不是所愿的。

最后一类依赖列表是 LFS 未涉及但对用户可能有用的可选软件包。这些软件包可能有它们自己的额外的强制性或可选依赖关系。对于这些依赖关系，推荐的做法是在完成 LFS 手籍后安装它们，然后返回重新构建 LFS 软件包。在某些情况下，BLFS 会处理重安装问题。

### Acl
- **安装依赖于：** Attr, Bash, Binutils, Coreutils, GCC, Getext, Grep, M4, Make, Perl, Sed 和 Texinfo
- **运行时需要：** Attr 和 Glibc
- **测试套件依赖于：** Automake, Diffutils, Findutils, 和 Libtool
- **必须先安装：** Coreutils, Sed, Tar 和 Vim
- **可选依赖：** 无

### Attr
- **安装依赖于：** Bash, Binutils, Coreutils, GCC, Glibc, Grep, M4, Make, Perl, Sed 和 Texinfo
- **运行时需要：** Attr 和 Glibc
- **测试套件依赖于：** Automake, Diffutils, Findutils, 和 Libtool
- **必须先安装：** Acl 和 Libcap
- **可选依赖：** 无

### Autoconf
- **安装依赖于：** Bash, Coreutils, Grep, M4, Make, Perl, Sed 和 Texinfo
- **运行时需要：** Bash, Coreutils, Grep, M4, Make, Sed 和 Texinfo
- **测试套件除第一类外还需要：** Automake, Diffutils, Findutils, GCC, 和 Libtool
- **必须先安装：** Automake
- **可选依赖：** Emacs

## Linux From Scratch - Version 11

### Automake
安装依赖于：Autoconf, Bash, Coreutils, Gettext, Grep, M4, Perl, Sed, 和 Texinfo
运行时需要：Bash, Coreutils, Grep, M4, 和 Texinfo
测试套件依赖于：Binutils, Bison, Bzip2, DejaGNU, Diffutils, Expect, Findutils, Flex, GCC, Gettext, Gzip, Libtool, 和 Tar
必须安装之前：无
可选依赖：无

### Bash
安装依赖于：Bash, Binutils, Bison, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, Make, Ncurses, Patch, Readline, 和 Texinfo
运行时需要：Glib, Ncurses, 和 Readline
测试套件依赖于：Expect 和 Shadow
必须安装之前：无
可选依赖：Xorg

### Bc
安装依赖于：Bash, Binutils, Coreutils, GCC, Glibc, Grep, Make, 和 Readline
运行时需要：Glib, Ncurses, 和 Readline
测试套件依赖于：Gawk
必须安装之前：Linux
可选依赖：无

### Binutils
安装依赖于：Bash, Binutils, Coreutils, Diffutils, File, Flex, Gawk, GCC, Glibc, Grep, Make, Perl, Sed, Texinfo, 和 Zlib
运行时需要：Glib 和 Zlib
测试套件依赖于：DejaGNU 和 Expect
必须安装之前：无
可选依赖：Elfutils 和 Jansson

### Bison
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Grep, M4, Perl, 和 Sed
运行时需要：Glib
测试套件依赖于：Diffutils, Findutils, 和 Flex
必须安装之前：Kbd 和 Tar
可选依赖：Doxygen

### Bzip2
安装依赖于：Bash, Binutils, Coreutils, Diffutils, GCC, Make, 和 Patch
运行时需要：Glib
测试套件依赖于：无
必须安装之前：File
可选依赖：无

### Check
安装依赖于：Gawk, GCC, Grep, Make, Sed, 和 Texinfo
运行时需要：Bash 和 Gawk
测试套件依赖于：无
必须安装之前：无
可选依赖：无

### Coreutils
安装依赖于：Bash, Binutils, Coreutils, GCC, Gettext, Glibc, GMP, Grep, Libcap, OpenSSL, Patch, Perl, Sed, 和 Texinfo
运行时需要：Glibc
测试套件依赖于：Diffutils, E2fsprogs, Findutils, Shadow, 和 Util-linux
必须安装之前：Bash, Diffutils, Eudev, Findutils, 和 Man-DB
可选依赖：Expect.pm 和 io::Ty

### DejaGNU
安装依赖于：Bash, Coreutils, Diffutils, Expect, GCC, Grep, Make, Sed, 和 Texinfo
运行时需要：Expect 和 Bash
测试套件依赖于：无
必须安装之前：无
可选依赖：无

### Diffutils
安装依赖于：Bash, Binutils, Coreutils, Gawk, GCC, Gettext, Glibc, Grep, Make, Sed, 和 Texinfo
运行时需要：Glibc
测试套件依赖于：Perl
必须安装之前：无
可选依赖：无

### E2fsprogs
安装依赖于：Bash, Binutils, Coreutils, Diffutils, Gawk, GCC, Glibc, Grep, Gzip, Make, Texinfo, 和 Util-linux
运行时需要：Glibc 和 Util-linux
测试套件依赖于：Procs-ng 和 Pmisc
必须安装之前：无
可选依赖：无

### Eudev
