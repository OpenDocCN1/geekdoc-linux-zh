

可以通过指定此变量值的程序来指示其使用外部程序。可被 `GIT_ASKPASS` 环境变量覆盖。如果未设置，则回退到 `SSH_ASKPASS` 环境变量的值，若仍失败，则使用简单的密码提示。外部程序应接受一个合适的提示作为命令行参数，并将其在 STDOUT 上写入密码。

## core.attributesFile

除了 `.gitattributes`（每目录）和 `.git/info/attributes` 之外，Git 还会在此文件中查找属性（参见 *gitattributes*(5)）。路径扩展的方式与 `core.excludesFile` 相同。其默认值为 `$XDG_CONFIG_HOME/git/attributes`。如果 `$XDG_CONFIG_HOME` 未设置或为空，则使用 `$HOME/.config/git/attributes`。

## core.editor

如 commit 和 tag 等允许通过启动编辑器编辑消息的命令，若此变量已设置且环境变量 `GIT_EDITOR` 未设置，则使用该变量的值。参见 *git-editor*(1)。

## core.commentChar

如 commit 和 tag 等允许编辑消息的命令，将视为以该字符开头的行是注释，并在编辑器返回后将其移除（默认值为 `#`）。

如果设置为 `auto`，git-commit 会选择一个字符，该字符不是现有提交信息中任何一行的起始字符。

## core.packedRefsTimeout

在尝试锁定 packed-refs 文件时重试的时间长度，单位为毫秒。值为 0 表示完全不重试；-1 表示无限期尝试。默认值为 1000（即重试 1 秒）。

## sequence.editor

git rebase -i 用于编辑 rebase 指令文件的文本编辑器。该值的含义是将被 shell 解释。可被 `GIT_SEQUENCE_EDITOR` 环境变量覆盖。若未配置，则使用默认的提交消息编辑器。

## core.pager

用于 Git 命令的文本查看器（例如 less）。该值的含义是将被 shell 解释。优先级顺序为：`$GIT_PAGER` 环境变量，然后是 `core.pager` 配置，然后是 `$PAGER`，最后是编译时选择的默认值（通常是 less）。

当 `LESS` 环境变量未设置时，Git 会将其设置为 `FRX`（如果 `LESS` 环境变量已设置，Git 完全不会修改它）。如果想有选择性地覆盖 Git 对 `LESS` 的默认设置，可以将 `core.pager` 设置为例如 `less -S`。Git 会将其传递给 shell，shell 会将最终命令转换为 `LESS=FRX less -S`。环境变量没有设置 S 选项，但命令行设置了，这指示 less 截断长行。类似地，将 `core.pager` 设置为 `less -+F` 会禁用由命令行指定的环境变量中设置的 F 选项，从而停用 less 的“如果只有一屏则退出”行为。可以为特定命令专门启用某些标志：例如，将 `pager.blame` 设置为 `less -S` 仅为 git blame 启用行截断。

同样，当 `LV` 环境变量未设置时，Git 会将其设置为 `-c`。可以通过导出另一个值的 `LV` 或将 `core.pager` 设置为 `lv +c` 来覆盖此设置。

## core.whitespace

用于标记常见空白问题的逗号分隔列表。`git diff` 将使用 `color.diff.whitespace` 来高亮显示它们，而 `git apply --whitespace=error` 将把它们视为错误。可以在前面加 `-` 来禁用其中任意一个（例如 `-trailing-space`）：

- `blank-at-eol` 将行尾的空格视为错误（默认启用）。
- `space-before-tab` 将初始缩进部分中紧接在制表符字符之前的空格字符视为错误（默认启用）。
- `indent-with-non-tab` 将用空格字符而非等效制表符缩进的行视为错误（默认未启用）。
- `tab-in-indent` 将初始缩进部分中的制表符字符视为错误（默认未启用）。
- `blank-at-eof` 将文件末尾添加的空行视为错误（默认启用）。
- `trailing-space` 是涵盖 `blank-at-eol` 和 `blank-at-eof` 两者的简写。
- `cr-at-eol` 将行末的回车视为行终止符的一部分，即在这种情况下，如果此类回车前的字符不是空格，则不会触发 `trailing-space`（默认未启用）。
- `tabwidth=<n>` 指定制表符占据多少个字符位置；这与 `indent-with-non-tab` 相关，并在 Git 修复 `tab-in-indent` 错误时相关。默认制表符宽度为 8。允许的值为 1 到 63。

## core.fsObjectFiles

此布尔值将在写入对象文件时启用 `fsync()`。

对于正确排序数据写入的文件系统，这是时间和精力的完全浪费，但对于不使用日志记录（传统 UNIX 文件系统）或仅记录元数据而不记录文件内容的文件系统（如 OS X 的 HFS+，或带有“data=writeback”选项的 Linux ext3）可能很有用。

## core.preloadIndex

为 *git diff* 等启用并行索引预加载

