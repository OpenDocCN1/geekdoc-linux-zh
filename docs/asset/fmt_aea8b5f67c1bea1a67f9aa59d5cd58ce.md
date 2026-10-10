
### --recurse-submodules=check|on-demand

- 确保用于待推送修订版本的所有子模块提交（commits）在远程跟踪分支上可用。如果使用 `check`，Git 将验证在待推送修订版本中更改的所有子模块提交是否在子模块的至少一个远程上可用。如果缺少任何提交，推送将中止并以非零状态退出。如果使用 `on-demand`，将推送在待推送修订版本中更改的所有子模块。如果 `on-demand` 未能推送所有必要的修订版本，它也将中止并以非零状态退出。

### --[no-]verify

- 切换 `pre-push` 钩子（参见 `githooks`）。默认是 `--verify`，给予钩子阻止推送的机会。使用 `--no-verify` 时，钩子将被完全绕过。

## GIT URL

通常，URL 包含关于传输协议、远程服务器地址以及指向仓库路径的信息。根据传输协议的不同，这些信息中的某些部分可能缺失。

Git 支持 `ssh`、`git`、`http` 和 `https` 协议（此外，`ftp` 和 `ftps` 可用于拉取，`rsync` 可用于拉取和推送，但效率低下且已弃用；请勿使用它们）。

原生传输（即 `git://` URL）不进行身份验证，在未经安全保护的网络上应谨慎使用。

它们可以使用以下语法：

- `http[s]://host.xz[:port]/path/to/repo.git/`

- `ftp[s]://host.xz[:port]/path/to/repo.git/`

对于 ssh 协议，也可以使用类似 scp 的替代语法：

- `[user@]host.xz:path/to/repo.git/`

仅当第一个冒号前没有斜杠时才识别此语法。这有助于区分包含冒号的本地路径。例如，包含冒号的本地路径 `foo:bar` 可以指定为绝对路径或 `./foo:bar`，以避免被误认为 ssh url。

ssh 和 git 协议还支持 `~username` 扩展：

- `[user@]host.xz:~[user]/path/to/repo.git/`

对于本地仓库（Git 也原生支持），可以使用以下语法：

- `/path/to/repo.git/`

这两种语法基本等价，除了在克隆时，前者隐含 `--local` 选项。详见 `git-clone`。

当 Git 不知道如何处理某种传输协议时，如果存在相应的 `remote-<transport>` 远程辅助工具，它将尝试使用该工具。若要明确请求远程辅助工具，可以使用以下语法：

- `<transport>::<address>`

其中 `<address>` 可以是路径、服务器和路径，或者是被调用的特定远程辅助工具识别的任意类 URL 字符串。详见 `gitremote-helpers`。

如果存在大量名称相似的远程仓库，并且希望为它们使用不同的格式（使得您使用的 URL 将被重写为可用的 URL），您可以创建如下形式的配置部分：

```
[url "actual url base"] insteadof  = <other url base>
```

例如，使用以下配置：

```
[url ""] insteadOf = host.xz:/path/to/ insteadOf = work:
```

在需要 URL 的任何上下文中，类似 "`work:repo.git`" 或 "`host.xz:/path/to/repo.git`" 的 URL 将被重写为 `""`。

如果您只想在推送时重写 URL，可以创建如下形式的配置部分：

```
    [url "<actual url base>"] pushInsteadOf = <other url base>
```

例如，使用以下配置：

```
    [url ""] pushInsteadOf =
```

类似 `""` 的 URL 在推送时将被重写为 `''`，但拉取仍将使用原始 URL。

## 远程（REMOTES）

可以将以下各项的名称用作 `<repository>` 参数来替代 URL：Git 配置文件中的远程：`$GIT_DIR/config`，`$GIT_DIR/remotes` 目录中的文件，或 `$GIT_DIR/branches` 目录中的文件。

这些选项都允许您从命令行省略引用规范（refspec），因为它们各自包含 git 默认使用的引用规范。

