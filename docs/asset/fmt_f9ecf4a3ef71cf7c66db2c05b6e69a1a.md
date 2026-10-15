
### 53. 使模块分支为当前分支。
```
% git checkout modules
Switched to branch 'modules'
%
```

### 54. 在你喜欢的文本编辑器中，创建一个名为 `module1.c` 的 C 程序文件。然后暂存 `module1.c`。
```
% git add module1.c
%
```

### 55. 检查仓库的状态。
```
% git status
On branch modules
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        new file:   module1.c
%
```

### 56. 现在提交 `module1.c`。
```
% git commit -m "Added module1.c"
[modules 9b37c23] Added module1.c
 1 file changed, 1 insertion(+)
 create mode 100644 module1.c
%
```

### 57. 在你喜欢的文本编辑器中，在文件 `first.c`、`second.c` 和 `third.c` 中添加对 `module1.c` 中 C 代码的引用。

### 58. 暂存你在 `first.c`、`second.c` 和 `third.c` 中所做的更改。
```
% git add first.c second.c third.c
%
```

### 59. 检查项目仓库的状态。
```
% git status
On branch modules
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        modified:   first.c
        modified:   second.c
        modified:   third.c
%
```

### 60. 提交对文件 `first.c`、`second.c` 和 `third.c` 的更改。
```
% git commit -m "Add references to module1.c"
[modules 436a966] Add references to module1.c
 3 files changed, 3 insertions(+)
%
```

### 61. 现在检查此分支上的提交历史。
```
% git log --oneline
436a966 Add references to module1.c
9b37c23 Added module1.c
03ece49 Revert "Add an experimental C program"
1707e3e Add an experimental C program
b0a6b40 Revised all three files
4ea0534 second.c and third.c added
74088f6 The initial commit
%
```
此时项目仓库的 DAG 如图 17.13 所示。

### 62. 为合并 `modules` 分支与 `master` 分支做准备，请执行以下操作。首先，切换到 `master` 分支，然后检查工作目录中的文件。最后查看沿 `master` 分支所见的仓库提交历史。
```
% git checkout master
Switched to branch 'master'
% ls
first.c second.c third.c
% git log --oneline
03ece49 Revert "Add an experimental C program"
1707e3e Add an experimental C program
b0a6b40 Revised all three files
4ea0534 second.c and third.c added
74088f6 The initial commit
%
```

### 63. 我们现在将 `modules` 分支与 `master` 分支合并。此命令始终合并到当前分支。`modules` 分支保持不变。使用 `git log --oneline` 检查历史记录，以确保 `modules` 的提交历史已添加到 `master` 的提交历史中。表示仓库最终状态的 DAG 如图 17.14 所示。
```
% git merge modules
Updating 03ece49..436a966
```

![](img/02e070097d401d3bf7de4bf1c470b267_778_0.png)

![](img/02e070097d401d3bf7de4bf1c470b267_779_0.png)

FIGURE 17.14  DAG of final state of project repository.

Fast-forward
    first.c   | 1 +
    module1.c | 1 +
    second.c  | 1 +
    third.c   | 1 +
    4 files changed, 4 insertions(+)
    create mode 100644 module1.c
```
```
% git log --oneline
436a966 Add references to module1.c
9b37c23 Added module1.c
03ece49 Revert "Add an experimental C program"
1707e3e Add an experimental C program
b0a6b40 Revised all three files
4ea0534 second.c and third.c added
74088f6 The initial commit
%
```

**结论：** 在本示例中，我们使用文本编辑器在包含 Git 仓库的目录中按需创建了 C 源代码文件。然后我们编辑这些文件以更改其内容并提交这些更改。最后，我们展示了如何创建分支以沿不同分支进行源代码的不同开发路线，以及如何合并不同分支。我们在整个示例中强调了暂存模型，或编辑-暂存-提交工作流模型，如上一节所述。

## EXERCISE 17.13
在什么情况下你会想在与 C 程序开发和构建过程相关的 Git 仓库中跟踪或暂存其他类型的文件？

## EXERCISE 17.14
如果在步骤 63 之后，你在工作目录中创建一个新的文本文件，但不暂存也不提交，在你执行 `checkout` 到初始提交之后，该文件是否仍在工作目录中？为什么/为什么不？

## 17.5.7.7 GitHub 作为远程仓库

GitHub 是一个流行的远程仓库，您可以在其中轻松、安全地与团队协作进行软件项目的开发和维护。我们首先提供有关 Git URL 和 refspec 的一些背景信息。然后，在本节的示例中，我们展示了如何使用 UNIX 命令行将文件从本地仓库传输到 GitHub 仓库的基础知识。我们还展示了如何从 GitHub 获取文件并将其检索回本地仓库。这些操作的基础和准备工作在 UNIX 命令行上通过我们迄今为止所展示的 Git 命令来加速。因此，完成前面关于 Git 的小节对于理解此处所示的 GitHub 交互是必要的。我们还引入了新的 Git 命令，以便您能够与 GitHub 远程仓库协作。

我们没有展示如何在 GitHub 上获取账户，或如何使用 GitHub 的基于 Web 的 GUI 界面创建新仓库。假设在所有示例中，您都可以通过 Web 浏览器在 `www.github.com` 上完成这两个基本步骤，并且可以导航到我们显示的 URL。您系统上的仓库称为本地或当前仓库，而像 GitHub 这样的仓库称为远程仓库。

使用 `git remote` 命令及其选项和参数来创建、删除、操作和查看远程仓库。例如，要向当前本地仓库添加远程引用规范，或 refspec，请使用 `git remote add` 命令及其选项和参数。您也可以查看 `.git/config` 文件中已定义为远程的内容。您添加的所有远程仓库都记录在 `.git/config` 文件中，可以使用 `git config` 及其选项和参数进行操作。

引用远程仓库的基本 Git 命令是

| `git clone` | 将远程仓库传输到本地仓库 |
| `git fetch` | 从远程仓库检索对象及其相关数据结构 |
| `git pull` | 将远程仓库中的更改合并到对应的本地分支 |
| `git push` | 将对象及其相关数据结构复制到远程仓库 |
| `git ls-remote` | 列出给定远程仓库中的引用 |

### 17.5.7.7.1 Git URL

对于 `git remote` 命令，Git 将对远程仓库的引用参数形式命名为统一资源定位符（URLs）。引用本地文件系统上仓库的 Git URL 可以是：
```
/pathname/repo.git
file:///pathname/repo.git
```
