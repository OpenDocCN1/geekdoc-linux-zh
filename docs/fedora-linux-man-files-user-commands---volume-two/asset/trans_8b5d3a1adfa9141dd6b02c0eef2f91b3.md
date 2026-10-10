

## GIT-COUNT-OBJECTS

### 名称

git-count-objects - 统计未打包对象的数量及其磁盘占用

### 概要

```
git count-objects [-v] [-H | --human-readable]
```

### 描述

此命令统计未打包的对象文件数量及它们所占用的磁盘空间，帮助你判断何时是重新打包（repack）的好时机。

### 选项

- `-v, --verbose`
  报告更多详细信息：
  - `count`：松散对象（loose objects）的数量
  - `size`：松散对象占用的磁盘空间，单位为 KiB（除非指定了 `-H`）
  - `in-pack`：打包对象（in-pack objects）的数量
  - `size-pack`：包（packs）占用的磁盘空间，单位为 KiB（除非指定了 `-H`）
  - `prune-packable`：同时也存在于包中的松散对象数量。这些对象可以通过 `git prune-packed` 进行清理。
  - `garbage`：对象数据库中既不是有效松散对象也不是有效包的垃圾文件数量
  - `size-garbage`：垃圾文件占用的磁盘空间，单位为 KiB（除非指定了 `-H`）

- `-H, --human-readable`
  以人类可读的格式打印大小

## Git-credential-cache—daemon

### 名称

git-credential-cache—daemon - 在内存中临时存储用户凭证

### 概要

```
git credential-cache---daemon [--debug] <socket>
```

### 描述

#### 注意

你可能不希望手动调用此命令；当你使用 (1) 时，它会自动启动。

此命令监听由 `<socket>` 指定的 Unix 域套接字，以接收来自 git-credential-cache 客户端的连接。客户端可以存储和检索凭证。每个凭证由客户端指定的超时时间持有；一旦没有持有凭证，守护进程将退出。

如果指定了 `--debug` 选项，守护进程将不会关闭其 stderr 流，并且在开始监听客户端后，仍可能向其输出额外的诊断信息。

## GIT-CREDENTIAL-CACHE

### 名称

git-credential-cache - 用于在内存中临时存储密码的辅助工具

### 概要

```
git config credential.helper 'cache [options]'
```

### 描述

此命令在内存中缓存凭证，供未来的 Git 程序使用。存储的凭证永远不会触及磁盘，并且在可配置的超时时间后会被遗忘。该缓存通过 Unix 域套接字访问，并通过文件系统权限限制仅当前用户可访问。

你可能不希望直接调用此命令；它是作为其他 Git 部分的凭证辅助工具设计的。请参阅 (7) 或下方的示例。

### 选项

- `--timeout <seconds>`
  缓存凭证的秒数（默认：900）。

- `--socket <path>`
  使用 `<path>` 联系正在运行的缓存守护进程（如果守护进程未启动，则启动一个新的缓存守护进程）。默认为 `~/.git-credential-cache/socket`。如果你的主目录位于网络挂载的文件系统上，你可能需要将其更改为本地文件系统。

### 控制守护进程

如果你希望守护进程提前退出，在其超时之前忘记所有已缓存的凭证，你可以发出退出操作：

```
git credential-cache exit
```

### 示例

此辅助工具的目的是减少你需要输入用户名或密码的次数。例如：

```
$ git config credential.helper cache $ git push Username: <输入你的用户名> Password: <输入你的密码> [再工作 5 分钟] $ git push [你的凭证将被自动使用]
```

你可以通过 credential.helper 配置变量提供选项（此示例将缓存时间缩短为 5 分钟）：

```
$ git config credential.helper 'cache --timeout=300'
```

## GIT-CREDENTIAL-STORE

### 名称

git-credential-store - 用于在磁盘上存储凭证的辅助工具

### 概要

```
git config credential.helper 'store [options]'
```

