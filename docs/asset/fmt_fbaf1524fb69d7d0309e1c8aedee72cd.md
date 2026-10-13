
4. 输入 `yum install -y createrepo` 以确保已安装 `createrepo` RPM 包。

5. 输入 `createrepo /repo`。这将生成存储库元数据，允许你使用自己的存储库。

6. 现在既然你已经创建了存储库，不妨开始使用它。在 `/etc/yum.repos.d/` 中，创建一个名为 `my.repo` 的文件。确保该文件包含以下内容：

```
[myrepo]
name=myrepo
baseurl=file:///repo
```

7. 输入 `yum repolist` 验证新创建的存储库的可用性。它应该显示 `myrepo` 存储库的，以及通过该存储库提供的软件包数量（参见列表 11.3）。

提示：在练习 11.1 中，你挂载了安装磁盘的 ISO 文件来复制其中的文件。另一种获取存储库文件的方便方法是使用 `yumdownloader` 工具。该工具允许你直接从存储库将单个包下载到当前目录。例如，使用 `yumdownloader nmap` 将 RPM 包下载到当前目录。

### 列表 11.3 使用 yum repolist 验证存储库的可用性

```
[root@server1 Packages]# yum repolist
Loaded plugins: fastestmirror, langpacks
myrepo                                 | 2.9 kB 00:00
myrepo/primary_db                     | 77 kB 00:00
Loading mirror speeds from cached hostfile
* base: mirror.nl.leaseweb.net
* extras: mirror.nl.leaseweb.net
* updates: mirror.nl.leaseweb.net
repo id                               repo name               status
base/7/x86_64                         CentOS-7 - Base          8,465
extras/7/x86_64                       CentOS-7 - Extras       104
myrepo                                130
updates/7/x86_64                      CentOS-7 - Updates      1,668
relist: 10,367
```

## 使用 yum

到此时，你应该已经有了可以使用的存储库，所以是时候开始使用它们了。要使用存储库，你需要 `yum` 命令。该命令允许你对存储库执行若干项任务。表 11.4 提供了常用 yum 任务的概述。

### 表 11.4 常用 yum 任务

| 任务 | 说明 |
| :--- | :--- |
| search | 搜索软件包的精确名称 |
| `[what]`provides */name | 在包中进行深度搜索，查找包内的特定文件 |
| info | 提供有关软件包的更多信息 |
| install | 安装软件包 |
| remove | 软件包 |
| list [all \| installed] | 列出所有或已安装的软件包 |
| group list | 列出软件包组 |
| group install | 安装组中的所有软件包 |
| update | 更新指定的软件包 |
| clean all | 删除所有存储的元数据 |

## 使用 yum 查找软件包

要用 yum 安装软件包，你首先需要知道软件包的精确名称。`yum search` 命令可以为此提供帮助。当你使用 `yum search` 时，它首先连接到在线存储库（这可能需要一分钟），之后将最新的存储库元数据下载到本地机器。然后，`yum search` 会在包名和描述中查找你正在寻找的字符串。在列表 11.4 中，你可以看到使用 `yum search user.` 后的结果。

### 列表 11.4 yum search 示例输出

```
[root@server1 Packages]# yum search server user
Loaded plugins: fastestmirror, langpackages
Loading mirror speeds from cached hostfile
* base: mirror.sitb.nl
* extras: mirror.sitb.nl
* updates: mirror.sitb.nl
============================
nmap                    - Network discovery
nmap-data              - nmap
nmap-doc               - nmap
nmap-devel             - nmap
nmap-gui               - nmap
```

## 获取更多信息

在使用 yum 安装软件包之前，你首先需要知道软件包的精确名称。`yum search` 命令可以为此提供帮助。当你使用 `yum search` 时，它首先连接到在线存储库（这可能需要一分钟），之后将最新的存储库元数据下载到本地机器。然后，`yum search` 会在包名和描述中查找你正在寻找的字符串。在列表 11.4 中，你可以看到使用 `yum search user.` 后的结果。（*注：此处翻译根据原文逻辑调整*）

在安装软件包之前，一个主意是使用 `yum info` 获取关于该软件包的一些信息。在列表 11.5 中，你可以看到它的样子。

### 列表 11.5 yum info 示例

```
[root@server1]# yum info nmap
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
* base: mirror.sitb.nl
* extras: mirror.sitb.nl
* updates: mirror.sitb.nl
Name              : nmap
Version           : 2.4.2a
Release            :25.el7
Arch              : x86_64
Size              : 2.0 M
Summary           : Network discovery and security auditing
Description       : Nmap is a free tool for network discovery and security
License           : GPL2
URL               : https://nmap.org/
Source            : base/nmap-2.4.2a-25.el7.x86_64.rpm
gpgkey            : file://pubkeys.redhat.com/RPM/RPM-GPG-KEY-redhat
```

## 安装软件包软件包

如果你对 `yum info` 的输出满意，下一步是安装它。正如其他操作一样，你不需要猜测如何操作：只需使用 `yum install nmap`。当你这样使用 yum 命令时，它会向你确认。列表 11.6 显示了其结果。

* base: centrum.mirror.triple-it.nl

* extras: centrum.mirror.triple-it.nl

* updates: centrum.mirror.triple-it.nl

正在解析依赖

--> 运行事务检查

--> 将安装软件包 nmap.x86_64 2:60-4.el7

--> 正在处理依赖：软件包 nmap-6.40-4.el7.x86_64 的依赖 nmap-ncat = 2:60-4.el7

--> 运行事务检查

--> 将安装软件包 nmap-ncat.x86_64 2:60-4.el7

--> 完成依赖解析

依赖已解决

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| nmap | x86_64 | 2:60-4.el7 | base | 3.9 M |
| nmap-ncat | x86_64 | 2:60-4.el7 | base | 200 k |

正在安装：

事务摘要

安装 1 个软件包 (+1 个依赖包)

总下载大小：4.1 M

安装后大小：17 M

是否确认 [y/d/N]: y

正在下载软件包：

(1/2): nmap-ncat-6.40-4.el7.x86_64.rpm

| 200 kB 00:00:00
