

# 使用 YUM 安装和更新软件包

# 目标

完成本节内容后，你将能够使用 `yum` 命令查找、安装和更新软件软件包。

# 使用 YUM 管理软件包

低层级 `rpm` 命令可以用于安装软件包，但它设计时并非为了处理依赖关系，也不会自动从多个源解析依赖关系。

`yum` 设计用于一个更优的系统来管理基于 RPM 的软件安装和更新。`yum` 命令允许你安装、更新、删除以及获取软件软件包及其依赖项的信息。你可以获取执行过的事务历史，并与多个 Red Hat 和第三方仓库一起工作。

## 使用 Yum 查找软件

- `yum help` 显示用法信息。
- `yum list` 显示已安装和可用的软件包。

```
[]$ yum list 'http'
Available Packages
http-parser.1686             2.8.0-el8                   rhel8-appstream
http-parser.x86_64           2.8.0-el8                   rhel8-appstream
httpcomponents-client.noarch  4.5.10-module+el8+2452+b359bfcd  rhel8-appstream
httpcomponents-core.noarch   4.4.37-module+el8+2443+b359bfcd  rhel8-appstream
httpd.x86_64                2.4.37-module+el8+2443+60547b7   rhel8-appstream
httpd-devel.noarch           2.4.37-module+el8+2443+60547b7   rhel8-appstream
httpd-filesystem.noarch       2.4.37-module+el8+2443+60547b7   rhel8-appstream
httpd-manual.noarch           2.4.37-module+el8+2443+60547b7   rhel8-appstream
httpd-tools.x86_64            2.4.37-module+el8+2443+60547b7   rhel8-appstream
```

- `yum search KEY` 仅通过名称（name）和摘要（summary）字段中找到关键词列出软件包。

要查找名称、摘要和描述字段中包含“server”的软件包，请使用 `search all`：

```
[]$ yum search all 'web server'
==================== Name & Description Matched: web server ==================
cp-pmda-weblog.x86_64         Performance Co-Pilot (PCP) metrics from web server logs
nginx.x86_64                 A high performance web server and reverse proxy server
==================== Summary Matched: web server ==================
libcurl.x86_64                A library for getting files from web servers
libcurl.1686                  A library for getting files from web servers
libcurl.x86_64                A library for getting files from web servers
==================== Description Matched: web server ==================
httpd.x86_64                  Apache HTTP Server
```

# 第 1 章 | 安装和更新软件包

```
git-instaweb.x86_64 : Repository browser in gitweb
...output omitted...
```

- `yum info PACKENAME` 返回有关软件包的详细信息，包括安装所需的磁盘空间。

获取 Apache HTTP Server 的信息：

```
[user@host ~]$ yum info httpd
Available Packages
Name            : httpd
Version         : 2.4.37
Release         : 7.module+el8+2443+605475b7
Arch            : x86_64
Size            : 1.4 M
Source          : httpd-2.4.37-7.module+el8+2443+605475b7.src.rpm
Repo            : rhel8-appstream
Summary         : Apache HTTP Server
URL             : https://http.apache.org/
License         : ASL 2.0
Description     : The Apache HTTP Server is a powerful, efficient, and extensible
                web server.
```

- `yum provides PATHNAME` 显示匹配指定路径名称的软件包（通常包含通配符）。

要查找提供 `/var/www/html` 目录的软件包：

```
[user@host ~]$ yum provides /var/www/html
httpd-filesystem-2.4.37-7.module+el8+2443+605475b7.noarch : The basic directory
layout for the Apache HTTP server
Repo            : rhel8-appstream
Matched from:
Filename        : /var/www/html
```

# 使用 yum 安装和删除软件

- `yum install PACKENAME` 获取并安装软件软件包，包括任何依赖项。

```
[user@host ~]$ yum install httpd
Dependencies===================================================================
Package        Arch            Version             Repository        Size
===================================================================
Installing:
httpd           x86_64          2.4.37-7.module...  rhel8-appstream   1.4 M
Installing dependencies:
apr             x86_64          1.6.3-8.el8         rhel8-appstream   125 k
apr-util        x86_64          1.6.1-6.el8         rhel8-appstream   105 k
...output omitted...
Transaction Summary
====================================================================
```

Install 9 Packages

Total download size: 2.0 M
Installed size: 5.4 M
Is this ok [y/N]: y
Downloading Packages:
(1/9): apr-util-bdb-1.6.1-6.6.el18.x64.rpm   464 kB/s | 25 kB   00:00
(2/9): apr-1.6.3-8.el18.x64.rpm         1.9 MB/s | 125 kB   00:00
(3/9): apr-util-1.6.1-6.6.el18.x64.rpm         105 kB   00:00

...output omitted...
Total
Running transaction check
Transaction succeeded.
Running transaction test
Transaction succeeded.
Running transaction 8.6 MB/s   00:00
Preparing
Installing: apr-1.6.3-8.el18.x64      1/9
Running-script: apr-1.6.3-8.el18.x64      2/9
Installing: apr-util-1.6.1-6.6.el18.x64      3/9
...output omitted...
Installed: httpd-2.4.37-7.module+el8+2443+60547b7.rpm   4/9
apr-util-bdb-1.6.1-6.6.el18.x64      5/9
apr-util-openssl-1.6.1-6.el18.x64      6/9
...output omitted...
Complete!
```

- `yum update PACKENAME` 获取软件包的新版本，包括任何依赖项。过程通常会保留配置文件，但在某些情况下，如果新内核启动失败，旧内核可以使用。

# 注意

使用 `yum list kernel` 列出所有已安装和可用的内核。要查看运行中的内核，使用 `uname` 命令。`-r` 选项仅显示版本和发布版本，`-a` 选项显示更多信息。

```
[user@host ~]$ yum list kernel
Installed Packages
kernel.x86_64         4.18.0-60.el8 @anaconda
kernel.x86_64         4.18.0-67.el8 @rhel-8-x86_64-baseos-rpms
[user@host ~]$ uname -r
4.18.0-60.el8.x86_64
[user@host ~]$ uname -a
linux host.lab.example.com 4.18.0-60.el8.x86_64 #1 SMP Jan 11 19:08:11 UTC 2019 x86_64 GNU/Linux
```

- `yum remove PACKENAME` 删除已安装的软件包，包括任何支持的软件包。

```
[user@host ~]$ sudo yum remove httpd
```

> 警告
yum remove 命令删除列出的软件包以及任何需要这些软件包的软件包（以及需要这些的软件包，以此此类推）。这可能会意外删除软件包，请仔细检查要删除的软件包列表。

# 使用 yum 安装和删除软件

- `yum` 有“组”的概念，组是为特定目的而一起安装的相关软件集合。在 Red Hat Enterprise Linux 8 中，有两种组。普通组是软件包的集合。环境组是普通组的集合。组提供的软件包或组可能是强制性的（如果安装组则必须安装）、默认的（如果安装组时不安装）或可选的（除非明确请求否则不安装）。

类似于 `yum list`，`yum group` 命令显示已安装和可用组的名称。

```
[user@host ~]$ yum group list
Available Environment Groups:
Server with GUI
Minimal Install
Server
...output omitted...
Available Groups:
Container Management
.NET Core Development
```

