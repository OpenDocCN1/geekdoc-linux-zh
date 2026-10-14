
working directory. 要查看当前已定义的所有环境变量的列表，请在提示符下输入 set。

当你在 shell 提示符下输入命令时，shell 会按顺序在 PATH 变量列出的每个目录中查找该命令的程序文件。找到的第一个与你输入的命令匹配的程序将被运行。如果命令的程序文件不在你的 PATH 环境变量列出的目录中，shell 会返回 “command not found” 错误。

默认情况下，shell 不会在你的当前工作目录或主目录中查找命令。这实际上是一种安全机制，可以防止你意外执行程序。如果恶意用户在你的主目录中放置了一个名为 ls 的有害程序怎么办？如果你输入 ls 而 shell 在 /bin 目录中的真实程序之前先在你的主目录中查找假程序，你认为会发生什么？如果你认为会发生坏事，你的想法是对的。

由于你的 PATH 中没有当前目录 (.) 作为搜索位置，因此当前目录中的程序必须使用绝对路径或相对路径 ./programname 指定调用。

要查看哪些目录是你的 PATH 的一部分，输入以下命令：

```
echo $PATH
```

```
[alberto@digital alberto]$ echo $PATH
/bin:/usr/bin:/opt/bin:/usr/local/bin:/usr/X11R6/bin:/opt/kde/bin:
```

请注意，目录路径之间用冒号 (:) 分隔。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Filename Expansion: Tab

正如我前面所说，shell 并不是很符合人体工学，大多数人都不喜欢经常输入命令或长路径名。根据你使用的 shell，你可能有 shell 为你补全文件名和命令名的能力。每当你指定的路径部分不会引起混淆时，shell 就会这样做。

要在 bash 上激活补全，你所需要做的就是在输入足够字符后按 Tab。如果你想要列出 /usr/local/bin 目录的内容，你可以输入 ls /u<Tab>/lo<Tab>/b<Tab>，shell 会为你展开每条路径，节省你的按键次数。

如果 shell 无法完成扩展，因为存在多个可能的补全，再次按 Tab 会列出所有可能的匹配项。这在你忘记命令名称时非常有用。例如，如果你输入 l<Tab><Tab>，shell 会响应并列出所有以 l 开头的程序：

```
[alberto@digital alberto]$ l<Tab><Tab>
laser        lesskey      lkbib        lockfile     lpr
last         let          lmorph       logger       lprm
lastb        lex          ln           login        lptest
lastcomm     lha          lnd ir       logname      ls
latex        lightning    loadkeys     logout       lsattr
lbxproxy     lintopvf     loadunimap   look         lsdev
ld           lisa         local        lookbib      lynx
ld86         lispm tpgm   locale       lout         lz
ldd          listalias    localedef    lpq
less         listres      locate       lpqall.faces
```

## Exiting the Console

要退出控制台，请发出 logout 命令。此命令将结束你的会话，清除屏幕并返回到登录提示符。要从控制台重新启动计算机，可以按 Ctrl+Alt+Delete。

如果使用 kvt 或 xterm 等终端模拟器，你只需关闭窗口并像以前一样退出系统即可。

如果你让系统保持登录状态（这在你的家庭机器上可能是可以接受的），请记住任何人都可以查看和编辑你的文件。然而，永远不要让 root 会话保持打开状态，因为这可能导致致命的安全问题甚至灾难性的用户错误。

通常，Linux 系统会永久运行，只有在升级或某种软件故障需要时才关闭。

## Shutting Down a Linux Box

关闭系统与你在 PC 上习惯的方式有点不同。与 DOS 或其他一些系统不同，类 UNIX 系统需要温和地关闭。即使没有人登录，也会运行许多进程。这些进程需要正确停止，否则会发生坏事。关闭是通过 shutdown 命令完成的。

在使用 shutdown 命令之前，你需要拥有 root 权限。这意味着你需要在使用该命令之前以 root 身份登录。

shutdown 命令接受多个参数。这些选项指定系统将如何关闭以及何时关闭。此处必需的选项是 -h，表示“halt”，以及关键字 now，表示系统应立即开始关闭。

要在 root 控制台上优雅地关闭系统，输入以下内容：

```
[root@digital root]# shutdown -h now
```

## Rebooting a Linux Box

重启只是重新启动计算机的 fancy 名称。前面显示的 shutdown 命令可用于重启，如果你指定 -r 选项而不是 -h 选项。-r 选项表示 reboot：

```
[root@digital root]# shutdown -r now
```

重启系统的最简单方法是同时按下 Ctrl+Alt+Del 键，使系统进入重启序列。你可以在未登录控制台的情况下执行此操作。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

## Chapter 12
Working with Files on the Shell

## In This Chapter

- How to Manage and Organize Your Files Using a Shell
- How to Read Files

## Working with Files and Folders

在第 11 章“Shells and Consoles”中，你学习了如何登录和注销以及如何使用 shell 导航文件系统。在本章中，你将继续探索 UNIX shell 并学习如何使用它来操作文件和目录。

## Creating a New Empty File: touch

大多数时候，你会通过使用某些应用程序或 shell 程序来创建文件。出于教学目的，我在这里介绍一个允许你创建空文件的命令。这种凭空生成文件的能力将使你的探索更有趣一些。

如果你需要创建空文件，可以轻松使用 touch 命令完成。touch 的目的是修改文件的访问和创建时间，但作为副作用，如果文件尚不存在，它会创建文件。

要创建文件，输入命令 touch 后跟文件名：

```
[alberto@digital alberto]$ touch afile
```

要验证文件是否已创建，你可能想使用第 11 章中解释的 ls 命令。

你可以向该命令提供多个文件名。文件名可以使用相对或绝对路径，或两者混合指定。命令执行时，它会创建指定的文件。

## Removing Files: rm

要删除文件，使用 rm 命令。这个命令非常危险，原因只有一个：在 Linux（或通常的 UNIX）下删除的文件，除非你在磁带、软盘或其他介质上有备份，否则无法恢复。

要删除文件，输入以下内容：

```
[alberto@digital alberto]$ rm afile
```

由于其固有的危险，rm 命令提供了一个选项，可以询问你尝试删除的任何文件。如果你提供 -i 选项，它会先询问你的意图：

```
[alberto@digital alberto]$ rm -i afile
rm: remove `afile'? y
```

命令别名在第 11 章“Making Shell Options the Default”部分描述。要查看已激活的命令别名列表，在命令提示符下输入 alias。所有活动的别名列表将被打印出来供你检查。

> Check This Out:
> Oops! I deleted file x rm on tape or another disk, can I get it back?
> Is there a backup on tape or another disk?
> • Yes: yes, you can.
> • No: nope, the file is gone.

## Creating a Directory: mkdir

要创建目录，使用命令 mkdir 并指定目录名称（通常，名称可以是“相对”文件名或绝对路径）：

```
[alberto@digital alberto]$ mkdir adir
```

如果你需要创建整个目录树，指定选项 -p 和你需要的路径：

```
[alberto@digital alberto]$ mkdir -p
adir/anotherdir/yetanother
```