### 配置文件中的命名远程

您可以选择提供之前使用 `git remote add`、`git config` 甚至通过手动编辑 `$GIT_DIR/config` 文件配置的远程名称。此远程的 URL 将用于访问仓库。此远程的引用规范将默认在命令行未提供引用规范时使用。配置文件中的条目将如下所示：

```
    [remote "<name>"] url = <url> pushurl = <pushurl> push = <refspec> fetch = <refspec>
```

`<pushurl>` 仅用于推送。它是可选的，默认值为 `<url>`。

### $GIT_DIR/remotes 中的命名文件

您可以选择提供 `$GIT_DIR/remotes` 中文件的名称。此文件中的 URL 将用于访问仓库。此文件中的引用规范将在命令行未提供引用规范时作为默认值使用。此文件应具有以下格式：

```
    URL: one of the above URL format Push: <refspec> Pull: <refspec>
```

`Push:` 行由 `git push` 使用，`Pull:` 行由 `git pull` 和 `git fetch` 使用。可以为额外的分支映射指定多个 `Push:` 和 `Pull:` 行。

### $GIT_DIR/branches 中的命名文件

您可以选择提供 `$GIT_DIR/branches` 中文件的名称。此文件中的 URL 将用于访问仓库。此文件应具有以下格式：

```
    <url>#<head>
```

`<url>` 是必需的；`#<head>` 是可选的。

根据操作的不同，如果在命令行中未提供引用规范，git 将使用以下引用规范之一。`<branch>` 是 `$GIT_DIR/branches` 中此文件的名称，`<head>` 默认为 `master`。

`git fetch` 使用：

`refs/heads/<head>:refs/heads/<branch>`

`git push` 使用：

`HEAD:refs/heads/<head>`

## 输出（OUTPUT）

"`git push`" 的输出取决于所使用的传输方法；本节描述了通过 Git 协议（无论是本地还是通过 ssh）推送时的输出。

推送的状态以表格形式输出，每行代表单个引用的状态。每行的形式为：

```
<flag> <summary> <from> -> <to> (<reason>)
```

如果使用 `--porcelain`，则输出的每行形式为：

```
<flag> \t <from>:<to> \t <summary> (<reason>)
```

最新引用的状态仅在使用了 `--porcelain` 或 `--verbose` 选项时显示。

### 标志（flag）

单个字符，指示引用的状态：

- 对于成功推送的快速前进（fast-forward），显示 `(空格)`；

- 对于成功强制更新，显示 `+`；

- 对于成功删除的引用，显示 `-`；

- 对于成功推送的新引用，显示 `*`；

- 对于被拒绝或推送失败的引用，显示 `!`；以及

- 对于最新且无需推送的引用，显示 `=`。

### 摘要（summary）

对于成功推送的引用，摘要以适合用作 `git log` 参数的形式显示引用的旧值和新值（在大多数情况下是 `<old>…<new>`，对于强制非快速前进更新则是 `<old>…<new>`）。

对于失败的更新，将提供更多详细信息：

- `rejected`：Git 根本没有尝试发送该引用，通常因为它不是快速前进且您没有强制更新。

- `remote rejected`：

## 远端拒绝更新

通常由远端的钩子（hook）引起，或者因为远端仓库启用了以下安全选项之一：`receive.denyCurrentBranch`（用于向已检出分支的推送）、`receive.denyNonFastForwards`（用于强制非快进更新）、`receive.denyDeletes` 或 `receive.denyDeleteCurrent`。请参阅手册页。

## 远端故障

远端没有报告引用（ref）更新成功，可能是由于远端的临时错误、网络连接中断或其他瞬时错误。

## from

被推送的本地引用的名称，去除其 `refs/<type>/` 前缀。在删除的情况下，省略本地引用的名称。

## to

被更新的远端引用的名称，去除其 `refs/<type>/` 前缀。

## reason

人类可读的解释。对于成功推送的引用，无需解释。对于失败的引用，将描述失败原因。
