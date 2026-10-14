

# rcmgr (8) 命令选项

| 选项 | 描述 | 示例 | 解释 |
|---|---|---|---|
| c | 使用 rc.config.common | # rcmgr -c set TCRHB 1 | 将 "TCRHB" 变量的值设置为 "1"，保存在 rc.config.common 中。 |
| h | 使用 memberid 等于 "-h" 后输入的 id 的成员的 rc.config。 在 get 或 mget 时也包括 rc.config.common 和 rc.config.site | # rcmgr -h 3 get GATED | 从 member3 的 rc.config 文件中获取 "GATED" 变量。 |
| n | 使用 memberid 等于 "-n" 后输入的 id 的成员的 rc.config。 | # rcmgr -n 2 mget | 获取 member2 的 rc.config 文件中设置的所有变量。 |
| s | 使用 rc.config.site（如果存在） | # rcmgr -s get TCRHB | 从 rc.config.site（如果存在）中获取变量 "TCRHB"。 如果站点特定文件不存在，则返回以下错误："Error: Cannot open /etc/rc.config.site" |

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

现在让我们从 /etc/rc.config 中删除该变量，然后重复测试。

```
# rcmgr delete TCRHB
```

验证该变量已不再存在于 /etc/rc.config 中。

```
# grep TCRHB /etc/rc.config*
/etc/rc.config.common:TCRHB="from Cluster-common file"
/etc/rc.config.common:export TCRHB
```

我们将跳过 "-c" 测试，因为它将返回 /etc/rc.config.common 的内容，正如您从之前的输出中看到的那样，变量仍在公共文件中定义。

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

请注意，"-n" 开关仅搜索成员特定的文件。 然而，"-h" 开关首先搜索 rc.config，然后如果变量不在其中，它将搜索 rc.config.common 文件。 当未提供开关时，将执行 "-n" 和 "-h" 搜索序列。 有关 rcmgr 命令的更多信息，请参阅相关参考页面。

## 6.2 文件系统层次结构

Tru64 UNIX 版本 5 中的文件系统层次结构与版本 4 的布局相比略有修改。

版本 5 的文件系统布局如图 6-4 所示。 根目录 (/)、/usr 和 /var 目录都新增了一个名为 /cluster 的目录。 在每个 cluster 目录下是 members 目录。 members 目录是成员特定目录所在的位置。 如图所示，每个 members 目录目前包含两个文件：

- member
- member0

member0 文件是独立系统的成员特定目录，而 member 文件是一个成员中立的身份链接，即 CDSL，用于快速访问该成员的成员特定目录。

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

图中另一个 CDSL 是根目录 (/) 中的一个隐藏文件，名为 ".local.."。

```
# ls -l /.local.. | awk '{ print $9,$10,$11 }'
/.local.. -> cluster/members/(memb)
```

此示例说明了快速显示文件名及其链接的方法。 由于此命令在整章（以及本书其余部分）中都会很有用，让我们创建一个函数来使用此命令，以便您可以减少输入。 为了使此更改更永久，您可以将其放在您的 ".profile" 文件中。 注意：此特定函数在 Korn shell 中有效。

