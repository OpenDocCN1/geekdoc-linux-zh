
激活已解决冲突的记录，以便相同的冲突块如果再次遇到，可以自动解决。默认情况下，如果 `$GIT_DIR` 下存在 `rr-cache` 目录，则启用 (1)，例如，如果在仓库中之前使用过 `rerere`。

### `sendemail.identity`

一个配置身份。当给定此值时，`*sendmail.identity*` 小节中的值将优先于 `*sendemail*` 部分中的值。默认身份是 `*sendemail.identity*` 的值。

### `sendemail.smtpEncryption`

参见 (1) 了解描述。注意，此设置不受 `*identity*` 机制的影响。

### `sendemail.smtpssl` (已弃用)

`*sendemail.smtpEncryption = ssl*` 的已弃用别名。

### `sendemail.smtpsslcertpath`

ca-certificates 的路径（可以是目录或单个文件）。将其设置为空字符串以禁用证书验证。

### `sendemail.<identity>.*.`

`*sendemail.*` 参数的身份特定版本，当通过命令行或 `*sendemail.identity*` 选择此身份时，它们优先于上述参数。

### `sendemail.aliasesFile`, `sendemail.aliasFileType`, `sendemail.annotate`, `sendemail.bcc`, `sendemail.cc`, `sendemail.ccCmd`, `sendemail.chainReplyTo`, `sendemail.confirm`, `sendemail.envelopeSender`, `sendemail.from`, `sendemail.multiEdit`, `sendemail.signedoffbycc`, `sendemail.smtpPass`, `sendemail.suppresscc`, `sendemail.suppressFrom`, `sendemail.to`, `sendemail.smtpDomain`, `sendemail.smtpServer`, `sendemail.smtpServerPort`, `sendemail.smtpServerOption`, `sendemail.smtpUser`, `sendemail.thread`, `sendemail.transferEncoding`, `sendemail.validate`, `sendemail.xmailer`

参见 (1) 了解描述。

### `sendemail.signedoffcc` (已弃用)

`*sendemail.signedoffbycc*` 的已弃用别名。

### `showbranch.default`

(1) 的默认分支集合。参见 (1)。

### `status.relativePaths`

默认情况下，(1) 显示相对于当前目录的路径。将此变量设置为 `*false*` 将显示相对于仓库根目录的路径（这是 Git `*v1.5.4*` 之前的默认行为）。

### `status.short`

设置为 `*true*` 以在 (1) 中默认启用 `--short`。选项 `--no-short` 优先于此变量。

### `status.branch`

设置为 `*true*` 以在 (1) 中默认启用 `--branch`。选项 `--no-branch` 优先于此变量。

## `status.displayCommentPrefix`

如果设置为 true，(1) 将在每一行输出前插入注释前缀（以 `core.commentChar` 开头，默认即为 #）。这是 Git 1.8.4 及更早版本中 (1) 的行为。默认为 false。

## `status.showUntrackedFiles`

默认情况下，(1) 和 (1) 会显示当前未被 Git 跟踪的文件。仅包含未跟踪文件的目录，只显示目录名称。显示未跟踪文件意味着 Git 需要 `lstat()` 整个仓库中的所有文件，这在某些系统上可能很慢。因此，该变量控制命令如何显示未跟踪文件。可能的值如下：

- no - 不显示未跟踪文件。
- normal - 显示未跟踪的文件和目录。
- all - 还显示未跟踪目录中的单个文件。

如果未指定此变量，默认为 normal。该变量可以通过 (1) 和 (1) 的 `-u|--untracked-files` 选项进行覆盖。

## `status.submoduleSummary`

默认为 false。如果将其设置为非零数字或 true（等同于 -1 或无限数量），将启用子模块摘要，并显示已修改子模块的提交摘要（参见 (1) 的 `--summary-limit` 选项）。请注意，当 `diff.ignoreSubmodules` 设置为 all 时，或者仅针对那些 `submodule.<name>.ignore=all` 的子模块时，摘要输出命令将被抑制。该规则唯一的例外是 `status` 和 `commit` 会显示已暂存的子模块更改。若要查看被忽略子模块的摘要，可以使用 `--ignore-submodules=dirty` 命令行选项或 `git submodule summary` 命令，后者显示类似的输出，但不会遵循这些设置。

## `submodule.<name>.path`, `submodule.<name>.url`

子模块在此项目中的路径和 URL。这些变量最初由 `git submodule init` 填充。详见 (1) 和 (5)。

## `submodule.<name>.update`

子模块的默认更新过程。该变量由 `git submodule init` 从 (5) 文件中填充。参见 (1) 中 `update` 命令的描述。

## `submodule.<name>.branch`

子模块的远程分支名称，由 `git submodule update -remote` 使用。设置此选项以覆盖 `.gitmodules` 文件中找到的值。详见 (1) 和 (5)。

## `submodule.<name>.fetchRecurseSubmodules`

此选项可用于控制此子模块的递归获取。可以通过使用 "`git fetch`" 和 "`git pull`" 的 `[--]no-]recurse-submodules` 命令行选项进行覆盖。此设置将覆盖 (5) 文件中该文件的设置。

## `submodule.<name>.ignore`

定义 "`git status`" 和 `diff` 家族何时将子模块显示为已修改。当设置为 "all" 时，它永远不会被视为已修改（但如果在它已暂存的情况下，它仍会显示在 `status` 和 `commit` 的输出中）；"dirty" 会忽略子模块工作树中的所有更改，并仅考虑子模块的 HEAD 与父项目中记录的提交之间的差异。"untracked" 此外还会让工作树中具有已修改跟踪文件的子模块显示出来。使用 "none"（此选项未设置时的默认值）还会将工作树中具有未跟踪文件的子模块显示为已更改。此设置会覆盖 `.gitmodules` 中针对此子模块的任何设置，这两个设置都可以通过使用 "`[--]ignore-submodules`" 选项在命令行上覆盖。`*git submodule*` 命令不受此设置影响。

## `tag.sort`

此变量控制标签在 (1) 中显示时的排序顺序。如果未提供 "`--sort=<value>`" 选项，将使用此变量的值作为默认值。

## `tar.umask`

此变量可用于限制 tar 归档条目的权限位。默认值为 0002，这会关闭全局写权限位。特殊值 "user" 表示将使用归档用户的 umask 代替。参见 (2) 和 (1)。

## `transfer.fsckObjects`

当 `fetch.fsckObjects` 或 `receive.fsckObjects` 未设置时，将使用此变量的值代替。默认为 false。

## `transfer.hideRefs`

此变量可用于同时设置 `receive.hideRefs` 和 `uploadpack.hideRefs` 为相同的值。参见这些其他变量的条目。

## `transfer.unpackLimit`

当 `fetch.unpackLimit` 或 `receive.unpackLimit` 未设置时，将使用此变量的值代替。默认值为 100。

## `uploadarchive.allowUnreachable`

如果为 true，允许客户端使用 `git archive --remote` 请求任何树，无论其是否可从引用尖端到达。更多详情请参见 (1) 的 SECURITY 部分中的讨论。默认为 false。

## `uploadpack.hideRefs`
