

$ git bisect start HEAD <known-good-commit> [ <boundary-commit> ... ]
$ git bisect run sh -c '
  GOOD=$(git for-each-ref "--format=%(objectname)" refs/bisect/good-*)
  git rev-list --objects BISECT_HEAD --not $GOOD >tmp.$$
  git pack-objects --stdout >/dev/null <tmp.$$
  rc=$?
  rm -f tmp.$$
  test $rc = 0
'
$ git bisect reset # 退出二分查找会话

在这种情况下，当 *git bisect run* 完成时，bisect/bad 将指向一个提交，该提交至少有一个父提交，其可达性图在 *git pack objects* 所需的意义上是完全可遍历的。

## 参见

使用 git bisect(1) 对抗回归。

## 注释

- 使用 git bisect 对抗回归

## GIT-BRANCH

### 名称

git-branch - 列出、创建或删除分支

### 概要

```
git branch [--color[=<when>] | --no-color] [-r | -a] [--list] [-v [--abbrev=<length> | --no-abbrev]] [--column[=<options>] | --no-column]
    [[--merged | --no-merged | --contains] [<commit>]] [<pattern>...]
git branch [-set-upstream | --track | --no-track] [-l] [-f] <branchname> [<start-point>]
git branch (--set-upstream-to=<upstream> | -u <upstream>) [<branchname>]
git branch --unset-upstream [<branchname>]
git branch (-m | -M) [<oldbranch>] <newbranch>
git branch (-d | -D) [-r] <branchname>...
git branch --edit-description [<branchname>]
```

### 描述

如果提供了 --list，或者没有非选项参数，则列出现有分支；当前分支将通过星号突出显示。选项 -r 会导致列出远程跟踪分支，而选项 -a 会同时显示本地和远程分支。如果提供了 <pattern>，则将其用作 shell 通配符，以将输出限制为匹配的分支。如果提供了多个模式，只要分支匹配其中任何一个模式，就会显示该分支。请注意，当提供 <pattern> 时，必须使用 --list；否则命令将被解释为创建分支。

使用 --contains 时，仅显示包含指定提交的分支（换句话说，就是分支尖端提交是指定提交的后代的分支）。使用 --merged 时，仅列出已合并到指定提交的分支（即分支尖端提交可从指定提交到达的分支）将被列出。使用 --no-merged 时，仅列出未合并到指定提交的分支。如果缺少 <commit> 参数，则默认为 HEAD（即当前分支的尖端）。

该命令的第二种形式创建一个名为 <branchname> 的新分支头，它指向当前的 HEAD，或者如果提供了则指向 <start-point>。

请注意，这将创建新分支，但不会将工作树切换到该分支；请使用 “git checkout <newbranch>” 切换到新分支。

当本地分支从远程跟踪分支启动时，Git 会设置分支（具体来说是 branch.<name>.remote 和 branch.<name>.merge 配置项），以便 git pull 能够从远程跟踪分支适当合并。可以通过全局 branch.autoSetupMerge 配置标志更改此行为。该设置可以使用 --track 和 --no-track 选项覆盖，并可以使用 git branch --set-upstream-to 稍后更改。

使用 -m 或 -M 选项时，<oldbranch> 将被重命名为 <newbranch>。如果 <oldbranch> 有对应的引用日志，则重命名以匹配 <newbranch>，并创建一条引用日志条目以记录分支重命名。如果 <newbranch> 已存在，必须使用 -M 来强制执行重命名。

使用 -d 或 -D 选项时，将删除 <branchname>。可以指定多个分支进行删除。如果当前分支有引用日志，则引用日志也将被删除。与 -d 一起使用 -r 来删除远程跟踪分支。请注意，仅当远程仓库中不再存在这些远程跟踪分支，或者配置 git fetch 不再获取它们时，删除远程跟踪分支才有意义。有关清理所有过时的远程跟踪分支的方法，还请参见 git-remote(1) 的 prune 子命令。

### 选项

- -d, --delete

  删除分支。该分支必须已完全合并到其上游分支中，或者如果未通过 --track 或 --set-upstream 设置上游，则必须已完全合并到 HEAD 中。

