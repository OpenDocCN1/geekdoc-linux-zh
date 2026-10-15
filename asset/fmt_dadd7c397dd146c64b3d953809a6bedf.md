
最后，`make`工具从底部的叶子节点到根节点处理树，检查每个子节点的最后修改时间是否比其直接父节点的最后修改时间更晚。对于每这种情况，如果关联的文件不存在，无论其子节点的最后修改时间如何，都将执行其规则。为了说明节点被检查的顺序，我为图 12.6 显示的图标记了编号。

![](img/4245b8ee77539f33ff090ce0a0dd7eb6_432_2.png)

图 12.6

`make`排序。

# 执行 Make

一旦创建了`make`文件，你就可以运行`make`来重新创建由`make`文件指定依赖信息的可执行文件。为了向你展示其工作原理，我删除了所有的对象模块和可执行文件，以强制执行每个命令列表。当我执行`make`时，我看到了这些：

```
$ make -f main1.make            ..make executable up-to-date
cc -c main1.c
cc -c reverse.c
cc main1.o reverse.o -o main1
```

注意，每个`make`规则都按照图 12.6 所示的精确顺序执行了。由于我在制作回文程序时创建了第二个可执行文件，我也制作了第二个`make`文件，名为"`main2.make`" 。这里是：

```
main2:
main2.o reverse.o palindrome.o
main2.o:
cc main2.o reverse.o palindrome.o -o main2
main2.c:
main2.c palindrome.h
cc -c main2.c
reverse.o:
reverse.c reverse.h
cc -c reverse.c
palindrome.o:
palindrome.c palindrome.h reverse.h
cc -c palindrome.c
```

当我使用此文件执行`make`时，我看到了以下内容：

```
$ make -f main2.make            ..make executable up-to-date
cc -c main2.c
cc -c palindrome.c
cc main2.o reverse.o palindrome.o -o main2
```

注意"`reverse.c`"没有被重新编译。这是因为之前的`make`已经创建了一个最新的对象模块，而`make`仅在需要时才重新编译文件。

# Make 规则

到目前向你展示的`make`文件比它们需要的要大。这是因为我提供的某些`make`规则已经被`make`工具以一种更通用的方式识别。例如，请注意几条规则的形式如下：

```
xxx.o:
reverse.c reverse.h
cc -c xxx.c
```

# UNIX 文件依赖系统：make 401

其中`xxx`在规则之间发生变化。`make`工具包含一个类似于下面的预定义规则：

```
.c:o:
/bin/cc -c -O $<
```

这个看起来很晦涩的规则告诉`make`工具如何从 C 源文件创建对象模块。这个通用规则的存在允许我省略 C 编译规则。因此，这里有一个更精简版本的"`main2.make`"：

```
main2:
main2.o reverse.o palindrome.o
main2.o:
cc main2.o reverse.o palindrome.o -o main2
main2.c palindrome.h
reverse.o:
reverse.c reverse.h
palindrome.o:
palindrome.c reverse.h
```

`make`还包含其他推理规则。例如，`make`知道对象模块的名称及其对应的源文件是相关的。它利用这些信息来推断标准依赖。例如，它推导出"`main2.o`"依赖于"`main2.c`" ，因此你可以从依赖列表中省略此信息。这里有一个更精简版本的"`main2.make`"：

```
main2:
main2.o reverse.o palindrome.o
main2.o:
cc main2.o reverse.o palindrome.o -o main2
main2.c palindrome.h
reverse.o:
reverse.c reverse.h
palindrome.o:
palindrome.c reverse.h
```

# 编写你自己的规则

遗憾的是，编写你自己的规则的方法，甚至是理解已存在的规则，都超出了本书的范围。更多信息，请参阅章节后部分“其他 Make 工具”标题下列出的来源。

# Touch

为了确认新版本的`make`文件有效，我请求了一个`make`并获得了以下内容：

```
$ make -f main2.make
main2 is up to date.
```

显然，由于我已经执行过一次成功的`make`，另一个`make`将不会触发任何规则！为了测试目的，我使用了一个名为`touch`的方便工具，它将所有命名文件的最后修改时间设置为当前时间。图 12.7 给出了`touch`的简要概述。

# 402 第 12 章 C 编程工具

工具：`touch -c {fileName}`

`touch`将命名文件的最后修改时间访问访问时间更新为当前时间。默认情况下，如果指定的文件不存在，则会创建一个大小为零的文件。为了防止这种情况，请使用`-c`选项。

图 12.7

`touch`命令的描述。

我碰了"`reverse.h`"文件，这随后导致了以下操作：

```
$ touch reverse.h
$ make -f main2.make
cc -c reverse.c
cc -c palindrome.c
cc main2.o reverse.o palindrome.o -o main2
```

# 宏

`make`支持原始宏。如果你在`make`文件顶部指定如图 12.8 所示的形式的行，`make`文件中每个`$(token)`都会被替换为`replacementText`。除了包含规则外，标准规则文件还包含了如`CFLAGS`等宏的默认定义。例如，`make`工具从 C 源文件更新对象文件的规则如下：

```
.c:o: /bin/cc -c -O $<
```

图 12.8

`make`中的宏。

标准规则文件包含如下

```
CFLAGS = -O
```

如果你想使用`cc`的`-p`选项重新编译一组程序，你会在`make`文件顶部覆盖`CFLAGS`的默认值，并在"`main2`"规则的最后的`cc`调用中使用`-p`选项，如下：

```
CFLAGS = -p
main2: main2.o reverse.o palindrome.o
```

# UNIX 归档系统：ar

中型 C 项目通常使用数百个对象模块。在文件规则中指定许多对象模块可能非常麻烦，我建议学习如何使用 UNIX 归档工具`ar`来组织和分组对象模块。归档工具（称为管理员）允许你执行以下任务：

- 创建以“a”结尾的特殊归档文件
- 向归档中添加、删除、替换和追加任何类型的文件
- 获取归档的目录

图 12.9 `ar`的概览。

> 工具：`ar keyArchiveName {fileName}`

`ar`允许你创建和操作归档。`archiveName`是你想要访问的文件名，它应该以“.a”后缀结尾。`key`可以是以下之一：

- `dletes`从归档中删除文件
- `q`appends 将文件追加到归档末尾，即使它已经存在

# UNIX 归档系统：ar 403

```
cc -p main2.o reverse.o palindrome.o -o main2
palindrome.h
reverse.o:
reverse.c reverse.h
palindrome.o:
palindrome.c reverse.h
```

为了重新编译程序组，我使用了`touch`工具强制重新编译所有源文件：

```
$ touch *.c
$ make .. make to recompile everything
$ make -f main2.make
cc -c reverse.c
cc -c palindrome.c
cc -c reverse.c
```

# 其他 Make 工具

`make`是一个相当复杂的工具，包含了处理库和推理规则的规定。除了这些以外的信息都包含在书中，许多其他书籍关于`make`的信息比本书少，因此我建议查阅 UNIX 手页获取更多详细信息。

## 404 第12章 C 编程工具

| r | 如果文件不存在，则将文件添加到归档；如果已存在，则替换它 |
| t | 向标准输出显示归档的内容列表 |
| x | 将归档中的所有文件复制到当前目录 |
| v | 生成详细输出 |

图 12.9（续）

当一组对象模块存储在归档文件中时，`cc`编译器和`ld`加载器可以通过提供归档文件名来访问它。归档所需的任何对象模块都会自动链接。这极大地减少了在链接大量对象模块时这些工具所需的参数数量。

本节其余部分提供了每个`ar`选项的示例。

创建归档
