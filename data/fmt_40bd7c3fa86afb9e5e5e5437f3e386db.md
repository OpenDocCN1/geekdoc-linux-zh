
如果你使用的是较新版本的 Net-SNMP，只需将 tar 包放入与 `Makefile` 相同的目录中，修改 ❶ `NETSNMP_VERSION` 行以匹配你的版本，并继续执行下面的说明。

我们将 `Makefile` 和 `configure.input` 文件放入刚刚下载的 tar 包所在的目录中。`configure.input` 包含了 `configure` 步骤预期的交互式答案。`--prefix` 选项告诉 `configure` 使用 `/opt/snmp` 前缀。

```bash
./configure
make
```

以下是 `configure.input` 的内容：

```text
prefix=/opt/snmp
```

*(注：原文后续部分存在大量重复的占位符，已根据上下文逻辑进行了处理。)*

# MIB 骨架：mib2c

Net-SNMP 提供了一个工具程序，它可以读取 MIB 文件并生成用于代理扩展的骨架代码。在本章的后半部分，我们将展示如何将这个骨架充实为 MIB 的完整实现。

在运行 `mib2c` 之前，你需要安装 SNMP Perl 模块，它位于 Net-SNMP tar 包中。当你之前运行 `make` 时，解压了该 tar 包并创建了 `net-snmp-5.2.1` 目录。进入该目录，然后运行 `perl/SNMP`。

在那里你将找到一个 README 文件，解释如何构建和安装 SNMP Perl 模块。或者，如果你的 Linux 发行版提供了该包，你也可以安装 `libsnmp-perl` 软件包。

我们还需要将我们的 MIB 文件（我们在第 12 章中创建的 `LADDIE-GROUP-SMI.txt`）复制到包含其他 MIB 的目录中（`/snmp/share/snmp/mibs`），以便 `mib2c` 可以使用。或者，如果你愿意，可以在你的 `MIBDIRS` 列表中添加点 (`.`)，例如：

```
export MIBDIRS=:/snmp/share/snmp/mibs
```

现在让我们运行 `mib2c` 来生成骨架代码。如果你在目录路径中添加了 `.`，那么你可能需要与 MIB 文件位于同一个目录。请注意，我们运行 `mib2c` 时使用的是 MIB 模块或 OID，而不是 MIB 文件的名称。

```
$ mib2c LAD-MIB:ladProject
writing to
```

`mib2c` 有多个配置文件，取决于你编写的代码类型。你必须根据需要选择其中一个。

请求运行 `mib2c` 以处理 MIB 树的以下部分：
OID: `1.3.6.1.4.1.23528.1.1`
数字翻译：
内部标量数量：4
内部表格数量：1
内部通知数量：2

首先，你是想生成一个与 ucd-snmp 4.X 系列代码兼容的代码，还是为较新的 Net-SNMP 5.X 代码库生成代码（它提供了更多的 API 可供选择）：

+ 1) ucd-snmp 风格代码
2) Net-SNMP 风格代码 1

选择你的选项： 1
********************************************************************
正在为 4.X 系列代码生成代码（旧 API）
********************************************************************

使用 `mib2c.old-api.conf` 配置文件生成你的代码。
正在写入 `ladProject.h`
正在写入 `ladProject.c`

********************************************************************
* 注意：mib2c 生成的代码只是一个模板。*TODO* *
* 在大多数情况下，必须填充代码才能运行。在许多
* 情况下，文件中必须编辑的地方已标记为
* /* XXX */ 或 /* TODO */ 注释。
********************************************************************

正在对 `ladProject.c` 执行缩进
正在对 `ladProject.h` 执行缩进

在这一切中间，你将在第 ① 行看到以下内容：

+ 1) ucd-snmp 风格代码
2) Net-SNMP 风格代码

选择你的选项： 1

我们使用选项一是因为我们在那里有经验。你可能想尝试更新且更灵活的 Net-SNMP 类型，但对于我们在这里的操作不需要那种灵活性。

