

## 示例

若只想更新和刷新已检出的文件：

```bash
$ git checkout-index -n -f -a && git update-index --ignore-missing --refresh
```

使用 git checkout-index “导出整棵树”

前缀功能基本上使得将 git checkout-index 用作“导出为树”的功能变得非常简单。只需将目标树读入索引，然后执行以下操作：

```bash
$ git checkout-index --prefix=git-export-dir/ -a
```

git checkout-index 会将索引“导出”到指定目录。

最后的“/”非常重要。导出的名称字面上只是加上了指定的字符串前缀。请对比以下示例。

带前缀导出文件

```bash
$ git checkout-index --prefix=.merged- Makefile
```

这将把当前缓存的 Makefile 副本检出到文件 .merged-Makefile 中。

# GIT-CHECKOUT

## 名称

git-checkout - 切换分支或恢复工作树文件

## 概要

```bash
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach <branch>
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B]--orphan] <new_branch> [<start_point>]
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [-] <paths>...
git checkout [-p|--patch] [<tree-ish>] [--] [<paths>...]
```

## 描述

将工作树中的文件更新为与索引或指定树中的版本一致。如果未给出路径，git checkout 还会更新 HEAD，将指定分支设置为当前分支。

### git checkout <branch>

为了准备在 <branch> 上进行工作，通过更新索引和工作树中的文件并将 HEAD 指向该分支来切换到该分支。工作树中文件的本地修改会被保留，以便可以提交到 <branch>。

如果 <branch> 未找到，但恰好有一个远程仓库（称为 <remote>）中存在同名跟踪分支，则视为等同于

```bash
$ git checkout -b <branch> --track <remote>/<branch>
```

你可以省略 <branch>，此时命令退化为“检出当前分支”，这是一种带有昂贵副作用的高调空操作，仅用于显示当前分支的跟踪信息（如果存在）。

### git checkout -b|-B <new_branch> [<start point>]

指定 -b 会创建一个新分支，就像调用 (1) 然后检出一样。在这种情况下，你可以使用 --track 或 --no-track 选项，这些选项将传递给 git branch。作为便捷功能，在没有 -b 的情况下使用 --track 隐含分支创建；见下文 --track 的描述。

如果给出 -B，若 <new_branch> 不存在则创建；否则重置。这是以下操作的事务等价形式：

```bash
$ git branch -f <branch> [<start point>]
$ git checkout <branch>
```

也就是说，只有当“git checkout”成功时，分支才会被重置/创建。

### git checkout --detach [<branch>], git checkout [--detach] <commit>

通过在 <commit> 处分离 HEAD（参见“分离 HEAD”部分）并更新索引和工作树中的文件，为在 <commit> 之上工作做准备。工作树中文件的本地修改会被保留，因此最终的工作树状态将是提交中记录的状态加上本地修改。

当 <commit> 参数是分支名时，可以使用 --detach 选项在分支顶端分离 HEAD（git checkout <branch> 会检出该分支而不分离 HEAD）。

省略 <branch> 会在当前分支顶端分离 HEAD。

### git checkout [-p|--patch] [<tree-ish>] [--] <pathspec> ...

当给出 <paths> 或 --patch 时，git checkout 不会切换分支。它根据索引文件或指定的 <tree-ish>（通常是提交）更新工作树中命名的路径。在这种情况下，-b 和 --track 选项没有意义，给出其中任何一个都会导致错误。可以使用 <tree-ish> 参数来指定一个特定的 tree-ish（即提交、标签或树），在更新工作树之前先更新给定路径的索引。

使用带有 <paths> 或 --patch 的 git checkout 用于将修改或删除的路径恢复为索引中的原始内容，或者用指定的 <tree-ish>（通常是 commit-ish）中的内容替换路径。

