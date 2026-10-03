
# 监听器响应连接请求的方式

监听器有多种方式响应客户端的连接请求。响应取决于多个因素，例如服务器端网络组件的配置情况以及客户端请求的连接类型。监听器将以两种方式之一响应连接请求。

监听器可以启动一个新的进程，并将客户端会话的控制权传递给该进程。在专用服务器环境中，每个客户端连接都由其自身的服务器进程提供服务。服务器端进程不在客户端之间共享。根据操作系统的功能，可能存在两种类型的专用服务器连接：遗留交付连接（bequeath connections）和重定向连接（redirect connections）。每种连接都会产生一个处理客户端任务的独立进程，但实际连接启动过程的机制是不同的。

> 从 Oracle9i 开始，不再支持预启动专用进程（prespawn dedicated processes）。

## 遗留交付连接 (Bequeath Connections)

当底层操作系统（如 Unix）支持网络端点的继承时，遗留交付连接是可行的。这意味着操作系统能够启动新进程并将信息传递给该进程；这允许操作系统进程立即与客户端建立会话。

遗留交付连接的另一个名称是直接交接连接（direct hand-off connections）。

图 2.1 显示了遗留交付连接的连接过程及其步骤：

### 图 2.1 遗留交付连接过程

![](img/a183fd041839741f5ab6df3caffc6b52_100_0.png)

> 注意：为了在 Windows NT/2000 上支持遗留会话，需要设置注册表项 `USE_SHARED_SOCKET`。该设置可以在 `HKEY_LOCAL_MACHINE > SOFTWARE > ORACLE > HOMEX` 中设置，其中 X 等于你正在使用的 HOME。默认情况下，此注册表设置未初始化，因此当使用专用客户端时，Windows NT/2000 将使用重定向类型连接。

## 重定向连接 (Redirect Connections)

监听器也可以将用户重定向到服务器进程或调度器进程（dispatcher process）。当操作系统不支持遗留交付或监听器与 Oracle 服务器不在同一台机器上，就会发生此类连接。图 2.2 展示了以下步骤：

- 客户端在解析服务名后联系 Oracle 服务器。
- 对于 Oracle 服务器，监听器启动一个新的进程或调度器。对于共享服务器，如果现有服务器还有剩余容量，则需要启动一个调度器。
- 新进程或线程选择用于与客户端交互的 TCP/IP 端口。此信息将传回给监听器。
- 监听器将信息传回客户端，将客户端重定向到新的服务器或调度器。监听器与客户端之间的原始网络连接被断开。
- 客户端向服务器或调度器发送连接信号以建立网络连接。
- 调度器或服务器进程向客户端发送确认。
- 如果正在使用 Oracle 共享服务器进程，PMON 会向监听器发送有关调度器服务的连接数的信息。监听器使用这些信息来保持调度器之间的负载均衡。

### 图 2.2 重定向连接过程

![](img/a183fd041839741f5ab6df3caffc6b52_102_0.png)

# 第 2 章 · 在服务器上配置 Oracle Net

## 管理监听器

DBA 有多种方法配置服务器端监听器文件。在初始安装过程中，安装程序会提示 DBA 创建默认监听器。如果 DBA 不想以这种方式提供监听器，也可以使用 Oracle Net 助手（Oracle Net Assistant）来配置监听器。如果选择此方法，安装程序将使用该助手包含的屏幕进行初始监听器配置。图 2.3 显示了 Oracle Net 配置助手的启动界面示例。

### 图 2.3 Oracle Net 配置助手启动界面

![](img/a183fd041839741f5ab6df3caffc6b52_103_0.png)

Oracle Net 配置助手旨在作为一个简单、基于向导的工具，您可以使用它对客户端和服务器端网络产品进行基础设置。

静态注册是指使用 Oracle Net 助手手动向 `listener.ora` 文件添加条目时发生的情况。之所以称为静态的，是因为你是手动添加这些信息的。如果你将使用 Oracle Enterprise Manager 连接到 Oracle 8 之前的实例，或者你将连接到外部服务，则静态注册是必要的。

