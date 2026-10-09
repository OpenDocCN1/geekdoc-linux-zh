

# 使用相对路径名时，请明确当前工作目录

使用相对路径名访问文件时，该文件的位置取决于（相对于）当前工作目录。在使用相对路径名之前，请务必确认当前的工作目录。可以使用 `pwd` 命令来验证目录。如果你正在使用 `vim` 创建文件，而实际所在位置与你以为的文件层级位置不符，新文件将会出现在一个意料之外的位置。

当你使用绝对路径名时，工作目录是哪个并不重要。因此，以下命令始终会编辑你主目录中名为 **goals** 的文件：

```
$ vim ~/.goals
```

阅读本段内容时，请参考图 6-6。作为工作目录子项的文件可以通过简单的文件名来引用。工作目录的“孙辈”文件（即子目录中的文件）可以通过短相对路径名来引用：由斜杠分隔的两个文件名。当你在一个大型目录结构中操作文件时，使用短相对路径名可以为你节省时间并避免麻烦。如果你选择一个包含特定任务最常用文件作为工作目录，就不需要使用那些冗长且繁琐的路径名了。

## 处理目录

本节讨论如何创建目录 (mkdir)、在目录之间切换 (cd)、删除目录 (rmdir)、使用路径名使工作更轻松，以及在目录之间移动和复制文件和目录。最后，本节将列出并简要描述 Ubuntu 文件系统中的重要标准目录和文件。

![](img/2344fc4a798f29dca9e8b5ed7288171a_257_0.png)

![](img/2344fc4a798f29dca9e8b5ed7288171a_258_0.png)

### mkdir：创建目录

**mkdir** 实用程序用于创建目录。传递给 **mkdir** 的 **参数**（第 1135 页）将成为新目录的路径名。以下示例展示了如何开发图 6-7 中所示的目录结构。在图中，新添加的目录比其他目录颜色浅，并用虚线连接。

在图 6-8 中，**pwd** 显示 Max 正在其主目录（**/home/max**）中工作，而 **ls** 显示其主目录中的文件名：**demo**、**names** 和 **temp**。使用 **mkdir**，Max 在其主目录下创建了一个名为 **literature** 的目录。由于他希望 **literature** 目录成为工作目录的子目录，因此他使用了相对路径名（即简单的文件名）。Max 也可以使用绝对路径名来创建相同的目录：`mkdir /home/max/literature`。

图 6-8 中的第二个 **ls** 命令验证了新目录的存在。**ls** 命令的 **-F** 选项会在每个目录名称后显示斜杠，并在每个可执行文件（shell 脚本、实用程序或应用程序）名称后显示星号。当你调用 ls 并传入一个目录名称作为参数时，ls 会列出该目录的内容。最后的 ls 没有显示任何内容，因为 literature 目录中没有文件。

```
$ pwd
/home/max
$ ls
demo names temp
$ mkdir literature
$ ls
demo literature names temp
$ ls -F
demo literature/ names temp
$ ls literature
$
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_258_1.png)

以下命令展示了两种方法，可以将 promo 目录作为新创建的 literature 目录的子目录进行创建。第一种方法检查 /home/max 是否为工作目录，并使用相对路径名：

```
$ pwd
/home/max
$ mkdir literature/promo
```

第二种方法使用绝对路径名：

```
$ mkdir /home/max/literature/promo
```

使用 mkdir 的 -p (parents) 选项，可以用一条命令同时创建 literature 和 promo 目录：

```
$ pwd
/home/max
$ ls
demo names temp
$ mkdir -p literature/promo
```

```
或
$ mkdir -p /home/max/literature/promo
```

### cd：更改到另一个工作目录

cd (change directory) 实用程序将另一个目录设为工作目录，但不会更改工作目录的内容。图 6-9 展示了两种将 /home/max/literature 目录设为工作目录的方法，并可通过 pwd 进行验证。首先，Max 使用带有绝对路径名的 cd 命令将 literature 设为他的工作目录——在使用绝对路径名发出命令时，当前工作目录是哪个并不重要。

pwd 命令确认了 Max 所做的更改。在不带参数使用时，cd 会将你的主目录设为工作目录，这就像你登录时的情况一样。图 6-9 中的第二个 cd 命令没有参数，因此它将 Max 的主目录设为工作目录。最后，在知道他在主目录中工作的情况下，Max 使用简单的文件名将 **literature** 目录设为他的工作目录（**cd literature**），并使用 **pwd** 确认更改。

```
$ cd /home/max/literature
$ pwd
/home/max/literature
$ cd
$ pwd
/home/max
$ cd literature
$ pwd
/home/max/literature
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_259_0.png)

