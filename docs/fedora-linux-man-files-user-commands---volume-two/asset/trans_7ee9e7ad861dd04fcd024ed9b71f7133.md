

## 配置

可选配置变量 `gc.reflogExpire` 可以设置为指示每个分支的 reflog 中的历史条目在此仓库中应保持可用多长时间。该设置表示为一段时间长度，例如 *90 天* 或 *3 个月*。默认为 *90 天*。

可选配置变量 `gc.reflogExpireUnreachable` 可以设置为指示不属于当前分支的历史 reflog 条目在此仓库中应保持可用多长时间。这些类型的条目通常是由于使用 `git commit --amend` 或 `git rebase` 而创建的，并且是发生在修订或变基之前的提交。由于这些更改不属于当前项目，大多数用户希望它们更早过期。此选项默认为 *30 天*。

上述两个配置变量可以应用于某种模式。例如，这仅为远程跟踪分支设置非默认过期值：

```
[gc "refs/remotes/*"] reflogExpire = never reflogExpireUnreachable = 3 days
```

可选配置变量 `gc.rerereResolved` 指示之前解决冲突合并的记录保留多长时间。默认为 *60 天*。

可选配置变量 `gc.rerereUnresolved` 指示未解决的冲突合并记录保留多长时间。默认为 *15 天*。

可选配置变量 `gc.packRefs` 决定 `git gc` 是否运行 `git pack-refs`。可以将其设置为“notbare”以在所有非裸仓库中启用它，也可以将其设置为布尔值。默认为 true。

可选配置变量 `gc.aggressiveWindow` 控制当指定 `--aggressive` 选项时，用于优化仓库中对象的 delta 压缩花费的时间。值越大，花费在优化 delta 压缩上的时间越多。有关更多详细信息，请参阅 (1) 中 `--window` 选项的文档。默认为 *250*。

类似地，可选配置变量 `gc.aggressiveDepth` 控制 (1) 中的 `--depth` 选项。默认为 *250*。

可选配置变量 `gc.pruneExpire` 控制在修剪之前，未引用的松散对象必须存在多久。默认为“*2 周前*”。

## 备注

*git gc* 非常努力地确保其收集垃圾的安全性。特别是，它不仅保留由当前分支和标签集合引用的对象，还保留由索引、远程跟踪分支、由 *git filter-branch* 在 refs/original/ 中保存的引用或 reflog（可能引用后来经过修订或回滚的分支中的提交）引用的对象。

如果你期望某些对象被收集但未被收集，请检查所有这些位置，并决定在你的情况下移除这些引用是否有意义。

# 钩子

`git gc --auto` 命令将运行 `pre-auto-gc` 钩子。有关更多信息，请参阅 (5)。

► 参见

(1) (1) (1) (1)

# Git-get-tar-commit-id

## 名称

git-get-tar-commit-id - 从使用 git-archive 创建的存档中提取提交 ID

## 概要

```
git get-tar-commit-id < <tarfile>
```

## 描述

作为一个过滤器，提取存储在由 *git archive* 创建的存档中的提交 ID。它只读取输入的前 1024 个字节，因此其运行时间不受 `<tarfile>` 大小的太大影响。

如果未找到提交 ID，*git get-tar-commit-id* 会安静地退出，返回代码为 1。这可能会发生，如果 `<tarfile>` 没有使用 *git archive* 创建，或者如果 *git archive* 的第一个参数是树 ID 而不是提交 ID 或标签。

# GIT-GREP

## 名称

git-grep - 打印匹配模式的行

## 概要

```
git grep [-a | --text] [-I] [--textconv] [-i | --ignore-case] [-w | --word-regexp] [-v | --invert-match] [-h|-H] [--full-name] [-E | --extended-regexp] [-G | --basic-regexp] [-P | --perl-regexp] [-F | --fixed-strings] [-n | --line-number] [-l | --files-with-matches] [-L | --files-without-match] [(-O | --open-files-in-pager) [<pager>]] [-z | --null] [-c | --count] [--all-match] [-q | --quiet] [--max-depth <depth>] [--color[=<when>] | --no-color] [--break] [--heading] [-p | --show-function] [-A <post-context>] [-B <pre-context>] [-C <context>] [-W | -function-context] [-f <file>] [-e] <pattern> [--and|--or|--not|(())|-e <pattern>…] [ [--[no-]exclude-standard] [-cached | --no-index | --untracked] | <tree>…] [--] [<pathspec>…]
```

