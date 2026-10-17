
```sh
$ showrpms.sh | head
redhat-logos-1.1.3-1: Red Hat-related icons and pictures.
glibc-2.2.4-13: The GNU libc libraries.
cracklib-2.7-12: A password-checking library.
dosfstools-2.7-1: Utilities for making and checking MS-DOS FAT filesystems on Linux.
gdbm-1.8.0-10: A GNU set of database routines which use extensible hashing.
ksymoops-2.4.1-1: Kernel oops and error message decoder
mktemp-1.5-11: A small utility for safely making /tmp files.
perl-5.6.0-17: The Perl programming language.
setserial-2.17-4: A utility for configuring serial ports.
netconfig-0.8.11-7: A text-based tool for simple configuration of ethernet devices.
```

一个更具吸引力且对系统管理员更友好的输出！

![](img/5ced0c78d748bd190e9027e5549a3622_180_0.png)

> 实际上，如果你深入研究，可以让 RPM 以这种格式输出信息。有一个命令选项 `--queryformat`，允许你指定要呈现的确切信息以及其形式。如果你使用

```bash
rpm -qa --queryformat '%{NAME}: %{SUMMARY}\n'
```

你的输出将与 `showrpms` 脚本相同。

### 4. 现在我们可以更有效地搜索，例如查看安装了哪些命令行 shell：

```
$ showrpms.sh | grep -i shell
sharutils-4.2.1-8: The GNU shar utilities for packaging and unpackaging shell archives.
mc-4.5.51-80: A user-friendly file manager and visual shell.
docbook-utils-0.6.9-2: Shell scripts for managing DocBook documents.
bash-2.05-8: The GNU Bourne Again shell (bash) version 2.05.
ash-0.3.7-2: A smaller version of the Bourne shell (sh).
tcsh-6.10-6: An enhanced version of csh, the C shell.
sh-utils-2.0.11-5: A set of GNU utilities commonly used in shell scripts.
```

RPM 软件包是在系统上管理软件包的强大方式，但当你可以从互联网获取不同的软件包并轻松扩展系统的功能时，它才真正令人兴奋！

#### 从互联网添加新的 RPM 软件包

`rpm` 命令本身没有能力访问网络存档并搜索可用软件包，因此你需要打开图形 Web 浏览器（也许是流行的 Linux 浏览器 Konqueror）并四处查看一下。

##### 任务 8.2：安装新的基于 Web 的 RPM 软件包

要在系统上安装新软件包，你需要探索网络并确定所需的特定软件包。

> 开始搜索 RPM 软件包的一个好地方是 Pbone 网站 http://rpm.pbone.net/。你也可以通过访问 http://www.rpm.org/ 来确保你拥有最新版本的 RPM。

1. 因为网络并不总是可用，我喜欢在自己的系统上保留相关文档的副本以备备份。我访问了 Pbone 并了解到优秀的 Linux FAQ 集合可作为名为 `faq-7.2.1.noarch.rpm` 的 RPM 软件包提供。网站上还列出了世界各地各种服务器上的特定软件包的完整 URL。

我将从俄克拉荷马大学选择一个链接，并使用 `-i` 安装、`-v` 获取更详细的输出以及 `-h` 在文件下载时显示一系列哈希标记将其提供给 RPM 软件包：

```bash
# rpm -ivh ftp://ftp.ou.edu/mirrors/linux/redhat/redhat-7.2-en/doc/RedHat/RPMS/faq-7.2.1.noarch.rpm
Retrieving ftp://ftp.ou.edu/mirrors/linux/redhat/redhat-7.2-en/doc/RedHat/RPMS/faq-7.2.1.noarch.rpm
Preparing...
######################################## [100%]
1:faq ######################################## [100%]
```

2. 看起来安装得很顺利。让我们使用 `-qi` 标志再次确认：

```bash
# rpm -qi faq
Name        : faq                     Relocations: (not relocatable)
Version     : 7.2                     Vendor: Red Hat, Inc.
Release     : 1                       Build Date: Thu 30 Aug 2001
Install Date: Sat 26 Jan 2002 11:31:11 AM PST   Build Host: strippies.devel.redhat.com
Group       : Documentation           Source RPM: faq-7.2.1.src.rpm
Size        : 1596478                 License: distributable
Packager    : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary     : Frequently Asked Questions (FAQ) about Linux.
Description :
The faq package includes the text of the Frequently Asked
Questions (FAQ) about Linux from
http://metalab.unc.edu/pub/Linux/docs/faqs/. These FAQs are a great source
of information (sometimes historical) about Linux.
```

如果你想在自己的机器上阅读 Linux FAQ，请安装 `faq` 软件包。

RPM 还有一个有用的标志，可以显示软件包安装的所有文件的确切名称——`-l` 标志：

```bash
# rpm -ql faq | wc -l
121
```

你可以看到，通过这个简单的 `rpm` 安装安装了超过 120 个文件。要预览一下，让我们使用 `head`：

```bash
# rpm -ql faq | head -20
/etc/X11/applnk/Documentation
/etc/X11/applnk/Documentation/Linux Community
/etc/X11/applnk/Documentation/Linux Community/faq.desktop
/usr/share/doc/FAQ
/usr/share/doc/FAQ/html
/usr/share/doc/FAQ/html/AfterStep-FAQ
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-1.html
```
