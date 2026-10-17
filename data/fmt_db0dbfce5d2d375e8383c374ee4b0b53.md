
用于在签入时将工作树文件内容转换为 blob 的命令。请参阅 `(5)` 以获取详细信息。

### `filter.<driver>.smudge`
用于在签出时将 blob 对象内容转换为工作树文件的命令。请参阅 `(5)` 以获取详细信息。

### `gc.aggressiveDepth`
`git gc` `--aggressive` 使用的 delta 压缩算法中的深度参数。这默认为 `250`。

### `gc.aggressiveWindow`
`git gc` `--aggressive` 使用的 delta 压缩算法中的窗口大小参数。这默认为 `250`。

### `gc.auto`
当仓库中松散对象的数量大约超过这个数值时，`git gc --auto` 将对它们进行打包。一些 Porcelain 命令使用此命令定期执行轻量级垃圾回收。默认值为 `6700`。将其设置为 `0` 将禁用此功能。

### `gc.autoPackLimit`
当仓库中未标记有 `*.keep` 文件的 pack 数量超过此数值时，`git gc --auto` 会将它们合并为一个更大的 pack。默认值为 `50`。将其设置为 `0` 将禁用此功能。

### `gc.autoDetach`
如果系统支持，使 `git gc --auto` 立即返回并在后台运行。默认为 `true`。

### `gc.packRefs`
在仓库中运行 `git pack-refs` 会使其无法通过 `1.5.1.2` 之前的 Git 版本在如 HTTP 等哑传输协议下进行克隆。此变量确定 `git gc` 是否运行 `git pack-refs`。可以将其设置为 `notbare` 以在所有非裸仓库中启用，或者设置为布尔值。默认为 `true`。

### `gc.pruneExpire`
当运行 `git gc` 时，它会调用 `prune --expire 2.weeks.ago`。使用此配置变量覆盖宽限期。值 `now` 可用于禁用此宽限期并立即修剪不可达对象。

### `gc.pruneWorktreesExpire`
当运行 `git gc` 时，它会调用 `prune --worktrees --expire 3.months.ago`。使用此配置变量覆盖宽限期。值 `now` 可用于禁用宽限期并立即修剪 `$GIT_DIR/worktrees`。

### `gc.reflogExpire`, `gc.<pattern>.reflogExpire`
`git reflog expire` 删除早于此时间的 reflog 条目；默认为 `90` 天。如果在中间使用 `<pattern>`（例如 `refs/stash`），则该设置仅应用于匹配 `<pattern>` 的 refs。

### `gc.reflogExpireUnreachable`, `gc.<ref>.reflogExpireUnreachable`
`git reflog expire` 删除早于此时间且不可达自当前 tip 的 reflog 条目；默认为 `30` 天。如果在中间使用 `<pattern>`（例如 `refs/stash`），则该设置仅应用于匹配 `<pattern>` 的 refs。

### `gc.rerereResolved`
当运行 `git rerere gc` 时，您之前解决的冲突合并记录将保留此天数。默认为 `60` 天。请参阅 `(1)`。

### `gc.rerereUnresolved`
当运行 `git rerere gc` 时，您尚未解决的冲突合并记录将保留此天数。默认为 `15` 天。请参阅 `(1)`。

### `gitcvs.commitMsgAnnotation`
将此字符串附加到每个提交消息。设置为空字符串以禁用此功能。默认为 `via git-CVS emulator`。

### `gitcvs.enabled`
是否为此仓库启用 CVS 服务器接口。请参阅 `(1)`。

### `gitcvs.logFile`
CVS 服务器接口记录各种内容的日志文件路径。请参阅 `(1)`。

### `gitcvs.usercrfileattr`
如果为 `true`，服务器将查找文件的行尾转换属性以确定要使用的 `-k` 模式。如果属性强制 Git 将文件视为文本，则 `-k` 模式将留空，以便 CVS 客户端将其视为文本。如果它们抑制文本转换，则文件将设置为 `-kb` 模式，这会抑制客户端可能做的任何换行符处理。如果属性不允许确定文件类型，则使用 `gitcvs.allBinary`。请参阅 `(5)`。

