
# useradd 命令选项

| 选项 | 描述 |
| :--- | :--- |
| `-f inactive-time` | 此选项指定密码过期后账户仍可用的天数。值为 `-1`（零）表示账户立即被禁用。值为 `0` 将永远不会禁用账户，即使密码已过期（例如，`-f 3` 将允许账户在密码过期后存在三天）。默认值为 `-1`。 |
| `-g initial-group` | 使用此选项，你可以指定用户在密码文件中的默认组。你可以使用组的编号或名称；但是，如果使用组名，该组必须存在于 `/etc/group` 文件中——例如，`-g project`。 |
| `-G group[,...]` | 此选项允许你指定新用户将属于的附加组。如果使用 `-G` 选项，必须至少指定一个附加组。但是，你可以通过用逗号分隔来指定额外的组。例如，要将用户添加到 `project` 和 `admin` 组，你应该指定 `-G project,admin`。 |
| `-m [-k skel-dir]` | 默认情况下，系统会自动创建用户的主目录。此选项是创建用户主目录的显式命令。创建目录的一部分是将默认配置文件复制到其中。这些文件默认来自 `/etc/skel` 目录。你可以使用次要选项 `-k skel dir` 更改此设置。（为了使用 `-k`，必须指定 `-m`。）例如，要指定 `/etc/admiskel` 目录，你将使用 `-m -k /etc/admiskel`。 |
| `-M` | 如果你使用了 `-m` 选项，就不能使用 `-M`，反之亦然。此选项告诉命令不要创建用户的主目录。 |
| `-n` | Red Hat Linux 在添加用户的过程中创建与新用户登录名同名的新组。你可以使用此选项禁用此行为。 |
| `-s shell` | 用户的登录 shell 是用户登录系统时运行的第一个程序。这通常是一个命令行环境，除非你是从 X 登录屏幕登录。默认情况下，这是 Bourne Shell（`/bin/bash`），尽管有些人喜欢其他 shell，如 Turbo C Shell（`/bin/tcsh`）。此选项让你在登录时选择希望新用户运行的任何 shell。（`/etc/shells` 中有一个 shell 列表。） |
| `-u uid` | 默认情况下，程序会自动找到下一个可用的 UID 并使用它。如果由于某种原因你需要强制新用户的 UID 为特定值，可以使用此选项。请记住，UID 对于所有用户必须是唯一的。 |
| `login` | 最后，唯一不是可选的参数！你必须指定新用户的登录名。 |

表 5-1 `useradd` 命令的选项（续表）

例如，要创建一个名为 Mike Pawlawski 的新用户，他是 `admin` 和 `support` 组的成员（默认组为 `admin`），他偏好使用 Turbo C Shell 并希望登录名为 `mpawlawski`，你可以使用这一行：

```
[root@tedford /root]# useradd -c "Mike Pawlawski" -g admin -G support \
> -s /bin/tcsh mpawlawski
```

## userdel

`userdel` 命令与 `useradd` 的作用完全相反——它删除现有用户。这个简单的命令只有一个可选参数和一个必需参数：

```
userdel [-r] username
```

通过仅指定用户在命令行上的登录名运行该命令，例如，`userdel rwhite`，`/etc/passwd` 和 `/etc/shadow` 文件中的所有条目以及 `/etc/group` 文件中的引用都会自动删除。通过使用可选参数（例如，`userdel -r rwhite`），其主目录中由该用户拥有的所有文件也会随之删除。

## usermod

`usermod` 命令允许你修改系统中的现有用户。它的工作方式与 `useradd` 非常相似。确切的命令行用法如下：

```
usermod [-c comment] [-d homedir] [-m] [-e expire date]
[-f inactive time] [-g initial group]
[-G group[,...]] [-l login] [-s shell]
[-u uid] login
```

使用此命令时指定的每个选项都会导致该特定参数关于用户的更改。这里列出的参数中除一个外都与 `useradd` 程序记录的参数相同。那个选项是 `-l`。

