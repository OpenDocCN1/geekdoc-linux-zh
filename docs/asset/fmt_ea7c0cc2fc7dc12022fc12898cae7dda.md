
使用上述设置创建的提交对象会在其编码头中记录 `i18n.commitencoding` 的值。这是为了帮助后来查看这些对象的人。缺少该头意味着提交日志消息是以 UTF-8 编码的。

- 2. `git log`、`git show`、`git blame` 及其相关命令会查看提交对象的编码头，并尝试将日志消息重新编码为 UTF-8，除非另有指定。你可以在 `.git/config` 文件中通过 `i18n.logoutputencoding` 指定所需的输出编码，如下所示：

```
[i18n] logoutputencoding = ISO-8859-1
```

如果你没有设置此配置变量，则会使用 `i18n.commitencoding` 的值作为替代。

请注意，我们在提交时故意选择不重新编码提交日志消息，以强制在提交对象层面使用 UTF-8，因为重新编码为 UTF-8 并不一定是可逆操作。

### 环境和配置变量

用于编辑提交日志消息的编辑器将从 `GIT_EDITOR` 环境变量、`core.editor` 配置变量、`VISUAL` 环境变量或 `EDITOR` 环境变量（按此顺序）中选择。详情请参见 (1)。

### 钩子

此命令可以运行 `commit-msg`、`prepare-commit-msg`、`pre-commit` 和 `post-commit` 钩子。更多信息请参见 (5)。

### 文件

```
$GIT_DIR/COMMIT_EDITMSG
```

此文件包含正在进行中的提交的提交信息。如果 `git commit` 在创建提交之前因错误而退出，用户提供的任何提交信息（例如在编辑器会话中）都将保存在此文件中，但会被下一次调用 `git commit` 时覆盖。

### 另见

`git-config(1)`, `gitweb(1)`, `git(1)`, `githowto(1)`, `gittutorial(1)`

## GIT-CONFIG

> 名称

`git-config` - 获取和设置仓库或全局选项

### 概要

```
git config [<file-option>] [type] [-z|--null] name [value [value_regex]]
git config [<file-option>] [type] --add name value
git config [<file-option>] [type] --replace-all name value [value_regex]
git config [<file-option>] [type] [-z|--null] --get name [value_regex]
git config [<file-option>] [type] [-z|--null] --get-all name [value_regex]
git config [<file-option>] [type] [-z|--null] --get-regexp name_regex [value_regex]
git config [<file-option>] [type] [-z|--null] --get-urlmatch name URL
git config [<file-option>] --unset name [value_regex]
git config [<file-option>] --unset-all name [value_regex]
git config [<file-option>] --rename-section old_name new_name
git config [<file-option>] --remove-section name
git config [<file-option>] [-z|--null] -l | --list
git config [<file-option>] --get-color name [default]
git config [<file-option>] --get-colorbool name [stdout-is-tty]
git config [<file-option>] -e | --edit
```

### 描述

你可以使用此命令查询/设置/替换/取消设置选项。名称实际上是由点分隔的章节和键，值将被转义。

可以使用 `--add` 选项向选项添加多行。如果你想更新或取消设置可能出现在多行上的选项，则需要提供一个 POSIX 正则表达式 `value_regexp`。只有与正则表达式匹配的那些现有值会被更新或取消设置。如果你想要处理那些**不**匹配正则表达式的行，只需在前面添加一个感叹号（参见“示例”章节）。

类型说明符可以是 `--int` 或 `--bool`，以确保 `git config` 保证变量为给定类型，并将值转换为规范形式（对于 int 为简单十进制数，对于 bool 为“true”或“false”字符串），或者 `--path`，它会进行一些路径扩展（参见下面的 `--path`）。如果未传递类型说明符，则不会对值进行任何检查或转换。

读取时，默认从系统、全局和仓库本地配置文件中读取值，并且可以使用选项 `--system`、`--global`、`--local` 和 `--file <filename>` 来告诉命令只从该位置读取（参见“文件”章节）。

写入时，默认将新值写入仓库本地配置文件，并且可以使用选项 `--system`、`--global`、`--file <filename>` 来告诉命令写入该位置（你可以说 `--local`，但那是默认的）。

发生错误时，此命令将以非零状态码失败。一些退出代码如下：

- 1. 配置文件无效 (ret=3)，
- 2. 无法写入配置文件 (ret=4)，
- 3. 未提供章节或名称 (ret=2)，
- 4. 章节或键无效 (ret=1)，
- 5. 你尝试取消设置一个不存在的选项 (ret=5)，
- 6. 你尝试取消设置/设置一个有多行匹配的选项 (ret=5)，或者
- 7. 你尝试使用无效的正则表达式 (ret=6)。

成功时，命令返回退出码 0。

### 选项

- **--replace-all**

  默认行为是替换最多一行。这会替换所有匹配键的行（以及可选的 value_regex）。

- **--add**

  向选项添加新行，而不改变任何现有值。这与在 --replace-all 中提供 ^$ 作为 value_regex 相同。

- **--get**

  获取给定键的值（可选地通过匹配值的正则表达式进行过滤）。如果未找到键则返回错误码 1，如果找到多个键值则返回最后一个值。

- **--get-all**

  类似于 get，但即使键的值数量不正好为一个也不会失败。

- **--get-regexp**

  类似于 --get-all，但将名称解释为正则表达式并写出键名。正则表达式匹配目前区分大小写，并且针对键的规范化版本进行匹配，其中章节和变量名被小写化，但子章节名称不被小写化。

- **--get-urlmatch name URL**

  当给定由两部分组成的名称 section.key 时，返回 section.<url>.key 的值，其中 <url> 部分与给定的 URL 最佳匹配（如果不存在这样的键，则使用 section.key 的值作为回退）。当仅给定章节作为名称时，对该章节中的所有键执行此操作并列出它们。

- **--global**

  对于写入选项：写入全局 ~/.gitconfig 文件，而不是仓库 .git/config；如果该文件存在且 ~/.gitconfig 文件不存在，则写入 $XDG_CONFIG_HOME/git/config 文件。

  对于读取选项：仅从全局 ~/.gitconfig 和 $XDG_CONFIG_HOME/git/config 读取，而不是从所有可用文件读取。

  另见“文件”章节。

- **--system**

  对于写入选项：写入系统范围的 $(prefix)/etc/gitconfig，而不是仓库 .git/config。

  对于读取选项：仅从系统范围的 $(prefix)/etc/gitconfig 读取，而不是从所有可用文件读取。

  另见“文件”章节。

- **--local**

  对于写入选项：写入仓库的 .git/config 文件。这是默认行为。

  对于读取选项：仅从仓库的 .git/config 读取，而不是从所有可用文件读取。

  另见“文件”章节。

- **-f config-file, --file config-file**

  使用给定的配置文件，而不是由 GIT_CONFIG 指定的配置文件。

- **--blob blob**

  类似于 --file，但使用给定的 blob 而不是文件。例如，你可以使用 *master::gitmodules* 从 master 分支的文件 .gitmodules 中读取值。有关拼写 blob 名称的更完整列表，参见 git(1) 中的“指定修订版本”章节。
