
## 运行脚本

此脚本没有参数，任何人或 `root` 都可以运行，产生可用磁盘空间的简洁摘要。

## 结果

对于生成早期 `df` 输出的同一系统，此脚本报告的结果与列表 5-10 所示的类似。

```
$ diskspace
96199 MB (93.94GB) of available disk space
```

Listing 5-10: 测试 `diskspace` 脚本

另一个需要考虑的问题是，了解所有设备（包括那些无法增长的分区，如 `/boot`）更有用，还是仅报告用户卷就足够了？如果是后者，你可以在调用 `df` 之后立即调用 `grep` 来改进此脚本。使用 `grep` 配合所需的设备名称来包含特定设备，或者使用 `grep -v` 过滤掉你不需要的特定设备名称。

### #39 实现一个安全的 locate

`locate` 脚本（第 68 页的第 19 脚本）很有用，但存在一个安全问题：如果以 `root` 身份运行构建过程，它会构建整个系统中所有文件和目录列表，无论所有者是谁，这允许用户看到他们没有权限访问的目录和文件名。构建过程可以以普通用户运行（如 OS X 所示，以 `nobody` 用户运行 `locatedb`），但这样做不对，因为你希望能够在目录树的任何位置定位文件，无论 `nobody` 是否对这些特定的文件和目录有访问权限。

解决这一困境的方法是扩展数据库，使每个条目都拥有所有者、组和权限字符串。这样，`mlocateddb` 本身仍然是不安全的，除非 `locate` 脚本以 `setid` 或 `setgid` 脚本的形式运行，而为了系统安全，必须不一切避免这样做。

折中方案是为每个用户准备一个独立的 `locatedb`。这不是一个很坏的选择，因为只有实际使用 `locate` 命令的用户才需要个人数据库。一旦调用，系统会在用户的家目录中创建一个 `locatedb` 文件，并且 `cron` 任务可以很好地更新这些 `locatedb` 文件以保持同步。当用户第一次运行安全 `locate` 脚本时，它会输出一条警告信息，提醒他们可能只能看到公开访问的文件匹配。从第二天开始（取决于 `cron` 调度），用户将获得他们的个性化结果。

#### 代码

实现安全的 `locate` 需要两个脚本：数据库构建器 `mlocateddb`（如列表 5-11 所示）和实际的搜索工具 `locate`（如列表 5-12 所示）。

```bash
#!/bin/bash
```

```
# mlocateddb--以用户 nobody 的身份构建中央公共 locate 数据库
# 同时遍历每个用户的家目录，寻找
# 包含 locatedb 文件的目录。如果找到，将为该用户创建一个
# 额外的私有 locate 数据库版本。
```

`slocateddb`="/var/locate.db"

`slocateddb`="`.slocateddb`"

```bash
if [ "$(id -nu) != "root" ]; then
  echo "$0: Error: 你必须以 root 身份运行此命令。" >&2
  exit 1
fi
```

```bash
if [ "$(grep '^nobody': '/etc/passwd') = "" ]; then
  echo "$0: Error: 你必须拥有用户 'nobody' 账户 >&2
  echo "以创建默认的 slocated 数据库。" >&2
  exit 1
fi
```

`cd /` # 绕过 `su` 权限问题。

# 首先创建或更新数据库。

`su -fm nobody -c "find / -print" > $slocateddb 2>/dev/null`

`echo "building default slocated database (user = nobody)"`

`echo ... result is $(wc -l < $slocateddb) lines long.`

# 现在遍历系统上的用户账户，查看谁的家目录中有

# .slocated 文件。

`for account in $(cut -d: -f1 /etc/passwd)`

`do`

`homedir="$(grep '^$account:' /etc/passwd | cut -d: -f6)"`

`if [ "$homedir" = "" ]; then`

`continue # 拒绝为 root 目录构建。`

`elif [ -e $slocateddb ]; then`

`echo "building slocated database for user $account"`

`su - $account -c "find / -print" > $homedir/$slocateddb 2>/dev/null`

`chmod 600 $slocateddb`

`chown $account $homir/$slocateddb`

`echo ... result is $(wc -l < $homedir/$slocateddb) lines long.`

`fi`

`done`

```

列表 5-11：`msocateddb` 脚本

`slocated` 数据库本身（如列表 5-12 所示）是 `slocated` 数据库的用户界面。

```bash

#!/bin/bash

# locate--尝试在用户的安全 lococated 数据库中搜索

# 指定模式。如果模式不匹配，则意味着数据库

# 不存在，它会输出警告并创建一个。如果个人的 .slocateddb

# 为空，它将使用系统数据库 slocated 代替。

```

```bash

slocateddb="/var/locate.db"

slocateddb="$HOME/.slocateddb"

```

```bash

if [ ! -e $slocateddb -o "--explain" ]; then

  cat << "EOF" >&2

警告: 安全 locate 为每个用户提供私有数据库，而你的

数据库尚未创建。在创建之前（可能可能在今晚），

我将仅使用公共 locate 数据库，它将向你显示

公开访问的匹配，而不是显式对账户 ${USER:$SLOGAME} 可用的；

EOF

fi

```

```bash

if [ "$1" = "--explain" ]; then

  exit 0

fi

```

```bash

# 在离开之前，创建一个 .slocatedb 文件，以便 cron 在

# 下一次运行 mlocateddb 运行时填充它。

```

```bash

touch $slocateddb # mlocateddb 将通过构建它。

chmod 600 $slocateddb # 从正确的权限开始。

```

```bash

elif [ -z "$1" ]; then

  slocateddb=$slocateddb

else

  echo "警告: 使用公共数据库。使用 \$0 --explain 查看详情。" >&2

fi

```

```bash

if [ -z "$1" ]; then

  echo "用法: $0 pattern" >&2

  exit 1

fi

```

```bash

exec grep -i "$1" $slocateddb

```

列表 5-12：`locate` 脚本，`mlocdb` 的配套脚本

## 工作原理

`mlocateddb` 脚本围绕这样一个观点：以 `root` 身份运行的进程可以通过 `su -fm user` 变为另一个用户的所有。它可以以该用户的身份在用户的家目录下运行，创建一个特定的用户文件数据库。但是，`su` 命令在脚本中比较棘手，因为默认情况下，它只更改有效用户。

## 运行脚本

`mlocateddb` 脚本围绕这样一个观点：以 `root` 身份运行的进程可以通过 `su -fm user` 变为另一个用户的所有。它可以以该用户的身份在用户的家目录下运行，创建一个特定的用户文件数据库。但是，`su` 命令在脚本中比较棘手，因为默认情况下，它只更改有效用户。

## 结果

为 `nobody`（公共数据库）和用户 `taylor` 构建 `slocate` 数据库产生了列表 5-13 所示的输出。

```
# mslateddb
building default slocated database (user = nobody)
... 99809 lines long.
building slocate database for user taylor
... 99809 lines long.
```
