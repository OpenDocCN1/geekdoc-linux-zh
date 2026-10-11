

如今，开头的 **if** 语句已是老朋友。正如你可能预期的那样，我们通过查找该包中的某个文件来验证客户端软件包是否已安装。如果不存在客户端软件包，条目将从 `/etc/services` 中移除。这就结束了。

显然，这些脚本必须经过仔细测试。就 amanda 而言，由于这两个软件包之间存在一定的依赖性，有必要尝试不同的安装和卸载这两个软件包的顺序，以确保 `/etc/services` 逻辑在所有情况下都能正常工作。

经过一番测试，我们的安装和卸载脚本以出色的成绩通过。从技术角度来看，客户端和服务器子软件包已经准备就绪。

### 20.4.3.3. 零碎事项

然而，仅仅因为一个软件包构建正确、安装顺利且能无问题卸载，并不意味着软件包构建者的工作已经完成。有必要从用户的角度审视每个新构建的软件包。该软件包是否包含用户有效部署所需的一切？还是说用户需要对其进行摸索，在过程中不断猜测？

就我们的 amanda 软件包而言，显然需要一些额外的文档，以便用户知道需要做什么来完成安装。仅仅将用户引导至标准的 amanda 文档也不是正确的解决方案。`INSTALL` 文档中列出的许多步骤已经由 postinstall 脚本完成了。不，需要一份中间文档。实际上需要两份：一份用于客户端，一份用于服务器。

因此创建了两个文件，每个子软件包各添加一个文件。问题在于，如何实现？基本上有两种选择：

- 将文件放入用于执行初始构建并生成新补丁文件的 amanda 目录树中
- 创建一个包含这两个文件的 tar 文件，并修改 spec 文件以将文档解压缩到 amanda 目录树中
- 不使用 tar，直接将文件放入 amanda 目录树中

由于第二种方法更有趣，我们选择了该方法。它需要在 spec 文件中增加一个额外的 source 标签：

```
Source1: amanda-rpm-instructions.tar.gz
```

还需要在 `%prep` 脚本中增加一个额外的 `%setup` 宏：

```
%setup -T -D -a 1
```

虽然 `%setup` 宏可能看起来令人望而生畏，但构建它并没有那么难。以下是每个选项的含义：

-T — 不执行默认的归档解包。

最后，需要在 `%files` 列表中增加两项，一项用于客户端：

```
%doc amanda-client.README
```

一项用于服务器：

```
%doc amanda-server.README
```

至此，软件包已完成。当然，有些软件在打包时不需要这么多的工作。同样确定的是，有些软件更具挑战性。

## 21. RPM 库 API 指南

在本章中，我们将探讨 RPM 内部使用的函数。这些函数可供任何人使用，这使得向现有和新程序中增加 RPM 功能成为可能。与其在本章中不断提及“RPM 库”，我们将使用该库主包含文件的名称——rpmlib。

### 21.1. rpmlib 概述

由若干文件组成 rpmlib。首先且最重要的是，当然是 rpmlib 库，`librpm.a`。此库包含实现 RPM 中包含的所有基本功能所需的所有函数。

其余文件定义了 rpmlib 使用的各种数据结构、参数和符号：

- `rpmlib.h`
- `dbindex.h`
- `header.h`

通常，`rpmlib.h` 总是必需的。当使用 rpmlib 的 header 相关函数时，需要 `header.h`，而数据库相关函数需要 `dbindex.h`。在本章中描述每个函数时，我们将提供函数的原型以及该函数所需的 `#include` 语句。

### 21.2. rpmlib 函数

rpmlib 中有 60 多个不同的函数。它们执行的任务范围从低级的数据库记录遍历到高级的软件包操作。我们将这些函数分组到不同的类别中，以便轻松参考。

#### 21.2.1. 错误处理

本节的函数执行 rpmlib 的基本错误处理。所有错误处理都围绕使用特定的状态代码进行。状态代码定义在 `rpmlib.h` 中，形式为 `RPMERR_xxx`，其中 `xxx` 是错误名称。

