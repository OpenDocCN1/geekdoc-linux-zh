
如果 NIS+ 主服务器未运行，此命令将失败。

> 注意 — 当此命令更新受影响 NIS+ 服务器的提供列表时，可能会存在特定的服务器和目录访问限制。

更多信息请参见 `nisopaccess(1)`。

### 选项

- `-f`

强制命令成功，即使它可能无法联系受影响的副本。当已知副本已宕机且无法响应删除通知时，使用此选项。当副本最终重启时，它会读取更新后的目录对象，注意到它不再是该目录的副本，并停止响应对该目录的查找。你可以通过删除 `/var/nis` 目录中相应的文件来手动清理持有这些现已删除目录的文件（更多信息请参见 `nfiles(4)`）。

- `-i`

类似于 `rm` 命令，在删除目录前交互式地请求确认。如果由 `dirname` 指定的不是完全限定名称，则对该目录强制开启此选项。此选项可防止删除意外的目录。

- `-s hostname`

移除 `hostname` 作为名为 `dirname` 的目录的副本。如果不存在此选项，则移除该目录的所有副本和主服务器，并从命名空间中移除该目录。

### 操作数

- `dirname`

一个存在的 NIS+ 目录。

### 示例

以下示例从 `foo.com` 域下删除目录 `bar`。`castle@ nisrmdir bar.foo.com.`

以下以下示例移除一个提供 `bar.foo.com.` 目录服务的副本。`castle@ nisrmdir - replica.foo.com. bar.foo.com.`

以下示例强制从命名空间中删除 `bar.foo.com.` 目录。`castle@ nisrmdir -f bar.foo.com.`

## 环境变量

- `NIS_PATH`

当此变量已设置且 NIS+ 名称不是完全限定的时，将搜索每个指定的目录直到找到对象（参见 `nisdefaults(1)`）。

## 退出状态

- `0`

成功。

- `1`

失败。

## `nistbladm`

### 属性

后续属性的描述请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | `SUMwnisu` |

# 阅

`nis+(1)`, `nisdefaults(1)`, `nisopaccess(1)`, `nisrm(1)`, `nisfiles(4)`, `attributes(5)`

# `nistbladm` — 管理 NIS+ 表

### 概要

```
/usr/bin/nistbladm -a|-A [-D defaults] colname=value... tablename
/usr/bin/nistbladm -a -A [-D defaults] indexname
/usr/bin/nistbladm -c [-D defaults] [-p path] [-s sep] type
classname=[flags] [access...] tablename
/usr/bin/nistbladm -d tablename
/usr/bin/nistbladm -e|E colname=value... indexname
/usr/bin/nistbladm -m colname=value... indexname
/usr/bin/nistbladm -r -R colname=value... tablename
/usr/bin/nistbladm -r -R indexname
/usr/bin/nistbladm -u [-p path] [-s sep] [-t type] [access...]
tablename
```

### Description

使用 `nistbladm` 命令管理 NIS+ 表。它执行五种操作：

- 创建表。
- 删除表。
- 向表中添加条目。
- 修改表条目。
- 从表中移除条目。

虽然 NIS+ 对表或条目的的大小没有限制，但表的设计支持总大小为 10 兆字节的对象。如果超过了上述要求，建议你存储数据的指针而不是存储数据本身。

在创建表时，你必须指定表类型以及一系列列定义。

## `nistblad`

`type` 是存储在表的字符串，稍后用于验证添加的条目是否正确。列定义使用以下语法：

```
colname=[flags] {access}
```

`flags` 是以下组合：

- `S` 可以对值进行搜索（参见 `nismatch(1)`）。
- `I` 忽略大小写（仅与 `S` 结合）。
- `C` 加密列值。
- `B` 二进制数据（不与 `S` 结合）。如果没有设置，则预期列值为空终止的 ASCII 字符串。
- `X` XDR 编码数据（仅与 `B` 结合）。

`access` 由 `nismod(1)` 命令定义的格式指定。操作条目时，此命令有两种条目名称的形式。第一种使用空格分隔的 `colname=value` 对来指定条目的列值。第二种是 NIS+ 索引名称 `indexname`，格式如下：
`[colname=value, ...], tablename`

