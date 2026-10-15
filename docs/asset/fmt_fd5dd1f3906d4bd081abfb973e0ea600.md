
```
# caa_stat -v nicUP
NAME=nicUP
TYPE=network
FAILURE_THRESHOLD=2
FAILURE_COUNT=0 on molari
FAILURE_COUNT=0 on sheridan
TARGET=ONLINE on molari
TARGET=ONLINE on sheridan
STATE=ONLINE on molari
STATE=ONLINE on Sheridan
```

与资源注册表数据库一样（如果你是 CT²S² 的话），你可以使用 `caa_dbConvert` 命令转储资源注册表历史数据库。

```
/usr/sbin/cluster/caa_dbConvert DUMP caa.his.binaryDB /tmp/caa.his.txt
```

以下是转换数据库的摘录，显示了 `nicUP` 资源的信息。

```
__RESOURCE__,nicUP
2_FAILURE_HISTORY,1018678401 1018682922
_
```

你可以看到 `nicUP` 资源最后两次失败的时间如下：

```
# perl -e 'foreach $i (1018678401,1018682922)
> { printf ("%s\n", scalar localtime $i) };'
Sat Apr 13 02:13:21 2002
Sat Apr 13 03:28:42 2002
```

## 23.3.5 目录布局

图 23.2 显示了大多数 CAA 相关目录和文件所在的位置。请注意，我们并未包含每一个文件或目录位置。如需完整列表，可使用 `find(1)` 命令。

```
# find / -name "*[Cc] [Aa] [Aa]*"
```

如果你恰好有一个运行了 V5.1A 修补版本的集群，你会看到一个混合的目录布局，其中包含 V5.1B 中看到的一些文件。这是因为 CAA 工程组为 “Compaq Database Utility with Oracle® Real Application Clusters” 所做的支持工作。

## V5.0A, V5.1, & V5.1A

![](img/a0df85c2e542a8d6c913113908553aa4_670_0.png)

## V5.1B

![](img/a0df85c2e542a8d6c913113908553aa4_670_1.png)

图 23-2：CAA 目录和文件

请注意，`/var/cluster/caa` 下的 `log` 子目录已过时，不应再使用。

## 23.3.6 CAA 命令

CAA 既提供命令行界面，也提供图形用户界面（GUI）。要确定有哪些 CAA 命令可用（或实际上有哪些 CAA 信息可用），最简单的方法是使用带 “-k” 选项的 `man(1)` 命令（或 `apropos(1)` 命令）。

```
# man -k caa
```

另一个选择是使用我们编写的 `sman` 脚本。`sman` 命令本质上是一个基于章节的 “man -k” 命令，同时还会格式化输出。`sman` 的优点是你可以将搜索条件缩小到你感兴趣的章节。例如，如果你只想要命令，可以将搜索限制在第 1 和第 8 节。

```
# sman [18] caa
```

| Section | Reference Page | Description |

|---|---|---|

| 8 | `caa_balance` | 查找应用程序资源的最佳成员，并在资源未放置在该成员上时将其迁移到该成员。 |

| 8 | `caa_profile` | 创建、验证、删除和更新 Cluster Application Availability（CAA）资源配置文件 |

| 8 | `caa_register` | 在 Cluster Application Availability（CAA）中注册资源 |

| 8 | `caa_relocate` | 将应用程序资源从一个集群成员迁移到另一个集群成员 |

| 1 | `caa_report` | 报告应用程序资源的可用性统计信息 |

| 8 | `caa_start` | 启动已在 Cluster Application Availability（CAA）中注册的资源。 |

| 1 | `caa_stat` | 提供集群中 Cluster Application Availability（CAA）资源的状态。 |

| 8 | `caa_stop` | 停止 Cluster Application Availability（CAA）应用程序资源 |

| 8 | `caa_unregister` | 注销 Cluster Application Availability（CAA）资源。 |

| 8 | `caad` | Cluster Application Availability（CAA）守护进程 |

使用 “all” 关键字将搜索所有 man 章节。

```
# sman all caa
Section  Reference Page  Description
-------- --------------- ------------------------------------------------
4         caa             Cluster Application Availability（CAA）
                          information
```

CAA 的好消息是，你将使用的命令都以 “caa_” 开头。你只需要记住想要执行的操作即可。

请注意，GUI 不会出现在 “man -k” 或 “sman” 的输出中。这是因为 GUI 是 `sysman(8)` 应用程序插件。使用 “sysman -list” 命令查找 sysman 加速器的列表。

```
# sysman -list | grep -i caa
| Cluster Application Availability (CAA) Management [caa]
```

要使用 “caa” 加速器通过 sysman 管理 CAA。

```
# sysman caa
```

# NOTE:

`caa_balance(8)` 和 `caa_report(1)` 命令是在 V5.1B 中添加的。

## 23.4 Resources

TruCluster Server 中，DRD 管理存储，CLSM 管理磁盘组，CFS 管理文件系统，而 CLUA 管理别名。

那么 CAA 管理什么？资源。

存在哪些类型的资源？

## 23.4.1 资源类型

截至本文撰写时，CAA 支持四种资源类型：

- Application

- Changer

- Network

- Tape

`Application` 资源必须具有资源配置文件（参见第 23.4.3 节）和一个动作脚本（参见第 23.4.5 节）。

非 `Application` 资源必须具有资源配置文件（当然，配置正确且功能正常的硬件也很重要）。

## 23.4.2 资源状态

表 23-3 显示了资源可以具有的状态以及每个状态相对于每个资源的描述。请注意，每个资源都将具有一个 TARGET 状态和一个当前 STATE。

## 23.4.3 资源配置文件

资源的配置文件包含定义该资源的属性。资源配置文件是一个 ASCII 文件，因此可以使用您喜欢的编辑器进行编辑，尽管您可能会发现使用 `caa_profile` 命令或使用 `sysman` 并使用“caa”关键字加速器来创建它很方便。

所有资源类型都需要资源配置文件。创建资源并不是沿途的最后一步。一旦配置文件被创建（以及任何时候它被修改），它必须在资源管理器中注册。

在以下各节中，我们将向您展示可用于每种资源类型的属性，以及必须使用的属性。我们还将向您展示如何注册资源，在配置文件被修改时更新注册，以及注销不再需要的资源。

让我们开始定义资源属性。

## 23.4.4 资源属性

截至本文撰写时，有四种资源类型。每种资源类型使用某些属性。某些属性是必需的，而其他属性是可选的。某些属性对所有资源类型都是通用的。

在以下各节中，我们将列出每个属性，说明它是否必需，确定其默认值，并描述其使用方式。

**资源属性类别** | **章节**

- Common — 23.4.4.1

- Application — 23.4.4.2

- Network — 23.4.4.3

- Tape and Media Changer — 23.4.4.4

有关最新资源属性信息，请参阅 `caa(4)` 参考页。

### 资源状态

| Resource | State | Description | TARGET* |

|---|---|---|---|

| Application | **ONLINE** | 由资源启动的应用程序正在运行。 | 资源已被设置为启动（即执行了 `caa_start`）。 |

| Application | **OFFLINE** | 由资源启动的应用程序未运行或资源已被管理停止。 | 资源已被设置为停止（即执行了 `caa_stop`）。 |
