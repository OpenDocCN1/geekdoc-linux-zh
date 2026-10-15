
如果你已经习惯阅读 `git status` 的结果，你会发现它经常会给出下一步应该采取的建议。Git 表明 `readme.txt` 的两个版本都修改了相同的文本。让我们查看 `readme.txt` 看看发生了什么：

```
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## <<<<<<< HEAD
## It's windy outside today.
## =======
## It's cloudy outside today.
## >>>>>>> update-readme
```

这个文件的前三行看起来正常，然后事情变得有趣了！位于 `<<<<<<< HEAD` 和 `=======` 之间的行显示了当前分支上冲突行的版本。在 Git 术语中，`HEAD` 代表当前检出的分支上最近的提交（在本例中是 `master`）。位于 `=======` 和 `>>>>>>> update-readme` 之间的行显示了 `update-readme` 分支上该行的版本。为了解决这个冲突，我们只需要用 `nano` 打开 `readme.txt` 就可以删除我们想要去掉的行。在本例中让我们保留 “cloudy” 版本。

```
nano readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It's cloudy outside today.
```

现在我们可以提交这次冲突的解决。

```bash
git add -A
git commit -m "resolved conflict"
```

你现在已经熟悉了 Git 的基础知识！如果你想更深入地学习 Git，我强烈推荐免费的开源书籍 Pro Git²¹。

# Summary

+   - Git 分支允许你和其他人一起在同一个代码库上工作。
+   - 你可以用命令 `git branch [name of branch]` 创建一个分支。
+   - 要切换到一个分支请使用 `git checkout [name of branch]`。
+   - 你可以通过使用 `git merge` 将一个分支合并到你的当前分支。

# Exercises

+   1. 开始一个新的分支。
+   2. 切换到该分支并向其添加提交。切换到一个较旧的分支然后将新分支合并到你的当前分支。
+   3. 有意地创建并解决一个合并冲突。

# Quick setup — If you’ve done this kind of thing before

我们建议每个仓库都包含 `README`、`LICENSE` 和 `.gitignore`。

# ...or create a new repository on the command line

```
echo "# my-first-repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/seanross/my-first-repo.git
git push -u origin master
```

# ...or push an existing repository from the command line

```
git remote add origin https://github.com/seanross/my-first-repo.git
git push -u origin master
```

# ...or import code from another repository

你可以用 Subversion、Mercurial 或 TFS 项目的代码来初始化此仓库。

GitHub 对我们新的远程仓库该做什么提供了一些建议。我们已经在使用本地 Git 仓库，而 GitHub 提供的是远程 Git 仓库。远程 Git 仓库只是一个存储在始终打开并连接到互联网的计算机上的 Git 仓库，因此它可以作为一个中心点，让我们可以与朋友和同事共享和同步对文件的更改。我们可以用 `git remote` 命令查看本地仓库连接了哪些远程仓库，同时将工作目录设置为 `my-first-repo`：

```
git remote
```

由于你还没有设置任何远程，所以控制台不会打印任何内容！现在让我们在本地仓库中将你的新 GitHub 仓库添加为远程：

在上述命令中，`git remote add` 在你的本地仓库中添加了一个新的远程仓库，`origin` 是我们给这个远程仓库分配的名称，`https://github.com/seankross/my-first-repo.git` 是远程仓库的 URL。你当然应该将 `seankross` 替换为你自己的 GitHub 用户名，以便与你自己的远程仓库 URL 对应。稍后我会解释为什么我们选择“origin”作为这个远程仓库的名称。让我们再次运行 `git remote` 来确认我们已经成功添加了 `origin` 远程仓库：

```
git remote
```

```
origin
```

既然已经添加了 GitHub 远程仓库，现在让我们执行第一次 Git push。`Git push` 会用我们本地 Git 仓库中所有的提交来更新远程仓库。在 GitHub 上设置远程仓库时，你执行的第一次 Git push 与以后的 Git push 略有不同。我们需要使用 `-u` 标志来将 `origin` 设置为默认的远程仓库，这样我们就不必在每次想要与它交互时都提供它的名称。请输入以下命令，并修改为你的 GitHub 用户名：

```
git push -u origin master
```

```
Counting objects: 23, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (19/19), done.
Writing objects: 100% (23/23), 1.88 KiB | 0 bytes/s, done.
Total 23 (delta 9), reused 0 (delta 0)
remote: Resolving deltas: 100% (9/9), done.
To https://github.com/seankross/my-first-repo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

上述命令将我们的所有提交推送到了 GitHub 上的远程仓库，并将 `origin` 远程仓库的 `master` 分支设置为默认的远程仓库。回到你在 GitHub 上的仓库页面，它应该看起来像这样：

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_193_0.png)

GitHub 的一个巧妙功能是，`readme` 文件会渲染在仓库页面上，因此你可以编写文档来说明仓库的内容。让我们通过学习一种叫做 Markdown 的小语言，来更有创意地编写这些 readme 文档。

# Markdown

Markdown 是一种标记语言。标记语言是用于为文本添加装饰性功能的规则集合。最流行的标记语言是 HTML，但你可能也听说过 XML 和 LaTeX。Markdown 是一种强大的标记语言，因为它简洁、直观，并且以纯文本形式书写时具有很好的可读性。GitHub 会将 Markdown 文件（以 `.md` 文件扩展名结尾）转换为仓库中简单的 HTML 网页。如果你的仓库中任何文件夹里有一个名为 `README.md` 的文件，那么该文件会被渲染为 HTML 并显示在 GitHub 上。让我们创建一个包含代码的 `README.md` 文件：

```
Here is how you make [a link](https://www.wikipedia.org/).

![This is an image. ](https://github.com/yihui/xaringan/releases/download/v0.0.2/karl-moustache.jpg)

nano README.md

Now let’s add our changes, make a commit, and push those changes to our remote repository:
```

```
git add -A
git commit -m "added README.md"
git push
```
