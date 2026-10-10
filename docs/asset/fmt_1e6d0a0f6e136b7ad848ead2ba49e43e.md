
每次 superproject 更新移动已填充的子模块时（例如在移动前后的提交之间切换时），旧位置会保留一个过时的子模块检出，而新位置会出现一个空目录。要在新位置重新填充子模块，用户之后必须运行 `git submodule update`。仅当使用 gitfile 时，删除旧目录才是安全的，否则子模块的历史记录也会被删除。当递归子模块更新实现后，这两个步骤将变得过时。

# GIT-NAME-REV

## 名称

`git name-rev` - 为给定的修订版查找符号名称

## 用法

```
git name-rev [ --tags ] [ --refs=<pattern> ] ( --all | --stdin | <commit-ish>... )
```

## 描述

查找适合人类阅读的符号名称，用于以 `git rev-parse` 可解析的任何格式给出的修订版。

### 选项

- `--tags`

  不使用分支名称，而仅使用标签来命名提交

- `--refs=<pattern>`

  仅使用名称匹配给定 shell 模式的 refs。该模式可以是分支名、标签名或完全限定 ref 名称之一。

- `--all`

  列出所有 refs 可达的所有提交

- `--stdin`

  通过将所有 40 位字符的 SHA-1 十六进制数（例如 `$hex`）替换为 `"$hex ($rev_name)"` 来转换 stdin。当与 `--name-only` 一起使用时，替换为 `"$rev_name"`，完全省略 `$hex`。旨在供脚本使用者使用。

- `--name-only`

  不打印 SHA-1 和名称，仅打印名称。如果与 `--tags` 一起使用，名称中通常的 `tags/` 前缀也会被省略，更接近 `git-describe` 的输出。

- `--no-undefined`

  当引用未定义时，以非 0 错误码终止，而不是打印 undefined。

- `--always`

  作为回退，显示唯一缩写的提交对象。

### 示例

给定一个提交，找出它相对于本地 refs 的位置。假设有人给你写了一封关于那个精彩提交 `33db5f4d9027a10e477ccf054b2c1ab94f74c85a` 的信。当然，你会查看该提交，但这只告诉你发生了什么，而不告诉你上下文。

进入 `git name-rev`：

```
% git name-rev 33db5f4d9027a10e477ccf054b2c1ab94f74c85a
33db5f4d9027a10e477ccf054b2c1ab94f74c85a tags/v0.99~940
```

现在你更明智了，因为你知道它发生在 v0.99 之前的 940 个修订版之前。另一件你可以做的很棒的事是：

```
% git log | git name-rev --stdin
```

# GIT-NOTES

## 名称

`git-notes` - 添加或检查对象笔记

## 用法

```
git notes [list [<object>]]
git notes add [-f] [--allow-empty] [-F <file> | -m <msg> | (-c | -C) <object>] [<object>]
git notes copy [-f] ( --stdin | <from-object> <to-object> )
git notes append [--allow-empty] [-F <file> | -m <msg> | (-c | -C) <object>] [<object>]
git notes edit [--allow-empty] [<object>]
git notes show [<object>]
git notes merge [-v | -q] [-s <strategy> ] <notes-ref>
git notes merge --commit [-v | -q]
git notes merge --abort [-v | -q]
git notes remove [--ignore-missing] [--stdin] [<object>...]
git notes prune [-n | -v]
git notes get-ref
```

## 描述

添加、删除或读取附加到对象的笔记，而不触碰对象本身。

默认情况下，笔记保存在 `refs/notes/commits` 并从中读取，但此默认值可以被覆盖。参见下方的 OPTIONS、CONFIGURATION 和 ENVIRONMENT 部分。如果此 ref 不存在，当首次需要存储笔记时，它会静默创建。