还有另一种管理监听器的方法，不需要手动更新 `listener.ora` 文件中的服务信息。这被称为动态注册（dynamic registration）。动态服务注册是一项功能，允许 Oracle 实例自动向 Oracle 监听器注册自己。该功能的用处是，当创建新的 Oracle 实例时，不需要 DBA 对服务器端网络文件进行任何更新。动态服务注册将在本章后面的“服务的动态注册”章节中进行更详细的介绍。

如果您正在使用 Oracle9i，则必须配置 Oracle9i 监听器以连接 Oracle 服务器。Oracle9i 监听器具有向后兼容性，可以监听对早期版本数据库的连接请求。

如果您想能够配置网络文件的基础设置，则必须使用 Oracle Net Manager。在接下来的几节中，您将学习如何使用 Oracle Net Manager 配置网络文件。

## 使用 Oracle Net Manager

Oracle Net Manager 是一个可以使用来创建和管理客户端和服务器端配置文件的工具。Oracle Net Manager 从 Oracle7 的 Network Manager 演变为最新的 Oracle9i 版本。在演变过程中，Oracle 不断增强该工具的功能和可用性。

我们建议使用 Oracle Net Manager 创建和管理所有的网络文件。这是因为这些文件需要特定的格式，而 Oracle Net Manager 可以确保按该格式创建文件。如果文件格式错误，可能会出现连接问题。即使是微小的空格或制表符也会导致连接问题，因此如果您习惯在这些文件中剪切粘贴条目，现在最好使用 Oracle Net Manager 创建新条目。

如果您在使用 Windows NT/2000 环境，可以通过选择 `开始 > 程序 > Oracle9i > 配置和迁移工具 > Oracle Net Manager` 来启动 Oracle Net Manager。在 Unix 环境中，可以在 `$ORACLE_HOME/bin` 目录下运行 `./netmgr` 启动。

图 2.4 显示了 Oracle Net Manager 的首页示例。

### 图 2.4 Oracle Net Manager 界面

![](img/a183fd041839741f5ab6df3caffc6b52_105_0.png)

## 使用 Oracle Net Manager 配置监听器服务

您将希望使用 Oracle Net Manager 配置监听器。正如第一章“网络管理简介”所述，Oracle Net Manager 为您将使用的大多数网络文件提供了一个易于使用的图形界面。通过使用 Oracle Net Manager，可以确保文件以一致的格式创建，从而减少连接问题的可能性。

当首次启动 Oracle Net Manager 时，启动界面会在屏幕右侧的 Network 文件夹下显示一组图标。Local 文件夹下的选项对应不同的网络配置文件。以下是不同的网络文件选项及其各自配置的内容。

| 图标 | 配置的文件 |
| --- | --- |
| 配置文件 | `sqlnet.ora` |
| 服务命名 | `tnsnames.ora` |
| 监听器 | `listener.ora` |
| Oracle 名称服务器 | `names.ora` |

> 如上一章所述，Oracle Names Server 正在被 Oracle Internet Directory 作为中心式 Oracle 服务名称解析的首选方法。然而，Oracle Names Server 仍然可以通过 Oracle Net Manager 进行配置，并在 Oracle 9i 中支持。但是，该产品不再进行任何修订，未来的 Oracle 版本可能不再支持 Names Server。

### 创建监听器

之前我们提到，默认情况下，Oracle 在安装时会创建一个名为 `LISTENER` 的监听器。Oracle 用于 `listener.ora` 文件的默认设置如下所示。

| 文件部分 | 设置 |
| --- | --- |
| 监听器名称 | `LISTENER` |
| 端口 | `1521` |
| 协议 | `TCP/IP` 和 `IPC` |
| 主机名 | 默认主机名 |
| SID 名称 | 默认实例 |

