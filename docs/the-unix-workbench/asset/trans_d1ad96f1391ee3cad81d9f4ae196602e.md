

```text
## On branch master
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
##      toby.jpg
##
## nothing added to commit but untracked files present (use "git add" to track)
```

现在我们已经向仓库添加了一张图片，让我们添加一个 .gitignore 文件以确保 Git 不会跟踪这类文件。

```bash
echo "*.jpg" > .gitignore
git status
```

```text
## On branch master
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
##
##      .gitignore
##
## nothing added to commit but untracked files present (use "git add" to track)
```

现在我们可以看到 Git 已经检测到新的 .gitignore 文件，但它看不到 toby.jpg。让我们添加并提交我们的 .gitignore 文件：

```bash
git add -A
git commit -m "added gitignore"
```

```text
## [master adef548] added gitignore
## 1 file changed, 1 insertion(+)
## create mode 100644 .gitignore
```

现在如果我们再添加一个 .jpg 文件，Git 将不会看到该文件：

```bash
touch bernie.jpg
git status
```

```text
## On branch master
## nothing to commit, working tree clean
```

```bash
ls
```

```text
## bernie.jpg
## toby.jpg
## file1.txt
## file2.txt
## readme.txt
```

## Summary

- git help 允许你阅读特定 Git 命令的手册页。
- git log 会显示你的提交历史。
- git diff 显示上次提交与当前未跟踪更改之间的差异。
- 你可以指定一个 .gitignore 文件来告诉 Git 不要跟踪某些文件。

## Exercises

- 1. 查看 `git log` 和 `git diff` 的帮助页面。
- 2. 在你已开始的 `.gitignore` 中添加一个特定的文件名，然后将该文件添加到你的仓库。
- 3. 创建一个包含此仓库 Git 日志的文件。使用 `grep` 查看大多数提交发生在星期几。

## Branching

分支是 Git 提供的最强大的功能之一。创建不同的 Git 分支允许你独立于仓库的其它“副本”来处理特定功能或一组文件。这样你和朋友可以在不同的分支上处理同一文件的不同部分，然后 Git 可以帮助你优雅地合并分支和更改。

你可以使用命令 `git branch` 列出所有可用的分支：

```bash
git branch
```

```text
## * master
```

星号 (*) 表示你当前所在的分支。创建的默认分支始终称为 master。通常人们使用此分支作为他们正在编写的软件的工作版本，而在其它分支上开发新的且可能不稳定的功能。

要添加分支，我们也会使用 git branch 命令，后跟我们想要创建的分支的名称：

```bash
git branch my-new-feature
```

现在让我们再次输入 git branch 以确认我们已创建了分支：

```bash
git branch
```

```text
## * master
## my-new-feature
```

我们可以使用 git checkout 加上分支名称使 my-new-feature 成为当前分支：

```bash
git checkout my-new-feature
```

```text
## Switched to branch 'my-new-feature'
```

```bash
git branch
```

```text
##   master
## * my-new-feature
```

如果我们查看 git status，我们也可以看到它会告诉我们我们所在的分支：

```bash
git status
```

```text
On branch my-new-feature
nothing to commit, working tree clean
```

我们可以使用 git checkout 切换回 master 分支：

```bash
git checkout master
```

```text
## Switched to branch 'master'
```

```bash
git branch
```

```text
## * master
##   my-new-feature
```

现在我们可以通过使用 -d 标志与 git branch 以及我们想要删除的分支的名称来删除分支：

```bash
git branch -d my-new-feature
```

```text
## Deleted branch my-new-feature (was adef548).
```

```bash
git branch
```

```text
## * master
```

让我们为 readme.txt 创建一个新的分支以添加一个部分。我们可以使用命令 `git checkout -b` 同时创建新分支并切换到该分支，并指定我们想要创建的新分支的名称：

```bash
git checkout -b update-readme
```

```text
## Switched to a new branch 'update-readme'
```

现在我们已经创建并切换到新分支，让我们对文件进行一些更改。正如你可能预期的那样，现在我们将在 readme.txt 中添加一行新内容：

```bash
echo "I added this line in the update-readme branch." >> readme.txt
cat readme.txt
```

```text
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
```

现在我们添加了一行新内容，让我们提交这些更改：

