
## 应用替代方案 323

绑定器需要对 `PROD3.PAYROLL` 对象进行授权，但绑定器的 ID 不会被用于限定，因为该引用已经完全定义。

## 调整限定符和所有者

除了简单引用的限定外，DBA 还应该关注 `Precompile` 命令上可以指定的几个选项。在这种情况下，我们将识别绑定上的选项，用于指定 SQL 的限定符和所有者 ID。在这种情况下（见图 9.8），任何未限定的 SQL 将用 `U2` schema 进行限定。这是由 `QUALIFIER` 关键字引起的。`U2` 拥有该包，由 `OWNER` 关键字指定。这意味着 `U2` 可以对该包执行删除、重新绑定和授予权限，包括在具有授予权限的情况下授予权限的能力。

最后，`DYNAMICRULES BIND` 表示，当动态 SQL 通过此程序运行时，应该检查 `OWNER` 的权限。

- Jill 了：
- 未限定的 SQL 使用 schema
- u2 拥有包
  - 针对动态 SQL 检查了删除、重新绑定、授予权限
  - u2 的（权限）

```
db2 bind myapp.bnd qualifier u1 owner u2 dynamicrules bind
```

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_340_0.png)

`QUALIFIER` 为包中包含的未限定对象提供 8 字符的隐式限定符。默认是所有者的授权 ID，无论是否显式指定 `OWNER`。

`OWNER` 指定包所有者的授权标识符。所有者必须具有执行包中 SQL 语句所需的权限。如果未显式指定此选项，则默认是预编译/绑定过程的主授权 ID。

`DYNAMICRULES` 选项及其值可以在 `BIND` 时提供，它决定了在运行时针对授权 ID 适用于动态 SQL 的规则，以及用于未限定对象引用进行隐式限定的数值的初始设置。有效的 `DYNAMICRULES` 选项有 `RUN` 和 `BIND`；`RUN` 是默认值。

## 预编译应用程序

除了简单引用的限定外，DBA 还关注 `Precompile` 命令上可以指定的几个选项。图 9.9 显示了通用的

### 324 DB2 通用数据库：Linux、UNIX 和 Windows

`PRECOMPILE` (`PREP`) 命令的语法，并突出显示 DBA 特别感兴趣的选项。

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_341_0.png)

图 9.9 预编译应用程序。

`PRECOMPILE` 或 `PREP` 可以互换使用。在执行此命令之前必须存在数据库连接。语法允许指定许多选项，但并非所有情况下都需要。作为一个简单的示例，考虑以下：

```
db2 connect to
db2 prep myapp.sqc bindfile
db2 connect
```

- 使用 `BINDFILE` 选项和 `PACKAGE` 选项。
- 省略 `BINDFILE` 选项。

通过 `USING` 选项提供了显式命名绑定文件/包的能力。然而，并不建议这样做，因为默认名称可以与原始源关联。例如，假设你正在准备 `myapp.sqc`——默认绑定文件将是 `myapp.bind`，默认包将是 `myapp`。

`BLOCKING` 允许从服务器到客户端的数据传输以多行为单位进行，而不是逐行。有关上述 `BLOCKING` 设置的详细信息将在本书后部分提供。

## 应用替代方案 | 325

如果在 `EXPLAIN` 参数上选择了 `YES` 选项，`EXPLAIN` 将解释表中存储包中每个 SQL 语句的访问计划。`ALL` 值将对每个有效的 SQL 语句收集信息。即使 `CURRENT EXPLAIN SNAPSHOT` 设置为 `NO`，运行时也会为动态 SQL 收集信息。`DRDA` 不支持此选项的 `ALL` 值。

`EXPLAIN` 参数上的 `NO` 选项意味着不会收集 `EXPLAIN` 信息。

`EXPLSNAP` 决定是否在解释表中存储 Snapshot。`YES` 指定仅解释静态语句。`NO` 禁用创建 Snapshot。

`ISOLATION` 决定此应用程序与其他应用程序的更改的隔离程度。此选项影响行锁的获取和持续时间。选项是游标稳定（`CS`）、重复读（`RR`）、读取稳定（`RS`）和未提交读（`UR`）的缩写。

`QUERYOPT` 决定应执行的优化级别。值越高（最高 9），考虑的访问路径越多。`DRDA` 环境下的预编译命令具有特定环境的选项。此外，预编译命令还有其他选项。

## 绑定应用程序

如果你选择了 `bindfile` 选项，你需要在以后某个点使用 `BIND` 命令绑定包。在这里我们介绍 `BIND` 命令的语法。注意，在 `BIND` 上指定的选项将覆盖在 `PRECOMPILE` 上指定的选项。

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_342_0.png)

图 9.10 绑定应用程序。

### 326 | DB2 通用数据库：Linux、UNIX 和 Windows 管理

在执行 `BIND` 命令之前，必须存在数据库连接。该语法允许指定许多选项，但并非所有情况下都需要指定所有选项。作为一个简单的示例，请考虑以下内容。

```
db2 connect to musicdb
db2 bind myapp.bind blocking all
db2 connect reset
```

这将绑定指定的 bind 文件中的语句，并使用该选项阻塞所有不可显式更新的游标。

此命令上指定的文件名必须具有 `bind` 扩展名。通过指定一个实际上是 bind 文件列表的文件名，可以绑定多个包。指定列表的语法是在列表名称前加一个符号 `@`。列表文件中的 bind 文件根据以下语法指定：

```
first.bnd+second.bnd+
third.bnd+(etc) n.bnd+
last.bind
```
