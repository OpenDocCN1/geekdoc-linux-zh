
每一层都会覆盖前一层中的值，例如，`.git/config`中的值优先于`/etc/gitconfig`中的值。这些文件当然是纯 ASCII 文本，你可以通过手动编辑文件并插入正确的语法来设置值，但通常运行`git config`命令更容易。

首先，设置你的用户信息：

```
$ git config --global user.name "Homer Simpson"
$ git config --global user.email homer@thesimpsons.com
```

这些命令暗示了配置文件的基本结构。所有配置变量都指定为`section.variable`。在配置文件中，节名称被方括号包围。方括号也可以包含用引号括起来的子节名称。该语法变为`section.subsection.variable`。

为了更好地理解这一切是如何结合在一起的，执行`git config --list`，它会列出所有当前定义的配置变量。然后用编辑器打开`hello-world/.git/config`来查看这些值来自哪里。

Git 提供了一个帮助命令`git help`，它列出了所有命令。如果你执行`git help <command>`，你将获得`<command>`的 man 页面。执行`git help config`，最终你会看到一个 git 识别的配置变量列表。

## 图形化 git

Eclipse 支持 git 这一点可能并不令人惊讶。启动 Eclipse 并切换到 Git 透视图。项目资源管理器视图已被 Git 仓库视图取代。该视图的菜单栏上有图标，用于：

- 在视图中添加本地仓库
- 在视图中克隆仓库
- 在视图中创建新的 git 仓库

既然我们已经有`hello_world`仓库，让我们将其添加到 Eclipse 中。单击添加图标以显示图 16.11 的对话框。从`hello_world/`目录或任何父目录开始，单击搜索按钮。Eclipse 应该能找到`hello_world`仓库。选择该条目并单击确定。该仓库将被添加到 Git 仓库视图。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_255_0.png)

将仓库添加到 Eclipse。

展开 Git 仓库视图中的`hello_world`条目和各种子条目，以显示类似图 16.12 的内容。此处显示的对象的上下文菜单大致是你所期望的。如果你右键单击分支，可以创建新分支。当前检出的分支由勾选标记标识。右键单击其他分支名称以将其检出。

为了在 Eclipse 的上下文中管理`hello_world`，我们需要将其变成 Eclipse 项目。右键单击工作树条目并选择“复制路径到剪贴板”。严格来说，这不是一个 C/C++ 项目，所以我们将选择 文件 > 新建 > 项目，展开 General 并选择 Project。单击 Next 并给项目起个名字，“Hello World”是个不错的选择。取消勾选 Use default location，在位置框中右键单击并选择粘贴。然后单击 Finish。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_256_0.png)

**图 16.12**

Git 仓库视图。

对一个或多个文件进行更改。只需双击工作目录下的文件条目即可在编辑器中打开它们。然后右键单击已更改的条目以将它们添加到暂存区域。现在右键单击 hello-world 条目并选择 Commit。这将显示图 16.13 的对话框。Author 和 Committer 字段已为你填写，并且编辑器已打开以输入提交消息。

修改的文件列在 Author 和 Committer 条目下方。状态中的勾选标记表示文件已暂存。工具栏中有一个勾选标记图标，可以选择所有文件。注意，由于我们创建了一个 Eclipse 项目，工作目录中现在有一个 `.project` 文件。单击 Finish，提交即被保存。

## 创建新仓库

最终，这一切的目的是将你自己的项目纳入 git 控制。作为一个例子，让我们用我们之前书中使用过的一个 Eclipse 项目创建一个新仓库。比如网络项目怎么样？

![](img/f03d6fa2c5faefc793771df52bbb2ef9_257_0.png)

**图 16.13**

提交对话框。

要将现有的 Eclipse 项目放入 git 仓库，请在项目资源管理器中选择项目条目，右键单击并选择 Team > Share Project。这将显示图 16.14 的对话框。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_258_0.png)

**图 16.14**

配置 git 仓库对话框。

