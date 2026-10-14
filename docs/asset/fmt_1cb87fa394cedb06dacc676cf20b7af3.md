
- `NIS_MODERROR`: 当组在命令执行期间被其他人修改时，返回此错误。重新执行命令并可选地检查组成员列表。

## `nisln` — 符号链接 NIS 对象

### 概要

```
/usr/bin/nisln [-L] [-D defaults] name linkname
```

### 描述

`nisln` 命令将名为 `name` 的 NIS+ 对象链接到 NIS+ 链接 `name`。如果 `name` 是一个索引名称（参见 `mismatch(1)`），则链接指向 NIS 表中的条目。想要在命名服务中查找信息的客户端可以使用 `FOLLOW_LINKS` 标志，强制客户端库跟踪到它们所指向的名称。此外，所有 NIS+ 管理命令都接受 `-L` 选项，表示它们应该跟踪链接 (5)。

注意 — 在创建链接时，`nisln` 会验证被链接的对象是否存在。一旦创建了链接，你就可以删除或替换被链接的对象。此时，链接将失效，尝试跟踪该链接将向客户端返回 `NIS_LINKNAMEERROR`。当表中的 `path` 属性指定为链接而非另一个表时，如果调用 `nislist()` 时存在 `FOLLOW_LINKS` 标志（参见 `nis_tables(3)`），则会跟踪链接；如果不存在该标志，则会被忽略。如果标志存在但链接不再有效，将向系统日志记录器发送警告并忽略该链接。

### 选项

- `-D defaults` 指定用于创建链接对象的另一组默认值。默认值字符串是一系列由冒号分隔的令牌。这些令牌代表了用于通用对象属性的默认值。所有合法的令牌均见下文。

- `ttl=time` 为使用此命令创建的对象设置默认生存时间。你按照 `nisctl(1)` 命令定义的格式指定时间值。默认值为 12 小时。

- `owner=originalname` 指定 NIS+ 实体所有者 `name` 拥有创建的对象。通常，此值与执行命令的实体相同。

- `group=groupname` 指定组 `groupname` 为创建对象的所属组。默认值为空。

- `access=rights` 指定要授予给定对象的访问权限集。你按照 `nismod(1)` 命令定义的格式指定权限值。默认值为 `----rmcdr---r---`。

- `-L` 如果 `name` 本身是一个链接，则跟踪它到指向的被链接对象。新链接将指向该被链接对象而非 `name`。

### 示例

以下示例在 `foo.com` 域中创建一个名为 `hosts` 的链接，它指向 `hosts.bar.com.` 对象：

```
nisln hosts.bar.com. hosts.foo.com.
```

以下示例创建了一个 `example.sun.com.` 的链接，它指向 `eng.sun.com` 中 `hosts` 表中的一个条目：

```
nisln '[name=example],hosts.eng.sun.com.' example.sun.com.
```

## 环境变量

`NIS_PATH` 如果设置了此变量且 NIS+ 名称不是完全限定的，则搜索每个指定的目录直到找到对象为止 (`nisdefaults(1)`)

## 退出状态

- `0` 成功。
- `1` 失败。

## `nisis` 962

### 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 | 可用性 |
| :--- | :--- | :--- |

## 参见

`nisdefaults(1)`, `nismatch(1)`, `nismod(1)`, `niserror(1)`, `nisgroups(3)`, `attributes(5)`

## `nisls` — 列出目录内容

### 概要

```
/usr/bin/nisls [-d defaults] name
```

### 描述

使用 `nisls` 命令列出 NIS+ 对象的内容。如果 `name` 是目录，`nisls` 将列出内容。对于 NIS+ 对象，`nisls` 仅显示 `name`。

### 选项

- `-d defaults` 指定用于搜索的另一组默认值。
- `-g` 显示组而非所有者。
- `-m` 显示修改时间而非创建时间。
- `-M` 仅主。将查询发送到命名数据的主服务器。
- `-R` 递归列出。

## 环境变量

`NIS_PATH` 如果设置了此变量且 NIS+ 名称不是完全限定的，则搜索每个指定的目录直到找到对象为止 (`nisdefaults(1)`)。

