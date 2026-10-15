
>> Just showing how a new version of a file can be created.

>> .

```
## 666 第 20 章 用于开发的 Linux 工具

done
$
```

### 检出特定版本的副本
在 RCS 中，你可以使用 `co` 命令配合 `-r` 选项检出文件的现有版本。如果检出的版本具有最高修订号，则提交时生成的新版本具有相同的发布号，但层级号（如果文件是特定发布版本的分支，则为序列号）会自动递增 1。如果检出的版本不是最新版本，则会生成文件的分支。

在下面的会话中，我们检出 `input.c` 的版本 1 进行编辑。默认情况下，`co` 命令总是检出发布版本的最高版本，在此处为版本 1.2。注意我们在上一节中使用了 `ci` 命令为该文件创建了新发布版本（发布 2）。`input.c` 存在更高的发布版本，因此 `ci` 命令在检出的层级创建了一个新分支，导致产生了版本 1.2.1.1。

```
$ co -r1 input.c

RCS/input.c,v --> input.c

revision 1.2 (locked)

done

$ vi input.c

... editing session

$ ci input.c

RCS/input.c,v <-- input.c

new revision: 1.2.1.1; previous revision 1.2

enter log message, terminated with single '.' or end of file

>> Just showing how a branch of a file can be created.

>>

done

$
```

要显式地创建 RCS 文件的分支，我们在 `ci` 命令中指定版本号及其分支号。在下面的示例中，我们为 `input.c` 修订号 2.1 创建分支 1，导致产生了文件的版本 2.1.1.1。

```
$ co -l1 input.c

RCS/input.c,v --> input.c

## 程序生成工具 667

revision 2.1 (locked)

done

$ vi input.c

... editing session

$ ci -r2.1.1 input.c

RCS/input.c,v <-- input.c; previous revision 2.1

new revision: 2.1.1;

enter log message, terminated with single '.' or end of file

>> Just how a branch of a file can be created.

>> .

done

$
```

图 20.7 展示了 `input.c` 修订号的关系。第一个数字（最左）是发布号，第二个数字是层级号，第三个数字是分支号，第四个数字（最右）是序列号。在接下来的章内练习中，你将使用 `co` 和 `ci` 命令创建文件的特定版本。

## 章内练习

20.10. 创建 `input.c` 的 1.2 和 2.1 版本。你使用哪个命令？

### 放弃修改
如果你对文件所做的修改没有效果，可以使用 `rcs` 工具撤销修改并检出文件。以下是 `rcs` 工具的简要描述。

## 689 rcs [options] file-list

**目的：** 该工具允许控制 RCS 文件，即允许更改属性。

常用的选项/功能：
- `-a[logins]` 将逗号分隔的列表 `logins` 中的登录名添加到访问列表中（即允许 `logins` 中的用户检出 `file-list` 中的可编辑版本并提交）。
- `-e[logins]` 从访问列表中移除逗号分隔的列表 `logins` 中的登录名（即不允许 `logins` 中的用户检出 `file-list` 中的可编辑版本）。
- `-l[rev]` 在不覆盖的情况下检出文件的版本 `rev`，即锁定版本 `rev`；使用最新版本 `rev`；`rev:rev` 表示从 `rev` 到 `rev` 的修订范围；`rev` 表示从包含 `rev` 的分支开始（并包括）`rev`。
- `-u[rev]` 解锁版本 `rev`：放弃文件的修改

当你使用 `co -1` 命令检出文件时，它是被锁定的，你可以编辑它，但 `ci` 命令不会提交对文件的修改。你可以使用 `rcs -u` 命令解锁已检出的文件。尽管你的目录中有一个检出的文件副本，但在解锁之前之后进行的任何修改都无法提交到 RCS 文件。为了能够提交对文件的修改，你必须解锁它或重新检出以覆盖现有的（解锁的）版本。在下面的会话中，我们使用 `co -l` 命令检出 `input.c` 文件，保存备份副本 `input.c.bak`，对检出的文件进行修改并使用 `rcs -u input.c` 命令将其解锁。然后我们使用 `ci` 命令提交对文件的修改。尽管 `ci` 命令没有告诉我们对文件的修改未提交，但通过再次检出 `input.c` 文件并与之前保存的 `input.c` 进行比较，我们确认了这一点。

```
$ co -l input.c

RCS/input.c,v --> input.c

revision 2.1 (locked)

done

$ cp input.c input.c.bak

$ vi input.c

...

$ rcs -u input.c

RCS file: RCS/input.c,v

2.1 unlocked

done

$ ci input.c

RCS/input.c,v <-- input.c

ci: RCS/input.c,v: no lock set by rcs

$ co -l input.c

RCS/input.c,v --> input.c

revision 2.1 (locked)

writable input.c exists; remove it? [ny](n): y

done

$ diff input.c input.c.bak

```

### 不覆盖覆盖保存文件（处理错误）
当你执行 `ci -u input.c` 命令时，当前目录下会留下一个只读的 `input.c` 副本。警告：如果你更改了 `input.c` 的权限使其可写并对其进行修改，这些修改可能是问题的，因为你没有使用 `co -l input.c` 命令正确地检出文件的可编辑版本，所以它们无法安装到 RCS 数据库中的文件名中。

你可以通过 `rcs -l` 命令锁定 `input.c` 来避免这个问题，而无需从 RCS 目录检出并覆盖现有文件（你误操作更新的文件）。执行此命令后跟随 `ci -u input.c` 命令会将修改提交到 `RCS/input.c,v` 文件，并在当前目录下留下一个只读副本。此命令创建了一个新版本。下面的会话说明了这些点。

