

# 964

# nismatch, nisgrep

-c
仅打印匹配搜索标准的条目计数。

-h
在匹配的条目之前显示一个标题行，该行包含表列的名称。

-i
在比较时忽略大小写。

-M
仅限主服务器。将查询发送到命名数据的主服务器。此选项可确保看到最新的信息，但可能以主服务器忙碌为代价。

-o
显示匹配的 NISM+ 对象的内部表示。

-P
遵循连接路径（concatenation path）。指定如果初始搜索失败，则查询应遵循表的连接路径。

-s sep
指定用于分隔表列的字符。如果未指定字符，则使用表的默认分隔符（空格）。

-v
在显示匹配的条目时，不要抑制二进制数据的输出。在没有此选项的情况下，二进制数据将显示为字符串 *BINARY*。

# 示例

以下示例在 `zotz.domain` 的 `org_dir` 子目录下搜索名为 `passwd` 的表。它返回用户名为 `skippy` 的条目。在以下示例中，所有工作均在服务器上完成。

```
castle% nismatch name=skippy passwd.org_dir.zotz.com.
```

以下示例与上面类似，不同在于使用 `nisgrep` 查找名为 `passwd` 的表中所有使用 `ksh(1)` 或 `csh(1)` 的用户。

```
castle$ nisgrep shell=[ck]sh passwd.org_dir.zotz.com.
```

# 环境变量

NIS_PATH
如果设置此变量且 NIS+ 名称是完全限定的，则搜索每个目录直到找到对象为止（参见 `nisdefaults(1)`）。

# 退出状态

0
成功匹配某些条目。

1
成功搜索表但未找到匹配项。

2
发生错误条件。同时也打印了错误信息。

# 属性

有关以下属性的描述参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUN+wisu |

# nismkddir 965

# 另请

niscat(1), nisdefaults(1), nisls(1), nistbladm(1), nis_objects(3NSL), attributes(5)

# 诊断

尝试为搜索分配内存失败。

tablename 不是一个表。

名为 tab 的对象不是表对象。

无法编译正则表达式

`keypat` 中的正则表达式格式不正确。

未找到列：colname

在名为 `tablename` 的表中不存在名为 `colname` 的列。

# nismkddir — 创建 NIS+ 目录

# 语法

```
/usr/bin/nismkddir [-D defaults] [-m hostname] [-s hostname] dirname
```

# 描述

使用 `nismkddir` 命令在现有域内创建 NIS+ 目录。你也可以使用它来创建副本目录。如果不带选项，此命令将创建一个与其父目录具有相同主和副本的子目录。

建议使用 `nisserver(1)` 创建一个由 `org_dir` 和 `groups_dir` 子目录组成的指定目录的 NIS+ 域。

创建目录时受控制的两个主要方面是其访问权限和复制程度。

> 注意：提供 NIS+ 目录的主机必须是其所服务的上方目录的 NIS+ 客户端。该规则的例外是根 NIS+ 服务器，它们既是同一个 NIS+ 目录的客户端也是服务器。

当主机的默认域与执行命令的客户端上的默认域不同时，作为 `-s` 或 `-m` 选项参数提供的主机名必须是完全限定的。

当此命令更新受影响 NIS+ 服务器的提供列表时，可能会应用特殊的每主机和每目录访问限制。参见 Solaris 8 版本中新增的 `nisopaccess(1)`。

# 选项

-D defaults 指定在创建新目录时使用的另一组默认值。默认字符串是一系列由冒号分隔的令牌（tokens）。这些令牌代表了用于通用对象属性的默认值。所有合法的令牌均见下文描述。

ttl=time 为由此命令创建的对象设置默认的生存时间（TTL）。按 `nisttl(1)` 命令定义的格式指定时间值。默认值为 12 小时。

owner=ownername 指定 NIS+ 主体所有者 `ownername` 应拥有创建的对象。该值的默认值是执行命令的主体。

group=groupname 指定组 `groupname` 应为创建的对象的组所有者。默认值为空。

access=rights 指定授予给定对象的访问权限集。按 `nischmod(1)` 命令定义的格式指定权限值。默认值为 `is --rmcdir--r--r---`。

-m hostname 如果名为 `dirname` 的目录不存在，则创建一个非的新目录，并将 `hostname` 作为其主服务器。如果目录 `dirname` 存在，则名为 `hostname` 的主机将成为其主服务器。

