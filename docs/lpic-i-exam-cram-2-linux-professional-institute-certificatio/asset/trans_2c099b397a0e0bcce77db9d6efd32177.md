

如果软件包是通过 `-u` 选项进行升级的，一套复杂的算法将发挥作用，以确保配置被正确应用。

## 查询软件包

查询软件包数据只是管理软件包过程中的一步，尽管在所有 RPM 执行的任务中，它可能拥有最多的选项。

理解已安装在系统上的软件包（显示在 RPM 数据库中）与仅作为磁盘或其他资源上文件存在的软件包之间的区别非常重要。rpm 命令使用上的主要区别在于添加 `-p` 选项，以指定要操作的软件包是磁盘上的一个文件。

最基本的查询是返回特定软件包是否在系统上的输出：

```
rpm -q krbafs
```

这将返回如下所示的输出：

```
krbafs-1.1.1-1
```

只需在此查询中添加几个修饰字符，你就可以获取有关任何软件包的更多信息。我通常建议使用的第一个修饰符是获取软件包信息：

```
rpm -qi krbafs
```

这将返回以下输出：

```
Name     : krbafs                  Relocations: (not relocatable)
Version    : 1.1.1                   Vendor: Red Hat, Inc.
Release    : 1
--Build Date: Tue 05 Mar 2002 05:00:20 PM EST
Install date: Wed 13 Aug 2003 10:30:50 AM EDT
--Build Host: porky.devel.redhat.com
Group    : System Environment/Libraries
--Source RPM: krbafs-1.1.1-1.src.rpm
Size     : 46832
--License: Freely Distributable
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary    : A Kerberos to AFS bridging library, built against Kerberos 5.
Description : This package contains the krbafs shared library, which allows programs to obtain AFS network filesystem tokens using Kerberos IV credentials, without having to link with official AFS libraries which may not be available for a given platform.
```

要获取软件包文件的信息，同时使用 `-q`（查询）选项和 `-l`（文件列表）选项：

```
rpm -ql krbafs
```

这返回

```
/etc/krb.conf
/etc/krb.realms
/usr/kerberos/lib/libkrbafs.so.0.0.0
/usr/share/doc/krbafs-1.1.1
/usr/share/doc/krbafs-1.1.1/COPYRIGHT
/usr/share/doc/krbafs-1.1.1/ChangeLog
```

![](img/49f4f38f3aec011238fa50f89e643db3_284_0.png)

当你遇到关于列出软件包文件或信息的问题时，请记住列出数据库中软件包内容和对磁盘上软件包执行相同操作之间的区别：
- `rpm -qil` package_name—用于已安装的软件包
- `rpm -qilp` package_name—用于未安装的软件包

此外，请记住，只要所有选项都存在，你可以以任何顺序指定这些选项。实际上，**rpm -qilp**、**rpm -qlip** 和 **rpm -pliq** 都能正常工作。

要查看软件包的修订历史或变更日志，请使用此命令：

```
rpm -q --changelog krbafs
```

这将返回以下输出（为了可读性进行了截断）：

+ * Fri Mar 01 2002 Nalin Dahyabhai <nalin@redhat.com> 1.1.1-1
+   - update to 1.1.1
+   - build shared only, and use a map file to only export symbols from the shared library which are declared in the header

+ * Fri Feb 22 2002 Nalin Dahyabhai <nalin@redhat.com> 1.1-4
+   - rebuild

此输出类似于大多数软件包源代码库中找到的 CHANGELOG、REVISIONS 或 RELEASES 文件，这些文件描述了软件包变更的历史。

![](img/49f4f38f3aec011238fa50f89e643db3_284_1.png)

这是 LPI 喜欢放在考试中的那种内容。如果你从未如此深度使用过 rpm，这些题目可能会让你头疼。别忘了必须一起使用 **-q** 和 **--changelog** 选项；否则，你会得到语法错误。

要找到软件包的所有配置文件，使用查询和配置选项，如下所示：

```
rpm -qc sendmail
```

这返回

```
/etc/aliases
/etc/mail/Makefile
/etc/mail/access
/etc/mail/domainstable
/etc/mail/helpfile
/etc/mail/local-host-names
/etc/mail/mailetable
/etc/mail/sendmail.mc
/etc/mail/statistics
/etc/mail/trusted-users
/etc/mail/virtusertable
/etc/rc.d/init.d/sendmail
/etc/sendmail.cf
/etc/sysconfig/sendmail
/usr/lib/sasl/Sendmail.conf
```

