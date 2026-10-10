

推送到。此外，`.`（一个点）表示当前本地仓库（一个点仓库），请参阅下方 `branch.<name>.merge` 的最后一项说明。

## branch.<name>.pushRemote

当处于分支 `<name>` 时，该配置项会覆盖 `branch.<name>.remote` 用于推送。它也会覆盖 `remote.pushDefault` 用于从分支 `<name>` 进行推送。当你从某处（例如你的上游）拉取并推送到另一处（例如你自己的发布仓库）时，你可以设置 `remote.pushDefault` 来指定所有分支推送的目标远程，并使用此选项针对特定分支进行覆盖。

## branch.<name>.merge

与 `branch.<name>.remote` 一起定义给定分支的上游分支。它告诉 *git fetch*/*git pull*/*git rebase* 要合并哪个分支，并且也会影响 *git push*（参见 `push.default`）。当处于分支 `<name>` 时，它告诉 *git fetch* 在 `FETCH_HEAD` 中标记为合并的默认 refspec。该值的处理方式类似于 refspec 的远程部分，并且必须匹配由 `branch.<name>.remote` 指定的远程获取的某个 ref。合并信息被 *git pull*（其首先调用 *git fetch*）用于查找默认合并分支。如果没有此选项，*git pull* 默认合并第一个获取的 refspec。指定多个值以获取章鱼合并。如果你希望设置 *git pull* 使其从本地仓库的另一分支合并到 `<name>`，你可以将 `branch.<name>.merge` 指向所需的分支，并使用相对路径设置 `.`（一个点）作为 `branch.<name>.remote`。

## branch.<name>.mergeOptions

为合并到分支 `<name>` 设置默认选项。语法和支持的选项与 (1) 相同，但当前不支持包含空白字符的选项值。

## branch.<name>.rebase

当为 true 时，在运行 “*git pull*” 时，将分支 `<name>` 变基到获取的分支之上，而不是从默认远程合并默认分支。关于以非分支特定方式执行此操作，请参阅 `pull.rebase`。

```
when preserve, also pass `--preserve-merges` along to 'git rebase' so that locally commited merge commits will not be flattened by running 'git pull'.
```

> **注意：** 这是一个可能危险的操作；除非你了解其影响（请参阅 (1) 以获取详细信息），否则**不要**使用它。

## branch.<name>.description

分支描述，可以使用 `git branch --edit-description` 进行编辑。分支描述会自动以格式补丁封面信或请求拉取摘要的形式添加。

## browser.<tool>.cmd

指定调用指定浏览器的命令。指定的命令会在 shell 中评估，URL 作为参数传递。（参见 (1)。）

### browser.<tool>.path

覆盖给定工具的路径，该工具可用于浏览 HTML 帮助（参见 (1) 中的 `-w` 选项）或 gitweb 中的工作仓库（参见 (1)）。

### clean.requireForce

一个布尔值，使 `git-clean` 在不提供 `-f`、`-i` 或 `-n` 的情况下不执行任何操作。默认为 true。

### color.branch

一个布尔值，启用/禁用 (1) 输出中的颜色。可以设置为 always、false（或 never）或 auto（或 true），在这种情况下，颜色仅当输出到终端时使用。默认为 false。

### color.branch.<slot>

为分支着色使用自定义颜色。`<slot>` 是 current（当前分支）、local（本地分支）、remote（`refs/remotes/` 中的远程跟踪分支）、upstream（上游跟踪分支）或 plain（其他 refs）之一。

### color.diff

是否使用 ANSI 转义序列为补丁添加颜色。如果设置为 always，(1)、(1) 和 (1) 将为所有补丁使用颜色。如果设置为 true 或 auto，这些命令仅当输出到终端时使用颜色。默认为 false。

这不会影响 (1) 或 `git-diff-*` 管道命令。可以通过命令行选项 `--color[=<when>]` 进行覆盖。

### color.diff.<slot>