### 描述

#### 注意

使用此辅助工具会在磁盘上未加密地存储你的密码，仅由文件系统权限保护。如果这种安全权衡不可接受，请尝试 (1)，或者寻找一个能与你操作系统提供的安全存储集成的辅助工具。

此命令将凭证永久存储在磁盘上，供未来的 Git 程序使用。你可能不希望直接调用此命令；它是作为 git 其他部分的凭证辅助工具设计的。请参阅 (7) 或下方的示例。

### 选项

- `--file=<path>`
  使用 `<path>` 查找和存储凭证。该文件的文件系统权限将设置为防止系统中的其他用户读取它，但它不会被加密或以其他方式保护。如果未指定，凭证将从 `~/.git-credentials` 和 `$XDG_CONFIG_HOME/git/credentials` 中查找，并且如果 `~/.git-credentials` 存在，则凭证将写入该文件；否则，如果 `$XDG_CONFIG_HOME/git/credentials` 存在而前者不存在，则写入后者。另请参阅“FILES”部分。

### 文件

如果没有通过 `--file` 显式设置，git-credential-store 将按优先级顺序在以下两个文件中查找凭证：

- `~/.git-credentials`
  用户特定的凭证文件。
- `$XDG_CONFIG_HOME/git/credentials`
  第二个用户特定的凭证文件。如果 `$XDG_CONFIG_HOME` 未设置或为空，将使用 `$HOME/.config/git/credentials`。如果 `~/.git-credentials` 中也有匹配的凭证，则此文件中存储的凭证将不会被使用。如果你有时使用不支持此功能较旧版本的 Git，最好不要创建此文件。

对于凭证查找，文件按上述顺序读取，找到的第一个匹配凭证优先于列表中更下方文件中的凭证。

凭证存储默认写入列表中第一个存在的文件。如果这些文件都不存在，将创建并写入 `~/.git-credentials`。

在擦除凭证时，匹配的凭证将从所有文件中擦除。

### 示例

此辅助工具的目的是减少你需要输入用户名或密码的次数。例如：

```
$ git config credential.helper store
$ git push
Username: <输入你的用户名>
Password: <输入你的密码>
[几天后]
$ git push
[你的凭证将被自动使用]
```

### 存储格式

`.git-credentials` 文件以明文存储。每个凭证作为一行 URL 存储，格式如下：

当 Git 需要针对特定 URL 上下文进行身份验证时，credential-store 将该上下文视为一个模式，以匹配凭证文件中的每个条目。如果协议、主机名和用户名（如果已有）匹配，则返回密码给 Git。有关配置的更多讨论，请参阅 (7)。

## GIT-CREDENTIAL

### 名称

git-credential - 获取和存储用户凭证

### 概要

```
git credential <fill|approve|reject>
```

### 描述

Git 具有内部接口，用于从系统特定的辅助工具存储和检索凭证，以及提示用户输入用户名和密码。git-credential 命令将此接口暴露给脚本，以便脚本可以以与 Git 相同的方式检索、存储或提示凭证。此可脚本化接口的设计模拟了内部 C API；有关这些概念的背景信息，请参阅**Git 凭证 API**[1]。

git-credential 在命令行接受一个“action”选项（fill、approve 或 reject 之一），并从标准输入读取凭证描述（参见输入/输出格式）。

如果操作是 fill，git-credential 将尝试通过读取配置文件、联系已配置的凭证辅助工具或提示用户，向描述中添加“username”和“password”属性。然后，凭证描述中的用户名和密码属性将与已提供的属性一起打印到标准输出。

如果操作是 approve，git-credential 将把描述发送给已配置的凭证辅助工具，它们可能会存储该凭证供以后使用。

如果操作是 reject，git-credential 将把描述发送给已配置的凭证辅助工具，它们可能会擦除与该描述匹配的任何已存储凭证。

如果操作是 approve 或 reject，不应发出任何输出。

