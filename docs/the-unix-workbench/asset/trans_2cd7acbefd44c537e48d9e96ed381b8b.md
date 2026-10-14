

```
git add -A
git commit -m "added a third line to readme.txt"
```

```
## [update-readme 6e378a9] added a third line to \
readme.txt
## 1 file changed, 1 insertion(+)
```

现在我们在 update-readme 分支上完成了一次提交，让我们切回 master 分支，然后再来看一下 readme.txt：

```
git checkout master
```

```
## Switched to branch 'master'
```

现在我们在 master 分支上，让我们快速查看一下 readme.txt：

```
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
```

我们添加的第三行不见了！不用担心，我们添加的那一行并没有永远消失。我们是在 update-readme 分支上对该文件进行了提交，所以更新后的文件安全地保存在那个分支中。让我们切回该分支以确认一下：

```
```bash
git checkout update-readme
cat readme.txt
```
```

```
```text
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
```
```

第三行回来了！让我们在当前分支上再添加并提交一行：

```
```bash
echo "It's sunny outside today." >> readme.txt
git add -A
git commit -m "added weather info"
```
```

```
```text
## [update-readme d7946e9] added weather info
##  1 file changed, 1 insertion(+)
```
```

这是一个使用 Git 分支的小例子，但你可以看到如何对纯文本（通常是代码文件）进行增量编辑，而不会影响 master 分支（你软件的经过测试且可用的版本）也不会影响其他分支。你可以想象这个系统如何被用于多个人同时在同一代码库上工作，或者如何开发和测试多个软件功能而互不干扰。现在我们已经对 readme.txt 做了几次更改，让我们将这些更改与 master 分支中的内容合并。这可以通过 Git 合并来实现。合并允许你优雅地组合两个分支之间所做的更改。让我们合并

update-readme 分支中我们所做的更改与 master 分支。Git 默认会将其他分支合并到当前分支中。合并时，当前分支也称为基分支。让我们切换到 master 分支，以便我们可以合并来自 update-readme 分支的更改：

```
git checkout master
```

```
## Switched to branch 'master'
```

要合并来自另一个分支的更改，我们需要使用 git merge 和分支名称：

```
git merge update-readme
```

```
## Updating adef548..d7946e9
## Fast-forward
## readme.txt | 2 ++
## 1 file changed, 2 insertions(+)
```

```
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It's sunny outside today.
```

看起来你已经在 Git 中完成了第一次分支合并！分支是 Git 如此强大的原因之一，因为它使在同一代码库上进行并行开发成为可能。但如果两个分支中的两个提交对同一行文本做了不同的编辑会怎样？当这种情况发生时，就称为冲突。让我们创建一个冲突，以便学习如何解决它们。

首先我们将切换到 update-readme 分支。使用 nano 编辑 readme.txt 的最后一行，然后提交你的更改：

```
git checkout update-readme
nano readme.txt
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It's cloudy outside today.
```

注意我们将最后一行的“sunny”改成了“cloudy”。

```
git add -A
git commit -m "changed sunny to cloudy"
```

现在我们在 update-readme 分支上提交了更改，让我们切回 master：

```
git checkout master
```

让我们使用 nano 修改同一行代码：

```
nano readme.txt
```

```
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It’s windy outside today.
```

现在让我们提交这些更改：

```
git add -A
```

```
git commit -m "changed sunny to windy"
```

我们现在创建了两个直接冲突的提交。在 update-readme 分支上，最后一行是 It’s cloudy outside today.，而在 master 分支上，最后一行是 It’s windy outside today.。让我们看看当我们尝试将 update-readme 合并到 master 时会发生什么。

```
git merge update-readme
```