由于之前合并失败，索引中可能包含未合并的条目。默认情况下，如果你尝试从索引中检出这样的条目，检出操作将失败，并且不会检出任何内容。使用 -f 将忽略这些未合并的条目。可以使用 --ours 或 --theirs 从索引中检出合并特定一侧的内容。使用 -m，可以丢弃对工作树文件所做的更改，以重新创建原始的冲突合并结果。

## 选项

- -q, --quiet
  静默，抑制反馈消息。

- -f, --force
  切换分支时，即使索引或工作树与 HEAD 不同也继续执行。这用于丢弃本地更改。
  从索引中检出路径时，不要在未合并条目上失败；相反，忽略未合并条目。

- --ours, --theirs
  从索引中检出路径时，对于未合并路径，检出 #2 阶段（*ours*）或 #3 阶段（*theirs*）。

- -b <new_branch>
  创建名为 <new_branch> 的新分支，并使其起始于 <start_point>；详情参见 (1)。

- -B <new_branch>
  创建分支 <new_branch> 并使其起始于 <start_point>；如果它已经存在，则将其重置为 <start_point>。这等同于使用“-f”运行“git branch”；详情参见 (1)。

- -t, --track
  创建新分支时，设置“上游”配置。详情参见 (1) 中的“--track”。
  如果未给出 -b 选项，新分支名称将从远程跟踪分支推导出来，通过查看为相应远程配置的 refspec 的本地部分，然后去除“*”之前的部分。这会告诉我们在从“origin/hack”（或“remotes/origin/hack”，甚至“refs/remotes/origin/hack”）创建分支时，使用“hack”作为本地分支。如果给定的名称没有斜杠，或者上述猜测结果为空名称，则中止猜测。在这种情况下，你可以使用 -b 显式给出名称。

- --no-track
  不设置“上游”配置，即使 branch.autoSetupMerge 配置变量为 true。

- -1
  创建新分支的 reflog；详情参见 (1)。

- --detach
  不是检出分支以在其上工作，而是检出提交以进行检查和可丢弃的实验。当 <commit> 不是分支名时，这是 "git checkout <commit>" 的默认行为。详情见下文"DETACHED HEAD"部分。

- --orphan <new_branch>
  创建一个名为 <new_branch> 的新孤儿分支，起始于 <start_point> 并切换到它。在此新分支上创建的第一个提交将没有父提交，并且将是一个与所有其他分支和提交完全断开的新历史的根。
  索引和工作树将如同你之前运行过 "git checkout <start_point>" 一样进行调整。这允许你通过轻松运行 "git commit -a" 来创建记录与 <start_point> 相似的一组路径的新历史，从而创建根提交。
  当你希望发布来自提交的树而不暴露其完整历史时，这可能很有用。你可能希望这样做来发布项目的开源分支，该分支的当前树是“干净”的，但其完整历史包含专有或其他受限的代码片段。
  如果你希望开始一个记录与 <start_point> 的路径完全不同的断开历史，那么在创建孤儿分支后，你应立即通过在工作树顶层运行 "git rm -rf ." 来清除索引和工作树。之后，你将准备好通过从其他位置复制、解包 tar 包等方式重新填充工作树来准备你的新文件。

- --ignore-skip-worktree-bits
  在稀疏检出模式下，git checkout -- <paths> 将仅更新由 <paths> 和 $GIT_DIR/info/sparse-checkout 中稀疏模式匹配的条目。此选项忽略稀疏模式并添加 <paths> 中的所有文件。

- -m, --merge
  切换分支时，如果你对一个或多个在当前分支和你正在切换到的分支之间不同的文件有本地修改，该命令会拒绝切换分支，以在上下文中保留你的修改。然而，使用此选项时，会在当前分支、你的工作树内容和新分支之间进行三路合并，你将位于新分支上。
  当发生合并冲突时，冲突路径的索引条目将保持未合并状态，你需要解决冲突并使用 git add（或如果合并应导致路径删除，则使用 git rm）标记已解决的路径。
  从索引中检出路径时，此选项允许你在指定路径中重新创建冲突的合并。