### 工作目录与主目录

**提示**
工作目录与你的主目录不同。你的主目录在会话期间以及通常从一个会话到下一个会话保持不变。登录后，你始终在同一个目录中工作：你的主目录。

与主目录不同，工作目录可以随你的意愿频繁更改。你没有固定的工作目录，这解释了为什么有些人称之为 *当前目录*。从你登录开始，直到你使用 **cd** 更改目录之前，你的主目录就是工作目录。如果你更改到 Sam 的主目录，那么 Sam 的主目录就会成为工作目录。

### . 和 .. 目录条目

**mkdir** 实用程序会自动在其创建的每个目录中放入两个条目：一个点 (.) 和两个点 (..)。. 等同于工作目录的路径名，可以替代其使用；.. 等同于工作目录父目录的路径名。由于这些条目的文件名以点开头，因此它们是隐藏的。

以 **literature** 目录为工作目录时，以下示例三次使用了 ..：第一次用于列出父目录（**/home/max**）的内容，第二次用于将 **memoA** 文件复制到父目录，第三次再次列出父目录的内容。

```
$ pwd
/home/max/literature
$ ls ..
demo    literature    names    temp
$ cp memoA ..
$ ls ..
demo    literature    memoA    names    temp
```

在使用 **cd** 将 **promo**（**literature** 的一个子目录）设为工作目录后，Max 可以使用相对路径名调用 **vim** 来编辑其主目录中的文件。

```
$ cd promo
$ vim ../../names
```

你几乎可以在任何需要文件名或路径名的实用程序或程序中，使用绝对路径名或简单的文件名。这种用法适用于 **ls**、**vim**、**mkdir**、**rm** 以及大多数其他 Linux 实用程序。

### rmdir：删除目录

**rmdir** (remove directory) 实用程序用于删除目录。你不能删除工作目录，也不能删除包含除 . 和 .. 条目以外文件的目录。如果需要删除包含文件的目录，请首先使用 rm 删除文件，然后再删除该目录。你不需要（也无法）删除 . 和 .. 条目；rm -r 会自动删除它们。以下命令删除 promo 目录：

```
$ rm -r /home/max/literature/promo
```

rm 实用程序有一个 -r 选项 (rm -r filename)，可以递归删除目录内的文件（包括子目录），同时也删除该目录本身。

**谨慎使用 rm -r**

> **注意** 虽然 rm -r 是一个便捷的命令，但必须谨慎使用。不要使用模糊的文件引用（如 \*）。一条简短的命令就可能非常容易导致你误删整个主目录，这非常危险。

### 使用路径名

如果想尝试以下示例，请使用文本编辑器创建一个名为 letter 的文件。或者，你可以使用 touch 创建一个空文件：

```
$ cd
$ pwd
/home/max
$ touch letter
```

在 /home/max 作为工作目录的情况下，以下示例使用 cp 配合相对路径名将文件 letter 复制到 /home/max/literature/promo 目录。（如果你之前删除了 promo，你需要重新创建它。）该文件副本的简单文件名为 letter.0610：

```
$ cp letter literature/promo/letter.0610
```

如果 Max 不切换到其他目录，他可以如所示使用 vim 来编辑刚刚创建的文件副本：

```
$ vim literature/promo/letter.0610
```

如果 Max 不想使用长路径名来指定文件，他可以在使用 vim 之前使用 cd 将 promo 设为工作目录：

```
$ cd literature/promo
$ pwd
/home/max/literature/promo
$ vim letter.0610
```

为了将工作目录的父目录（名为 /home/max/literature）设为新的工作目录，Max 可以给出以下命令，利用 .. 目录条目：

```
$ cd ..
$ pwd
/home/max/literature
```

