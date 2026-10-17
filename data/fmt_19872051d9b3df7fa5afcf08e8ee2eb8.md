
- 6. 按建议操作：执行命令 `cvs commit` 以使添加的文件和目录永久化。如果你不想输入日志消息，按 `Esc` 键并输入 `ZZ` 保存并退出。当你看到 vi 会话后，你看到的输出将类似于下面：

```
$ cvs commit

cvs commit: Examining .

RCS file: /space/cvs/hello/hello.c

done

Checking in hello.c:

/space/cvs/newhello/hello.c <-- hello.c

initial revision: 1.1

done

RCS file: /space/cvs/newhello/msg.c

done

Checking in msg.c:

/space/cvs/newhello/msg.c <-- msg.c

initial revision: 1.1

done

RCS file: /space/cvs/newhello/showit.c

done

Checking in showit.c:

/space/cvs/newhello/showit.c <-- showit.c

initial revision: 1.1

done
```
（注：此处示例输出根据 `showit.c` 逻辑补全，原文在此处略有截断或重复，但逻辑一致）

修正后的示例输出如下：
```
$ cvs commit

cvs commit: Examining .

RCS file: /space/cvs/hello/hello.c

done

Checking in hello.c:

/space/cvs/newhello/hello.c <-- hello.c

initial revision: 1.1

done

RCS file: /space/cvs/newhello/msg.c

done

Checking in msg.c:

/space/cvs/newhello/msg.c <-- msg.c

initial revision: 1.1

done

RCS file: /space/cvs/newhello/showit.c

done

Checking in showit.c:

/space/cvs/newhello/showit.c <-- showit.c

initial revision: 1.1

done
```

注意，CVS 允许使用 `ci` 命令来签入文件：`ci -u -r2.1 howdy.c`。同样，`ci -u -r3 howdy.c` 会签入 `howdy.c`，为其分配修订号 3.1，并将只读修订版本 3.1 工作文件存回到你的当前工作目录。

下面的示例创建了 `howdy.c` 的 2.1 版本。在执行此命令之前，请确保你已经某种方式检出（checkout）并修改了 `howdy.c`。
```
$ ci -r2 howdy.c

RCS/howdy.v <- howdy.c

revision: 2.1: previous revision: 1.2

enter log message, terminated with single '.' or end of file:

>> Added something

>>

done
```

此命令等于 `ci -r2.1 howdy.c`。

下一个示例检出 `howdy.c` 的 1.2 版本，而忽略工作目录中存在的更高版本的修订。
```
$ ci -r1.2 howdy.c

RCS/howdy.c.v --> howdy.c

revision 1.2

done
```

方便的命令 `show next` 会将你对版本 1.2 所做的所有更改重定向（显示），并让你从一个已知的源文件重新开始。
```
$ ci -1 -f howdy.c

RCS/howdy.c.v --> howdy.c

revision 2.1 (locked)

done
```

当与 `ci,-f` 使用时，强制 RCS 即使在文件没有变化的情况下也签入文件。

# 使用 CVS 进行源码控制

你可能会注意到 RCS 存在一些缺点，这使得它不适用于大型项目。首先，在没有更复杂的封装脚本来处理目录处理机制的情况下，RCS 在单中心化仓库上的工作效果并不理想。而且，对于一个成员多于几个人的编程团队，你需要一个仓库。

除非你费力使用其他地方的目录，否则 RCS 始终是当前目录。更与 Linux 和其他开源项目相关的是，RCS 完全不适用于分布式开发，因为它不支持网络协议。（也就是说，它无法在互联网上运行。）

此外，RCS 经常受到程序员忘记命令的影响。如果你忘记使用特定选项检出文件，你可能会在以后后悔。即使你是独立工作，也可能发现 CVS 是更好的选择。

并发版本系统（CVS）同时支持中心化仓库和基于网络的访问。它非常适合多个程序员，且一个仓库可以支持多个项目。然而，为了保持讨论简单，本章中的示例仅处理本地访问的仓库。接下来的步骤类似于之前描述的 RCS 过程，但它们稍微复杂一些，并且显然使用了 CVS 概念：

- 1. 创建一个 CVS 仓库：

```
$ mkdir /space/cvs
$ export CVSROOT=/space/cvs
$ cvs init
```

第一个命令创建一个 `/space/cvs` 目录，在其中建立仓库。第二个命令用该目录定义环境变量 `$CVSROOT`。定义 `$CVSROOT` 使 CVS 变得简单得多。第三个命令初始化仓库，它会创建 CVS 正常工作所需的某些管理目录。

- 2. 创建一个顶层工作目录，以存储你的各种项目，然后将其切换到该目录：

```
$ mkdir projects
$ cd projects
```

- 3. 将 CVS 根目录的副本检出到你刚刚创建的目录中：

```
$ cvs -d $CVSROOT co -l
ccvs checkout: Updating
```

`-d` 选项告诉 `cvs` 包含 CVS 仓库的目录名称（`$CVSROOT` 或 `/space/cvs`）；`co` 表示检出（与 RCS 一样）；`-l` 选项代表本地（local），意味着只在当前目录工作，而不是递归遍历子目录；而 `-d` 指定当前目录。

- 4. 创建一个存放项目的目录并将其添加到仓库：

```
$ mkdir newhello
$ cvs add newhello
Directory /space/cvs/newhello added to the repository
```

- 5. 进入新目录，将你的项目文件复制到其中（将 `your_new_hello_code` 替换为你存放新项目实际源文件文件的目录名称），然后将这些文件（任何可能存在的目录）添加到仓库。

```
$ cd newhello
$ cp /your_new_hello_code/* *
$ cvs add * -h
cvs add: scheduling file 'hello.c' for addition
cvs add: scheduling file 'msg.c' for addition
cvs add: scheduling file 'main.c' for addition
cvs add: scheduling file 'showit.c' for addition
cvs add: use 'cvs commit' to add these files permanently
```

- 6. 按建议操作：执行命令 `cvs commit` 以使添加的文件和目录永久化。如果你不想输入日志消息，按 `Esc` 键并输入 `ZZ` 保存并退出。当你看到 vi 会话后，你看到的输出将类似于下面：

```
$ cvs commit

cvs commit: Examining .
RCS file: /space/cvs/hello/hello.c

done

Checking in hello.c:

/space/cvs/newhello/hello.c <-- hello.c

initial revision: 1.1

done

RCS file: /space/cvs/newhello/msg.c

done

Checking in msg.c:

/space/cvs/newhello/msg.c <-- msg.c

initial revision: 1.1

done

RCS file: /space/cvs/newhello/showit.c

done

Checking in showit.c:

/space/cvs/newhello/showit.c <-- showit.c

initial revision: 1.1

done
```
（注：此处示例输出根据 `showit.c` 逻辑补全，原文在此处略有截断或重复，但逻辑一致）

修正后的示例输出如下：
```
$ cvs commit

cvs commit: Examining .
