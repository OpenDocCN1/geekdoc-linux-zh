
指定 `--no-symlinks` 指示 `git difftool` 创建副本而不是符号链接。`--no-symlinks` 是 Windows 上的默认值。

### `-x <command>, --extcmd=<command>`

指定用于查看 diff 的自定义命令。当指定此选项时，`git-difftool` 忽略配置的默认值，并运行 `$command $LOCAL $REMOTE`。此外，`$BASE` 会在环境变量中设置。

### `-g, --gui`

当使用 `-g` 或 `--gui` 选项调用 `git-difftool` 时，默认的 diff 工具将从配置的 `diff.guitool` 变量读取，而不是从 `diff.tool` 读取。

### `--[no-]trust-exit-code`

`git-difftool` 对每个文件单独调用 diff 工具。默认情况下，diff 工具报告的错误会被忽略。使用 `--trust-exit-code` 可使 `git-difftool` 在调用的 diff 工具返回非零退出代码时退出。

当使用 `--trust-exit-code` 时，`git-difftool` 将转发被调用工具的退出代码。

完整的支持选项列表参见 (1)。

## 配置变量

当未定义 difftool 等效配置时，`git difftool` 将回退到 `git mergetool` 配置变量。

**`diff.tool`**

要使用的默认 diff 工具。

**`diff.guitool`**

指定 `--gui` 时要使用的默认 diff 工具。

**`difftool.<tool>.path`**

覆盖给定工具的路径。这在你的工具不在 `PATH` 中时有用。

**`difftool.<tool>.cmd`**

指定调用指定 diff 工具的命令。有关更多详细信息，参见上述 `--tool=<tool>` 选项。

**`difftool.prompt`**

在每次调用 diff 工具前提示。

**`difftool.trustExitCode`**

如果调用的 diff 工具返回非零退出状态，则退出 difftool。有关更多详细信息，参见上述 `--trust-exit-code` 选项。

### 另请参阅

(1)

显示提交之间、提交与工作树之间的更改等

(1)

运行合并冲突解决工具以解决合并冲突

(1)

获取和设置仓库或全局选项

## GIT-FAST-EXPORT

### 名称

`git-fast-export` - Git 数据导出器

### 概要

```
git fast-export [options] | git fast-import
```

### 描述

此程序将以适合通过管道输入 `git fast-import` 的形式转储给定的修订版本。

你可以将其用作人类可读的 bundle 替代方案（参见 (1)），或作为一种交互式的 `git filter-branch`。

#### 选项

**`--progress=<n>`**

每 `<n>` 个对象插入一次进度语句，以便在导入期间由 `git fast-import` 显示。

**`--signed-tags=(verbatim|warn|warn-strip|strip|abort)`**

指定如何处理签名的标签。由于导出后的任何转换都可能改变标签名称（在排除修订时也可能发生），签名将不再匹配。

当请求中止时（这是默认行为），遇到签名标签时此程序将终止。使用 `strip` 时，标签将静默地变为未签名；使用 `warn-strip` 时，标签将变为未签名，但会显示警告；使用 `verbatim` 时，标签将被静默导出；使用 `warn` 时，标签将被导出，但你会看到警告。

**`--tag-of-filtered-object=(abort|drop|rewrite)`**

指定如何处理其指向的对象被过滤掉的标签。由于要导出的修订和文件可以按路径限制，指向的对象可能被完全过滤掉。

当请求中止时（这是默认行为），遇到这样的标签时此程序将终止。使用 `drop` 时，将从输出中省略这些标签。使用 `rewrite` 时，如果指向的对象是一个提交，它将通过重写该标签以指向祖先提交（通过父提交重写；参见 (1)）来重写该标签。

**`-M`, `-C`**

执行移动和/或复制检测，如 (1) 手册页中所述，并在输出转储中使用它生成重命名和复制命令。

注意此命令的早期版本不会抱怨并产生错误结果如果你给了这些选项。

**`--export-marks=<file>`**