此时你很可能想创建一个新的仓库。问题是，放在哪里？你可以通过勾选“在项目父文件夹中创建或使用仓库”将仓库放在项目文件夹中。或者你可能想把它放在项目目录的父目录中，以便可以轻松地在同一个 git 仓库中管理所有项目。当你单击 Create 时，会出现一个对话框，要求输入路径和名称。名称最终将成为路径下的一个目录，该目录必须为空或不存在。`.git/`目录就存储在那里。当你单击 Finish 时，你的项目会被移动到仓库目录中。

回到项目资源管理器视图，网络条目现在显示 "[my_projects NO-HEAD]"。这表明该项目现在由 my_projects 仓库管理，但尚未进行初始提交。如果你右键单击并选择 Team，其中一个选项是 Commit，这将显示我们在图 16.13 中看到的提交对话框。选择所有文件，输入提交消息，并单击 Commit。

你仍然可以从 C/C++ 透视图完成大部分工作。Git 对开发过程的干扰并不大。当您需要做“git 风格”的事情，例如管理分支时，您需要切换到 Git 透视图。

这结束了我们关于使用 git 进行源代码控制的探索。在下一章也是最后一章中，我们将看看 Linux 和实时系统。

### 资源

- [http://git-scm.com](http://git-scm.com) - git 主页
- [http://git-scm.com/book](http://git-scm.com/book) -- Scott Chacon 的 *Pro Git*。这是一本可读性很强且完整的 git 入门书。整本书都可以在 git-scm 网站上以 HTML 格式阅读，或者你可以下载 PDF 版本。
- [http://en.wikipedia.org/wiki/Comparison_of_revision_control_software](http://en.wikipedia.org/wiki/Comparison_of_revision_control_software) -- 对包括 git 在内的约 30 个版本控制系统的非常好比较。
- [https://github.com](https://github.com) - 一个声称托管来自近 200 万人的 300 多个仓库的 git 托管服务。它对开源项目免费。私有仓库需支付每月订阅费。
- [http://git-scm.com/docs](http://git-scm.com/docs) -- 除此之外，你还可以找到一份紧凑的、方便使用的“git 速查表”PDF。
- [gitious.org](http://gitious.org) - 另一个 git 托管服务。这个服务似乎比 github 更有社区感。

## 章节大纲

- 硬实时与软实时
- 为什么 Linux 不是实时的
- 测量延迟：Cyclctest
- 改进 Linux 延迟
- 两种方法
- 抢占改进
- 中断抽象
- 第三种方式：Xenomai
- 使用 PREEMPT_RT
- 总结
- 资源

> 你可以给推土机贴上赛车条纹，但它并不会因此跑得更快。
> 维克多·尤代坦（Victor Yodaiten）

我们在第 1 章“嵌入式与实时空间”中简要回顾过实时编程的概念。让我重复一下我在那里引用的那句话：

> 实时系统是指计算的正确性不仅取决于计算逻辑的正确性，还取决于结果产生的时间。如果系统的时序约束未得到满足，则认为发生了系统故障。
> 唐纳德·吉尔斯（Donald Gillies）在《实时计算常见问题解答》中所述

换句话说，迟到的答案就是错误的答案。请记住，实时并不意味着真实得快，而是指快得足够，但更重要的是，可靠地快得足够。在实践中，这意味着我们可以为系统响应事件所需的时间设定一个上限。这被称为延迟（Latency）。

### 硬实时与软实时

实时系统可以分为硬实时或软实时。它们之间的主要区别在于错过调度截止时间点的后果。在硬实时中，调度截止时间必须每次都得到满足。错过截止时间意味着系统失败，可能会导致灾难性的后果。

硬实时的一个好例子是线传飞行控制系统（fly-by-wire），其中计算机介入飞行员与发动机及控制面之间。控制算法依赖于对空速、高度、爬升或下降速率等精确计时的样本。如果这些样本延迟，算法可能会变得不稳定，导致飞机坠毁。
