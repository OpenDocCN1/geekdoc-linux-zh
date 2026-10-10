

## status.displayCommentPrefix

如果设置为 true，(1) 将在每一行输出前插入注释前缀（以 core.commentChar 开头，默认即为 #）。这是 Git 1.8.4 及更早版本中 (1) 的行为。默认为 false。

## status.showUntrackedFiles

默认情况下，(1) 和 (1) 会显示当前未被 Git 跟踪的文件。仅包含未跟踪文件的目录，只显示目录名称。显示未跟踪文件意味着 Git 需要 lstat() 整个仓库中的所有文件，这在某些系统上可能很慢。因此，该变量控制命令如何显示未跟踪文件。可能的值如下：

- no - 不显示未跟踪文件。
- normal - 显示未跟踪的文件和目录。
- all - 还显示未跟踪目录中的单个文件。

如果未指定此变量，默认为 normal。该变量可以通过 (1) 和 (1) 的 -u|--untracked-files 选项进行覆盖。

## status.submoduleSummary

默认为 false。如果将其设置为非零数字或 true（等同于 -1 或无限数量），将启用子模块摘要，并显示已修改子模块的提交摘要（参见 (1) 的 --summary-limit 选项）。请注意，当 diff.ignoreSubmodules 设置为 all 时，或者仅针对那些 submodule.<name>.ignore=all 的子模块时，摘要输出命令将被抑制。该规则唯一的例外是 status 和 commit 会显示已暂存的子模块更改。若要查看被忽略子模块的摘要，可以使用 --ignore-submodules=dirty 命令行选项或 git submodule summary 命令，后者显示类似的输出，但不会遵循这些设置。

## submodule.<name>.path, submodule.<name>.url

子模块在此项目中的路径和 URL。这些变量最初由 git submodule init 填充。详见 (1) 和 (5)。

## submodule.<name>.update

子模块的默认更新过程。该变量由 git submodule init 从 (5) 文件中填充。参见 (1) 中 update 命令的描述。

## submodule.<name>.branch

子模块的远程分支名称，由 git submodule update -remote 使用。设置此选项以覆盖 .gitmodules 文件中找到的值。详见 (1) 和 (5)。

## submodule.<name>.fetchRecurseSubmodules

此选项可用于控制此子模块的递归获取。可以通过使用 "git fetch" 和 "git pull" 的 `[--]no-]recurse-submodules` 命令行选项进行覆盖。此设置将覆盖 (5) 文件中该文件的设置。

## submodule.<name>.ignore

定义 "git status" 和 diff 家族何时将子模块显示为已修改。当设置为 "all" 时，它永远不会被视为已修改（但如果在它已暂存的情况下，它仍会显示在 status 和 commit 的输出中）；"dirty" 会忽略子模块工作树中的所有更改，并仅考虑子模块的 HEAD 与父项目中记录的提交之间的差异。"untracked" 此外还会让工作树中具有已修改跟踪文件的子模块显示出来。使用 "none"（此选项未设置时的默认值）还会将工作树中具有未跟踪文件的子模块显示为已更改。此设置会覆盖 .gitmodules 中针对此子模块的任何设置，这两个设置都可以通过使用 "`[--]ignore-submodules`" 选项在命令行上覆盖。*git submodule* 命令不受此设置影响。

## tag.sort

此变量控制标签在 (1) 中显示时的排序顺序。如果未提供 "`--sort=<value>`" 选项，将使用此变量的值作为默认值。

## tar.umask

此变量可用于限制 tar 归档条目的权限位。默认值为 0002，这会关闭全局写权限位。特殊值 "user" 表示将使用归档用户的 umask 代替。参见 (2) 和 (1)。

## transfer.fsckObjects

当 fetch.fsckObjects 或 receive.fsckObjects 未设置时，将使用此变量的值代替。默认为 false。

## transfer.hideRefs

此变量可用于同时设置 receive.hideRefs 和 uploadpack.hideRefs 为相同的值。参见这些其他变量的条目。

## transfer.unpackLimit

当 fetch.unpackLimit 或 receive.unpackLimit 未设置时，将使用此变量的值代替。默认值为 100。

## uploadarchive.allowUnreachable

