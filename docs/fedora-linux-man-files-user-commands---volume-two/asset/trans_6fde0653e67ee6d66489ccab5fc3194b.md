

## GIT-REFLOG

### 名称
git-reflog - 管理引用日志（reflog）信息

### 概要

```
git reflog <子命令> [<选项>]
```

### 描述
该命令接受各种子命令，并根据不同的子命令接受不同的选项：

```
git reflog [show] [log-options] [<ref>]
git reflog expire [--expire=<时间>] [--expire-unreachable=<时间>] [--rewrite] [--updateref] [--stale-fix] [--dry-run] [--verbose] [--all] [<ref>...]
git reflog delete [--rewrite] [--updateref] [--dry-run] [--verbose]
ref@{<指定符>}...
```

引用日志（或称“reflogs”）记录本地仓库中分支顶端及其他引用何时被更新。引用日志在 various Git 命令中非常有用，可用于指定引用的旧值。例如，`HEAD@{2}` 表示“HEAD 在两次提交之前所在的位置”，`master@{one.week.ago}` 表示“在本本地仓库中，master 一周前指向的位置”，等等。更多详细信息请参见 `gittutorial-revisions(7)`。

此命令管理记录在引用日志中的信息。

“show”子命令（在没有指定任何子命令时也是默认子命令）显示命令行中提供的引用（或默认情况下为 HEAD）的日志。引用日志涵盖所有最近的操作，并且 HEAD 的引用日志还记录了分支切换操作。`git reflog show` 是 `git log -g --abbrev-commit --pretty=oneline` 的别名；更多信息请参见 `gitlog(1)`。

“expire”子命令用于清理较旧的引用日志条目。早于 expire 时间的条目，或早于 expire-unreachable 时间且不可从当前顶端访问的条目，将从引用日志中删除。终端用户通常不会直接使用此功能——相反，请参见 `gc(1)`。

“delete”子命令从引用日志中删除单个条目。其参数必须是一个*精确*的条目（例如 "git reflog delete master@{2}"）。此子命令通常也不被终端用户直接使用。

### 选项

**show 的选项**
git reflog show 接受 git log 接受的任何选项。

**expire 的选项**

- `--all`：处理所有引用的引用日志。
- `--expire=<时间>`：删除早于指定时间的条目。如果未指定此选项，过期时间将从配置设置 `gc.reflogExpire` 中获取，该设置的默认值为 90 天。`--expire=all` 无论年龄如何都会删除条目；`--expire=never` 关闭对可访问条目的删除（但请参见 `--expire-unreachable`）。
- `--expire-unreachable=<时间>`：删除早于 <时间> 且不可从分支当前顶端访问的条目。如果未指定此选项，过期时间将从配置设置 `gc.reflogExpireUnreachable` 中获取，该设置的默认值为 30 天。`--expire-unreachable=all` 无论年龄如何都会删除不可访问的条目；`--expire-unreachable=never` 关闭对不可访问条目的早期删除（但请参见 `--expire`）。
- `--updateref`：如果之前最顶端的条目被清理，则将引用更新为顶端引用日志条目（即 `<ref>@{0}`）的值。（此选项对符号引用无效。）
- `--rewrite`：如果引用日志条目的前驱被清理，则将其“旧”SHA-1 调整为等于现在位于其之前的条目的“新”SHA-1 字段。
- `--stale-fix`：删除指向“损坏提交”的任何引用日志条目。损坏提交是指不可从任何引用顶端访问，并且直接或间接引用缺失的提交、树或 blob 对象的提交。此计算涉及遍历所有可访问对象，即其成本与 `git prune` 相同。它主要用于修复由旧版本 Git 的垃圾收集引起的损坏，这些旧版本没有保护被引用日志引用的对象。
- `-n, --dry-run`：不实际删除任何条目；仅显示将被删除的内容。
- `--verbose`：在屏幕上打印额外信息。

**delete 的选项**
git reflog delete 接受选项 `--updateref`、`--rewrite`、`-n`、`--dry-run` 和 `--verbose`，其含义与它们在 expire 中使用时的含义相同。

## 另见
`gittutorial-revisions(7)`, `gitlog(1)`

## GIT-RELINK

### 名称
git-relink - 在本地仓库中硬链接公共对象

### 概要

```
git relink [--safe] <dir>... <master_dir>
```

### 描述
这将扫描一个或多个对象仓库，并查找与主仓库共有的对象。尚未硬链接到主仓库的对象将被替换为主仓库的硬链接。

### 选项
- `--safe`：如果存在两个具有相同哈希值但大小不同的对象，则停止。默认是发出警告并继续。
- `<dir>`：包含 .git/objects/ 子目录的目录。