## 头文件：ladProject.h

我们生成了两个文件：`ladProject.c` 和 `ladProject.h`。头文件 `ladProject.h` 简短明了，我们不需要再费心于它了。它的样子如下：

```
/*
* 注意：此文件最初由 mib2c 使用
* mib2c-old-api.conf 自动生成，v 1.4 2004/07/28 08:04:58 dts12 Exp $
*/
#ifndef LADPROJECT_H
#define LADPROJECT_H
/*
* 函数声明
*/
void init_ladProject(void);
FindVarMethod var_ladProject;
FindVarMethod var_ladAlarmTable;
WriteMethod write_ladAlarmEnable;
WriteMethod write_ladAlarmLatching;
WriteMethod write_ladAlarmState;
/* LADPROJECT_H */
```

它们是为代码文件 `ladProject.c` 生成的例程原型。

## 代码文件：ladProject.c

`ladProject.c` 文件是我们要修改的文件。与其描述生成的代码并进行第二遍以添加修改，我们直接逐步处理它，边走边修改。我们将使用**粗体文本**将我们添加的代码与 `mib2c` 生成的代码区分开。具体来说，我们需要对生成的骨架代码进行以下修改：

- 1. 包含 libpq（PostgreSQL 库）的头文件。
- 2. 提供一个连接到 `ladd` 守护进程 RTA 的函数。
- 3. 提供通过连接到 `ladd` 守护进程读写 RTA 表格的函数。
- 4. 提供读取 MIB 中每个标量的代码。
- 5. 提供读取 `ladAlarmTable` 中每个表格对象的代码。
- 6. 为 MIB 中的每个可写对象提供写入函数。

### 包含

我们首先包含必要的头文件。记住，我们将用**粗体**标记我们的添加和修改。

```
/*
* 注意：此文件最初由 mib2c 使用
 * mib2c.old-api.conf v 1.4 2004/07/28 08:04:58 dts12 Exp $
 */
```

```
#include net-snmp/net-snmp-config.h
#include net-snmp/net-snmp-includes.h
#include net-snmp/agent/net-snmp-agent-includes.h
#include "pq-lib-fe.h" /* libpq 头文件 */
#include "ladProject.h"
```

通过包含定义 `libpq` 的头文件完成了第一个目标。

### 基础 OID

在这段代码中，`mib2c` 生成的注释基本上是我们 MIB 中所有对象的基础 OID。

```
/*
* ladProject_variables_oid:
* 这是我们要注册的顶层 OID。
* 本质上是变量块中的后缀。
*/
```

```
ladProject_variables_oid[] =
{ 1, 3, 6, 4, 1, 23528, 1, 1 };
```

### MIB 对象

后续代码定义了 MIB 中所有的叶子对象（leaf objects），即我们将返回的对象。对于这些叶子对象，生成了定义以提供一个唯一编号。定义是对象名称的大写版本。

每个对象在 `ladProject_variables` 表中都有自己的条目（所示），提供了对象的以下信息：

- 之后使用的唯一标识符（定义的名称）
- 数据类型
- 是只读还是读写
- 用于读取对象值的函数
- OID 后缀，当附加到基础 OID 时，将得到对象的完整 OID

我们发现 `mib2c` 的原始输出有点难读，因为唯一标识符混合在表格中。为了让这更易访问，我们将所有定义放在在一起。不幸的是，`mib2c` 没有为我们生成完美的代码，但我们将利用这一点来提供关于应该生成什么的的内容。`mib2c` 之类的工具很棒，但你应该始终意识到应该生成什么，并检查输出。最终，你将为你编写的代码负责。首先，让我们看看代码，然后我们讨论我们看到的问题。

```
#LADVERSION 1
#LADNUMBEROFONES 2
#LADTRAPZONE 3
#LADTRAPZENAME 4
#LADALARMZONEID 5
```