笔记的一个典型用途是在不更改提交本身的情况下补充提交信息。笔记可以通过 `git log` 与原始提交信息一起显示。为了将这些笔记与存储在提交对象中的信息区分开来，笔记在一条未缩进的 `Notes (<refname>:);`（或针对 `refs/notes/commits` 的 `Notes:`）行之后像信息一样进行缩进。

通过使用 `--notes` 选项，还可以向使用 `git format-patch` 准备的补丁添加笔记。这样的笔记作为补丁注释添加在三破折号分隔线之后。

要更改 `git log` 显示的笔记，请参阅 `notes.displayRef` 配置。

请参阅 `notes.rewrite.<command>` 配置，了解一种在重写提交时携带笔记通过命令的方法。

## 子命令

- `list`

  列出给定对象的笔记对象。如果未给出对象，则显示所有笔记对象及其注释的对象列表（格式为 `"<note object> <annotated object>"`）。如果未给出子命令，这是默认子命令。

- `add`

  为给定对象添加笔记（默认为 HEAD）。如果对象已有笔记则中止（使用 `-f` 覆盖现有笔记）。但是，如果你交互使用 add（使用编辑器提供笔记内容），那么 - 而不是中止 - 现有笔记将在编辑器中打开（类似于 edit 子命令）。

- `copy`

  将第一个对象的笔记复制到第二个对象。如果第二个对象已有笔记，或第一个对象没有笔记，则中止（使用 `-f` 覆盖第二个对象的现有笔记）。此子命令等价于：`git notes add [-f] -C $(git notes list <from-object>) <to-object>`

  在 `--stdin` 模式下，从标准输入读取格式为 `<from-object> SP <to-object> [ SP <rest> ] LF` 的行，并将每个 `<from-object>` 的笔记复制到其对应的 `<to-object>`。（可选的 `<rest>` 被忽略，以便该命令可以读取提供给 post-rewrite 钩子的输入。）

- `append`

  追加到现有对象的笔记（默认为 HEAD）。如果需要，创建新的笔记对象。

- `edit`

  编辑给定对象的笔记（默认为 HEAD）。

- `show`

  显示给定对象的笔记（默认为 HEAD）。

- `merge`

  将给定的笔记 ref 合并到当前笔记 ref。这将尝试合并给定的笔记 ref（称为 "remote"）自 merge-base（如果有）以来所做的更改到当前笔记 ref（称为 "local"）。

  如果产生冲突且未给出自动解决冲突笔记的策略（参见 `-s`/`--strategy` 选项），则使用 "manual" 解决器。此解决器在一个特殊的工作树（`.git/NOTES_MERGE_WORKTREE`）中检出冲突的笔记，并指示用户在那里手动解决冲突。完成后，用户

## REMOVE

移除给定对象的注释（默认为 HEAD）。如果从命令行提供零个或一个对象，这等价于为 edit 子命令指定一个空的注释消息。

## PRUNE

移除所有不存在/不可达对象的注释。

## GET-REF

打印当前的注释引用（ref）。这提供了一种从脚本等环境中检索当前注释引用的便捷方式。

## OPTIONS

- `-f, --force`

  当为已有注释的对象添加注释时，覆盖现有注释（而不是中止）。

- `-m <msg>, --message=<msg>`

  使用给定的注释消息（而不是提示输入）。如果提供了多个 `-m` 选项，它们的值将作为单独的段落拼接在一起。以 `#` 开头的行以及段落间单行之外的空行将被剔除。

- `-F <file>, --file=<file>`

  从给定文件读取注释消息。使用 `-` 从标准输入读取注释消息。以 `#` 开头的行以及段落间单行之外的空行将被剔除。

- `-C <object>, --reuse-message=<object>`

  将给定的 blob 对象（例如，另一条注释）作为注释消息使用。（若要复制对象间的注释，请使用 `git notes copy <object>`。）

- `-c <object>, --reedit-message=<object>`

  与 `-C` 类似，但在使用 `-c` 时会调用编辑器，允许用户进一步编辑注释消息。