完成时将内部标记表转储到 `<file>`。标记每行写一个，格式为 `:markid SHA-1`。仅转储修订的标记；blob 的标记会被忽略。后端可以使用此文件在完成导入后验证导入，或跨增量运行保存标记表。由于 `<file>` 仅在完成时打开并截断，因此相同的路径也可以安全地用于 `--import-marks`。如果没有新对象被标记/导出，则不会写入文件。

**`--import-marks=<file>`**

在处理任何输入之前，加载 `<file>` 中指定的标记。输入文件必须存在，必须可读，并且必须使用与 `--export-marks` 产生的相同格式。

已经标记过的任何提交都不会再次导出。如果后端使用类似的 `--import-marks` 文件，通过在多次运行中保持一致的标记，可以实现仓库的增量双向导出。

- `--fake-missing-tagger`

  一些旧仓库具有没有标签创建者（tagger）的标签。`fast-import` 协议对此相当严格，不允许这种情况。因此，伪造一个标签创建者以便能够 `fast-import` 输出。

- `--use-done-feature`

  使用 *feature done* 片段启动流，并使用 `done` 命令终止它。

- `--no-data`

  跳过 blob 对象的输出，而是通过其原始 SHA-1 哈希值来引用 blob。这在重写仓库的目录结构或历史而不触及单个文件内容时很有用。请注意，生成的流只能用于已经包含必要对象的仓库。

- `--full-tree`

  此选项将导致 `fast-export` 对每个提交发出一个“deleteall”指令，随后是该提交中所有文件的完整列表（与仅列出与提交的第一个父提交不同的文件相反）。

- `--anonymize`

  在保留历史和存储树形状的同时，对仓库内容进行匿名化。请参阅下方的 ANONYMIZING 部分。

- `--refspec`

  对每个导出的 ref 应用指定的 refspec。可以指定多个。

- `[<git-rev-list-args>...]`

  一系列参数，可被 `git rev-parse` 和 `git rev-list` 接受，用于指定要导出的特定对象和引用。例如，`*master~10..master*` 会导致导出当前的 `master` 引用，以及自其第 10 个祖先提交以来添加的所有对象。

#### 示例

```
$ git fast-export --all | (cd /empty/repository && git fast-import)`
```

这将导出整个仓库并将其导入到现有的空仓库中。除了重新编码非 UTF-8 的提交外，它将是镜像的一比一副本。

```
$ git fast-export master~5..master | sed "s|refs/heads/master|refs/heads/other|" | git fast-import
```

这从 `*master*~5..*master*`（即，如果 `*master*` 具有线性历史，它将获取最后 5 个提交）创建了一个名为 `*other*` 的新分支。

请注意，这假设该修订范围引用的任何 blob 和提交消息都不包含字符串 `*refs/heads/master*`。

# 匿名化

如果提供 `--anonymize` 选项，`git` 将试图从仓库中移除所有识别信息，同时保留足够的原始树和历史模式以复现某些 bug。目标是，如果在私有仓库中发现的 git bug 在匿名化后的仓库中持续存在，并且后者可以与 git 开发者分享以帮助解决 bug。

使用此选项，`git` 将用匿名化数据替换输出中的所有 ref 名称、路径、blob 内容、提交和标签消息、姓名以及电子邮件地址。相同字符串的两个实例将被等效替换（例如，具有相同作者的两次提交在输出中将有相同的匿名作者，但与原始作者字符串没有相似之处）。提交、分支和标签之间的关系得以保留，同样保留的还有提交时间戳（但提交消息和 ref 名称与原始内容没有相似之处）。树的相对结构得以保留（例如，如果你有一个根树，包含 10 个文件和 3 个子树，输出也将如此），但它们的名字和文件内容将被替换。

如果你认为发现了 git bug，可以开始导出整个仓库的匿名化流：

```
$ git fast-export --anonymize --all >anon-stream
```

然后确认该 bug 在由该流创建的仓库中持续存在（许多 bug 不会持续存在，因为它们确实依赖于确切的仓库内容）：