这可以加速 *git diff* 和 *git status* 等操作，尤其是在缓存语义较弱且 I/O 延迟相对较高的 NFS 等文件系统上。启用后，Git 将并行执行索引与文件系统数据的比较，允许 I/O 重叠。默认为 true。

## core.createObject

您可以将此设置为 *link*，在这种情况下，将使用硬链接后删除源文件，以确保对象创建不会覆盖现有对象。

在某些文件系统/操作系统组合上，这是不可靠的。请在那里将此配置设置为 *rename*；然而，这将移除确保现有对象文件不会被覆盖的检查。

## core.notesRef

显示提交消息时，也显示存储在给定引用中的注释。引用必须完全限定。如果给定的引用不存在，这不是错误，但意味着不应打印任何注释。

此设置默认为 `refs/notes/commits`，可被 `GIT_NOTES_REF` 环境变量覆盖。参见 *git-notes*(1)。

## core.sparseCheckout

启用“稀疏检出”功能。更多信息请参见 *git-config*(1) 中的“Sparse checkout”部分。

## core.abbrev

设置对象名称缩写长度。如果未指定，许多命令会缩写为 7 个十六进制数字，这对于缩写对象名称在足够长的时间内保持唯一性可能不够。

## add.ignoreErrors, add.ignore-errors（已弃用）

指示 *git add* 在由于索引错误导致某些文件无法添加时继续添加文件。等同于 *git-add*(1) 的 *--ignore-errors* 选项。`add.ignore-errors` 已弃用，因为它不符合配置变量的通常命名约定。

## alias.*

*git* 命令包装器的命令别名 - 例如，在定义 `alias.last = cat-file commit HEAD` 之后，调用 `git last` 等同于 `git cat-file commit HEAD`。为了避免与脚本使用产生混淆和麻烦，隐藏现有 Git 命令的别名将被忽略。参数通过空格分割，支持普通的 shell 引用和转义。可以使用引号对或反斜杠来引用它们。

如果别名扩展以感叹号开头，则将其视为 shell 命令。例如，定义 `alias.new = !gitk --all --not ORIG_HEAD` 后，调用 `git new` 等同于运行 shell 命令 `gitk --all --not ORIG_HEAD`。请注意，shell 命令将从仓库的顶级目录执行，这可能不一定是当前目录。`GIT_PREFIX` 设置为从原始当前目录运行 `git rev-parse --show-prefix` 返回的值。参见 *git-config*(1)。

## am.keepcr

如果为 true，`git-am` 将在 mbox 格式的补丁上调用 `git-mailsplit` 并带有参数 `--keep-cr`。在这种情况下 `git-mailsplit` 不会从以 `\r\n` 结尾的行中删除 `\r`。可以通过从命令行提供 `--no-keep-cr` 来覆盖。参见 *git-am*(1)，*git-mailsplit*(1)。

## apply.ignoreWhitespace

当设置为 `change` 时，指示 `git apply` 忽略空白变化，方式与 `--ignore-space-change` 选项相同。当设置为以下之一时：`no`、`none`、`never`、`false` 指示 `git apply` 尊重所有空白差异。参见 *git-apply*(1)。

## apply.whitespace

指示 `git apply` 如何处理空白，方式与 `--whitespace` 选项相同。参见 *git-apply*(1)。

## branch.autoSetupMerge

指示 `git branch` 和 `git checkout` 设置新分支，以便 *pull* 能够适当地从起点分支进行合并。请注意，即使未设置此选项，也可以使用 `--track` 和 `--no-track` 选项针对每个分支选择此行为。有效的设置为：

- `false` -- 不进行自动设置
- `true` -- 当起点是远程跟踪分支时进行自动设置
- `always` -- 当起点是本地分支或远程跟踪分支时进行自动设置

此选项默认为 `true`。

## branch.autoSetupRebase

当使用 `git branch` 或 `git checkout` 创建跟踪另一个分支的新分支时，此变量指示 Git 将 pull 设置为 rebase 而不是 merge（参见 `branch.<name>.rebase`）。当为 `never` 时，rebase 永远不会自动设置为 `true`。当为 `local` 时，对于跟踪其他本地分支的分支，rebase 设置为 `true`。当为 `remote` 时，对于跟踪远程跟踪分支的分支，rebase 设置为 `true`。当为 `always` 时，对于所有跟踪分支，rebase 将设置为 `true`。有关如何设置分支以跟踪另一个分支的详细信息，参见 `branch.autoSetupMerge`。此选项默认为 `never`。

## branch.<name>.remote

当在分支 `<name>` 上时，它告诉 `git fetch` 和 `git push` 从哪个远程获取/推送到哪个远程。推送到哪个远程可以被 `remote.pushDefault`（对所有分支）覆盖。当前分支推送到哪个远程可以进一步被 `branch.<name>.pushRemote` 覆盖。如果未配置远程，或您不在任何分支上，对于获取，它默认为 `origin`，对于