-s hostname 指定主机 `hostname` 是名为 `dirname` 的现有目录的副本。

# 操作数

dirname 要创建目录的完全限定 NIS+ 名称。

# 示例

以下示例在 `foo.com.` 域下创建一个新目录 `bar`，它与 `foo.com.` 目录共享相同的主和副本。

```
castle@ nismkd bar.foo.com.
```

以下示例在 `foo.com.` 域下创建一个非副本的新目录 `bar.foo.com.`。

```
castle@ nismkdir -m myhost. bar.foo.com.
```

以下示例为 `bar.foo.com.` 目录添加一个副本服务器。

```
castle@ nismkdir -s replica.foo.com. bar.foo.com.
```

# nisopaccess

# 环境变量

NIS_DEFAULTS
指定一个覆盖 NIS+ 标准默认值的默认字符串。如果你使用 `-D` 选项，则这些值将同时覆盖 `NIS_DEFAULTS` 变量和默认值。

NIS_PATH 如果设置此变量且 NIS+ 目录名称不是完全限定的，则搜索每个指定的目录直到找到目录为止。参见 `nisdefaults(1)`。

# 退出状态

- 0 成功。
- 1 失败。

# 属性

有关以下属性的描述参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUMnisu |

# 另请

nis+(1), nischmod(1), nisctl(1), nisdefaults(1), nisls(1), nisopaccess(1), nisrmdir(1), nisserver(1), attributes(5)

# nisopaccess — NIS+ 操作控制

# 语法

```
/usr/lib/nis/nisopaccess [-v] directory operation
/usr/lib/nis/nisopaccess [-v] [-r] directory operation
/usr/lib/nis/nisopaccess [-v] directory [operation]
```

# 描述

使用 Solaris 8 版本新增的 `nisopaccess` 命令控制对 NIS+ 的访问。
大多数 NIS+ 操作通过其对象隐含访问控制。例如，要读取一个条目，你对该条目具有读取权限。然而，某些 NIS+ 操作默认不进行访问检查并允许所有人访问，如下所示。

使用的操作示例

```
NIS_CHECKPOINT
nisping -Ca
```

# 操作示例

NIS_CPTIME nisping, rpc.nisd

NIS_MKDIR nismdir

NIS_PING nisping, rpc.nisd

NIS_RMDIR nismdir

NIS_SERVSTATE nisbackup, nisrestore

NIS_STATUS nisstat, rpc.nisw

你可以使用 nisaccess 命令对这些操作执行访问控制。

将目录参数作为完全限定名称指定，nisaccess 将被应用。作为简写，如果目录名称没有以点结尾（例如 `org_dir`），则将附加域名。域名也会附加到部分路径如 `org_dir.xyz`。

操作参数可以使用大小写；但是你不能省略 `NIS_` 前缀。例如，你可以指定 `NIS_PING` 为 `nis_ping`、`PING` 或 `ping`。

按 `nischmod(1)` 命令定义的格式指定权限。由于使用读取（r）权限来决定谁有权操作，你可以使用修改和删除权限来控制谁可以访问操作。

> 注意 访问控制是通过在应应用访问控制的每个 NIS+ 目录创建一个名为 `proto_op_access` 的 NIS+ 表实现的。你可以使用普通的 NIS 命令操作它。然而，nisaccess 是 NIS+ 操作控制的支持接口。

每个操作的访问检查如下。当操作需要对所有目录进行访问检查时，如果其中一个目录禁止了该操作，则拒绝访问。

NIS_CHECKPOINT 检查目录，或者如果没有目录参数则检查所有目录（当 NIS_CHECKPOINT 由 `nisping -Ca` 命令发出时）。访问拒绝时返回 NIS_PERMISSION。

NIS_CPTIME 检查目录。访问拒绝时返回 0。

NIS_MKDIR 检查指定目录的父目录。访问拒绝时返回 NIS_PERMISSION。

如果父目录在本地不可用（即不是由其 rpc.nisd 服务），则 NIS_MKDIR 访问是允许的，但仅当此 rpc.nisd 是该目录的已知副本时才执行操作。

注意 NIS_MKDIR 操作并不创建 NIS+ 目录；它在合适的情况下添加到此 rpc.nisd 的提供列表中。