如果为 true，允许客户端使用 git archive `--remote` 请求任何树，无论其是否可从引用尖端到达。更多详情请参见 (1) 的 SECURITY 部分中的讨论。默认为 false。

## uploadpack.hideRefs

upload-pack 使用的字符串，用于决定在初始通告中省略哪些引用。使用多个定义来指定多个前缀字符串。位于此变量值所列层次结构下的引用将被排除，并对 git ls-remote、git fetch 等隐藏。尝试通过 git fetch 获取隐藏引用将会失败。另见 uploadpack.allowTipSHA1InWant。

## uploadpack.allowTipSHA1InWant

当 uploadpack.hideRefs 生效时，允许 upload-pack 接受请求获取隐藏引用尖端处的对象的 fetch 请求（默认情况下，此类请求会被拒绝）。另见 uploadpack.hideRefs。

## uploadpack.allowReachableSHA1InWant

允许 upload-pack 接受请求获取可从任何引用尖端到达的对象的 fetch 请求。但请注意，计算对象可达性在计算上是昂贵的。默认为 false。

## uploadpack.keepAlive

当 upload-pack 已启动 pack-objects 时，在 pack-objects 准备打包期间可能会有一个静默期。通常它会输出进度信息，但如果获取时使用了 — quiet，pack-objects 在打包数据开始之前将完全不输出任何内容。某些客户端和网络可能会认为服务器已挂起并放弃。设置此选项指示 upload-pack 每隔 uploadpack.keepAlive 秒发送一个空的心跳包。将此选项设置为 0 将完全禁用心跳包。默认值为 5 秒。

## url.<base>.insteadOf

任何以此值开头的 URL 都会被重写为以 <base> 开头。在某些站点提供大量仓库、并通过多种访问方式提供服务、且某些用户需要使用不同访问方式的情况下，此功能允许人们指定任何等效的 URL，并让 Git 自动将 URL 重写为该特定用户的最佳替代方案，即使对于该站点上从未见过的仓库也是如此。当多个 insteadOf 字符串匹配给定 URL 时，使用最长的匹配。

## url.<base>.pushInsteadOf

任何以此值开头的 URL 都不会被推送；相反，它将被重写为以 <base> 开头，并将重写后的 URL 作为推送目标。在某些站点提供大量仓库、并通过多种访问方式提供服务（其中某些方式不允许推送）的情况下，此功能允许人们指定一个仅限拉取的 URL，并让 Git 自动使用适当的 URL 进行推送，即使对于该站点上从未见过的仓库也是如此。当多个 pushInsteadOf 字符串匹配给定 URL 时，使用最长的匹配。如果远程仓库有显式的 pushurl，Git 将忽略此设置对该远程仓库的影响。

## user.email

要在任何新创建的提交中记录的电子邮件地址。可被 `GIT_AUTHOR_EMAIL`、`GIT_COMMITTER_EMAIL` 和 `EMAIL` 环境变量覆盖。参见 (1)。

## user.name

要在任何新创建的提交中记录的全名。可被 `GIT_AUTHOR_NAME` 和 `GIT_COMMITTER_NAME` 环境变量覆盖。参见 (1)。

## user.signingKey

如果 (1) 或 (1) 在创建签名标签或提交时未自动选择您想要的密钥，您可以使用此变量覆盖默认选择。此选项原封不动地传递给 gpg 的 “—local-user” 参数，因此您可以使用 gpg 支持的任何方法指定密钥。

## versionsort.prereleaseSuffix

当在 (1) 中使用版本排序时，预发布标签（例如 “1.0-rc1”）可能出现在主发布版本 “1.0” 之后。通过在此变量中指定后缀 “-rc”，“1.0-rc1” 将出现在 “1.0” 之前。

此变量可以指定多次，每个后缀一次。配置文件中的后缀顺序决定了排序顺序（例如，如果 “-pre” 在配置文件中出现在 “-rc” 之前，则 1.0-preXX 的排序在 1.0-rcXX 之前）。如果它们位于多个配置文件中，不同后缀之间的排序顺序是未定义的。

## web.browser

指定一个可能由某些命令使用的 Web 浏览器。目前只有 (1) 和 (1) 可能会使用它。