### `gitcvs.allBinary`
如果 `gitcvs.usercrfileattr` 未能解决要使用的正确 `-kb` 模式，则使用此设置。如果为 `true`，所有未解析的文件将以 `-kb` 模式发送到客户端。这导致客户端将它们视为二进制文件，从而抑制其可能做的任何换行符处理。或者，如果设置为 `guess`，则检查文件内容以决定它是否为二进制，类似于 `core.autocrlf`。

### `gitcvs.dbName`
`git-cvsserver` 用于缓存从 Git 仓库派生的修订信息的数据库。确切含义取决于使用的数据库驱动程序，对于 SQLite（默认驱动程序）这是一个文件名。支持变量替换（详见 `(1)`）。不得包含分号 `;`。默认值: `%Ggitcvs.%m.sqlite`

### `gitcvs.dbDriver`
使用的 Perl DBI 驱动程序。您可以在此指定任何可用驱动程序，但它可能无法工作。`git-cvsserver` 已使用 `DBD::SQLite` 进行测试，据报道与 `DBD::Pg` 兼容，

### `gitcvs.dbDriver`
并且报告与 `DBD::mysql` 不兼容。实验性功能。可能不包含双冒号 `:`。默认值：`SQLite`。参见 `(1)`。

### `gitcvs.dbUser`, `gitcvs.dbPass`
数据库用户名和密码。仅当设置了 `gitcvs.dbDriver` 时才有用，因为 `SQLite` 没有数据库用户和/或密码的概念。`gitcvs.dbUser` 支持变量替换（详情参见 `(1)`）。

### `gitcvs.dbTableNamePrefix`
数据库表名前缀。前置到任何使用的数据库表名称之前，允许单个数据库用于多个仓库。支持变量替换（详情参见 `(1)`）。任何非字母字符都将被替换为下划线。

除了 `gitcvs.usercrlfattr` 和 `gitcvs.allBinary` 之外，所有 `gitcvs` 变量也可以指定为 `gitcvs.<access_method>.<varname>`（其中 `access_method` 是 `ext` 和 `pserver` 之一），使其仅适用于给定的访问方式。

### `gitweb.category`, `gitweb.description`, `gitweb.owner`, `gitweb.url`
描述参见 `(1)`。

### `gitweb.avatar`, `gitweb.blame`, `gitweb.grep`, `gitweb.highlight`, `gitweb.\ patches`, `gitweb.pickaxe`, `gitweb.remote_heads`, `gitweb.showSizes`, `gitweb.snapshot`
描述参见 `(5)`。

### `grep.lineNumber`
如果设置为 `true`，则默认启用 `-n` 选项。

### `grep.patternType`
设置默认匹配行为。使用值 `basic`、`extended`、`fixed` 或 `perl` 将相应地启用 `--basic-regexp`、`--extended-regexp`、`--fixed-strings` 或 `--perl-regexp` 选项，而值 `default` 将恢复默认匹配行为。

### `grep.extendedRegexp`
如果设置为 `true`，则默认启用 `--extended-regexp` 选项。当 `grep.patternType` 选项设置为除 `default` 以外的值时，此选项将被忽略。

### `gpg.program`
在创建或验证 PGP 签名时，使用此自定义程序代替 `$PATH` 中找到的 `gpg`。该程序必须支持与 `GPG` 相同的命令行接口，即验证分离签名时运行 `"gpg --verify $file - <$signature"`，程序预期通过退出代码 `0` 来信号表示签名良好；生成 ASCII 护符式分离签名时，将待签名内容输入到 `"gpg -bsau $key"` 的标准输入，程序预期将结果发送到其标准输出。

### `gui.commitMsgWidth`
定义 `(1)` 中提交信息窗口的宽度，`75` 是默认值。

### `gui.diffContext`
指定由 `(1)` 执行的 diff 调用中应使用多少上下文行。默认值为 `5`。

### `gui.displayUntracked`
确定 `(1)` 是否在文件列表中显示未跟踪的文件。默认值为 `true`。

### `gui.encoding`
