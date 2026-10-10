
## 配置

像“work:repo.git”或“host.xz:/path/to/repo.git”这样的 URL 将在任何接受 URL 的上下文中被重写为“work:repo.git”或“host.xz:/path/to/repo.git”。

如果你只想为推送重写 URL，可以创建如下形式的配置段：

```
[url "<actual url base>"] pushInsteadOf = <other url base>
```

例如，有了以下内容：

```
[url ""] pushInsteadOf =
```

像“...”这样的 URL 在推送时会被重写为“...”，但拉取仍会使用原始 URL。

## 示例

从上流克隆：

```
$ git clone my-linux
$ cd my-linux
$ make
```

创建一个本地克隆，它借用当前目录而不进行检出：

```
$ git clone -l -s -n ../copy
$ cd ../copy
$ git show-branch
```

从上流克隆，同时借用现有的本地目录：

```
$ git clone --reference /git/linux.git \
    my-linux
$ cd my-linux
```

创建一个裸仓库，以便将你的更改发布到公共领域：

```
$ git clone --bare -l /home/proj/.git /pub/scm/proj.git
```

## GIT-COLUMN

### 名称

git-column - 以列形式显示数据

### 概要

`git column` [--command=<name>] [--[raw-]mode=<mode>] [-width=<width>] [-indent=<string>] [-nl=<string>] [-padding=<n>]

### 描述

此命令将其输入格式化为多列。

### 选项

- `--command=<name>`
  使用配置变量 `column.<name>` 和 `column.ui` 查找布局模式。
- `--mode=<mode>`
  指定布局模式。有关选项语法，请参阅配置变量 `column.ui`。
- `--raw-mode=<n>`
  与 `--mode` 相同，但接受以数字编码的模式。这主要用于其他已解析布局模式的命令。
- `--width=<width>`
  指定终端宽度。默认情况下，*git column* 会检测终端宽度，如果无法检测则回退为 80。
- `--indent=<string>`
  在每行开头打印的字符串。
- `--nl=<N>`
  在每行末尾打印的字符串，包括换行符。
- `--padding=<N>`
  列之间的空格数。默认为 1 个空格。

## GIT-COMMIT-TREE

### 名称

git-commit-tree - 创建一个新的提交对象

### 概要

`git commit-tree <tree> [-p <parent>...] [-S[<keyid>]] [(-m <message>)...] [(-F <file>)...] <tree>`

### 描述

这通常不是最终用户想要直接运行的。请参见 `git commit`。

根据提供的树对象创建一个新的提交对象，并在标准输出上输出新的提交对象 ID。除非给出 -m 或 -F 选项，否则日志消息从标准输入读取。

提交对象可以有任意数量的父对象。如果恰好有一个父对象，它是一个普通的提交。拥有多个父对象使该提交成为多个历史线的合并。初始（根）提交没有父对象。

虽然树表示工作目录的特定目录状态，但提交表示该状态在“时间”上的表示，并解释如何到达该状态。

通常，提交会识别一个新的“HEAD”状态，虽然 Git 不在乎你将关于该状态的笔记保存在哪里，但在实践中，我们倾向于将结果写入 `.git/HEAD` 指向的文件，这样我们就可以随时看到最后一次提交的状态。

### 选项

- **tree**
  一个现有的树对象
- **-p parent**
  每个 -p 指定一个父提交对象的 ID。
- **-m message**
  提交日志消息中的一个段落。这可以多次给出，每个 `<message>` 成为自己的段落。
- **-F file**
  从给定文件读取提交日志消息。使用 - 从标准输入读取。
- **-S<keyid>**, **--gpg-sign[=<keyid>]**
  GPG 签名提交。
- **--no-gpg-sign**
  抵消设置为强制每个提交都签名的 `commit.gpgSign` 配置变量。

### 提交信息

一个提交封装了：

- 所有父对象 ID
- 作者姓名、电子邮件和日期
- 提交者姓名、电子邮件和提交时间。

虽然父对象 ID 在命令行上提供，但作者和提交者信息取自以下环境变量（如果已设置）：

```
GIT_AUTHOR_NAME
GIT_AUTHOR_EMAIL
GIT_AUTHOR_DATE
GIT_COMMITTER_NAME
GIT_COMMITTER_EMAIL
GIT_COMMITTER_DATE
```

（注意“<”、“>”和“\n”会被去除）

如果（部分）这些环境变量未设置，则信息取自配置项 `user.name` 和 `user.email`，或者如果不存在，则取自环境变量 `EMAIL`，或者如果那也未设置，则取自系统用户名和用于发出邮件的主机名（取自 `/etc/mailname`，如果该文件不存在则回退到完全限定主机名）。

提交注释从标准输入读取。如果没有通过“<”重定向提供变更日志条目，`git commit-tree` 将等待输入并以 ^D 终止。

### 日期格式

`GIT_AUTHOR_DATE` 和 `GIT_COMMITTER_DATE` 环境变量支持以下日期格式：

**Git 内部格式**

它是 `<unix 时间戳> <时区偏移>`，其中 `<unix 时间戳>` 是自 UNIX 纪元以来的秒数。`<时区偏移>` 是相对于 UTC 的正或负偏移量。例如，CET（比 UTC 早 2 小时）是 +0200。

**RFC 2822**

由 RFC 2822 描述的标准电子邮件格式，例如 `Thu, 07 Apr 2005 22:13:13 +0200`。

**ISO 8601**

由 ISO 8601 标准指定的日期和时间，例如 `2005-04-07T22:13:13`。解析器也接受 T 字符替换为空格。

**注意** 此外，日期部分接受以下格式：`YYYY.MM.DD`、`MM/DD/YYYY` 和 `DD.MM.YYYY`。

### 讨论

在核心层面，Git 对字符编码无感知。

索引和树对象中记录的文件名被视为未解释的非 NUL 字节序列。`git ls-files` 返回的是已记录并与 Git 跟踪的数据进行比较的内容，反过来，这些内容被期望是 `git add` 和 `git rm` 接受的。不存在文件名编码转换。

Blob 对象的内容是未解释的字节序列。在核心层面没有编码转换。

提交日志消息是未解释的非 NUL 字节序列。

虽然我们鼓励提交日志消息以 UTF-8 编码，但核心和 Git Porcelain 的设计都不强制项目使用 UTF-8。如果特定项目的所有参与人员发现使用传统编码更方便，Git 并不禁止。但是，有一些事情需要注意。

1. 如果给定的提交日志消息看起来不像有效的 UTF-8 字符串，除非你明确说明你的项目使用传统编码，否则 *git commit* 和 *git commit-tree* 会发出警告。说明这一点的方法是在 `.git/config` 文件中拥有 `i18n.commitencoding`，如下所示：

   ```
   [i18n]  commitencoding = ISO-8859-1
   ```

   使用上述设置创建的提交对象在其 `encoding` 头部记录 `i18n.commitencoding` 的值。这是为了帮助后来查看它们的人。缺少此头部意味着提交日志消息以 UTF-8 编码。

2. *git log*、*git show*、*git blame* 及类似命令查看提交对象的 `encoding` 头部，并尝试将日志消息重新编码为 UTF-8，除非另有指定。你可以在 `.git/config` 文件中通过 `i18n.logoutputencoding` 指定所需的输出编码，如下所示：

   ```
   [i18n]  logoutputencoding = ISO-8859-1
   ```

   如果你没有这个配置变量，则会使用 `i18n.commitencoding` 的值。

请注意，我们特意选择不将提交日志消息重新编码为 UTF-8 以在提交对象层面强制使用 UTF-8，因为重新编码为 UTF-8 并不一定是一个可逆操作。
