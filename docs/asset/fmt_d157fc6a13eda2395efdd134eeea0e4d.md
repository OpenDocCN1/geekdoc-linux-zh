
## makefile

```makefile
bookrec : main.o iolib.a(input.o) iolib.a(print.o)
ranlib iolib.a
cc main.o iolib.a -o bookrec
```

## ioir Library Directory

```makefile
ilib:
cd ioir
```

```makefile
iolib.a: iolib.a(input.o) iolib.a(print.o)
ranlib iolib.a

$ touch input.c
$ make
gcc -c -O input.c
ar rv iolib.a input.o
a - input.o
rm -f input.o
ranlib iolib.a
gcc main.o iolib.a -o bookrec
```

# 版本控制系统：RCS 231

最后，`.DEFAULT` 特殊目标会在用户指定了一个不存在的目标时显示一条错误消息。

```makefile
CFILES = main.c input.c print.c
OBJECTS = main.o
LIBS = iolib.a
IOLIBMEMS = iolib.a(input.o) iolib.a(print.o)
SYSTEMS = -lm
CFLAGS = -g -O

c.o:
$(CC) $(CFLAGS) -c $$

c.a:
@$(CC) $(CFLAGS) -c $$
@ar r $@ $%
@echo Member $@ updated in library $@$

bookrec : $(OBJECTS) $(LIBS)
$(CC) $(CFLAGS) $(OBJECTS) $(SYLIBS) -o $@$

main.o: types.h
iolib.a: $(IOLIBMEMS)
@ranlib iolib.a

print : $(CFILES)
lp$? @touch print

.DEFAULT:
@echo Unknown target $@
```

# 版本控制系统：RCS

当你开发一个大型项目时，你会不断修改源代码。你可能会发现 Bug，也可能会添加其他功能。有时，更改可能会在无意中导致新的 Bug。对程序所有更改的记录可以帮助你追踪 Bug 和任何可能的的设计错误。版本控制系统（RCS）是一个 Linux 实用程序，用于跟踪对程序所做的所有更改。实际上，RCS 为你提供了程序的多个先前版本。你可以查看每个版本并检查其中所做的更改。

在一个程序员团队共同开发同一个程序的情况下，RCS 非常有用。每个程序员可能在不同的时间对程序进行修改。RCS 可以记录程序员进行的每项更改以及修改的时间。它甚至可以包含关于更改的注释。

RCS 存储文件的原始版本，并记录对文件的所有更改。利用这些信息，它可以生成文件的可能版本中的任意一个。RCS 实际上并不存储文件的独立完整版本，而是利用信息和原始文件来创建文件的完整版本。

对文件的记录更改集被称为“版本”。每个版本都被分配了一个包含多个组件的版本号，其中前两个组件是发布号（release）和级别号（level）。默认情况下，第一个版本的发布号为 1，级别号为 1。版本通常通过其发布号和级别号来引用。第一个版本称为版本 1.1 或 delta 1.1。后续版本将具有相同的发布号，但级别号递增。下一个版本将是 1.2，然后是 1.3 等。你也可以手动更改发布号。

版本通常是顺序生成的。每个版本都包含之前版本中所做的所有更改。然而，你可以创建一个针对特定版本的修改分支版本（branch）。对分支进行的更改将不会包含在后续版本中。分支版本有四个元素：发布号、级别号、分支号和序列号。其中分支号指定了该版本的一个分支。序列号是该分支中版本的数量。每个分支本身也可以有多个版本。从某种意义上说，一个分支可以被认为开始了一个全新的版本序列。分支号 1.1.1.1 引用第一个版本的第一个分支。1.1.1.2 引用该分支但分支中的第二个版本。1.1.2.1 引用第一个版本的第二个分支。

你可以轻松创建极其复杂的 RCS 文件，其中包含许多发布版本、版本和分支，每个分支都有自己的版本和其他分支。你应该谨慎操作，只在需要时生成版本，并尽可能保持结构简单。

# 版本控制系统：RCS 233

## 创建 RCS 文件