为差异着色使用自定义颜色。`<slot>` 指定使用指定颜色的补丁部分，是 context（上下文文本 - plain 是一个历史同义词）、meta（元信息）、frag（块头）、func（块头中的函数）、old（删除的行）、new（添加的行）、commit（提交头）或 whitespace（突出显示空白错误）之一。

### color.decorate.<slot>

为 `git log --decorate` 输出使用自定义颜色。`<slot>` 分别是 local branches（本地分支）、remote-tracking branches（远程跟踪分支）、tags（标签）、stash（贮藏）或 HEAD 中的 branch、remoteBranch、tag、stash 或 HEAD。

### color.grep

当设置为 always 时，始终突出显示匹配项。当为 false（或 never）时，从不。当设置为 true 或 auto 时，仅当输出写入终端时使用颜色。默认为 false。

### color.grep.<slot>

为 grep 着色使用自定义颜色。`<slot>` 指定使用指定颜色的行部分，是以下之一：

- context
  上下文行中不匹配的文本（使用 -A、-B 或 -C 时）
- filename
  文件名前缀（不使用 -h 时）
- function
  函数名行（使用 -p 时）
- linenumber
  行号前缀（使用 -n 时）
- match
  匹配文本（等同于设置 matchContext 和 matchSelected）
- matchContext
  上下文行中的匹配文本
- matchSelected
  选中行中的匹配文本
- selected
  选中行中不匹配的文本
- separator
  一行中字段之间的分隔符（:, -, 和 =）以及块之间的分隔符（—）

### color.interactive

当设置为 always 时，始终为交互式提示和显示（例如由 “git-add —interactive” 和 “git-clean —interactive” 使用的那些）使用颜色。当为 false（或 never）时，从不。当设置为 true 或 auto 时，仅当输出到终端时使用颜色。默认为 false。

### color.interactive.<slot>

为 `git add —interactive` 和 `git clean —interactive` 输出使用自定义颜色。`<slot>` 可以是 prompt、header、help 或 error，用于交互式命令的四种不同类型的正常输出。

### color.pager

一个布尔值，启用/禁用使用分页器时的彩色输出（默认为 true）。

### color.showBranch

一个布尔值，启用/禁用 (1) 输出中的颜色。可以设置为 always、false（或 never）或 auto（或 true），在这种情况下，颜色仅当输出到终端时使用。默认为 false。

## color.status

一个布尔值，启用/禁用 (1) 输出中的颜色。可以设置为 always、false（或 never）或 auto（或 true），在这种情况下，颜色仅当输出到终端时使用。默认为 false。

### color.status.<slot>

为状态着色使用自定义颜色。`<slot>` 是 header（状态消息的头部文本）、added 或 updated（已添加但未提交的文件）、changed（已更改但未在索引中添加的文件）、untracked（Git 未跟踪的文件）、branch（当前分支）、nobranch（显示无分支警告的颜色，默认为红色）或 unmerged（具有未合并更改的文件）之一。

## color.ui

该变量确定控制每个命令族中颜色使用（如 `color.diff` 和 `color.grep`）的变量的默认值。其范围将随着更多命令学习设置 `—color` 选项默认值的配置而扩展。如果你希望 Git 命令除非通过其他配置或 `—color` 选项明确启用否则不使用颜色，请将其设置为 false 或 never。如果你希望所有不打算供机器读取的输出都使用颜色，请将其设置为 always；如果你希望此类输出在写入终端时使用颜色，请将其设置为 true 或 auto（自 Git 1.8.4 起这是默认设置）。

## column.ui

指定支持的命令是否应输出为列。该变量由空格或逗号分隔的令牌列表组成：

这些选项控制何时启用该功能（默认为 never）：

- always
  始终以列形式显示
- never
  从不以列形式显示
- auto
  如果输出到终端，则以列形式显示

这些选项控制布局（默认为 column）。如果未指定 always、never 或 auto 中的任何一个，设置其中任何一个都隐式表示 always。

- column
  先填充列再填充行