你可以使用 Oracle Net Manager 创建非默认监听器或更改现有监听器的定义。Oracle Net Manager 具有用于创建大多数网络元素的向导界面，例如 `listener.ora` 和 `tnsnames.ora` 文件。

按照以下步骤创建监听器：

1. 点击 Local 图标旁边的加号（`+`）。
2. 点击 Listeners 文件夹。
3. 点击加号图标或从 Edit 菜单中选择 Create。
4. 出现 Choose Listener Name 对话框。如果是首次创建监听器，在未配置监听器的情况下，Oracle Net Manager 认为 `LISTENER`；如果已创建了默认监听器，则默认为 `LISTENER1`。如果正确，请点击 OK 或输入新名称。这里是 Choose Listener Name 屏幕示例。

![](img/a183fd041839741f5ab6df3caffc6b52_107_0.png)

5. 选择监听器名称后，你可以配置监听位置；要进行此操作，点击 Listener Locations 下拉列表并进行选择。然后点击屏幕底部的 Add Address，如图 2.5 所示。

#### 图 2.5 来自 Oracle Net Manager 的 Listener Locations 屏幕

![](img/a183fd041839741f5ab6df3caffc6b52_107_1.png)

6. Oracle Net Manager 右侧会出现一个新屏幕。根据你的协议，提示内容会有所不同。默认显示 TCP/IP 信息。如果你使用 TCP/IP，系统会自动为你填写 Host 和 Port 字段。主机是运行监听器的机器名称，端口是 TCP/IP 连接的监听位置。端口的默认值为 `1521`。
7. 选择 `File > Save Network Configuration` 保存你的信息。保存信息后，查看其保存所在的目录。

你可以通过查看 Oracle Net Manager 屏幕顶部的横幅随时知道文件的存储位置。

Oracle Net Manager 在此过程中实际上创建了三个文件：`listener.ora`、`tnsnames.ora` 和 `sqlnet.ora`。`tnsnames.ora` 不包含任何信息。`sqlnet.ora` 文件此时可能包含少量条目，但目前可以忽略。`listener.ora` 文件将包含下方代码列表所示的信息。我们将在本文稍后讨论 `listener.ora` 文件的结构和内容。

```
### LISTENER.ORA Network Configuration File:
D:\oracle\ra90\network\admin\listener.ora
```

```
LISTENER1 =
(DESCRIPTION =
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = TCP)(HOST = mjworn)
(PORT = 1521))))
```

## 向监听器添加服务名称信息

在使用名称、协议和监听位置信息创建监听器后，你需要定义由监听器负责为用户连接的网络服务。监听器可以监听的网络服务名称数量没有限制。

添加服务名称信息的步骤如下：

1. 点击 Listeners 图标并突出显示你想要配置的监听器名称，以选择该监听器。
2. 选择监听器后，从屏幕右上角的下拉列表中选择 Database Services。
3. 点击底部的 Add Database 按钮。
4. 在 Global Database Name、Oracle Home Directory 和 SID 的提示中输入值。如果你使用扁平化命名法，SID 和全局数据库名称的条目是相同的（参见图 2.6）。

#### 图 2.6 来自 Oracle Net Manager 的 Add Service 屏幕

![](img/a183fd041839741f5ab6df3caffc6b52_109_0.png)

5. 选择 `File > Save` 保存你的配置。这里是完成的 `listener.ora` 文件示例：

### LISTENER.ORA Network Configuration File

`D:\oracle\ora90\network\admin\listener.ora`

### Generated by Oracle configuration tools.

```
LISTENER =
(DESCRIPTION_LIST =
(DESCRIPTION =
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = TCP))
(HOST = mprntw507953)(PORT = 1521)) =
```

```
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROCO))
)
)
SID_LIST_LISTENER =
(SID_LIST =
(SID_DESC =
(SID_NAME = PLSExtProc)
(ORACLE_HOME = D:\oracle\ra90)
(PROGRAM = extproc)
(SID_DESC =
(GLOBAL_DBNAME = MJW)
(ORACLE_HOME = D:\oracle\ora90)
(SID_NAME = MJW)
)
)
```

