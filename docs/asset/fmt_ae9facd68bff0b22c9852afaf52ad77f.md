
如果你由于防火墙原因无法使用 `git` 协议，也可以通过 `http` 克隆，尽管这慢得多：

```bash
% clone perl
```

## 操作仓库

一旦你进入仓库目录，就可以对其进行检查。完成后仓库将包含一个本地分支，星号表示当前分支。

```bash
% branch *
```

使用 `-a` 切换显示仓库中的远程跟踪分支：

```bash
% branch -a * bleed origin/bleed
```

以 `origin` 开头的分支对应你克隆的远程。你不应该在这些远程跟踪分支上工作。本地分支可以配置为自动合并（pull）来自指定的远程跟踪分支。默认分支 `bleed` 就是这种情况，它配置为来自远程跟踪分支 `origin`。

你可以查看提交：

```bash
% log
```

从仓库拉取新更改并更新本地仓库（必须是干净的）：

```bash
% pull
```

假设 `pull` 之后我们在 `bleed` 分支上，此命令或等同于：

```bash
% fetch * git merge origin/bleed
```

实际上，如果你想在不接触工作目录的情况下更新本地仓库，执行：

```bash
% fetch
```

如果你想同时更新所有定义远程的远程跟踪分支，可以执行：

```bash
% remote update
```

这最后两个命令都不会更新你的工作目录，但都会更新远程跟踪分支。

为远程分支创建本地分支：

```bash
% checkout -b main-5.10 origin/main-5.10
```

切换回 `bleed`：

```bash
% checkout bleed
```

[PAGE 604]

# 查找你的状态

你最常用的 `git` 命令可能是：

```bash
% git status
```

此命令将生成仓库当前状态的输出，包括修改的文件和未跟踪的文件，此外，它还会显示哪些文件已暂存（staged）准备进行下一次提交，并且通常会提供一些关于如何更改内容的有用信息。例如：

```
$ git status # On branch bleed
Your branch is ahead of 'origin/bleed' by 1 commit. (use "git reset <file>..." 来取消暂存)
modified: pod/pergit.pod # 已修改但未更新 (使用 "git add <file>..." 来更新将提交的内容)
modified: pod/pergit.pod # 未跟踪的文件:
# (使用 "git add <file>..." 将其包含在待提交的内容中)
```

这显示此文档的更改已暂存等待提交，且工作目录中还有进一步的更改；或者显示工作目录中有一个未跟踪的文件，你可以你可以看到如何更改这些内容。它还显示工作分支 `bleed` 上有一个尚未推送到 `origin` 的提交。**注意**：如果你在执行 `git commit` 时没有提供信息，此输出也是你将看到的模板内容。

# 补丁工作流 (Patch workflow)

首先，请阅读 `perhack` 以了解关于修改 Perl 核心的细节。该文档涵盖了如何创建一个良好补丁的许多细节。

如果你已经有一个 Perl 仓库，你应该确保你正处于 `bleed` 分支，并且你的仓库是最新的：

```
% git checkout bleed
% git pull
```

最好针对最新的 `bleed` 版本进行补丁，因为除了关键修复（critical fix）之外，所有更改的新开发工作都在这里进行。关键修复补丁应该针对相关的维护分支（maint branches）制作，或者在提交时附带说明指出应应用修复的分支。

现在我们已经全部更新到最新状态，需要为这些更改创建一个临时新分支并切换进去：

```
% git checkout -b git orange
```

其简写形式为：

```
% git branch orange
% git checkout orange
```

创建一个主题分支（topic branch）让维护者更容易进行变基（rebase）或将其合并回主分支，从而获得更线性的历史。如果你不在主题分支上工作，维护者必须在应用你的更改之前手动将它们挑选到 `bleed` 分支上。

那会导致你在 `perl5-porters` 上被责骂，所以别这样做。太棒了。

然后进行你的更改。例如，如果 Leon Brocard 将他的名字改为 Orange Brorocad，我们应该更改 `AUTHORS` 文件中他的名字：

```
% perl -pi 's{Leon Brocad}{Orange Brocad}' AUTHORS
```

你可以看到哪些文件被修改了：

```
% git status # On branch
Changes to be committed:
# (使用 "git reset HEAD<file>..."取消暂存)
# modified: AUTHORS #
```

你可以看到更改：

```
% git diff -a a/AUTHORS b/AUTHORS index 293dd70.722c93e100644 --
a/AUTHORS ++ b/AUTHORS @@ -541,7 +541,7 @@ Lars Heck < Laszlo Molnar
< Left Hahn < Len Johnson <> -Leon Brocad <> +Orange Brocad < Les
Peters < Lesley Banks <> Lincoln D. Stein <
```

现在提交你的本地更改：

```
% git commit -a "Rename Leon Brocad to Orange Brocad Created commit 6196cid: Rename Leon Brocad to Orange Brocad 1 files changed, 1 insertions(+), 1 deletions(-)"
```

`-a` 选项用于包含你 `git` 跟踪的所有已文件。如果你只想提交你工作过的部分文件，可以省略 `-a` 并在提交前使用命令 `git add FILE...`。`git add interactive` 允许你仅提交文件的部分内容，而不是文件中的所有更改。

一旦你完成提交信息并退出编辑器，`git` 将写入你的更改并告知你类似如下的内容：

Created commit dafe863: explain git status and stuff about remotes 1 files hanged, 83 insertions(+), 3 deletions(-)

如果你重新运行 `git status`，你应该会看到类似下面的内容：

```
% git status # On branch bleed
Your branch is ahead of 'origin/bleed' 2 commits.
# Untracked files:
# (use "git add <file>..." 来包含待提交的内容)
# nothing added to commit
but untracked files present (use "git add" 来跟踪)
```

如有疑问，在执行任何其他操作之前，请检查你的状态并仔细阅读，问题现在直接由 `git status` 的输出回答。

你可以通过以下命令检查你的最后提交：

```
% git show HEAD
```

如果你对描述或补丁本身都不满意，可以通过再次编辑文件来修复它，然后执行：

```
% git commit -a --amend
```

现在你应该为你所有的本地更改创建一个补丁文件：

```
$ git format-patch -M bleed.. 0001-Rename-Leon-Brocad-to-Orange-Brocad.patch
```

或者对于大量的更改，例如从一个主题分支：

```
% git format-patch --stdout -M bleed.. > topic-branch-changes.patch
```

你应该向 `<mailto:>` 发送一封邮件，附带你更改的描述，并将此补丁文件作为附件。如有疑问，在执行任何其他操作之前，请检查你的状态并仔细阅读，问题现在直接由 `git status` 的输出回答。

核心部分提供了一个包装程序 `Porting/bisect.pl`，它尝试尽可能简化操作，使得二分查找（bisect）像运行一个 Perl 单行命令一样简单。例如，如果你想知道这个错误何时发生的：

```perl
perl -e 'my $sa := 2'
```

你只需要运行以下命令即可：

```
...Porting/bisect.pl -e 'my $sa := 2;'
```

使用 `bisect.pl`，通过一个命令（无需其他文件）就可以轻松找到：

- 是哪一个提交导致了该示例代码崩溃？

- 是哪一个提交导致该示例代码开始正常工作？

- 是哪一个提交添加了第一个匹配该正则表达式的文件？