```
$ co -u input.c

RCS/input.c,v --> input.c

revision 1.2 (unlocked)

done

$ chmod 700 input.c

$ vi input.c

...

$ ci input.c

RCS/input.c,v <-- input.c

ci no lock set by rcs

$ rcs -l input.c

RCS file: RCS/input.c,v

1.2 locked

done

$ ci -u input.c

RCS/input.c,v <-- input.c

new revision: 1.3; previous revision: 1.2

enter log message, terminated with single '.' or end of file

>> Demonstrated file locking.

>>

done

$
```

## 670 第 20 章 用于开发的 Linux 工具

移除版本
RCS 允许你使用 `rcs` 命令配合 `-o` 选项删除文件的任意（包括非叶节点）版本。如果删除删除的是中间版本，剩余的版本将不会重新编号。在下面的会话中，我们删除了 `input.c` 的 1.1 版本。

```
$ rcs -ol1.1 input.c

RCS file: RCS/input.c,v

deleting revision 1.1

done

$
```

## 程序生成工具 671

通过指定 `-o` 选项后的范围，可以删除多个版本。例如，`rcs -o2.1:3.2 input.c` 命令会删除 `input.c` 文件的 2.1 到 3.2 版本。同样，`rcs -o:2.2 input.c` 命令会删除 `input.c` 的 1.1 到 2.2 版本（包括 2.2），而 `rcs -o4.1:input.c` 命令会删除 `input.c` 上的 4.1 版本（包括 4.1）。

下面的章内练习旨在增强你对 RCS 中文件版本的理解。该练习特别要求你使用 `rcs -o` 命令删除文件的某个版本。

## 章内练习

- 20.11. 在 RCS 中删除刚刚讨论的 `input.c` 文件的 1.2 版本：给出执行此任务的命令行。

### 分组工作

分组工作非常简单。你只需要将 RCS 子目录（或多个子目录）放在一个共享目录中。然后你通过指定 RCS 文件的完整路径来运行 RCS 工具，并编辑本地目录中的文件。创建公共共享目录的替代方案是将所有 RCS 目录维护在一个用户的目录中，并在组内其他成员的目录中创建指向该目录的符号链接（参见第 11 章）。当然，必须为 `/home/shared` 目录中唯一 RCS 目录所在路径中的所有组件设置适当的权限。

在接下来的会话中，我们检出 `input.c` 文件的可编辑版本，假设唯一的 RCS 目录位于 `/home/shared` 中。

```
$ co -l /home/shared/RCS/input.c,v

RCS/input.c,v --> input.c

revision 2.1.1.1 (locked)

done
```

在对 `input.c` 文件进行修改后，我们可以使用以下命令将其签回。`-u` 选项用于在当前目录中保留一个只读副本。

```
$ ci -u /home/shared/input.c

/home/shared/RCS/input.c,v <-- input.c

new revision: 2.1.1.2; previous revision 2.1.1.1
```

```
enter log message, terminated with single '.' or end of file

>> Illustrated working in groups.

>> .

done

$
```

前面的命令行需要很长的路径，因此组中的用户可能想要创建单行脚本来处理签入和检出程序。以下是用于 `checkin` 和 `checkout` 程序的 Bash 脚本。

```
$ cat checkin
!/bin/bash

# 签入命令行；在当前目录中保留一个只读副本

ci -u /home/shared/RCS/$1,v
$ cat checkout
!/bin/bash

# 检出命令行； 检出文件的可编辑副本

co -l /home/shared/RCS/$1,v
$
```

创建这些脚本后，你需要使用 `chmod +x` 命令为自己赋予它们执行权限，如下所示：

```
$ chmod u+x checkin checkout
$
```

现在，你可以使用 `checkin input.c` 命令签入 `/home/shared/RCS` 目录下的 `input.c` 文件，并使用 `checkout input.c` 命令从 `/home/shared/RCS` 目录检出 `input.c` 的可编辑版本。创建 `checkin` 和 `checkout` 脚本的替代方案是让组用户创建一个指向 `/home/shared/RCS` 目录的名为 RCS 的符号链接，并短名称（简单文件名）。

### 显示 RCS 文件的历史

你可以使用 `rlog` 命令显示 RCS 文件的历史。以下是该命令的简要描述。

#### rlog [options] file-list

**目的：** 显示 'file-list' 中 RCS 文件的历史（日志消息和其他信息）

- 常用选项/功能：
- L 显示已检出用于编辑的文件历史（即已锁的文件）
- R 仅显示文件名
- -l[users] 显示由 'users' 中指定的登录名的用户锁定的文件信息，'users' 是用逗号分隔的登录名列表
- r[revs] 显示 'revs' 中修订版本的信息，'revs' 是用逗号分隔的修订列表；rev1:rev2, .rev2, 或 rev1 可用于指定版本范围

在不使用任何选项的情况下，`rlog` 命令会显示 'file-list' 中文件进行的所有修订历史。下面的命令显示了 `input.c` 的历史

```
$ rlog input.c

RCS file: RCS/input.c

Working file: input.c

head: 2.1

branch:

locks: strict

access list:

symbolic names:

keyword substitution:

total revisions: 6; selected revisions: 6

description:

The first version of the input.c file

----------------------

revision 2.1

date: 2001/03/16 01:18:55; author: sarwar; state: Exp; lines: -1 -0

branches: 2.1.1.1; 2.1.2;

Just showing how a new version of a file can be created.
```
revision 1.2
date: 2001/03/16 01:12:25; author: sarwar; state: Exp; lines: +2
```
