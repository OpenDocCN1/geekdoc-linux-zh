
* [new] main -> origin/main

$

如果下载项目文件的人在本地仓库中某个脚本的修改版本尚未上传到远程仓库，`git pull`命令将失败并保护该脚本。然而，错误消息将指示如何解决此问题。

> 警告
注意如果任何人想要最新的脚本版本但没有参与项目，他们在尝试执行`git remote`命令时会收到类似`fatal: not a git repository`的错误消息。他们他们是克隆项目，将介绍。

新团队成员可以使用`git clone`命令从远程仓库克隆整个脚本项目到他们的本地系统：

```
$ whoami

tim

$ ls

$ git clone https://github.com/Cresnahan/MWGuard

Cloning into 'MWGuard'...

remote: Enumerating objects: 6, done.

remote: Counting objects: 100% (6), done.

remote: Compressing objects: 100% (4/4), done.

remote: Total 6 (delta 0), reused 6 (delta 0), pack-used 0

Unpacking objects: 100% (6/6), 584 bytes | 0.00 KiB/s, done.

$ ls

MWGuard

$ cd MWGuard/

$ ls -a
```

.. .git MyGitExampleScript.sh README.md

```
$ git log

commit [...] (HEAD -> main, origin/main, origin/HEAD)

Author: Christine Breshnahan <cbres123@gmail.com>

Date: Mon Aug 24 15:58:52 2020 -0400
```

```
README.md

commit 3b4b6388c63e9d10a1b81694cba8c5f4bcce6

Author: Christine Bresnahan <cbres123@gmail.com>

Date: Mon Aug 24 14:56:56 2020 -0400
```
