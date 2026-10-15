
首先，列出两个目录中的文件，以确保要链接的文件存在，并且目标目录中没有同名文件。这里，我们列出 `/home/deb/Projects/schedule` 和 `/home/helper` 中以 `our` 开头的文件。在此示例中，我们验证该文件确实存在于 Deb 的目录中，并且在 helper 的目录中未找到匹配文件（代码清单 2.14）。

- 2. `ln /home/deb/Projects/schedule/our.projects.latest /home/helper/our.projects`

这里，`ln` 在 helper 的主目录中创建一个名称相似的新文件并将两个文件链接在一起，本质上使同一个文件存在于两个主目录中。

- 3. `ls -l /home/helper/o*`

通过此代码，你的 helper 可以通过列出以 `o*` 开头的文件来验证文件是否存在。现在该文件在两个位置具有完全相同的内容。任何用户都可以修改文件，两个位置的内容都会发生变化。

## 提示

- 你可以像删除普通文件一样删除硬链接，使用 `rm` 加上文件名即可。参见本章中名为 使用 `rm` 删除文件 的部分。

- 如果一个用户删除了文件，另一个用户仍然可以从其目录访问该文件。

- 硬链接仅在同一文件系统内从文件到文件才有效。要链接目录或跨文件系统链接，你必须使用软链接，这将在下一节中介绍。

- 如果你想耍点小聪明，你可以使用硬链接来链接目录，而不仅仅是文件。在你想要链接目录的位置新建一个目录，然后使用 `ln /home/whoever/existingdirectory/* /home/you/newdirectory/` 来将旧目录中的所有文件硬链接到新目录。新文件不会自动链接，但你可以使用 `cron` 作业定期刷新链接——比如每天一次。有关 `cron` 的详细信息，请参阅第 9 章。

## 使用 ln -s 链接（软链接）

现在假设你想把整个工作量都推给你的新 helper。与其只给他访问单个文件，不如让他轻松访问你的整个项目目录。你可以使用软链接（使用 `ln -s` 创建）来实现这一点，它本质上为其他用户提供了指向你指定的文件或目录的快捷方式。

与硬链接一样，软链接允许文件同时存在于多个位置；然而，使用软链接时只有一个副本，而且软链接也可以链接目录。链接的文件或目录依赖于原始文件或目录——也就是说，如果原始文件或目录被删除，链接的文件或目录将不再可用。

软链接特别方便，因为它们既适用于目录也适用于单个文件，并且可在不同的文件系统之间工作（即不仅限于 `/home`，而是在整个 Unix 系统中的任何位置）。

与硬链接一样，软链接有时需要你有权访问另一用户的目录和文件。有关文件权限和所有权的更多信息，请参阅第 5 章，有关文件系统的详细介绍，请参阅第 7 章。

### 创建软链接：

- 1. `ls -l /home/deb /home/helper`

首先，列出两个用户主目录的内容。这里，我们验证要链接的目录确实存在于 Deb 的目录中，并且 helper 的目录中不存在匹配的目录或文件。参见代码清单 2.15。

- 2. `ln -s /home/deb/Projects /home/helper/Projects`

此命令创建软链接，以便 Deb 主目录的内容也可以从 helper 的主目录轻松访问。

- 3. `ls -la /home/helper`

列出 `/home/helper` 的内容显示了指向该目录的软链接的存在。注意代码清单 2.15 中显示链接的箭头。

## 提示

- 如果你只需要在同一文件系统内在两个文件之间创建链接，请考虑使用上一节中讨论的硬链接，即 使用 `ln` 链接（硬链接）。

