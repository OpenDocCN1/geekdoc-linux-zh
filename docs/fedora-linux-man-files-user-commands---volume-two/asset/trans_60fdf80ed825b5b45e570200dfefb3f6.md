
## gvimdiff2
## gvimdiff3
## kdiff3
## kompare
## meld
## opendiff
## p4merge
## tkdiff
## vimdiff
## vimdiff2
## vimdiff3
## winmerge
## xxdiff

## diff.algorithm

选择一个差异算法。变体如下：

-   default, myers
    基本的贪心差异算法。目前，这是默认设置。
-   minimal
    花费额外时间以确保生成最小的可能差异。
-   patience
    在生成补丁时使用“patience diff”（耐心差异）算法。
-   histogram
    此算法扩展了耐心算法，以“支持低出现频率的公共元素”。

## difftool.<tool>.path

覆盖给定工具的路径。如果您的工具不在 PATH 中，这会有用。

## difftool.<tool>.cmd

指定调用指定差异工具的命令。指定的命令将在 shell 中评估，并提供以下变量：LOCAL 设置为包含差异前像内容的临时文件名称，REMOTE 设置为包含差异后像内容的临时文件名称。

## difftool.prompt

在每次调用差异工具之前进行提示。

## fetch.recurseSubmodules

此选项可以设置为布尔值或 *on-demand*。将其设置为布尔值会改变 fetch 和 pull 的行为：当设置为 true 时，无条件地递归进入子模块；当设置为 false 时，完全不递归。当设置为 *on-demand*（默认值）时，fetch 和 pull 仅在超级项目获取更新子模块引用的提交时，才递归到已填充的子模块中。

## fetch.fsckObjects

如果设置为 true，git-fetch-pack 将检查所有获取的对象。如果存在格式错误的对象或损坏的链接，它将中止。中止的结果仅是悬挂对象。默认为 false。如果未设置，则使用 transfer.fsckObjects 的值。

## fetch.unpackLimit

如果通过 Git 原生传输获取的对象数量低于此限制，则这些对象将解包为松散对象文件。但是，如果接收到的对象数量等于或超过此限制，则在添加任何缺失的 delta 基础后，接收到的 pack 将被存储为 pack。存储来自 push 的 pack 可以加快 push 操作完成速度，特别是在慢速文件系统上。如果未设置，则使用 transfer.unpackLimit 的值。

## fetch.prune

如果为 true，fetch 将自动表现得像在命令行中给出了 `--prune` 选项一样。另见 remote.<name>.prune。

## format.attach

启用 multipart/mixed 附件作为 *format-patch* 的默认设置。该值也可以是双引号字符串，这将启用附件作为默认设置并设置该值作为边界。请参阅 (1) 中的 `--attach` 选项。

## format.numbered

一个布尔值，可以启用或禁用补丁主题中的序列号。它默认为“auto”，仅当存在多个补丁时启用。可以通过将其设置为“true”或“false”来为所有消息启用或禁用。请参阅 (1) 中的 `--numbered` 选项。

## format.headers

要包含在通过邮件提交的补丁中的额外邮件头。请参阅 (1)。

## format.to, format.cc

要包含在通过邮件提交的补丁中的额外收件人。请参阅 (1) 中的 `--to` 和 `--cc` 选项。

## format.subjectPrefix

`format-patch` 的默认行为是输出带有 `[PATCH]` 主题前缀的文件。使用此变量更改该前缀。

## format.signature

`format-patch` 的默认行为是输出包含 Git 版本号的签名。使用此变量更改该默认设置。将此变量设置为空字符串（`""`）以抑制签名生成。

## format.signatureFile

它与 `format.signature` 的作用相同，除了使用此变量指定的文件内容作为签名。

## format.suffix

`format-patch` 的默认行为是输出带有后缀 `.patch` 的文件。使用此变量更改该后缀（如果您想要，请确保包含点号）。

## format.pretty

`log`/`show`/`whatchanged` 命令的默认 `pretty` 格式，请参阅 (1), (1), (1)。

## format.thread

`git format-patch` 的默认线程化样式。可以是布尔值，或者 `shallow` 或 `deep`。`shallow` 线程化使每封邮件都是系列顶部的回复，顶部按顺序从 cover letter、`--in-reply-to` 和第一封补丁邮件中选择。`deep` 线程化使每封邮件都是前一封的回复。布尔 true 值等同于 `shallow`，而 false 值禁用线程化。

## format.signOff

一个布尔值，允许默认启用 `format-patch` 的 `-s/--signoff` 选项。**注意：**向补丁添加 `Signed-off-by:` 行应该是有意识的行为，意味着您保证您有权在相同的开源许可下提交此工作。请参阅 *SubmittingPatches* 文档以获取进一步讨论。

## format.coverLetter

一个控制当调用 `format-patch` 时是否生成 cover-letter 的布尔值，但也可以设置为“`auto`”，仅在有一个以上的补丁时生成 cover-letter。

