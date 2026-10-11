
`/usr/share/doc/rsyslog-4.6.2/tls_client.html`

`/usr/share/doc/rsyslog-4.6.2/tls_certgs.html`

`/usr/share/doc/rsyslog-4.6.2/tls_machine.html`

`/usr/share/doc/rsyslog-4.6.2/tls_scenario.html`

`/usr/share/doc/rsyslog-4.6.2/tls_server.html`

`/usr/share/doc/rsyslog-4.6.2/tls_summary.html`

`/usr/share/doc/rsyslog-4.6.2/tls_udp.html`

`/usr/share/doc/rsyslog-4.6.2/troubleshoot.html`

`/usr/share/doc/rsyslog-4.6.2/v3.html`

`/usr/share/doc/rsyslog-4.6.2/v4.html`

`/usr/share/doc/rsyslog-4.6.2/version_naming.html`

早些时候，我们描述了包依赖以及你如何需要处理 `rpm` 命令。你可以使用 `-R` 选项来找出一个包是否有任何依赖：

```
# rpm -qR rsyslog
/bin/bash
/bin/sh
/bin/sh
/bin/sh
/sbin/chkconfig
/sbin/chkconfig
/sbin/service
/sbin/service
bash >= 2.0
config(rsyslog) = 4.6.2-el16
coreutils
libc.so.6 (64bit)
libc.so.6(GLIBC_2.2.5) (64bit)
libc.so.6(GLIBC_2.3) (64bit)
libc.so.6(GLIBC_2.3.4) (64bit)
libc.so.6(GLIBC_2.4) (64bit)
libdl.so.2 (64bit)
libdl.so.2(GLIBC_2.2.5) (64bit)
libgcc_s.so.1 (64bit)
libgcc_s.so.1(GCC_3.0) (64bit)
libgcc_s.so.1(GCC_3.3.1) (64bit)
libthread.so.0 (64bit)
libthread.so.0(GLIBC_2.2.5) (64bit)
```

## 命令：

- `clean` 清除缓存数据
- `erase` 从系统中删除一个包
- `grouplist` 显示可用的包组
- `groupinstall` 安装包组内的软件包
- `info` 显示软件包信息
- `install` 在系统上安装软件包
- `search` 允许你搜索软件包
- `update` 更新软件包

`Yum` 还有一个一个位于 `/etc/yum.conf` 的配置文件，其中包含了一些关于 `Yum` 行为的基本设置。这些选项包括 `Yum` 在安装软件包时在本地缓存哪些包、它将为日志文件生成什么样的输出内容，以及日志文件的位置。通常情况下，默认设置已经足够了，但你应该知道该文件的位置，以防你以后需要对 `Yum` 的设置进行调整。

## 安装和卸载软件包

让我们从获取 `postfix` 包开始。你可以直接从 `Red Hat` 仓库安装它：

```bash
# yum install -y postfix
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
* addons: mirrors.bluehost.com
* base: mirror.cisp.com
* extras: mirror.5ninesolutions.com
* updates: mirror.steadfast.net
Setting up Install Process
Resolving Dependencies
--> Running transaction check
--> Package postfix.x86_64 2:2.6.6-2.el6 set to be updated
--> Finished Dependency Resolution
```

依赖已解析

| Package | Arch | Version | Repository | Size |
|---|---|---|---|---|
| 安装中: postfix | x86_64 | 2:2.6.6-2.el6 | base | 2.0 M |

## 事务摘要

==============================================================================
Install         1 Package(s)
Update          0 Package(s)
Remove          0 Package(s)

Total download size: 2.0 M
Downloading Packages:
postfix.x86_64 2:2.6.6-2.el6.rpm      |3.6 MB      00:02
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
Installing             : postfix:2.6.6-2.el6.x64_86      1/1

Installed:
postfix.x86_64 2:2.6.6-2.el6

Complete!
你也可以更新 `postfix` 包。只需将命令从 `install` 改为 `update` 即可：

```bash
# yum update -y postfix
```

在输出中，你会看到一个在安装软件包时检查依赖项的区域。由于你现在还没有设置 `SMTP` 服务器，可以从系统中删除该软件包。和 `RPM` 工具一样，你也可以使用 `yum` 卸载软件包。然而，有两种不同的卸载选项。你可以使用 `erase` 或 `remove` 命令。区别在于，`erase` 会删除所有软件包，但会保留软件包的配置文件，以防你以后想重新安装它们。而 `remove` 命令则会删除软件包中的所有内容。

由于你现在不想留任何任何残留物，请使用 `remove`：

```bash
# yum remove -y postfix
Loaded plugins: fastestmirror
Setting up Remove Process
Resolving Dependencies
--> Running transaction check
--> Package postfix.x86_64 2:2.6.6-2.el6 set to be erased
--> Finished Dependency Resolution
```

依赖已解析
==============================================================================

# 180 Hands-on Guide to the Red Hat® Exams: RHCSA® and RHCE® Cert Guide and Lab Manual

| Package | Arch | Version | Repository | Size |
|---|---|---|---|---|
| 移除: postfix | x86_64 | 2:2.6.6-2.el6 | installed | 9.7 M |

## 事务摘要

- Install @ Package(s)
- Update @ Package(s)
- Remove 1 Package(s)

Downloading Packages:
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
Erasing : 2:postfix-2.6.6-2.el6.x86_64 1/1

Removed:
postfix.x86_64 2:2.6.6-2.el6

Complete!
`Yum` 的一个很棒的功能是，你不需要更新单个软件包，而是列出系统需要安装的所有更新：

```bash
# yum list updates
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
* addons: mirrors.bluehost.com
* base: mirror.cisp.com
* extras: mirror.5nolutions.com
* updates: mirror.speedfast.net
```
