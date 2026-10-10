

*CRAM-MD5*。如果未设置此选项，则 *git imap-send* 将使用基础的 IMAP 明文 LOGIN 命令。

## 示例

使用隧道模式：

```ini
[imap] folder = "INBOX.Drafts" tunnel = "ssh -q -C /usr/bin/imapd ./Maildir 2>/dev/null"
```

使用直接模式：

```ini
[imap] folder = "INBOX.Drafts" host = user = bob pass = p455w0rd
```

使用带 SSL 的直接模式：

```ini
[imap] folder = "INBOX.Drafts" host = user = bob pass = p455w0rd port = 123 sslverify = false
```

## 示例

要通过 GMail 的 IMAP 接口提交补丁，首先请编辑你的 ~/.gitconfig 以指定你的账户设置：

```ini
[imap] folder = "[Gmail]/Drafts" host = user = port = 993 sslverify = false
```

如果收到“文件夹不存在”的错误，你可能需要改为使用：`folder = "[Google Mail]/Drafts"`。

一旦提交准备好发送，请运行以下命令：

```bash
$ git format-patch --cover-letter -M --stdout origin/master | git imap-send
```

请务必在电子邮件客户端中禁用自动换行（GMail 的网页界面无论如何都会对行进行换行，因此你需要使用真正的 IMAP 客户端）。

## 注意

你仍有责任确保你的电子邮件程序发送的电子邮件消息符合你所在项目的标准。许多项目不喜欢以附件形式发送补丁。某些邮件代理会以导致补丁失败的方式转换补丁（例如，换行，以 format=flowed 格式发送）。如果你不检查这一点，你会招致愤怒的嘲讽。

Thunderbird 特别以存在问题而闻名。Thunderbird 用户可能希望访问此网页以获取更多信息：m[]

## 另请参阅

(1), (1), (5)

## GIT-INDEX-PACK

### 名称

git-index-pack - 为现有的打包归档构建包索引文件

### 用法

```bash
git index-pack [-v] [-o <index-file>] <pack-file>
git index-pack --stdin [--fix-thin] [--keep] [-v] [-o <index-file>] [<pack-file>]
```

### 描述

从指定文件读取打包归档（.pack），并为其构建包索引文件（.idx）。打包归档和包索引文件然后可以放置在 Git 仓库的 objects/pack/ 目录中。

### 选项

-   **-v**
    详细显示正在发生的事情，包括进度状态。
-   **-o <index-file>**
    将生成的包索引写入指定文件。如果没有此选项，包索引文件的名称将通过将打包归档文件名的 .pack 替换为 .idx 来构造（如果打包归档的名称不以 .pack 结尾，则程序会失败）。
-   **--stdin**
    提供此标志时，包从标准输入读取，然后复制到 `<pack-file>`。如果未指定 `<pack-file>`，包将写入当前 Git 仓库的 objects/pack/ 目录，其默认名称由包内容确定。如果未指定 `<pack-file>`，请考虑使用 `--keep` 以防止此进程与 git repack 之间的竞态条件。
-   **--fix-thin**
    通过添加被排除的对象（即 delta 化对象所基于的对象）来修复由 `git pack-objects --thin`（详见 (1)）生成的“瘦”包。此选项仅在结合 `--stdin` 使用时才有意义。
-   **--keep**
    在将索引移动到最终目的地之前，为相关的包文件创建一个空的 .keep 文件。此选项通常与 `--stdin` 一起使用，以防止并发的 git repack 进程在引用更新为使用包中包含的对象之前删除新构建的包和索引。
-   **--keep=<msg>**
    类似于 `--keep`，在将索引移动到最终目的地之前创建 .keep 文件，但不是在创建一个空文件，而是将 `<msg>` 后跟一个 LF 放入 .keep 文件。之后可以在所有 .keep 文件中搜索 `<msg>` 消息，以查找那些已过期的文件。
-   **--index-version=<version>[,<offset>]**
    这是专为测试套件设计的。它允许强制指定生成的包索引的版本，并强制对位于指定偏移量之上的对象使用 64 位索引条目。
-   **--strict**
    如果包包含损坏的对象或链接，则终止程序。
-   **--check-self-contained-and-connected**
    如果包包含损坏的链接，则终止程序。仅供内部使用。
