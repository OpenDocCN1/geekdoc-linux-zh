
```
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/FakeRequest.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/ExtUtils.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Include.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Status.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/PerRun.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Options.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/RegistryNG.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/RegistryBB.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Connection.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Constants.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/File.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Leak.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Log.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/ModuleConfig.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Symbol.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Server.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Table.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/URI.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache/Util.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/mod_perl_hooks.pm
> /usr/lib/perl5/site_perl5/5.005/386-linux/mod_perl_hooks.Pl
> /usr/lib/perl5/site_perl5/5.005/386-linux/mod_perl_tuning.pod
> /usr/lib/perl5/site_perl5/5.005/386-linux/mod_perl_cvs.pod
> /usr/lib/perl5/site_perl5/5.005/386-linux/mod_perl_method_handlers.pod
> /usr/lib/perl5/site_perl5/5.005/386-linux/mod_perl_traps.pod
> /usr/lib/perl5/site_perl5/5.005/386-linux/cgi_to_mod_perl.pod
> /usr/lib/perl5/site_perl5/5.005/386-linux/Apache.pm
```

# 第 20 章与 Apache 一起安装的可选组件

## 本章内容

- Webalizer
- 配置
- 告知 Apache 关于 Webalizer 的输出目录
- 首次手动运行 Webalizer
- 使用 cron 任务自动运行 Webalizer
- FAQ-O-Matic
- 告知 Apache 关于 FAQ-O-Matic 文件的位置
- 配置您的 FAQ-O-Matic 软件
- Webmail IMP
- 设置 Webmail IMP 程序运行所需的 PHPLib
- 配置并创建 Webmail IMP SQL 数据库
- 配置您的 PHP4 `php.ini` 文件
- 配置 Apache 以识别 Webmail IMP

## 与 Apache 一起安装的可选组件

在本章中，我将介绍三个可以安装在您的 Linux 服务器上的实用外部程序。这些程序是为配合 Apache Web 服务器设计的，且只有当您在组织中使用 Apache 时它们才有用处。如果情况并非如此，您可以跳过本章并继续阅读本书的其他部分。首先，我们将讨论 Webalizer，它是一个 Web 服务器日志文件分析程序。然后我们将讨论 FAQ-Matic，当您需要在服务器上提供 FAQ 列表、错误跟踪数据库、文档等更多功能时可以使用它。最后，我们将讨论一个名为 Webmail 的非常复杂且有趣的程序，它允许您为客户提供免费邮箱账户，或以安全的方式访问并读取邮件。

# Linux Webalizer

### 概述

像 Apache 这样的 Web 服务器会将所有预定义的日志记录记录到一个文本文件中，Web 管理员可以查看并分析。该文件还可以由特殊程序进行评估，该程序可以生成图形化演示的信息，便于管理员解读。正如 Webalizer 的 README 文件解释的：这是一个 Web 服务器日志文件分析程序，可以生成 HTML 格式的统计数据以便浏览器查看。年度、每月和每小时的统计数据按站点、引用页、用户代理和国家显示，前提是您的 Web 服务器生成了组合日志文件。这些指令兼容 Unix。源路径为 `"/var/tmp"`（可以是其他路径）。安装已在 RedHat Linux 6.1 和 6.2 上测试过。超级用户账户 `"root"`。Webalizer 版本为 1.30.4。

### 软件包

- 首页：http://www.linux.net/webalizer/
- FTP 站点：您必须下载：`webalizer-1.30.4-src.tgz`

### 编译

解压 tar 包 `tar.gz`。

```bash
root@deep# cp webalizer-version-src.tgz /var/tmp/
root@deep# cd /var/tmp/
root@deep# tar xzvf webalizer-version-src
```

### 前提

Webalizer 需要 GD 库来生成内联图形，如果系统中未安装，必须从 RedHat CD-ROM 安装。

- 使用以下命令验证 Linux 系统是否安装了 GD 包：

```bash
root@deep# rpm -qi gd
```

- 使用以下命令在 Linux 系统上安装 GD 包：

```bash
root@deep# mount /mnt/cdrom
root@deep# cd /mnt/cdrom/RedHat/RPMS/
root@deep# rpm -Uvh gd-i386.rpm
root@deep# rpm -Uvh gd-devel-i386.rpm
root@deep# cd /
```

- 系统中应该已经安装了 Apache Web 服务器。关于 Apache 服务器的更多信息，请参本书中的相关章节。

### 编译

进入新的 Webalizer 目录并在终端输入以下命令：

```bash
CC="gcc"
CFLAGS="-O3 -ffno-loops -fast-math -malign-debug -mcpu=pentium -march=pentium -fomit-frame-pointer -fno-exceptions"
./configure --prefix=/usr
```

```bash
root@deep webalizer-1.30.4# make
root@deep webalizer-1.30.4# make install
root@deep webalizer-1.30.4# mkdir /home/httpd/usage
```

`make` 命令将所有源文件编译为可执行的二进制文件，`make install` 将二进制文件和任何支持文件安装到适当的位置。`mkdir` 将 `/home/httpd/` 目录下创建一个名为 `usage` 的新目录，我们将处理所有的 Webalizer 文件。

### 清理

```bash
root@deep# cd /var/tmp
root@deep# rm -rf webalizer-version/ webalizer-src.tgz
```

`rm` 命令将删除我们编译和安装 Webalizer 使用的所有源文件。它还会删除 `/var/tmp/` 目录下的压缩包 Webalizer。

### 配置