## 描述

在工作树中的跟踪文件中查找指定模式，在索引文件中注册的 blob，或在给定的树对象中的 blob。模式是由换行字符分隔的一个或多个搜索表达式的列表。作为搜索表达式的空字符串匹配所有行。

## 配置

### grep.lineNumber
如果设置为 true，则默认启用 -n 选项。

### grep.patternType
设置默认匹配行为。使用值 *basic*、*extended*、*fixed* 或 *perl* 将分别启用 -basic-regexp、-extended-regexp、-fixed-strings 或 -perl-regexp 选项，而值 *default* 将返回默认匹配行为。

### grep.extendedRegExp
如果设置为 true，则默认启用 -extended-regexp 选项。当 grep.patternType 选项设置为 *default* 以外的值时，此选项被忽略。

### grep.fullName
如果设置为 true，则默认启用 -full-name 选项。

## 选项

- **-cached**
  不在工作树中搜索跟踪文件，而是搜索索引文件中注册的 blob。
- **—no-index**
  搜索当前目录中未被 Git 管理的文件。
- **—untracked**
  除了在工作树中的跟踪文件中搜索外，还在未跟踪文件中搜索。
- **—no-exclude-standard**
  通过不遵守 .gitignore 机制，也在被忽略的文件中搜索。仅与 —untracked 一起使用时有用。
- **—exclude-standard**
  不关注通过 .gitignore 机制指定的被忽略文件。仅在使用 —no-index 搜索当前目录中的文件时有用。
- **-a, —text**
  像处理文本一样处理二进制文件。
- **—textconv**
  遵守 textconv 过滤器设置。
- **—no-textconv**
  不遵守 textconv 过滤器设置。这是默认设置。
- **-i, —ignore-case**
  忽略模式和文件之间的大小写差异。
- **-I**
  不在二进制文件中匹配模式。
- **—max-depth <depth>**
  对于命令行上给出的每个 <pathspec>，最多下降 <depth> 层目录。负值表示无限制。如果 <pathspec> 包含活动通配符，则此选项被忽略。换句话说，如果 “a*” 匹配名为 “a*” 的目录，“*” 将被字面匹配，因此 —max-depth 仍然有效。
- **-w, —word-regexp**
  仅在单词边界处匹配模式（要么位于行首，要么由非单词字符跟随；要么位于行尾，要么由非单词字符跟随）。
- **-v, —invert-match**
  选择非匹配行。
- **-h, -H**
  默认情况下，该命令显示每个匹配的文件的文件名。-h 选项用于抑制此输出。-H 的存在是为了完整性，除了覆盖命令行上较早给出的 -h 外，它不执行任何操作。
- **—full-name**
  从子目录运行时，该命令通常输出相对于当前目录的路径。此选项强制输出相对于项目顶层目录的路径。
- **-E, —extended-regexp, -G, —basic-regexp**
  用于模式的 POSIX 扩展/基本正则表达式。默认使用基本正则表达式。
- **-P, —perl-regexp**
  用于模式的 Perl 兼容正则表达式。需要编译 libpcre。
- **-F, —fixed-strings**
  用于模式的固定字符串（不将模式解释为正则表达式）。
- **-n, —line-number**
  在匹配行前添加行号前缀。
- **-l, —files-with-matches, —name-only, -L, —files-without-match**
  不显示每个匹配行，只显示包含（或不包含）匹配项的文件名。为了与 *git diff* 更好的兼容性，—name-only 是 —files-with-matches 的同义词。
- **-O [<pager>], —open-files-in-pager [<pager>]**
  在分页器中打开匹配的文件（不是 *grep* 的输出）。如果分页器恰好是 "less" 或 "vi"，并且用户只指定了一个模式，则第一个文件会自动定位到第一个匹配项。
- **-z, —null**
  输出 \0 而不是通常跟随文件名的字符。
- **-c, —count**
  不显示每个匹配行，而是显示匹配的行数。
- **—color[=<when>]**
  显示彩色匹配。值必须是 always（默认）、never 或 auto。
- **—no-color**

