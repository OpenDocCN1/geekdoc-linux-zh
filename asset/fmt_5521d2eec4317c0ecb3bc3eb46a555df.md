
或像这样（当使用 `--cc` 选项时）：

```
diff --cc file
```

2. 它后面跟有一行或多行扩展头部行（此示例显示具有两个父级的合并）：

```
index <hash>,<hash>..<hash> mode <mode>,<mode>..<mode> new file mode <mode> deleted file mode <mode>,<mode>
```

`mode <mode>,<mode>..<mode>` 行仅当至少一个 `<mode>` 与其他不同时才出现。带有检测内容移动信息（重命名和复制检测）的扩展头部被设计为用于两个 `<tree-ish>` 之间的 diff，并不由组合 diff 格式使用。

3. 它后面跟有两行 from-file/to-file 头部

```
--- a/file +++ b/file
```

类似于传统统一 diff 格式的两行头部，使用 `/dev/null` 来指示创建或删除的文件。

4. 块头部格式经过修改，以防止人们将其错误地提供给 `patch -p1`。组合 diff 格式是为审查合并提交更改而创建的，并非旨在用于应用。更改类似于扩展 index 头部的更改：

```
@@@ <from-file-range> <from-file-range> <to-file-range> @@
```

在组合 diff 格式的块头部中，有（父级数量 + 1）个 `@` 字符。

与传统的 *unified* diff 格式不同，该格式显示文件 A 和 B，使用一列具有 -（减号 – 出现在 A 但在 B 中移除）、+（加号 – 在 A 中缺失但添加到 B）或 ” ”（空格 – 未更改）前缀，此格式比较两个或多个文件 `file1`、`file2`,... 与一个文件 `X`，并显示 `X` 如何不同于每个 `fileN`。在输出行前为每个 `fileN` 添加一列，以记录 `X` 的行如何与其不同。第 N 列中的 `-` 字符表示该行出现在 `fileN` 中，但未出现在结果中。第 N 列中的 `+` 字符表示该行出现在结果中，而 `fileN` 没有该行（换句话说，从该父级的角度来看，该行是被添加的）。

在上述示例输出中，函数签名从两个文件都发生了变化（因此从 `file1` 和 `file2` 中都有两个 `-` 删除，加上 `++` 表示添加的一行既不出现在 `file1` 也不出现在 `file2` 中）。另外八行在 `file1` 中相同，但不出现在 `file2` 中（因此以 `+` 为前缀）。

当通过 `git diff-tree -c` 显示时，它比较合并提交的父级与合并结果（即 `file1..fileN` 是父级）。当通过 `git diff-files -c` 显示时，它比较两个未解决的合并父级与工作树文件（即 `file1` 是阶段 2 即 “我们的版本”，`file2` 是阶段 3 即 “他们的版本”）。

### 示例

```
git log --no-merges
```

显示完整的提交历史，但跳过任何合并

```
git log v2.6.12.. include/scsi drivers/scsi
```

显示自版本 `v2.6.12` 以来更改 `include/scsi` 或 `drivers/scsi` 子目录中任何文件的所有提交

```
git log --since="2 weeks ago" -- gitk
```

显示过去两周对文件 `gitk` 的更改。"--" 是必需的，以避免与名为 *gitk* 的 **branch** 混淆

```
git log --name-status release..test
```

显示 "test" 分支中尚未包含在 "release" 分支中的提交，以及每个提交修改的路径列表。

```
git log --follow builtin/rev-list.c
```

显示更改 `builtin/rev-list.c` 的提交，包括在文件获得当前名称之前发生的提交。

```
git log --branches --not --remotes=origin
```

显示在任何本地分支中但不在任何 *origin* 远程跟踪分支中的所有提交（你拥有的但 origin 没有的）。

```
git log master --not --remotes=*/master
```

显示在本地 `master` 中但不在任何远程存储库 `master` 分支中的所有提交。

```
git log -p -m --first-parent
```