-   **--threads=<n>**
    指定在解析 delta 时生成线程的数量。这需要 index-pack 在编译时包含 pthreads，否则此选项将被忽略并发出警告。这旨在减少多处理器机器上的打包时间。但是，delta 搜索窗口所需的内存量会随线程数倍增。指定 0 将使 Git 自动检测 CPU 数量并使用最多 3 个线程。

## 注意

索引创建完成后，对象名称列表将被排序，并且该列表的 SHA-1 哈希值将打印到标准输出。如果也使用了 `--stdin`，则会以前缀“pack\t”或“keep\t”（如果成功创建新的 .keep 文件）开头。这对于删除作为锁使用的 .keep 文件（以防止上述与 *git repack* 的竞态）很有用。

## GIT-INIT-DB

### 名称

git-init-db - 创建一个空的 Git 仓库

### 用法

```bash
git init-db [-q | --quiet] [-bare] [--template=<template_directory>]
[--separate-git-dir <git dir>] [--shared[=<permissions>]]
```

### 描述

这是 (1) 的同义词。请参见该命令的文档。

## GIT-INIT

### 名称

git-init - 创建一个空的 Git 仓库或重新初始化现有仓库

### 用法

```bash
git init [-q | --quiet] [--bare] [--template=<template_directory>]
[--separate-git-dir <git dir>] [--shared[=<permissions>]] [directory]
```

### 描述

此命令创建一个空的 Git 仓库——基本上是一个包含 objects、refs/heads、refs/tags 以及模板文件子目录的 .git 目录。还会创建一个引用 master 分支 HEAD 的初始 HEAD 文件。

如果设置了 $GIT_DIR 环境变量，则它指定用于替代 ./.git 作为仓库基础的路径。

如果通过 $GIT_OBJECT_DIRECTORY 环境变量指定了对象存储目录，则 sha1 目录将在其下创建——否则使用默认的 $GIT_DIR/objects 目录。

在现有仓库中运行 *git init* 是安全的。它不会覆盖已存在的内容。重新运行 *git init* 的主要原因是获取新添加的模板（或者如果给出了 `--separate-git-dir`，则将仓库移动到另一个位置）。

### 选项

-   **-q, --quiet**
    仅打印错误和警告消息；其他所有输出都将被抑制。
-   **--bare**
    创建一个裸仓库。如果 GIT_DIR 环境变量未设置，则将其设置为当前工作目录。
-   **--template=<template_directory>**
    指定用于模板的目录。（参见下文“TEMPLATE DIRECTORY”部分。）
-   **--separate-git-dir=<git dir>**
    不是将仓库初始化为指向 $GIT_DIR 或 ./.git/ 的目录，而是在那里创建一个文本文件，其中包含指向实际仓库的路径。此文件充当文件系统无关的 Git 符号链接，指向该仓库。
    
    如果是重新初始化，仓库将被移动到指定路径。
-   **--shared[=(false|true|umask|group|all|world|everybody|0xxx)]**
    指定该 Git 仓库将在多个用户之间共享。这允许属于同一组的用户推送到该仓库。当指定时，配置变量“core.sharedRepository”将被设置，使得 $GIT_DIR 下的文件和目录以请求的权限创建。当未指定时，Git 将使用由 (2) 报告的权限。
    
    该选项可以具有以下值，如果没有给出值，则默认为 group：
    -   **umask (或 false)**
        使用由 (2) 报告的权限。这是未指定 --shared 时的默认值。
    -   **group (或 true)**
        使仓库组可写，（并且 g+s，因为 git 组可能不是所有用户的主组）。这用于放宽其他安全的 (2) 值权限。请注意，umask 仍然适用于其他权限位（例如，如果 umask 是 0022，使用 group 不会移除其他（非组）用户的读取权限）。参见 0xxx 以了解如何确切指定仓库权限。
    -   **all (或 world 或 everybody)**
        类似于 group，但使仓库对所有用户可读。
    -   **0xxx**
        0xxx 是一个八进制数，每个文件将具有模式 0xxx。0xxx 将覆盖用户的 (2) 值（而不仅仅是像 group 和 all 那样放宽权限）。0640 将创建一个

