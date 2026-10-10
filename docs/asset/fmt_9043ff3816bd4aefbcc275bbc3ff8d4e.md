
### 列表 27.13：通过 `git pull` 命令从远程仓库拉取最新项目文件

```
$ whoami
Rich
$
git remote add origin https://github.com/C-Bresnahan/MWGuard.git
$
git pull -u origin master
```

远程仓库非常棒的一点是，你的项目团队可以使用 `git pull` 命令下载项目的最新文件。你需要为他们设置远程仓库的访问权限，或者将其公开。拉取文件的代码片段示例见列表 27.13。

### 列表 27.9：创建、添加和提交一个 `README.md` 文件（续）

```
$ git add README.md
$
git status
# On branch master
# Changes to be committed:
# (use "git reset HEAD<file>..." to unstage)
#
# new file: README.md
#
$ git commit -m "README.md commit"
[master 4541578] README.md commit
1 file changed, 2 insertions(+)
create mode 100644 README.md
$
```

你可以通过使用 Markdown 语言的各种功能让你的 `README.md` 文件变得非常精美。可以在 `guides.github.com/features/mastering-markdown/` 了解更多关于 Markdown 的信息。

你可以随时查看 Git 日志，在将项目推送到远程仓库之前查看日志总是个好主意。查看日志的示例见列表 27.10。每个 `commit` 都是一个用于标识它的哈希值，它显示在日志中。此外，注意日期旁不同的注释行以及作者信息。

### 列表 27.10：通过 `git log` 命令查看 Git 日志

```
$ git log
commit 4541578c17c213bac9c47ce815b91b6a9ac986
Author: Christine Bresnahan <cbres377@ivytech.edu>
Date: Fri 8 13:49:49 2019 -0500

README.md commit

commit 6d2370d2907345671123aeaaa7e147bd3f08f36
Author: Christine Bresnahan <cbres377@ivytech.edu>
Date: Wed Feb 6 15:23:11 2019 -0500

Initial Commit
$
```

## 使用 Git 提交

在将项目推送到远程仓库之前，你需要在系统上配置它的地址。这是通过 `remote add URL` 命令完成的，其中 `URL` 是远程仓库的地址。示例见列表 27.11。

### 列表 27.11：通过 `git remote` 命令配置远程仓库

```
$ git remote add origin https://github.com/C-Bresnahan/MWGuard.git
$ git remote -v
```