### 选项

- `-a` 向 NIS+ 表添加条目。小写 `a` 和大写 `A` 的区别在于对现有条目的处理。条目的内容由命令行上的 `column=value` 对指定。注意，在向表中添加条目时必须为所有列指定值。

通常情况下，如果你尝试向已存在条目的表添加条目，NIS+ 会报告错误。此功能防止多个方添加重复条目并导致其中一个被覆盖。大写 `A` 指定如果条目已存在则进行添加。该选项类似于对条目执行修改操作。

- `-c` 在命名空间中创建一个名为 `tableName` 的表。创建的表必须至少有一列，且至少有一列是可搜索的。

- `-d` 销毁表 `tableName`。被销毁的表必须为空。先用 `-R` 选项删除表的内容。

- `-D defaults` 创建对象时，指定在此操作中使用的另一组默认值。默认字符串是由于冒号分隔的一系列令牌。这些令牌代表用于通用对象属性的默认值。所有合法的令牌下文所示。

# 978 `nistbladm`

`ttl=time`

为由此命令创建的对象设置默认生存时间（TTL）。请按照 `nischtl(1)` 命令定义的格式指定时间值。默认值为 12 小时。

`owner=ownername`

指定由 NIS+ 实体所有者 `ownername` 拥有创建的对象。通常，此值与执行命令的主所有者相同。

`group=groupname`

指定组 `groupname` 应为创建对象的组所有者。默认值为空（null）。

`access=rights`

指定要授予给定对象的访问权限集。请按照 `nischmod(1)` 命令定义的格式指定权限值。默认值为 `---rmcdr---r---`。

- `-e|E`

编辑由 `indexedname` 指定表中的条目。`indexedname` 必须唯一标识一个条目。可以编辑某个列中的值，这可能会更改条目的索引名称。

更改（`colname=value`）可能会影响表中的其他条目，如果该更改导致条目的索引名称与 `indexedname` 不同且与另一个现有条目匹配。在这种情况下，`-e` 选项失败并报告错误。`-e` 选项强制用新条目替换现有条目（实际上删除两个旧条目并添加一个新条目）。

- `-m`

`-E` 的别名。此选项已被 `-e` 选项取代。

- `-p path`

在创建或更新表时，指定表的搜索字符。当调用 `nis_list()` 函数时，可以指定标志 `FOLLOW_PATH`，以告诉客户端库：如果所使用的表搜索标准没有产生任何条目，则继续搜索表。路径由表名称的有序列表组成，并用冒号分隔。路径中的名称必须是全限定的。

在创建或更新表时，指定表的分割符。`niscat(1)` 在标准输出上显示表时会使用该分隔符。它的作用是在表处于 ASCII 格式时分离列数据。默认值为空格。

# `nistblad`

## 979

- `-r|R`

从表中删除条目。通过命令行上的系列 `column=value` 键对或通过指定为 `entryname` 的索引名称来指定条目。小写 `r` 和大写 `R` 的解释区别在于对非唯一条目指定的处理方式。通常情况下，NIS+ 服务器允许在为条目指定的搜索标准解析为表中多个条目时尝试删除条目。然而，你有时可能希望能够删除多个条目，例如，当你正尝试删除表中的所有条目时。在这种情况下，使用大写 `R` 将强制 NIS+ 服务器删除所有匹配的搜索标准。如果 `criteria` 为空且未指定列值，则表中的所有条目将被删除。

- `-t type`

在更新表时，指定类型。更新表的属性。此选项允许更改表的拼接路径（`-p`）、使用 `(-s)` 指定的分割符、访问权限以及表类型（`-t`）。列的数或可搜索的列均无法更改。

- `-u`

### 示例

以下示例在 `foo.com` 目录下创建一个名为 `hobbies` 的表，该表来自 `hobby-tbl`，具有两个可搜索列：`name` 和 `hobby`。

```
castle nistblad -c hobby_tbl name=S,a+r,o+m hobby=S,a+r

hobbies.foo.com.
```
