
> 您可以使用 Markdown 语言的各种功能，让您的 `README.md` 文件变得非常复杂。请访问 [guides.github.com/features/mastering-markdown](https://guides.github.com/features/mastering-markdown) 以了解有关 Markdown 的更多信息。

您可以随时审查 Git 日志，但在将脚本项目推送到远程仓库之前执行此操作总是个好主意。每个提交都会被分配一个哈希号以进行识别，并在日志中显示。此外，请注意各种注释行以及日期和作者信息。

```
$ git log
commit 898330bd0b01e0b6eee507c5eeb3c72f9544f506[ ... ]
Author: Christine Bresnahan <cbresn1723@gmail.com>
Date: Mon Aug 24 15:58:52 2020 -0400

      README.md commit

commit 3b484638bc6e391d0a1b816946cba8c5f4bbc8e6
Author: Christine Bresnahan <cbresn1723@gmail.com>
Date: Mon Aug 24 15:46:56 2020 -0400

      Initial Commit
$
```

在将项目推送到远程仓库之前，您需要在系统中配置其地址。当您使用 Git 服务提供商（如 GitHub）设置远程仓库时，会提供此地址。

要添加地址，请使用 `git remote add origin URL` 命令，其中 `URL` 是远程仓库的地址：

```
$ git remote add origin https://github.com/C-Bresnahan/MWGuard.git
$
$ git remote -v
origin	https://github.com/C-Bresnahan/MWGuard.git (fetch)
origin	https://github.com/C-Bresnahan/MWGuard.git (push)
$
```

请注意，我们通过 `git remote -v` 命令检查了远程地址的状态。在推送项目之前检查地址是个好主意。如果地址错误或存在拼写错误，推送将不起作用。因此，请仔细检查所有内容！

> **提示**
>
> 如果在地址中犯了错误（例如拼写错误），您可以通过 `git remote rm origin` 命令删除远程仓库的地址。删除后，使用正确的地址重新设置远程地址。

配置远程仓库地址后，我们可以将脚本项目推送到其位置。但是，在此之前，为了简化操作，我们将使用 `git branch` 命令将主分支重命名为 `main`：

```
$ git branch -m main
$
$ git branch --show-current
main
$
```

请注意，您可以使用 `git branch --show-current` 命令查看当前分支名称。在推送之前执行此操作是个好主意，以确保您拥有正确的分支名称，这是推送命令所需的。

现在，要将我们的脚本复制到远程仓库，我们需要在 `push` 命令后附加 `-u origin` 选项以指示仓库位置，以及我们当前使用的分支名称 `main`。

```
$ git push -u origin main
Username for 'https://github.com': C-Bresnahan
Password for 'https://C-Bresnahan@github.com':
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 604 bytes | 60.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To https://github.com/C-Bresnahan/MWGuard.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from
'origin'.
$
```

通常，远程仓库会要求输入用户名和密码。当项目被推送到远程仓库后，你应该能够使用你喜欢的 Web 浏览器查看它。如果它是一个私有仓库，你必须登录到远程仓库服务才能看到你的工作成果。

**图 25-2** 显示了该项目的 GitHub 远程仓库。请记住，不同的 Git 远程仓库提供商针对你的脚本项目会有不同的用户界面。

![](img/a5025f22e05b92f409563a958cac7312_937_0.png)

###### 图 25-2 MWGuard 远程仓库

远程仓库真正令人满意的一点是，你的 Linux 管理团队成员中任何正在参与该项目的人，都可以使用 `git pull` 命令拉取最新的脚本版本。你需要为他们在远程仓库中设置访问权限，或者将其设为公开仓库。

```
$ whoami
rich
$
$ pwd
/home/rich/MWGuard
$
$ git remote add origin https://github.com/C-Bresnahan/MWGuard.git
$
$ git pull origin main
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), 584 bytes | 58.00 KiB/s, done.
From https://github.com/C-Bresnahan/MWGuard
 * branch main -> FETCH_HEAD
 * [new branch] main -> origin/main
$
```

如果拉取项目文件的用户在其本地仓库中已经拥有某个脚本的修改版本，并且该版本尚未上传到远程仓库，那么 `git pull` 命令将失败，从而保护该脚本。不过，错误信息会说明如何修复此问题。

> **警告**
>
> 请记住，如果有人想要获取最新的脚本版本，而此前他们并未参与该项目，那么当他们尝试执行 `git remote add origin` 命令时，会遇到类似于 `fatal: not a git repository` 的错误信息。最好让他们克隆该项目，这在下一部分中会进行介绍。

新加入开发团队的成员可以使用 `git clone` 命令从远程仓库将*整个*脚本项目复制到其本地系统：

```
$ whoami
tim
$
$ ls
$
$ git clone https://github.com/C-Bresnahan/MWGuard.git
Cloning into 'MWGuard'...
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), 584 bytes | 58.00 KiB/s, done.
$
$ ls
MWGuard
$
$ cd MWGuard/
$
$ ls -a
. .. .git MyGitExampleScript.sh README.md
$
$ git log
commit [..](HEAD -> main, origin/main, origin/HEAD)
Author: Christine Bresnahan <cbresn1723@gmail.com>
Date: Mon Aug 24 15:58:52 2020 -0400

    README.md commit

commit 3b484638bc6e391d0a1b816946cba8c5f4bbbc8e6
Author: Christine Bresnahan <cbresn1723@gmail.com>
Date: Mon Aug 24 15:46:56 2020 -0400

    Initial Commit

$
```

当项目从远程仓库克隆时，工作目录会自动创建，同时还会创建 `.git/` 目录、Git 暂存区（索引）以及本地仓库。`git log` 命令显示了项目的历史记录。这是新团队成员获取开始该项目工作所需一切内容的便捷方式。
