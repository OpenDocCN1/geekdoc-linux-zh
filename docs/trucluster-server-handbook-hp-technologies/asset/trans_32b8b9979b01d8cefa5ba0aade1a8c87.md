

```
# /usr/sbin/lmfsetup
Register PAK (type q or quit to exit) [template]
    Issuer : dec
    Authorization Number : ala-ng-xxxxxx-xxxx
    Product Name : tcs-ua
    Producer : dec
    Number of units : 1050
    Version :
    Product Release Date :
    Key Termination Date :
    Availability Table Code : h
    Activity Table Code :
    Key Options : mod_units,alpha
    Product Token :
    Hardware-Id :
    Checksum : 2-wwww-xxxx-yyyy-zzzz
PAK registered for template successfully
Register PAK (type q or quit to exit) [template] q

You have registered at least one new PAK. Until it is loaded by use of the lmf reset, lmf load for each newly registered PAK, or rebooting your system, software dependent on them will be treated as if the registrations had not been performed.

Would you like a lmf reset to be performed at this time? [Yes] Yes
```

现在来验证一下 TruCluster Server 的许可证 PAK 是否已加载并激活。为此，我们使用 lmf(8) 命令。

```
$ /usr/sbin/lmf list for tcs-ua
TCS-UA                active                unlimited
```

## 10.2.2 安装 TruCluster Server 软件

请注意，虽然建议在安装 TruCluster Server 软件子集之前加载 TruCluster Server 许可证 PAK，但这不是必需的。可以在没有 TruCluster Server 许可证 PAK 的情况下安装 TruCluster Server 软件子集，但如果许可证 PAK 未激活，你将无法使用这些软件子集中的任何一个。

现在让我们继续安装 TruCluster Server 软件子集。

- 首先，让我们挂载 Tru64 UNIX 关联产品第 2 卷 CD-ROM。其中包含 TruCluster Server 软件子集。

```
$ mount -r /dev/disk/cdrom0c /mnt
```

- 现在，让我们“cd”到 *TruCluster Server* 套件目录，看看将要安装的内容。

```
# cd /mnt/TruCluster/kit && ls
TCRBASE520      TCRMAN520      TCRMIGRATE520      instrctl/
```

*TruCluster Server* 安装包含三个软件子集：

| 软件子集 | 描述 | 内容 |
|---|---|---|
| TCRBASE520 | *TruCluster Server* 基本组件 | 实现 *TruCluster Server* 所需的所有强制组件。 |
| TCRMAN520 | *TruCluster Server* 参考手册页 | 参考手册页。 |
| TCRMIGRATE520 | *TruCluster Server* 迁移工具 | 用于从 *TruCluster* 生产服务器和 *TruCluster* 可用服务器迁移的迁移工具。其中还包含对排查常规集群相关问题有用的工具。 |

使用 `setld(8)` 命令，我们执行 *TruCluster Server* 软件子集的安装。我们选择安装所有 *TruCluster Server* 子集，但如果你不打算从 *TruCluster* 1.5 或 1.6 版进行迁移（参见第 26 章），则不需要 TCRMIGRATE 子集。

```
# /usr/sbin/setld -l .

*** Enter subset selections ***

The following subsets are mandatory and will be installed automatically
unless you choose to exit without installing any subsets:

    - TruCluster Base Components

The subsets listed below are optional:

    There may be more optional subsets than can be presented on a single
    screen. If this is the case, you can choose subsets screen by screen
    or all at once on the last screen. All of the choices you make will
    be collected for your confirmation before any subsets are installed.

- TruCluster(TM) Software :
    1) TruCluster Migration Components
    2) TruCluster Reference Pages

Or you may choose one of the following options:
3) ALL mandatory and all optional subsets
4) MANDATORY subsets only
5) CANCEL selections and redisplay menus
6) EXIT without installing any subsets

Estimated free diskspace(MB) in root:293.1 usr:1428.5 var:1200.6
Enter your choices or press RETURN to redisplay menus.
Choices (for example, 1 2 4-6): 3
```

选择安装所有 TruCluster Server 软件子集后，系统会要求我们确认选择。

```
You are installing the following mandatory subsets:
    TruCluster Base Components
You are installing the following optional subsets:
- TruCluster(TM) Software :
    TruCluster Migration Components
    TruCluster Reference Pages
Estimated free diskspace(MB) in root:293.1 usr:1428.5 var:1200.6
Is this correct? (y/n): y
```

确认我们要安装的软件子集选择后，安装开始。

```
Checking file system space required to install selected subsets:
File system space checked OK.

3 subsets will be installed.
Loading subset 1 of 3 ...
TruCluster Migration Components
    Copying from . (disk)
    Verifying
Loading subset 2 of 3 ...
TruCluster Reference Pages
    Copying from . (disk)
    Verifying
Loading subset 3 of 3 ...
TruCluster Base Components
    Copying from . (disk)
    Verifying

3 of 3 subsets installed successfully.
```