显示包含更改 diff 的历史记录，但仅从 "主分支" 的角度出发，跳过来自合并分支的提交，并显示合并引入的更改的完整 diff。只有在遵循将所有主题分支合并到单个集成分支的严格策略时，这才有意义。

```
git log -L '/int main/,/^}/:main.c'
```

显示文件 `main.c` 中的函数 `main()` 如何随时间演变。

```
git log -3
```

限制显示的提交数量为 3。

### 讨论

在核心层面，Git 对字符编码没有特定要求。

记录在索引和树对象中的路径名被视为未解释的非 NUL 字节序列。`name` 返回的是记录下来的内容，并与 Git 跟踪的数据进行比较，而后者预期是 `name` 和 `name` 接受的内容。不存在路径名编码转换这回事。

Blob 对象的内容是未解释的字节序列。在核心层面没有编码转换。

提交日志消息是未解释的非 NUL 字节序列。

虽然我们鼓励提交日志消息使用 UTF-8 编码，但 Git 核心和 Git 外观（Porcelain）在设计上都不强制项目使用 UTF-8。如果某个特定项目的所有参与者发现使用传统编码更方便，Git 并不禁止这样做。不过，有几件事需要注意。

1. 如果提供给 `git commit` 和 `git commit-tree` 的提交日志消息看起来不像有效的 UTF-8 字符串，除非你明确说明你的项目使用的是传统编码，否则这两个命令会发出警告。说明这一点的方法是在 `.git/config` 文件中包含 `i18n.commitencoding`，如下所示：

```ini
[i18n]  commitencoding = ISO-8859-1
```

使用上述设置创建的提交对象会在其编码头中记录 `i18n.commitencoding` 的值。这是为了帮助后来查看这些对象的人。缺少此头意味着提交日志消息是用 UTF-8 编码的。

2. `git log`、`git show`、`git blame` 及其相关命令会查看提交对象的编码头，并尝试将日志消息重新编码为 UTF-8，除非另有指定。你可以在 `.git/config` 文件中通过 `i18n.logoutputencoding` 指定所需的输出编码，如下所示：

```ini
[i18n]  logoutputencoding = ISO-8859-1
```

如果你没有配置此变量，则使用 `i18n.commitencoding` 的值作为替代。

请注意，我们故意选择在提交时不重新编码提交日志消息，以在提交对象层面强制使用 UTF-8，因为重新编码为 UTF-8 并不一定是一个可逆操作。

### 配置

核心变量请参阅 (1)，与差异生成相关的设置请参阅 (1)。

#### format, pretty

`--format` 选项的默认值。（参见上文“Pretty Formats”。）默认为 `medium`（中等）。

#### i18n.logOutputEncoding

显示日志时使用的编码。（参见上文“讨论”。）如果已设置，则默认为 `i18n.commitEncoding` 的值，否则默认为 UTF-8。

#### log.date

人类可读日期的默认格式。（对比 `--date` 选项。）默认为 "default"，这意味着日期将写成类似 `Sat May 8 19:35:34 2010 -0500` 的形式。

#### log.showRoot

如果为 `false`，`git log` 和相关命令将不会将初始提交视为一次大规模的创建事件。`git log -p` 输出中的任何根提交将不附带差异显示。默认为 `true`。

#### mailmap.*

请参阅 (1)。

#### notes.displayRef

除了由 `core.notesRef` 或 `GIT_NOTES_REF` 设置的默认引用外，在使用日志系列命令显示提交消息时，还要从哪些引用读取笔记。请参阅 (1)。

可以是未缩写的引用名称或 glob（通配符），并且可以指定多次。对于不存在的引用会发出警告，但不匹配任何引用的 glob 会被静默忽略。

此设置可以通过 `--no-notes` 选项禁用，被 `GIT_NOTES_DISPLAY_REF` 环境变量覆盖，并被 `--notes=<ref>` 选项覆盖。

## GIT-LS-FILES

### 名称

`git-ls-files` - 显示索引和工作树中文件的信息

#### 语法