## filter.<driver>.clean

用于在签入时将工作树文件内容转换为 blob 的命令。请参阅 (5) 以获取详细信息。

## filter.<driver>.smudge

用于在签出时将 blob 对象内容转换为工作树文件的命令。请参阅 (5) 以获取详细信息。

## gc.aggressiveDepth

*git gc* `--aggressive` 使用的 delta 压缩算法中的深度参数。这默认为 250。

## gc.aggressiveWindow

*git gc* `--aggressive` 使用的 delta 压缩算法中的窗口大小参数。这默认为 250。

## gc.auto

当仓库中松散对象的数量大约超过这个数值时，git gc --auto 将对它们进行打包。一些 Porcelain 命令使用此命令定期执行轻量级垃圾回收。默认值为 6700。将其设置为 0 将禁用此功能。

## gc.autoPackLimit

当仓库中未标记有 *.keep 文件的 pack 数量超过此数值时，git gc `--auto` 会将它们合并为一个更大的 pack。默认值为 50。将其设置为 0 将禁用此功能。

## gc.autoDetach

如果系统支持，使 *git gc* `--auto` 立即返回并在后台运行。默认为 true。

## gc.packRefs

在仓库中运行 *git pack-refs* 会使其无法通过 1.5.1.2 之前的 Git 版本在如 HTTP 等哑传输协议下进行克隆。此变量确定 *git gc* 是否运行 *git pack-refs*。可以将其设置为 *notbare* 以在所有非裸仓库中启用，或者设置为布尔值。默认为 *true*。

## gc.pruneExpire

当运行 *git gc* 时，它会调用 *prune* `--expire 2.weeks.ago`。使用此配置变量覆盖宽限期。值“now”可用于禁用此宽限期并立即修剪不可达对象。

## gc.pruneWorktreesExpire

当运行 *git gc* 时，它会调用 *prune* `--worktrees` `--expire 3.months.ago`。使用此配置变量覆盖宽限期。值“now”可用于禁用宽限期并立即修剪 $GIT_DIR/worktrees。

## gc.reflogExpire, gc.<pattern>.reflogExpire

*git reflog expire* 删除早于此时间的 reflog 条目；默认为 90 天。如果在中间使用“<pattern>”（例如“refs/stash”），则该设置仅应用于匹配 <pattern> 的 refs。

## gc.reflogExpireUnreachable, gc.<ref>.reflogExpireUnreachable

git reflog expire 删除早于此时间且不可达自当前 tip 的 reflog 条目；默认为 30 天。如果在中间使用“<pattern>”（例如“refs/stash”），则该设置仅应用于匹配 <pattern> 的 refs。

## gc.rerereResolved

当运行 git rerere gc 时，您之前解决的冲突合并记录将保留此天数。默认为 60 天。请参阅 (1)。

## gc.rerereUnresolved

当运行 git rerere gc 时，您尚未解决的冲突合并记录将保留此天数。默认为 15 天。请参阅 (1)。

## gitcvs.commitMsgAnnotation

将此字符串附加到每个提交消息。设置为空字符串以禁用此功能。默认为“via git-CVS emulator”。

## gitcvs.enabled

是否为此仓库启用 CVS 服务器接口。请参阅 (1)。

## gitcvs.logFile

CVS 服务器接口记录各种内容的日志文件路径。请参阅 (1)。

## gitcvs.usercrfileattr

如果为 true，服务器将查找文件的行尾转换属性以确定要使用的 -k 模式。如果属性强制 Git 将文件视为文本，则 -k 模式将留空，以便 CVS 客户端将其视为文本。如果它们抑制文本转换，则文件将设置为 -kb 模式，这会抑制客户端可能做的任何换行符处理。如果属性不允许确定文件类型，则使用 gitcvs.allBinary。请参阅 (5)。

## gitcvs.allBinary

如果 gitcvs.usercrfileattr 未能解决要使用的正确 -kb 模式，则使用此设置。如果为 true，所有未解析的文件将以 -kb 模式发送到客户端。这导致客户端将它们视为二进制文件，从而抑制其可能做的任何换行符处理。或者，如果设置为“guess”，则检查文件内容以决定它是否为二进制，类似于 core.autocrlf。

## gitcvs.dbName

git-cvsserver 用于缓存从 Git 仓库派生的修订信息的数据库。确切含义取决于使用的数据库驱动程序，对于 SQLite（默认驱动程序）这是一个文件名。支持变量替换（详见 (1)）。不得包含分号 (;)。默认值: %Ggitcvs.%m.sqlite

## gitcvs.dbDriver

使用的 Perl DBI 驱动程序。您可以在此指定任何可用驱动程序，但它可能无法工作。git-cvsserver 已使用 DBD::SQLite 进行测试，据报道与 DBD::Pg 兼容，
