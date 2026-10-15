
```
ls -l /sbin/rc2.d | awk '{ printf("%-15s %3s %s\n", $9, $10, $11) }'

K00lpd    -> ../init.d/lpd
K03lat    -> ../init.d/lat
K04dhcp   -> ../init.d/dhcp

S25nologin -> ../init.d/enlogin
S35streams -> ../init.d/streams
S45atm     -> ../init.d/atm
```

## /etc/rc.config 中的执行流程

![](img/a0df85c2e542a8d6c913113908553aa4_150_0.png)

图 6-3：运行时配置执行流程

以 “K” 开头的链接表示与这些链接关联的脚本将在系统从较高运行级别更改到当前运行级别时执行。

以 “S” 开头的链接在系统从较低运行级别更改到当前运行级别时执行。这些脚本使用由 `/etc/rc.config*` 脚本设置的变量。

图 6-3 描述了 `rc.config` 文件的执行流程。如图所示，从 `/sbin/rc?` 脚本执行的 `init` 脚本执行 `rc.config`，后者又在设置任何变量之前调用 `rc.config.common`。`rc.config.common` 文件会立即调用 `rc.config.site`（如果存在）。一旦 `rc.config.site` 返回到 `rc.config.common`，则 `rc.config.common` 会设置其文件中的变量并返回到 `rc.config`。最后，`rc.config` 设置其变量。

如果一个变量在多个文件中被设置会怎样？

- 如果一个变量在 `rc.config` 和 `rc.config.common` 中都被定义，则使用 `rc.config` 中的值。
- 如果一个变量在 `rc.config.common` 和 `rc.config.site` 中都被定义，则使用 `rc.config.common` 中的值。

### 6.1.2.1 使用 rcMgr(8) 命令

`rcMgr` 命令是修改 Tru64 UNIX 上 `rc.config` 文件的推荐方法。使用 `rcMgr` 可以让你设置变量以及检索（get）变量。`rcMgr` 命令有四个命令选项，允许你指定使用哪个 `rc.config` 文件。参见表 6-1。

让我们看看 `rcMgr` 在设置和检索一些变量时如何响应。

首先，让我们在 `rc.config` 和 `rc.config.common` 中都设置同一个变量。

```
# rcMgr set TCRHB from Member-specific file
# grep TCRHB /etc/rc.config*
/etc/rc.config:TCRHB="from Member-specific file"
/etc/rc.config:export TCRHB
```

```
# rcMgr -c set TCRHB from Cluster-common file
# grep TCRHB /etc/rc.config*
/etc/rc.config:TCRHB="from Member-specific file"
/etc/rc.config:export TCRHB
/etc/rc.config.common:TCRHB="from Cluster-common file"
/etc/rc.config.common:export TCRHB
```

### rcmgr (8) 命令选项

| 选项 | 描述 | 示例 | 解释 |
|---|---|---|---|

| c | 使用 `rc.config.common` | # `rcmgr -c set TCRHB 1` | 将 "TCRHB" 变量的值设置为 "1"，保存在 `rc.config.common` 中。 |
| h | 使用 `memberid` 等于 "-h" 后输入的 id 的成员的 `rc.config`。 在 `get` 或 `mget` 时也包括 `rc.config.common` 和 `rc.config.site` | # `rcmgr -h 3 get GATED` | 从 `member3` 的 `rc.config` 文件中获取 "GATED" 变量。 |
| n | 使用 `memberid` 等于 "-n" 后输入的 id 的成员的 `rc.config`。 | # `rcmgr -n 2 mget` | 获取 `member2` 的 `rc.config` 文件中设置的所有变量。 |
| s | 使用 `rc.config.site`（如果存在） | # `rcmgr -s get TCRHB` | 从 `rc.config.site`（如果存在）中获取变量 "TCRHB"。 如果站点特定文件不存在，则返回以下错误："Error: Cannot open /etc/rc.config.site" |

## 表 6-1：rcmgr 命令选项

现在我们已在两个文件中设置了变量，让我们看看使用各种命令开关时返回什么值。

"-c" 开关：

```
# rcmgr -c get TCRHB
from Cluster-common file
```

"-h" 开关：

```
# rcmgr -h 0 get TCRHB
from Member-specific file
```

## 无开关：

```
# rcmgr get TCRHB
from Member-specific file
```

现在让我们从 `/etc/rc.config` 中删除该变量，然后重复测试。

```
# rcmgr delete TCRHB
```

验证该变量已不再存在于 `/etc/rc.config` 中。

```
# grep TCRHB /etc/rc.config*
/etc/rc.config.common:TCRHB="from Cluster-common file"
/etc/rc.config.common:export TCRHB
```

我们将跳过 "-c" 测试，因为它将返回 `/etc/rc.config.common` 的内容，正如您从之前的输出中看到的那样，变量仍在公共文件中定义。

## "-h" 开关：

```
# rcmgr -h 0 get TCRHB
from Cluster-common file
```

## "-n" 开关：

```
# rcmgr -n 0 get TCRHB
< no output >
```

## 无开关：

```
# rcmgr get TCRHB
from Cluster-common file
```

请注意，"-n" 开关仅搜索成员特定的文件。 然而，"-h" 开关首先搜索 `rc.config`，然后如果变量不在其中，它将搜索 `rc.config.common` 文件。 当未提供开关时，将执行 "-n" 和 "-h" 搜索序列。 有关 `rcmgr` 命令的更多信息，请参阅相关参考页面。

## 6.2 文件系统层次结构

Tru64 UNIX 版本 5 中的文件系统层次结构与版本 4 的布局相比略有修改。

版本 5 的文件系统布局如图 6-4 所示。 根目录 (`/`)、`/usr` 和 `/var` 目录都新增了一个名为 `/cluster` 的目录。 在每个 `cluster` 目录下是 `members` 目录。 `members` 目录是成员特定目录所在的位置。 如图所示，每个 `members` 目录目前包含两个文件：

- `member`
- `member0`

`member0` 文件是独立系统的成员特定目录，而 `member` 文件是一个成员中立的身份链接，即 CDSL，用于快速访问该成员的成员特定目录。

```
# for i in /usr /var
> do
> cd $i(/)/cluster/members
> print "$i(${PWD})"
> ls -ld *
> done

[/cluster/members]
lrwxr-xr-x 1 root system 6 Jan 26 08:46 member -> (memb)
drwxr-xr-x 9 root system 8192 Feb 6 18:41 member0

[/usr/cluster/members]
lrwxr-xr-x 1 root system 6 Jan 26 08:47 member -> (memb)
drwxr-xr-x 7 root system 8192 Jan 26 08:47 member0

[/var/cluster/members]
lrwxr-xr-x 1 root system 6 Jan 26 08:51 member -> (memb)
drwxr-xr-x 22 root system 8192 Feb 6 17:02 member0
```

图中另一个 CDSL 是根目录 (`/`) 中的一个隐藏文件，名为 ".local.."。

```
# ls -l /.local.. | awk '{ print $9,$10,$11 }'
/.local.. -> cluster/members/(memb)
```
