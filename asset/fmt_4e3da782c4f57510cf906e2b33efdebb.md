
请注意，我们需要指定要推送到的远程，因为 GitHub 之前不知道`update-readme`分支的存在。当你执行`git push`时，只有当前分支上的提交会被发送到远程仓库。这样你就可以创建只能从本地访问的分支，除非你明确将其推送到 GitHub。

现在让我们回到我们仓库的 GitHub 页面。页面左侧你应该会看到一个写着“Branch: `master`”的按钮。点击该按钮，一个小下拉菜单应该会出现，如下所示：

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_202_0.png)

点击菜单中的“`update-readme`”，即可查看该分支中的文件。你会看到`README.md`文件是不同的！你可以通过这个菜单在分支之间来回切换查看。

现在你已经将更新后的分支推送到了 GitHub，让我们来开启一个拉取请求。拉取请求就像是由 GitHub 促成的有向导的 git 合并。要发起拉取请求，请点击分支按钮旁边的“New pull request”按钮（见上图左上角）。该按钮会将你带到一个类似这样的页面：

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_203_0.png)

这个页面上有几个重要的细节，让我们逐一了解。首先，在“Open a pull request”标题下方，你可以看到两个分支的名称。“base:”后面的分支名称显示的是更改将要合并到的分支（本例中为`master`分支），而“compare:”后面的分支名称显示的是包含更改的分支（本例中为`update-readme`分支）。

在下面的文本框中，你可以为拉取请求编写标题（本例中的默认标题是最后一次提交的名称），并且可以编写关于拉取请求的评论，这些评论可以用 Markdown 格式化。如果你正在与其他人协作一个项目，编写良好的评论非常重要，这样你的协作者就能知道你在请求合并的分支中做了哪些更改。如果你向下滚动页面，可以看到“compare”分支与“base”分支之间更改的逐行比较。当你完成对这些更改的检查后，点击绿色的“Create pull request”按钮来开启拉取请求。现在你应该会看到这样一个屏幕：

![](img/a67f2d2ba01c2569ec78ab34ae6c3c5a_204_0.png)

恭喜你开启了第一个拉取请求！让我们来看看这个页面上有什么。在拉取请求标题下方，我们可以看到三个选项卡：Conversation、Commits 和 Files changed。在 Conversation 选项卡中，我们可以添加可以用 Markdown 格式化的拉取请求评论。Commits 选项卡列出了在此拉取请求中已提交到“compare”分支的提交。最后，Files changed 选项卡显示了我们之前看到的相同的逐行比较。

通常，当你与协作者一起工作时，在开启拉取请求之后会有大量的讨论。即使请求已经开启，推送到 GitHub 仓库“compare”分支（本例中为`update-readme`）的 git 提交也会反映在拉取请求中。这样，因讨论而产生的更改就可以轻松地被纳入。当你准备好后，返回 **Conversation** 选项卡，点击绿色的“Merge pull request”按钮，然后点击出现的绿色“Confirm merge”按钮。这将把“compare”分支 git 合并到远程仓库中的“base”分支。你刚刚合并了你的第一个拉取请求！现在点击页面左上角附近的 `<> Code` 选项卡，你应该会看到`update-readme`分支的更改已经合并到`master`中了。

当你在一个有许多其他人的远程 GitHub 仓库上工作时，如果提交影响到的代码部分不是你在处理的，这些拉取请求和合并完全可以在你不知情的情况下发生。尽管如此，保持你的本地仓库与远程仓库的最新更改同步仍然很重要。让我们回到你的终端，当前工作目录应该是`my-first-repo`。首先，让我们切换到`master`分支。

```
git checkout master
```

现在，让我们用已合并到远程`master`分支的提交来更新本地的`master`分支。repository. 我们可以使用命令`git pull`来完成此操作：

```
git pull
```

```
## remote: Counting objects: 1, done.
## remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
## Unpacking objects: 100% (1/1), done.
## From https://github.com/seankross/my-first-repo
##  2169912..b9217f6  master  -> origin/master
## Updating 2169912..b9217f6
## Fast-forward
## README.md | 38 +++++++++++++++++++++++++++++++-------
## file1.txt | 0
## file2.txt | 0
## 3 files changed, 18 insertions(+), 20 deletions(-)
## delete mode 100644 file1.txt
## delete mode 100644 file2.txt
```