> 记住，这只显示配置文件，而不是软件包内容的其余部分——内容通过 -ql 选项显示。

要查看给定软件包需要哪些其他功能或软件包，使用 --requires 或 -R 选项（记住它是一个磁盘上的软件包，所以使用 -p），如下所示：

```
rpm -qRp tree-1.2-7.i386.rpm
```

这返回此处显示的输出：

```
1d-linux.so.2
libbc.so.6
libbc.so.6(GLIBC_2.0)
```

> 如果系统不提供这些功能，你可能会进入一个下载和依赖解析的过程。查看 http://www.rpmfind.net 和 http://freshrpms.net 以获取搜索引擎和帮助。

如果你不记得软件包的名称怎么办？使用 rpm 命令的输出和 grep 过滤掉你不需要的内容，如下所示：

```
rpm -qa | grep string
```

那么，如何找到安装特定文件的软件包？例如，如果 /etc/krb.conf 文件以某种方式损坏，你可以用此命令找到它来自哪个软件包：

```
rpm -qf /etc/krb.conf
```

这返回以下输出：

```
krbafs-1.1.1-1
```

**警报**

使用 -f 选项需要被查询文件的完整路径和文件名。这就是它在从数据库查询的软件包信息中的列表方式。如果在回答填空题时未包含被查询文件的完整路径，答案将被判为错误。

## 构建 RPMs

对于考试过程而言，构建 RPMs 只需要理解一套步骤。实际的构建 RPMs 过程可能比这里看到的要复杂得多。

系统管理员使用源代码 RPM 并构建自定义 RPM，以获得更好的性能、保证 RPM 文件中的内容、环境的安全性、机器的完整性以及许多其他原因。

一个目录树构成了构建环境，可以在 `/usr/src/redhat` 目录中作为子目录找到。这些包括
- **BUILD** -- 这是软件包的源代码解压缩并构建软件的地方。
- **RPMs** -- 由构建过程创建的二进制软件包文件将写入此目录。
- **SOURCES** -- 这里包含源代码软件包、任何补丁和修复。
- **SPECS** -- 这里是保存 .spec 文件（本质上是美化的 Makefile）并从此启动构建的地方。
- **SRPMS** -- 这是存储由构建过程生成的任何源代码软件包的地方。

### 构建中发生了什么？

第一步是下载源代码 .rpm 或压缩代码的 tarball。两者的步骤相同，除了源代码 tarball 必须构建一个 .spec 文件，而源代码 .rpm 包含了所有这些。

如果是源代码 .rpm，你安装 .rpm 文件（`rpm -i source_pkg.rpm`），这将把源文件放置在 /usr/src/redhat/SOURCES 目录中，把 spec 文件放置在 /usr/src/redhat/SPECS 目录中。

然后你编辑 /usr/src/redhat/SPECS/somepkg.spec 文件以进行所需的任何更改。.spec 文件由一组信息和宏、要包含的文件的路径以及软件包作为 .rpm 文件安装时的安装说明组成。

这里有一个 .spec 文件的示例：

```
# Preamble of spec file
Summary: a special program to do something.
Name: blah-woof
Version: 0.99
Release: 33
Copyright: GPL
Group: Applications/Special
Source: ftp://ftp.brunson.org/blahwoof.tar.gz
BuildRoot: /var/tmp/blahwoof-root

description
Blah-woof is the greatest program it does everything and nothing

prep
rm -rf $RPM_BUILD_DIR/blah-woof-1.0
tar xzf $RPM_SOURCE_DIR/blah-woof-1.0.tar.gz

build
make

install
rm -rf $RPM_BUILD_ROOT
mkdir -p $RPM_BUILD_ROOT/usr/{bin,man/man1}
make DESTDIR=$RPM_BUILD_ROOT install

clean
rm -rf $RPM_BUILD_ROOT

files

doc README
/usr/bin/blah-woof
/usr/bin/blah.inc
/usr/man/man1/blah-woof

changelog
* Wed 10th of Nov. Some developer <some@uy.int>
- fixed tendency to crash unexpectedly
```

对于用于安装软件包的文件，它必须包含以下部分：
- Preamble—摘要和其他显示在软件包信息页查询中的信息。
- description—这只是一个描述。
- prep—这是源代码 tarball 被解包并处理到构建目录的地方（包括应用的任何补丁）。
- build—这是实际构建软件的地方，通常使用 make 命令，就像普通软件一样。
- install—构成源文件安装的说明，通常是 make install。

