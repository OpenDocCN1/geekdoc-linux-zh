
- 20.3. 开始项目 ................................................................ 227
- 20.4. `git` 分支 ........................................................................ 230
- 20.5. 待续............................................................................... 231
- 20.6. `github.com` ............................................................................ 232
- 20.7. 将你的公钥添加到 `github` ................................................ 232
- 20.8. 练习：`git` ............................................................................ 233

# 第 20 章. `git`

本章介绍了如何在命令行中使用 `git`。`git` 仓库由 `github` 托管，但你可以自由选择其他服务器（或创建自己的服务器）。

有很多优秀的 `git` 在线教程。这个列表可以节省你一次 Google 搜索的时间：

```
http://gitimmersion.com/
http://git-scm.com/book
```

## 20.1. `git`

`Linus Torvalds` 在 2005 年创建了 `git`，当时 `Bitkeeper` 更改了许可证，`Linux` 内核开发者不再能够免费使用它了。

`git` 迅速流行起来，现在是世界上使用最广泛的分布式版本控制系统。

`Geek and Poke` 展示了为什么我们需要版本控制（`Geek and Poke 3.0` 的特性）。

![](img/d499a6177836f6f088a9e2a53114.png)

除了软件源代码，你还可以在 `github` 上找到它（当你读到这里时，可能会有更多）。

## 20.2. 安装 `git`

我们在 `Debian` 上安装 `git`，如截图所示：

```
root@debian64 ~]# aptitude install git
The following NEW packages will be installed:
git libcurl libperl
0 个软件包已升级，3 个新安装，0 个待删除。
Setting up libcurl...
Setting up libperl...
Setting up git...
```

## 20.3. 开始项目

我们创建一个包含简单文件的项目目录：

```
paul@debian64 ~]# mkdir project
paul@debian64 ~]# cd project
paul@debian64 ~]# echo "The answer is." > question.sh
```

然后我们在该目录下创建一个空的 `git` 仓库。

```
paul@debian64 ~]# git init
paul@debian64 ~]# ls -la
total 4
drwxr-xr-x 2 paul paul 4096 Oct 24 10:00 ..
rw-r--r-- 1 paul paul 12 Oct 24 10:00 question.sh
drwxr-xr-x 3 paul paul 4096 Oct 24 10:00 .git
```

### 20.3.2. 配置

接下来使用 `git config` 设置一些全局选项。

```
paul@debian64 ~]# git config --global user.name Paul
paul@debian64 ~]# git config --global user.email "paulbaud@gmail.com"
paul@debian64 ~]# git config --global core.editor vi
```

我们可以验证此配置，查看文件 `~/.gitconfig`：

```
paul@debian64 ~]# cat ~/.gitconfig
[user]
name = Paul
email = paulbaud@gmail.com
[core]
editor = vi
```

### 20.3.3. add

现在是时候用 `git add` 添加文件，并用 `git status` 验证其是否已添加。

```
paul@debian64 ~]# git add question.sh
paul@debian64 ~]# git status
# 在分支 master
# 待提交的更改：
# 使用 "git rm --cached <file>..." 来取消暂存
# 新文件: question.sh
```

`git status` 告诉我们有一个新文件准备提交。

### 20.3.4. commit

通过 `git commit`，你强制 `git` 永久记录所有已添加的文件（以及这些文件的所有更改）。

```
paul@debian64 ~]# git commit -m "starting a project"
[master 5c1768b] starting a project
1 个文件改变，1 次插入(+)
create mode 100644 question.sh
paul@debian64 ~]# git status
# 在分支 master
无可提交的（工作区干净）
```

### 20.3.5. 修改已提交的文件

下面的截图显示了几个步骤。首先，我们更改一个文件：

```
paul@debian64 ~]# git status
# 在分支 master
无可提交的（工作区干净）
paul@debian64 ~]# vi question.sh
```

然后我们验证状态并看到它被修改了：

```
paul@debian64 ~]# git status
# 在分支 master
# 未暂存到提交的更改：
# (使用 "git add <file>..." 来暂存更新)
#       修改: question.sh
```

*(注：修正上方显示错误)*

```
paul@debian64 ~]# git status
# 在分支 master
# 未暂存到提交的更改：
# (使用 "git add <file>..." 来暂存更新)
#       修改: question.sh
```

使用 `git add` 暂存更改，然后使用 `git commit` 提交。

接下来我们将其添加到仓库。

```
paul@debian64 ~]# git add question.sh
paul@debian64 ~]# git commit -m "adding a she-bang"
[master 8b6b3] adding a she-bang
1 个文件改变，1 次插入(+)
paul@debian64 ~]# git status
# 在分支 master
无可提交的（工作区干净）
```

## 20.4. `git` 分支

可以在一个或多个 `git` 分支上进行项目工作。在这里我们创建一个新分支来对脚本进行修改。当我们确定脚本工作正常时，将此分支合并到主分支。（在练习时添加 `git status` 命令会很有用）。

```
$ paul@debian6~/project42$ git branch
* master
$ paul@debian6~/project42$ git checkout -b newcomer
Switched to a new branch 'newcomer'
$ paul@debian6~/project42$ vi questionext.sh
$ paul@debian6~/project42$ git add questionext.sh
$ paul@debian6~/project42$ source questionext.sh
The answer is 42.
```

看起来工作工作正常，所以我们在这个分支中进行提交。

```
$ paul@debian6~/project42$ git commit -m "adding a new company header"
[newcomer 730a2bb] adding a new company header
1 file changed, 4 insertions(+)
$ paul@debian6~/project42$ git branch
* newcomer
$ paul@debian6~/project2$ cat questionext.sh
#!/bin/bash
```

> # copyright linux-training.be

echo The answer is 42.

让我们回到主分支，看看那里发生了什么。
