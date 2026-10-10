
```sh
git ls-files [-z] [-t] [-v] (-- [cached|deleted|others|ignored|stage|unmerged|killed|modified])*
            ([c|d|o|i|s|u|k|m])*
            [-x <pattern>|--exclude=<pattern>]
            [-X <file>|--exclude-from=<file>]
            [--exclude-per-directory=<file>]
            [--exclude-standard]
            [--error-unmatch]
            [--with-tree=<tree-ish>]
            [--full-name]
            [--abbrev]
            [--]
            [<file>...]
```

### 描述

此命令将目录缓存索引中的文件列表与实际工作目录列表合并，并显示两者的不同组合。

可以使用以下选项之一来确定显示的文件：

### 选项

- `-c, --cached`

  在输出中显示缓存文件（默认）

- `-d, --deleted`

  在输出中显示已删除的文件

- `-m, --modified`

  在输出中显示已修改的文件

- `-o, --others`

  在输出中显示其他（即未跟踪）文件

- `-i, --ignored`

  在输出中仅显示被忽略的文件。当显示索引中的文件时，仅打印由排除模式匹配的文件。当显示“其他”文件时，仅显示由排除模式匹配的文件。

- `-s, --stage`

  在输出中显示暂存内容的对象名称、模式位和阶段号。

- `--directory`

  如果整个目录被归类为“其他”，则只显示其名称（带尾随斜杠）而不显示其完整内容。

- `--no-empty-directory`

  不列出空目录。如果没有 `--directory`，则无效果。

- `-u, --unmerged`

  在输出中显示未合并的文件（强制使用 `--stage`）

- `-k, --killed`

  显示因文件/目录冲突而出现在文件系统中需要删除的文件，以便 `checkout-index` 成功。

- `-z`

  输出使用 `\0` 作为行终止符。

- `-x <pattern>, --exclude=<pattern>`

  跳过匹配该模式的未跟踪文件。注意模式是 shell 通配符模式。更多信息请参阅下文“排除模式”。

- `-X <file>, --exclude-from=<file>`

  从 `<file>` 读取排除模式；每行一个。

- `--exclude-per-directory=<file>`

  从 `<file>` 读取仅适用于该目录及其子目录的额外排除模式。

- `--exclude-standard`

  添加标准的 Git 排除项：`.git/info/exclude`、每个目录中的 `.gitignore` 以及用户的全局排除文件。

- `--error-unmatch`

  如果任何 `<file>` 未出现在索引中，则将其视为错误（返回 1）。

- `--with-tree=<tree-ish>`

  在使用 `--error-unmatch` 将用户提供的 `<file>`（即路径模式）参数扩展为路径时，假设自命名的 `<tree-ish>` 以来在索引中移除的路径仍然存在。此选项与 `-s` 或 `-u` 选项一起使用没有意义。

- `-t`

  此功能已半弃用。为了脚本目的，`--porcelain` 和 `--name-status` 几乎总是更优越的替代方案，用户应查看 `--short` 或 `--name-status` 以获取更多用户友好的替代方案。

  此选项在每行开头使用以下标签（后跟一个空格）来标识文件状态：

    - H: 缓存中

    - S: skip-worktree

    - M: 未合并

    - R: 已移除/已删除

    - C: 已修改/已更改

    - K: 待删除

    - ?: 其他

- `-v`

  类似于 `-t`，但对于标记为 *assume unchanged* 的文件使用小写字母（请参阅 `git-config`）。

- `--full-name`

  当从子目录运行时，命令通常输出相对于当前目录的路径。此选项强制输出相对于项目顶级目录的路径。

- `--abbrev[=<n>]`

  不显示完整的 40 字节十六进制对象行，而只显示部分前缀。可以使用 `--abbrev=<n>` 指定非默认的位数。

- `--debug`

  在描述文件的每一行之后，添加有关其缓存条目的更多数据。这是为了尽可能多地显示信息供人工检查；确切的格式可能会随时改变。

- `--`

  不再将任何后续参数解释为选项。

- `<file>`

  要显示的文件。如果没有提供文件，则显示符合其他指定标准的所有文件。

### 输出

`git ls-files` 仅输出文件名，除非指定了 `--stage`，在这种情况下它输出：

```
[<tag>  ]<mode> <object> <stage> <file>
```

`git ls-files --unmerged` 和 `git ls-files --stage` 可用于检查未合并路径的详细信息。

对于未合并的路径，索引不会记录单个模式/SHA-1 对，而是记录最多三对；分别来自阶段 1 中的树 O，阶段 2 中的 A，以及阶段 3 中的 B。用户可以（或外观层可以）使用此信息来查看最终应记录在该路径处的内容。（请参阅 `git-status` 获取更多关于状态的信息）

当未使用 `-z` 选项时，路径名中的 TAB、LF 和反斜杠字符分别表示为 `\t`、`\n` 和 `\\`。

## 排除模式

`git ls-files` 在遍历目录树并查找要显示的文件时，如果指定了 `--others` 或 `--ignored` 标志，可以使用一组“排除模式”。指定了排除模式的格式。

这些排除模式按以下顺序来源于：

- 命令行标志 `--exclude=<pattern>` 指定单个模式。模式按照它们在命令行中出现的顺序排列。

- 命令行标志 `--exclude-from=<file>` 指定一个包含模式列表的文件。模式按照它们在文件中出现的顺序排列。

- 命令行标志 `--exclude-per-directory=<name>` 指定 *git ls-files* 检查的每个目录中的文件名，通常是 `.gitignore`。较深层级目录中的文件优先级更高。模式按照它们在文件中出现的顺序排列。

通过 `--exclude` 在命令行上指定或从通过 `--exclude-from` 指定的文件中读取的模式，相对于目录树的根部。通过 `--exclude-per-directory` 指定的文件读取的模式，相对于该模式文件所在的目录。

### 另请参阅

`git-ls-files`, `gitignore`

# GIT-LS-REMOTE

### 名称

`git-ls-remote` - 列出远程仓库中的引用

### 概要

```
git ls-remote [--heads] [--tags] [-u <exec> | --upload-pack <exec>] [--exit-code] <repository> [<refs>...]
```

### 描述

显示远程仓库中可用的引用及其相关的提交 ID。

### 选项

- `-h, --heads`, `-t, --tags`

  分别限制仅显示 `refs/heads` 和 `refs/tags`。这些选项并非互斥；如果同时给出，将显示存储在 `refs/heads` 和 `refs/tags` 中的引用。

- `-u <exec>, --upload-pack=<exec>`

  指定远程主机上 `git-upload-pack` 的完整路径。这使得能够列出通过 SSH 访问且 SSH 守护进程未使用用户配置的 PATH 的仓库中的引用。

- `--exit-code`

  如果在远程仓库中未找到匹配的引用，则以状态“2”退出。通常，无论是否找到匹配的引用，只要成功与远程仓库通信，该命令就会以状态“0”退出。

- `--get-url`

  考虑任何 `url.<base>.insteadOf` 配置设置（参见 `git-config`），展开给定远程仓库的 URL，并在不与远程通信的情况下退出。

- `<repository>`

  要查询的“远程”仓库。此参数可以是 URL 或远程名称（参见 `git-clone` 中的 GIT URLS 和 REMOTES 章节）。

- `<refs>...`

  如果未指定，则显示在通过 `--heads` 和 `--tags` 过滤后的所有引用。如果指定了 `<refs>...`，则仅显示与给定模式匹配的引用。

### 示例