要创建一个 RCS 文件，你首先需要创建一个 RCS 目录。在该目录下放置你程序的 RCS 文件。你可以使用 `ci` 命令创建 RCS 文件。

```bash
ci -options filename
```

`ci` 命令接受一个参数，即原始文件的名称。RCS 文件将在 RCS 目录中创建，扩展名为 `.v`。`main.c` 文件将在 RCS 目录中有一个名为 `main.c,v` 的 RCS 文件。

你可以使用 `-r` 选项来指定创建新版本时想要开始的发布和版本号，所示：

```bash
$ ci -r5.2 main.c
```

如果你的程序最初由几个源代码文件组成，你需要为每个文件创建一个 RCS 文件，包括其源代码后缀。在下一个示例中，用户为 `main.c` 程序创建了一个 RCS 文件。

```bash
$ ci main.c
RCS/main.c,v <- main.c
enter description, terminated with single '.' or end of file:
NOTE: This is NOT the log message!
>> bookrec main program
>>
initial revision: 1.1
done
```

通常情况下，一个项目由几个不同的程序员同时工作。每个人都有权限访问并修改源代码。

```rcs
rcs -options filename
```

你可以使用带有 `-a` 选项的 `rcs` 命令来限制对 RCS 文件的访问。在 `-a` 选项后输入允许访问此文件的用户登录。对于每个允许访问的用户，使用一个 `-a` 选项。在下一个示例中，访问被限制为：

```bash
$ rcs -ausername main.c
```

如果有人决定检出（check out）项目，你可以拒绝他们的访问。`-e` 选项将他们从访问用户列表中移除。

```bash
$ rcs -e username main.c
```

如果你想允许用户访问文件，使用 `-a` 选项：

```bash
$ rcs -ausername main.c
```

如果你想阻止用户访问文件，使用 `-e` 选项：

```bash
$ rcs -e main.c
```

如果你想锁定文件的版本，使用 `-u` 选项：

```bash
$ rcs -u1.2 main.c
```

如果你想解锁文件的版本，使用 `-U` 选项：

```bash
$ rcs -U1.2 main.c
```

如果你想从 RCS 中删除一个版本，使用 `-d` 选项：

```bash
$ rcs -d1.2 main.c
```

# 版本控制系统：RCS 235

## 获取和记录 RCS 文件

要使用 RCS 编辑你的源代码，你必须先有一个源代码副本。该副本名称与 RCS 文件相同，但不包含 `.v` 后缀。对于 `main.v` 文件，RCS 将生成一个名为 `main.c` 的文件。

### co

```bash
co filename
```

RCS `co` 命令生成源代码的副本。不带选项的 `co` 命令仅生成只读副本。`-l` 选项生成你可以编辑的源代码副本。l 代表锁定（lock），当你使用此选项时，RCS 文件中的 `main.c` 程序将被锁定。其他程序员无法访问它。这意味着一次只有一个程序员可以更改给定文件。完成后，你提交（check in）程序，注册你的更改并解锁。

在下一个示例中，`co` 命令生成源代码 `main.c` 的可编辑副本。

```bash
$ co -l main.c
RCS/main.c,v --> main.c
revision 1.1 (locked)
done
```

### ci

```bash
filename
```

一旦完成源代码的编辑，你就使用 `ci` 命令在 RCS 文件中注册你的更改。你输入 `ci` 后跟 RCS 文件的名称。然后提示你输入注释。实际上，编辑由 `co` 生成的文件副本创建了源代码的新版本，即构成新版本的更改集。版本号（1.2）将显示出来。在下一个示例中，用户通过生成新版本 1.2 来保存 `main.c` 的更改。

```bash
$ ci main.c
RCS/main.c,v << main.c
new revision: 1.2; previous revision: 1.1
enter log message, terminated with single '. ' or end of file:
>> Added prompts
>> .
done
```

## 版本控制系统：RCS

你可以使用 `ci` 命令的 `-r` 选项来为新版本指定自己的编号，正如本章稍后“检索和删除特定的 RCS 版本”节所述。

### log

```bash
rlog 选项 文件名
```