## `nismatch`, `nisgrep`

### 状态

- `0` 成功。
- `1` 失败。

### 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 | 可用性 |
| :--- | :--- | :--- |

## 参见

`nisdefaults(1)`, `nisgrpd(1)`, `nismatch(1)`, `nisbladm(1)`, `nis_objects(3)`, `attributes(5)`

## `nismatch`, `nisgrep` — 搜索 NIS+ 表

### 概要

```
/usr/bin/nismatch [-AchNoPV] [-s sep] key tablename
/usr/bin/nismatch [-AchNoPV] [-s sep] colname=key... tablename
/usr/bin/nismatch [-AchNoPV] [-s sep] indexedname
/usr/bin/nisgrep [-AchNoPV] [-s sep] keypat tablename
/usr/bin/nisgrep [-AchNoPV] [-s sep] colname=keypat... tablename
```

### 描述

使用 `nismatch` 和 `nisgrep` 命令搜索 NIS+ 表。`nisgrep` 命令与 `nismatch` 命令的不同之处在于它能够接受正则表达式 `keypat` 而非简单的文本匹配。由于它使用了回调函数，因此不再局限于搜索表创建时可搜索的列。它比 `nismatch` 慢，但更灵活。

对于 `nismatch`，服务器执行搜索；对于 `nisgrep`，服务器返回所有可读条目，客户端执行匹配。

在两个命令中，参数 `tablename` 是要搜索的表的 NIS+ 名称。如果你在没有指定列名的情况下指定键或模式，则搜索第一列。可以使用 `colname=keysyntax` 搜索特定的命名列。

### 选项

- `-A` 返回表内的所有数据以及初始表拼接路径中所有表的数据。

## 964

# `nismatch`, `nisgrep`

- `-c`

仅打印匹配搜索标准的条目计数。

- `-h`

在匹配的条目之前显示一个标题行，该行包含表列的名称。

- `-i`

在比较时忽略大小写。

- `-M`

仅限主服务器。将查询发送到命名数据的主服务器。此选项可确保看到最新的信息，但可能以主服务器忙碌为代价。

- `-o`

显示匹配的 NISM+ 对象的内部表示。

- `-P`

遵循连接路径（concatenation path）。指定如果初始搜索失败，则查询应遵循表的连接路径。

- `-s sep`

指定用于分隔表列的字符。如果未指定字符，则使用表的默认分隔符（空格）。

- `-v`

在显示匹配的条目时，不要抑制二进制数据的输出。在没有此选项的情况下，二进制数据将显示为字符串 `*BINARY*`。

### 示例

以下示例在 `zotz.domain` 的 `org_dir` 子目录下搜索名为 `passwd` 的表。它返回用户名为 `skippy` 的条目。在以下示例中，所有工作均在服务器上完成。

```
castle% nismatch name=skippy passwd.org_dir.zotz.com.
```

以下示例与上面类似，不同在于使用 `nisgrep` 查找名为 `passwd` 的表中所有使用 `ksh(1)` 或 `csh(1)` 的用户。

```
castle$ nisgrep shell=[ck]sh passwd.org_dir.zotz.com.
```

## 环境变量

`NIS_PATH`

如果设置此变量且 NIS+ 名称是完全限定的，则搜索每个目录直到找到对象为止（参见 `nisdefaults(1)`）。

## 退出状态

`0`

成功匹配某些条目。

`1`

成功搜索表但未找到匹配项。

`2`

发生错误条件。同时也打印了错误信息。

### 属性

有关以下属性的描述参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUN+wisu |

# `nismkddir` 965

## 另请

`niscat(1)`, `nisdefaults(1)`, `nisls(1)`, `nistbladm(1)`, `nis_objects(3NSL)`, `attributes(5)`

### 诊断

尝试为搜索分配内存失败。

`tablename` 不是一个表。

名为 `tab` 的对象不是表对象。

无法编译正则表达式

`keypat` 中的正则表达式格式不正确。

未找到列：`colname`

在名为 `tablename` 的表中不存在名为 `colname` 的列。

# `nismkddir` — 创建 NIS+ 目录

### 语法
