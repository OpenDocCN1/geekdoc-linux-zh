
```
$ git config --list
user.name=Christine Bresnahan
user.email=cbresn1723@gmail.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
$ ls /home/christine/.gitconfig
/home/christine/.gitconfig
$ cat /home/christine/.gitconfig
[user]
    name = Christine Bresnahan
    email = cbresn1723@gmail.com
$ ls /home/christine/MwGuard/.git/config
/home/christine/MwGuard/.git/config
$ cat /home/christine/MwGuard/.git/config
[core]
repositoryformatversion = 0
filemode = true
bare = false
logallrefupdates = true
$
```

通过 `--list` 选项显示的设置使用 `file-section.name` 格式。请注意，当使用 `cat` 命令将两个 Git 配置文件（全局和项目本地仓库）输出到 STDOUT 时，会显示部分名称及其包含的数据。

配置好本地 Git 环境后，是时候建立你项目的远程仓库了。为了演示目的，我们选择了基于云的远程仓库 GitHub。如果你想跟随操作，可以通过 github.com/join 链接设置一个免费的远程仓库。

> **注意**
>
> 虽然 Git 可以处理任何类型的文件，但其工具主要针对纯文本文件，如 Bash shell 脚本。因此，请注意你无法对所有非文本文件使用所有的 `git` 实用工具。

建立项目的远程仓库后，你需要记录它提供的 web 地址。此地址用于将项目文件发送到远程仓库，这在本章后面会有详细介绍。

### 使用 Git 提交

当你建立了 Git 环境后，你可以开始使用它的各种组织功能。基本步骤如下四步：

- 1. 创建或修改脚本。
- 2. 将脚本添加到暂存区（索引）。
- 3. 将脚本提交到本地仓库。
- 4. 将脚本推送到远程仓库。

根据您的工作流程，在继续下一步之前，可能需要重复某些步骤。例如，Linux 管理员在一天内编写 Bash shell 脚本，每完成一个脚本，就将其移至暂存区。在一天结束前，脚本编写者将整个项目提交到本地仓库。之后，他们将项目工作推送到远程仓库，以便非本地团队成员访问。

此处，创建了一个简单的 shell 脚本 `MyGitExampleScript.sh`，作为使用 Git 的项目示例：

```
$ cat MyGitExampleScript.sh
#!/bin/bash
# Git example script
#
echo "Hello Git World"
exit
$
```

脚本创建后，将其添加到暂存区（索引）。这是通过 `git add` 命令完成的。由于脚本当前不在我们的工作目录 `/home/christine/MWGuard` 中，我们首先将其复制到该位置。现在脚本位于正确的位置，我们将执行 `git add` 命令，此时我们的当前工作目录（通过 `pwd` 命令显示）也位于正确的位置 `/home/christine/MWGuard`：

```
$ pwd
/home/christine/scripts
$
$ cp MyGitExampleScript.sh /home/christine/MWGuard/
$
$ cd /home/christine/MWGuard/
$
$ pwd
/home/christine/MWGuard
$
$ ls *.sh
MyGitExampleScript.sh
$
$ git add MyGitExampleScript.sh
$
$ git status
[ ... ]
No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
  new file:  MyGitExampleScript.sh
```

执行 `git add` 命令时没有任何输出。因此，为了查看它是否按预期工作，我们使用了 `git status` 命令。`git status` 命令显示一个新文件 `MyGitExampleScript.sh` 已被添加到索引中。这正是我们想要看到的结果。

> **提示**
>
> 如果需要，您可以同时将当前工作目录中的所有脚本添加到暂存区的索引中。为此，请执行 `git add .` 命令。注意命令末尾的句点（`.`）！它实际上是一个通配符，指示 Git 将工作目录中的所有文件添加到索引中。
>
> 但是，如果工作目录中有不想添加到暂存区索引的文件，请在工作目录中创建一个 `.gitignore` 文件。接下来，使用您喜欢的文本编辑器将这些不想包含在索引中的文件和目录的名称添加到该文件中。现在，`git add .` 命令将忽略这些文件，但会将其余的脚本文件移至暂存区的索引中。

暂存区索引文件的文件名是 `.git/index`，当对它使用 `file` 命令时，显示的文件类型为 Git 索引。这是 Git 用于跟踪更改的文件。

```
$ file .git/index
.git/index: Git index, version 2, 1 entries
$
```

流程的下一步是将项目提交到本地仓库。提交是通过 `git commit` 命令完成的。我们添加了 `-m` 选项以添加注释，这对记录提交很有用：

```
$ git commit -m "Initial Commit"
[ ... ] Initial Commit
1 file changed, 5 insertions(+)
create mode 100644 MyGitExampleScript.sh
$
$ cat .git/COMMIT_EDITMSG
Initial Commit
$
$ git status
[ ... ]
nothing to commit, working tree clean
$
```

> **提示**
>
> 注释存储在 `COMMIT_EDITMSG` 文件中，它们有助于跟踪为何对各个脚本进行了更改。在脚本生命周期后期进行提交时，请在 `-m` 选项参数中包含修改原因，例如 `-m "Improved script's user interface."`

在发出 `git commit` 之后，`git status` 命令将显示消息 **nothing to commit, working tree clean**。这告诉您，Git 现在认为工作目录中的所有脚本都已提交到本地仓库。

> **警告**
>
> 如果未在 `git commit` 命令中添加 `-m` 选项及其参数，您将被放入 `vim` 编辑器中，手动编辑 `.git/COMMIT_EDITMSG` 文件。`vim` 编辑器在第 10 章“使用编辑器”中有所介绍。

现在，脚本项目已提交到本地仓库，可以通过将其推送到远程仓库与其他脚本项目团队成员共享。如果脚本已完成，您还可以将其与特定人员或整个世界共享。

如果这是一个新的脚本项目，在建立远程仓库账户后，创建一个名为 *Markdown 文件* 的特殊文件。该文件的内容显示在远程仓库的网页上，并描述该仓库。它使用所谓的 *Markdown* 语言。您需要将该文件命名为 **README.md**。以下是创建此文件、将其添加到暂存区索引并提交到本地仓库的示例：

```
$ pwd
/home/christine/MWGuard
$
$ ls
MyGitExampleScript.sh
$
$ echo "# Milky Way Guardian" > README.md
$ echo "## Script Project" >> README.md
$
$ cat README.md
# Milky Way Guardian
## Script Project
$
$
$ git add README.md
$
$ git status
[ ... ]
Changes to be committed:
   (use "git restore --staged <file>..." to unstage)
  new file:   README.md
$
$ git commit -m "README.md commit"
[ ... ]
README.md commit
1 file changed, 2 insertions(+)
create mode 100644 README.md
$
$ git status
[ ... ]
nothing to commit, working tree clean
$
```

> **注意**
>