`-l` 选项允许你更改用户的登录名。这以及 `-u` 选项是需要特别小心的选项。在更改用户的登录名或 UID 之前，你必须确保用户未登录系统或未运行任何进程。如果用户已登录或正在运行进程时更改此信息，将导致不可预测的结果。

这里是一个使用 `usermod` 更改用户 `mpawlowski` 的示例，使其注释字段显示为 Number Nine 而不是 Mike Pawlowski：

```
[root@tedford /root]# usermod -c "Number Nine" mpawlowski
```

## groupadd

组命令与用户命令类似；但是，它们不是针对单个用户操作，而是针对 `/etc/group` 文件中列出的组进行操作。请注意，更改组信息不会导致用户信息自动更改。例如，如果你删除 GID 为 100 的组，而某用户的默认组指定为 100，该用户的默认组不会更新以反映该组不再存在的事实。

`groupadd` 命令将组添加到 `/etc/group` 文件。该程序的命令行选项如下：

```
groupadd [-g gid] [-r] [-f] group
```

表 5-2 显示了命令选项及其描述。

### groupadd 命令选项

| 选项 | 描述 |
| :--- | :--- |
| `-g gid` | 将新组的 GID 指定为 `gid`。默认情况下，此值通过查找第一个可用的值自动选择。 |
| `-r` | 默认情况下，Red Hat 会查找第一个大于 499 的 GID。`-r` 选项告知 `groupadd` 正在添加的组是系统组，并且应具有 499 以下的第一可用 GID。 |
| `-f` | 在添加新组时，如果指定的待添加组已存在，Red Hat Linux 将无错误退出。使用此选项时，程序在退出前不会更改组设置。这在脚本场景中非常有用，例如当组已存在时你希望脚本继续执行。 |
| `group` | 此选项是必需的。它指定你要添加的组名称为 `group`。 |

例如，假设你想添加一个名为 `research` 的新组，GID 为 800。为此，你会输入以下命令：

```
[root@tedford /root]# groupadd -g 800 research
```

## groupdel

比 `userdel` 更简单直接，`groupdel` 命令删除 `/etc/group` 文件中指定的现有组。此命令唯一需要的使用信息是

```
groupdel group
```

其中 `group` 是要删除的组名。例如，如果你想删除 `research` 组，你会发出此命令：

```
[root@tedford /root]# groupdel research
```

## groupmod

`groupmod` 命令允许你修改现有组的参数。此命令的选项为

```
groupmod -g gid -n group-name group
```

其中 `-g` 选项允许你更改组的 GID，`-n` 选项允许你指定组的新名称。当然，此外你还需要指定现有组的名称作为最后一个参数。

例如，如果超级英雄 `research` 组想将其名称更改为 `batman`，你会发出命令：

```
[root@tedford /root]# groupmod -n batman superman
```

## 项目 5-1 创建用户目录

抽象地看待用户管理工具固然很好，但现实落地时，你必须在自己的环境中整理和实施用户和组。在本项目中，你将使用小公司的员工列表来正确配置用户目录。

### 逐步操作

1. 首先掌握员工及其分组。该公司有两个主要组织：研发组和客户支持组。每个组内部都需要共享文件和资源。研究组由三个用户组成：`blee`、`dalbers` 和 `pddood`。支持组由五个用户组成：`dgranda`、`jwang`、`pvenet`、`dnnni` 和 `mmuller`。
2. 有一些次要组织分组需要配置。三名用户担任高管职务，需要共享其他用户无法访问的私密信息。这些高管是：`dalbers`、`dnnni` 和 `pddood`。
3. 另一个次要分组是应用工程师。用户 `dgranda`、`jwang` 和 `mmuller` 需要运行错误跟踪和文档数据库。
4. 最后一个分组是管理员用户。用户 `blee`、`dalbers` 和 `mmuller` 拥有账户信息、支持合同信息、路由器密码等需要保密的数据。
5. 按主要组和次要组排列用户。
