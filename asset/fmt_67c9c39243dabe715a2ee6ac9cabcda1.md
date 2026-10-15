
合并失败可能会阻止此过程完全自动完成。你必须解决任何此类合并失败并运行 `git rebase --continue`。另一个选择是通过 `git rebase --skip` 绕过导致合并失败的提交。若要签出原始 `<branch>` 并移除 `.git/rebase-apply` 工作文件，请改用命令 `git rebase --abort`。

假设存在以下历史，且当前分支是 "topic"：

```text
A---B---C topic
/
D---E---F---G master
```

从这一点开始，以下任一命令的结果：

```bash
git rebase master
git rebase master topic
```

将是：

```text
A'--B'--C' topic
/
D---E---F---G master
```

**注意：** 后一种形式只是 `git checkout topic` 后跟 `git rebase master` 的简写。当 rebase 退出时，topic 将保持为签出的分支。

如果上游分支已经包含了你做的更改（例如，因为你发送了一个在上游应用的补丁），那么该提交将被跳过。例如，在以下历史上运行 `git rebase master`（其中 A' 和 A 引入相同的更改集，但具有不同的提交者信息）：

### 配置

#### rebase.stat

是否显示自上次变基以来上游更改的差异统计（diffstat）。默认为 False。

#### rebase.autoSquash

如果设置为 true，则默认启用 `--autosquash` 选项。

#### rebase.autoStash

如果设置为 true，则默认启用 `--autostash` 选项。

### 选项

#### `--onto <newbase>`

创建新提交时的起点。如果未指定 `--onto` 选项，则起点为 `<upstream>`。可以是任何有效的提交，而不仅仅是现有的分支名。

作为一种特殊情况，如果 A 和 B 恰好只有一个合并基底，您可以使用 “A..B” 作为 A 和 B 的合并基底的简写。您可以省略 A 和 B 中最多一个，此时它默认指向 HEAD。

#### `<upstream>`

用于比较的上游分支。可以是任何有效的提交，而不仅仅是现有的分支名。默认为当前分支配置的上游。

#### `<branch>`

工作分支；默认为 HEAD。

#### `--continue`

在解决合并冲突后重启变基过程。

#### `--abort`

中止变基操作并将 HEAD 重置到原始分支。如果在启动变基操作时提供了 `<branch>`，则 HEAD 将重置到 `<branch>`。否则，HEAD 将重置到启动变基操作时的位置。

#### `--keep-empty`

保留结果中那些相对于其父提交没有任何变更的提交。

#### `--skip`

通过跳过当前补丁重启变基过程。

#### `--edit-todo`

在交互式变基期间编辑待办事项列表。

#### `-m`, `--merge`

使用合并策略进行变基。当使用递归（默认）合并策略时，这使得变基能够感知上游侧的重命名。

请注意，变基合并通过在工作分支的每个提交重放至 `<upstream>` 分支之上来进行工作。因此，当发生合并冲突时，报告为*ours*（我方）的一侧是迄今为止已重放的变基系列（从 `<upstream>` 开始），而*theirs*（对方）是工作分支。换句话说，两侧是互换的。

#### `-s <strategy>`, `--strategy=<strategy>`

使用指定的合并策略。如果没有 `-s` 选项，则使用 `git merge-recursive`。这隐含了 `--merge`。

因为 `git rebase` 使用给定的策略将工作分支的每个提交重放到 `<upstream>` 分支之上，使用 `ours` 策略会简单丢弃 `<branch>` 中的所有补丁，这没有太大意义。

#### `-X <strategy-option>`, `--strategy-option=<strategy-option>`

将 `<strategy-option>` 传递给合并策略。这隐含了 `--merge` 以及，如果未指定策略，则隐含 `-s recursive`。注意如上所述 `-m` 选项中 `ours` 和 `theirs` 的互换。

#### `-S[<keyid>]`, `--gpg-sign[=<keyid>]`

GPG 签名提交。

#### `-q`, `--quiet`

保持安静。隐含 `--no-stat`。

#### `-v`, `--verbose`

详细输出。隐含 `--stat`。

#### `--stat`

显示自上次变基以来上游更改的差异统计。差异统计还由配置选项 `rebase.stat` 控制。

#### `-n`, `--no-stat`

不在变基过程中显示差异统计。

#### `--no-verify`

此选项绕过 pre-rebase 钩子。另见 `git-hook(5)`。

#### `--verify`

允许 pre-rebase 钩子运行，这是默认行为。此选项可用于覆盖 `--no-verify`。另见 `git-hook(5)`。

#### `-C<n>`

确保每个更改前后至少有 `<n>` 行周围上下文匹配。当周围上下文行数较少时，它们必须全部匹配。默认情况下，永远不会忽略上下文。

#### `-f`, `--force-rebase`

即使当前分支是最新的，且不带 `--force` 的命令本应无操作返回，也强制进行变基。

在撤销主题分支合并后，您可能会发现这个（或者交互式变基中的 `--no-ff`）很有用，因为此选项会以新的提交重建主题分支，使其能够成功重新合并，而无需“撤销还原操作”（详情参见 revert-a-faulty-merge 指南[10]）。

#### `--fork-point`, `--no-fork-point`

使用 `git rev-list` 在计算 `<branch>` 引入了哪些提交时，在 `<upstream>` 和 `<branch>` 之间寻找更好的共同祖先。

当 `--fork-point` 激活时，将使用 `fork_point` 而不是 `<upstream>` 来计算要变基的提交集合，其中 `fork_point` 是 `git merge-base --fork-point <upstream> <branch>` 命令的结果（参见 `git-merge-base(1)`）。如果 `fork_point` 最终为空，则将使用 `<upstream>` 作为后备。

如果在命令行中给出了 `<upstream>` 或 `--root`，则默认为 `--no-fork-point`，否则默认为 `--fork-point`。

#### `--ignore-whitespace`, `--whitespace=<option>`

这些标志传递给 `git apply` 程序（参见 `git-apply(1)`）以应用补丁。与 `--interactive` 选项不兼容。

#### `--committer-date-is-author-date`, `--ignore-date`

这些标志传递给 `git am` 以轻松更改变基提交的日期（参见 `git-am(1)`）。与 `--interactive` 选项不兼容。

#### `-i`, `--interactive`

列出即将变基的提交。让用户在变基前编辑该列表。此模式也可用于拆分提交（见下文“拆分提交”）。

#### `-p`, `--preserve-merges`

通过重放合并提交引入的提交来重新创建合并提交，而不是将历史扁平化。合并冲突的解决或手动修改合并提交的操作不会被保留。

这在内部使用了 `--interactive` 机制，但显式地与 `--interactive` 选项结合通常不是一个好主意，除非您知道自己在做什么（见下文“错误”）。

#### `-x <cmd>`, `--exec <cmd>`

在最终历史中创建每个提交后追加 “exec <cmd>”。`<cmd>` 将被解释为一个或多个 shell 命令。

此选项只能与 `--interactive` 选项一起使用（见下文“交互式模式”）。

您可以通过使用带有多个命令的单个 `--exec` 实例来执行多个命令：

```
git rebase -i --exec "cmd1 && cmd2 && ..."
```

或者通过提供多个 `--exec`：

```
git rebase -i --exec "cmd1" --exec "cmd2"
```

## git rebase -i --exec "cmd1" --exec "cmd2" --exec...

如果使用 --autosquash 选项，“exec” 行不会为中间提交附加，而只会出现在每个 squash/fixup 序列的末尾。

### --root