```
$ ls /home/deb /home/helper
/home/deb:
Projects

/home/helper:
our_projects
$ ln -s /home/deb/Projects /home/helper/Projects
$ ls -la /home/helper/
total 11
d--------- 2 helper users 1024 Jun 29 21:18 .
drwxr-xr-x 11 root root 1024 Jun 29 21:03 ..
-rw-r--r-- 1 helper users 3768 Jun 29 21:03 .Adefaults
-rw-r--r-- 1 helper users 24 Jun 29 21:03 .bash_logout
-rw-r--r-- 1 helper users 220 Jun 29 21:03 .bash_profile
-rw-r--r-- 1 helper users 124 Jun 29 21:03 .bashrc
lrwxrwxrwx 1 ejr users 18 Jun 29 21:18 Projects -> /home/deb/Projects
-rw-r--r-- 3 ejr users 1055 Jun 26 11:00 our_projects
$
```

代码清单 2.15 使用 `ln -s` 创建软链接并连接目录。

## 使用你的 Shell

### 章节内容

- 发现你正在使用的 shell

- 理解 shell 和选项

- 更改你的 shell

- 临时更改你的 shell

- 在 bash shell 中使用补全

- 在 bash shell 中查看会话历史

- 在 zsh shell 中使用补全

- 在 zsh shell 中查看会话历史

- 在 ksh shell 中使用补全

- 在 ksh shell 中查看会话历史

- 在 csh shell 中查看会话历史

- 更改你的身份

- 修复终端设置

- 退出 shell

当你访问一个 Unix 系统时，你首先看到的是提示符，称为 shell 提示符，在此你与 Unix 交互。Shell 决定了你输入和重新输入命令的难易程度，以及你如何控制你的环境。Unix 的妙处在于你不必局限于一种 shell——也就是说，在大多数系统上你可以选择使用具有不同功能和能力的 shell。

在本章中，我们将查看你的 shell，展示如何更改你的 shell，并让你开始使用几种更常见的 shell。

### 发现你正在使用的 Shell

当你首次登录到你的 Unix 账户时，你将使用系统上的默认 shell。默认 shell、其功能和选项完全取决于你的系统管理员的指定。代码清单 3.1 和 3.2 显示了默认 shell 提示符在两个不同系统上如何不同的示例。

#### 要发现你正在使用的 shell：

- `echo $SHELL`

在你的 shell 提示符下，输入 `echo $SHELL`（大小写很重要！）。此命令告诉 Unix 显示（`echo`）有关 shell 设置的信息。顺便说一下，此信息包含在环境变量之一中，因此技术上的说法（你可能在 Unix 圈子里听到）是“`echo` 你的 shell 环境变量”。

系统的响应将是你的 shell 的完整路径——类似 `/bin/csh`、` /bin/bash` 或 `/bin/ksh`。

## ✓ 提示

- 你也可以使用 `finger userid` 来了解更多关于你的 shell 设置的信息，将你的登录名替换为 `userid`。你可以替换任何其他 `userid` 并查看其他账户持有者的可比信息。有关 `finger` 的更多信息，请参阅第 7 章。（一些系统不支持 `finger`，因为 `finger` 可能有点安全漏洞。）

- 你将在本章中关于不同 shell 及其功能找到更多信息。

```
xmision> echo $SHELL
/bin/csh
xmision> finger ejray
Login name: ejray   In real life: "RayComm
Directory: /home/users/eejray   Shell:
→ /bin/csh
On since Jul 23 06:58:48 on pts/16 from
→ calvin.raycomm.com
1 minute 28 seconds Idle Time
No unread mail
No Plan.
xmision>
```

代码清单 3.1 此 ISP 账户默认使用 `/bin/csh` shell。

```
[ejr@hobbes ejr]$ echo $SHELL
/bin/bash
[ejr@hobbes ejr]$ finger ejr
Login: ejr      Name: Eric J. Ray
Directory: /home/ejr   Shell: /bin/bash
On since Wed Jul 22 07:42 (MDT) on tty1
→ 3 hours 15 minutes idle
On since Thu Jul 23 08:17 (MDT) on ttyp0
→ from calvin
No mail.
Project:
Working on UNIX VQS.
Plan:
This is my plan-work all day, sleep all night.
[ejr@hobbes ejr]$
```