- -D

  --delete --force 的快捷方式。

- -l, --create-reflog

  创建分支的引用日志。这会启用记录对分支引用的所有更改，从而允许使用基于日期的 sha1 表达式，例如 “<branchname>@{yesterday}”。请注意，在非裸仓库中，引用日志通常通过 core.logAllRefUpdates 配置选项默认启用。

- -f, --force

  如果 <branchname> 已经存在，则将其重置为 <start-point>。如果没有 -f，git branch 将拒绝修改现有分支。与 -d（或 --delete）结合使用时，允许删除分支而不考虑其合并状态。与 -m（或 --move）结合使用时，允许重命名分支，即使新分支名称已存在。

- -m, --move

  移动/重命名分支及对应的引用日志。

- -M

  --move --force 的快捷方式。

- --color[=<when>]

  对分支进行着色，以突出显示当前、本地和远程跟踪分支。值必须为 always（默认）、never 或 auto。

- --no-color

  关闭分支颜色，即使配置文件默认给出颜色输出。等同于 --color=never。

- --column[=<options>], --no-column

  以列形式显示分支列表。有关选项语法，请参阅配置变量 column.branch。不带选项的 --column 和 --no-column 分别等同于 always 和 *never*。此选项仅适用于非详细模式。

- -r, --remotes

  列出或（如果与 -d 一起使用）删除远程跟踪分支。

- -a, --all

  列出远程跟踪分支和本地分支。

- --list

  激活列表模式。git branch <pattern> 会尝试创建分支，请使用 git branch --list <pattern> 来列出匹配的分支。

- -v, -vv, --verbose

  在列表模式下，显示每个头部的 sha1 和提交主题行，以及与其上游分支的关系（如果有的话）。如果给出两次，还会打印上游分支的名称（另请参阅 git remote show <remote>）。

- -q, --quiet

  在创建或删除分支时更安静，抑制非错误消息。

- --abbrev=<length>

  更改输出列表中 sha1 的最小显示长度。默认值为 7，可以通过 core.abbrev 配置选项覆盖。

- --no-abbrev

  在输出列表中显示完整的 sha1，而不是缩写。

- -t, --track

  创建新分支时，设置 branch.<name>.remote 和 branch.<name>.merge 配置项，将起始点分支标记为新分支的“上游”。此配置将指示 git 在 git status 和 git branch -v 中显示两个分支之间的关系。此外，它指示 git pull 在没有参数时，在新分支被检出时从上游拉取。当起点是远程跟踪分支时，这是默认行为。如果希望 git checkout 和 git branch 始终表现得像提供了 --no-track 一样，请将 branch.autoSetupMerge 配置变量设置为 false。如果希望当起点是本地或远程跟踪分支时具有此行为，请将其设置为 always。

- --no-track

  不设置“上游”配置，即使 branch.autoSetupMerge 配置变量为 true。

- --set-upstream

  如果指定分支尚不存在或提供了 --force，则其行为完全类似于 --track。否则，设置创建分支时 --track 会设置的配置，但不会更改 branch 指向的内容。

- -u <upstream>, --set-upstream-to=<upstream>

  设置 <branchname> 的跟踪信息，使 <upstream> 被视为 <branchname> 的上游分支。如果未指定 <branchname>，则默认为当前分支。

- --unset-upstream

  移除 <branchname> 的上游信息。如果未指定分支，则默认为当前分支。

- --edit-description

  打开编辑器并编辑文本以说明分支的用途，供其他命令（例如 request-pull）使用。

- --contains [<commit>]

  仅列出包含指定提交（未指定则为 HEAD）的分支。隐含 --list。

- --merged [<commit>]

  仅列出其尖端可从指定提交（未指定则为 HEAD）到达的分支。隐含 --list。

- --no-merged [<commit>]

  仅列出其尖端不可从指定提交（未指定则为 HEAD）到达的分支。隐含 --list。

- <branchname>

  要创建或删除的分支名称。新分支名称必须通过 git-checkout(1) 定义的所有检查。其中一些检查可能会限制分支名称中允许使用的字符。