##### 21.2.1.1. `rpmErrorCode()` — 返回错误代码

此函数返回由最后一个失败的 rpmlib 函数设置的错误代码。它只应用于由 `rpmErrorSetCallback()` 定义的错误回调函数中：

```c
#include <rpm/rpmlib.h>

int rpmErrorCode(void);
```

##### 21.2.1.2. `rpmErrorString()` — 返回错误字符串

此函数返回由最后一个失败的 rpmlib 函数设置的错误字符串。它只应用于由 `rpmErrorSetCallBack()` 定义的错误回调函数中：

```c
#include <rpm/rpmlib.h>
char *rpmErrorString(void);
```

##### 21.2.1.3. `rpmErrorSetCallBack()` — 设置错误回调函数

此函数将当前的错误回调函数设置为传递给它的错误回调函数。返回之前的错误回调函数：

```c
#include <rpm/rpmlib.h>
rpmErrorCallBackType rpmErrorSetCallBack(rpmErrorCallBackType);
```

#### 21.2.2. 获取软件包信息

本节描述的函数用于获取关于软件包文件的信息。

请注意，大多数信息以 Header 结构的形式返回。这种数据结构在 rpmlib 中广泛使用。我们将在 21.2.13 和 21.2.14 节中讨论更多的 header 相关函数。

##### 21.2.2.1. `rpmReadPackageInfo()` — 读取软件包信息

给定在 `fd` 上打开的软件包，读取 header 和 signature：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>
int rpmReadPackageInfo(int fd, Header *signatures, Header *hdr);
```

该函数按预期工作，接受套接字和管道文件描述符作为 `fd`。在非可 seek 的 `fd` 上使用是安全的。当函数返回时，`fd` 被定位为在软件包 archive 部分的开始处。

如果 `signatures` 或 `hdr` 为 `NULL`，则不会向调用者传回 `NULL` 参数的信息。否则，`signatures` 和 `hdr` 将分别返回软件包的 signature 和 header。

该函数返回以下状态值：

- 0 — 成功
- 1 — 在软件包中发现错误的 magic 数
- 2 — 其他错误

##### 21.2.2.2. `rpmReadPackageHeader()` — 读取软件包 Header

给定在 `fd` 上打开的软件包，读取 header：

```c
#include <rpm/rpmio.h>
#include <rpm/header.h>

int rpmReadPackageHeader(int fd,
Header * hdr,
int * isSource,
int * major,
int * minor);
```

该函数按预期工作，接受套接字和管道文件描述符作为 `fd`。在非可 seek 的 `fd` 上是安全的。当函数返回时，`fd` 被定位为在软件包 archive 部分的开始处。

如果 `hdr`、`isSource`、`major` 或 `minor` 为 `NULL`，则不会向调用者传回 `NULL` 参数的信息。否则，它们将返回软件包的 header (`hdr`)、关于软件包是否为源软件包文件的信息 (`isSource`)，以及软件包格式的 major 和 minor 修订号 (分别为 `major` 和 `minor`)。

该函数返回以下状态值：

- 0 — 成功
- 1 — 在软件包中发现错误的 magic 数
- 2 — 其他错误

#### 21.2.3. 变量操作

以下函数用于获取、设置和解释 RPM 的内部变量。变量根据各种系统信息片段以及从 `rpmrc` 文件设置。它们控制 RPM 操作的各种方面。

变量在 `rpmlib.h` 中具有形式为 `RPMSVAR_xxx` 的符号名称，其中 `xxx` 是变量名称。所有变量名称都定义在 `rpmlib.h` 中。

##### 21.2.3.1. `rpmGetVar()` — 返回 RPM 变量的值

此函数返回在 `var` 中指定的变量的值：

```c
#include <rpm/rpmlib.h>

char *rpmGetVar(int var);
```

出错时，函数返回 `NULL`。