### 表 2.1 关于 listener.ora 的 Listening Section 参数

| 参数 | 描述 |
| --- | --- |
| `LISTENER` | 监听器的定义。默认名称是 `LISTENER`。 |
| `DESCRIPTION` | 监听位置。 |
| `ADDRESS_LIST` | 关于监听位置的信息。 |
| `PROTOCOL` | 此监听位置协议。 |
| `HOST` | 监听器所在的机器名称。 |
| `PORT` | 监听器的端口。 |
| `SID_LIST_LISTENER` | 监听器配置的 SID 列表。 |
| `SID_DESC` | 每个 SID 定义。 |
| `SID_NAME` | SID 名称。 |
| `GLOBAL_DBNAME` | 全局数据库名称。 |
| `ORACLE_HOME` | Oracle 可执行文件的位置。 |

### 表 2.1 关于 listener.ora 的 Listening Section 参数（续）

| 参数 | 描述 |
| --- | --- |
| `PORT` | 监听器的端口。 |
| `SID_LIST` | 监听器配置的服务。 |
| `SID_DESC` | 每个 SID。 |
| `GLOBAL_DBNAME` | 标识全局数据库名称。 |
| `ORACLE_HOME` | 服务器上的 Oracle 位置。 |
| `SID_NAME` | SID 的名称。 |

## 添加监听器

要添加更多监听器，请按照上述步骤操作。监听器必须具有唯一的名称并在不同的端口上监听，因此为监听器分配一个新名称和不同的端口（例如 `1522`）。你必须为监听器分配服务名称。

## 可选 listener.ora 参数

你可以设置为监听器添加功能的可选参数。可选参数通过屏幕右上角的 General Parameters 添加。表 2.2 描述了这些参数以及在 Oracle Net Manager 中查找的位置。

如你所见，某些参数无法直接从 Net Manager 添加，必须手动添加。这些可选参数还附加了监听器名称，以便识别它们属于哪个定义。例如，如果为默认监听器设置了 `STARTUP_WAIT_TIME`，则创建的参数为 `START_WAIT_TIME_LISTENER`。

### 表 2.2 可选 listener.ora 参数定义

| Oracle Net Manager 提示 | listener.ora 参数 | 描述 |
| --- | --- | --- |
| Startup Wait Time | `STARTUP_WAIT_TIME` | 定义监听器在响应 `STATUS` 命令前等待的时间。 |
| Unavailable from Net Manager | `CONNECT_TIMEOUT` | 会话启动后监听器等待有效响应的时间。默认为 10 秒。 |
| Unavailable from Net Manager | `SAVE_CONFIG_ON_STOP` | 指定退出时是否保存在 `snrctl` 会话期间的修改。 |
| Log File | `LOG_FILE`（如果使用默认设置则不在 `listener.ora` 中。默认情况下启用监听器日志。） | 指定监听器写入日志信息的位置。默认开启并默认为 `%ORACLE_HOME%\network\listener.log` |
| Trace Level | `TRACE_LEVEL`（如果禁用跟踪则不存在。默认为 OFF。） | 设置监听器连接正在被跟踪时的详细程度。有效值包括 Off, User, Support, Admin。 |
| Trace File | `TRACE_FILE` | 指定监听器跟踪信息的位置。默认为 `%ORACLE_HOME%\network\trace\listener.trc`。 |

### 表 2.2 可选 listener.ora 参数定义（续）

| Oracle Net Manager 提示 | listener.ora 参数 | 说明 |
| --- | --- | --- |
| 为监听器操作请求密码 | `PASSWORDS` | 指定在 `lnrctl` 命令行工具中执行管理任务所需的密码。 |

## 使用 lnrctl 管理监听器

一旦你创建并保存了监听器定义，必须在客户端连接并请求数据库连接之前启动监听器。无法从 Oracle Net Manager 启动或停止监听器。
