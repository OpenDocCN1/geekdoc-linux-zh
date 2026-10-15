

## 17.5.7.5 对象存储的内容

现在我们已经说明了工作目录的结构、提交如何暂存，以及如 DAG 所示的仓库的总体布局，我们现在可以更细致地查看对象存储中包含的对象。图 17.10 显示了在对象存储中发现的四种对象类型以及这些对象之间的关系。

请记住图 17.9 中所示的 DAG，时间从左到右流动，箭头从子节点指向父节点。从顶部开始，我们看到右侧代表分支名称的矩形，以及代表标签对象的另一个较小的正方形。名称默认为 master，但可以分配更有意义的文本。标签是一个简写标签，可能代表初始发布号或软件代码的版本。圆圈代表提交。因此该图显示了两个提交。三角形代表树对象，可以将其视为目录或提交与 blob 之间的链接信息。最后，在底部有一系列 blob，显示链接到指向它们的树。

在下一节中，我们讨论几个涉及 Git 和 GitHub 的示例。在讨论这些示例之前，我们先简要介绍一下 git 命令。

### SYNTAX

```
git [options] [option arguments] <command> [<command arguments>]
```

Purpose: A distributed version control system with a rich command set that tracks the content of changes in source code files

### Commonly used commands and command arguments:

| add <file> | Stage a file to the index |
| commit | Take a snapshot of the working tree |
| config --global username "<name>" | Configure a repository global username |
| log --oneline | Display a short log of commits on the current branch |
| init | Initialize a repository in the current directory |
| status | Display the status of a repository |

![](img/02e070097d401d3bf7de4bf1c470b267_756_0.png)

## 17.5.7.6 使用 Git 和 GitHub 的示例

我们展示几个说明如何使用 Git 和 GitHub 的示例。每个示例都包括以下内容：

- 1. 示例中涵盖的主题
- 2. 示例的目标
- 3. 理解示例的介绍性材料
- 4. 示例中使用的 Git 命令
- 5. 执行示例的前提条件
- 6. 详细步骤
- 7. 结论

### Example 17.1: A Short Introduction to Git

Objectives: To briefly illustrate the Git staging model, and how to see differences between the various states of the parts of the repository.

Introduction: As shown previously, the workflow in Git basically follows a pattern of add, edit, modify, stage, and commit. This is the staging model. In this example, we show the essential Git commands that allow you to do that, repetitively if necessary. As you do more commits you add, in a linear fashion, more nodes on the branch named master downstream, after you create the first node in this example. Earlier commits are called upstream commits. The history of the repository flows downstream from the initial commit to the latest commit. Similar to the UNIX diff command, the four basic forms of the git diff command allow you to examine and compare the files and directories present during different states of the repository.

Git commands referenced: Table 17.1 shows the Git commands, and a brief description of each, that are used in this example. It is arranged in the order presented. Any argument enclosed in < > is a string of text. In order to get a more complete description of all the commands in the table, you can look at the man page for a particular command. For example, man git-status gives you a complete man page for the git status command.

Prerequisites: The following are the prerequisites for carrying out this example:

- 1. Having Git installed on your PC-BSD or Solaris system
- 2. Reading through and doing the in-chapter exercises shown in the previous subsections

Procedure: Do the following steps, in order, to meet the objectives of this example.

- 1. Create a working directory within which your Git repository will exist, and make that the current working directory.

```
% mkdir short-git
```
