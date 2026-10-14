

- 你可以使用 `git commit -m "message about changes since the last commit"` 来创建一个关于文件状态的里程碑。
- 要检查仓库中文件的状态，请使用 `git status`。

## 练习

1. 在新目录中启动一个仓库。
2. 在你的新 Git 仓库中创建一个新文件。确保 Git 正在跟踪该文件，然后创建一个新的提交。
3. 对文件进行更改，然后提交这些更改。
4. 向你的仓库添加两个新文件，但只提交其中一个。提交后你的仓库状态是什么？
5. 撤销上一次提交，添加未跟踪的文件，然后重新提交。

## 重要 Git 功能

### 获取帮助、日志和差异

Git 命令有自己的手册页。你可以使用 `git help [name of command]` 访问它们。例如，这里是 `git status` 帮助页的开头：

```
git help status
```

```
commit 12bb9f53b10c9b720dac8441e8624370e4e071b6
Author: seankross <sean@seankross.com>
Date:   Fri Apr 21 15:23:59 2017 -0400

    added two files

commit 7e53caae75301ce9b2821e1b195447241bbd17a
Author: seankross <sean@seankross.com>
Date:   Thu Apr 20 14:15:26 2017 -0400

    added readme.txt
```

如果你对一个仓库做了很多提交，你可能需要按 Q 键才能返回到提示符。每个提交都记录了其时间、日期和提交信息，以及唯一标识该提交的 SHA-1 哈希值。

Git 还可以帮助显示未暂存的更改与上一次提交之间的差异。让我们在 readme.txt 中添加一行新文本：

```
echo "The third line." >> readme.txt
git diff readme.txt
```

```
diff --git a/readme.txt b/readme.txt
index b965f6a..a3db358 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,3 @@
 Welcome to My First Repo
 Learning Git is going well so far.
+I added a line.
```

正如你所见，添加的行旁边会出现一个加号。现在让我们在文本编辑器中打开此文件，以便我们可以删除第二行。

```
nano readme.txt
# Delete the second line
git diff readme.txt
```

```
diff --git a/readme.txt b/readme.txt
index b965f6a..e173fdf 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
 Welcome to My First Repo
-Learning Git is going well so far.
+I added a line.
```

我们删除的行旁边会出现一个减号。让我们看看此时目录的状态。

```
git status
```

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

如果你仔细阅读 `git status` 的结果，你会看到此时我们可以朝两个方向处理这个仓库。我们可以 `git add` 我们已更改的文件以跟踪这些更改，或者我们可以使用 `git checkout` 来删除我们对文件所做的所有更改，将其内容恢复到上一次提交时的状态。让我们删除我们的更改来看看这是如何工作的。

```
cat readme.txt
```

```
Welcome to My First Repo
I added a line.
```

```
git checkout readme.txt
cat readme.txt
```

```
Welcome to My First Repo
Learning Git is going well so far.
```

正如你所见，我们对 readme.txt 所做的更改已被撤销。

### 忽略文件

有时你可能有一些文件你永远不想让 Git 跟踪，例如作为运行代码的副产品生成的二进制文件（PDF 或图像），或密码或 API 密钥等机密信息。Git 仓库中的一个名为 `.gitignore` 的文件可以列出文件名和子文件夹的名称，或简单的正则表达式（`ls` 中可用的任何内容），以指定不应被跟踪的文件。`.gitignore` 文件的每一行都应指定一个不应由 Git 跟踪的文件或一组文件。让我们创建一个 `.gitignore` 文件以确保我们永远不会在此仓库中跟踪图像文件：

```
touch toby.jpg
git status
```

