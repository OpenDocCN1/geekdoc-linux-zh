
## 关于运行命令的更多说明

精通 Linux 的很大一部分在于知道正确的命令行选项，以修改命令的行为以满足你的需求。大多数命令都有长格式和简写版本。例如，我们上面讨论过隐藏文件。我们可以使用命令 `-a` 或者使用 `--all` 来列出所有目录条目和隐藏文件。第一个是简写版本，而第二个是长写版本。你可以使用任何版本，因为它们所做的是一样的，所以没有区别。使用长写版本有一个优点，那就是你可能更容易记住你的命令在做什么。然而，简写方法的一个优点是你可以将多个命令链接在一起：

```
pwd
/home/Simon
ls -a
ls --all
ls -alh
```

以长写格式编写的命令行选项以两个短划线（--）开头，而简写版本以单个短划线（-）开头。单个短划线可以通过将表示这些选项的所有字母组合在一起放在短划线的后面来调用多个选项。

## 创建目录

随着时间的推移，你会积累大量的数据。因此，你应该建立一个目录系统，使用 Linux 的层级结构来组织和管理这些数据。养成为新内容创建新目录并将现有文件存储在正确目录中的习惯。

创建目录很容易；我们简单地使用命令 `mkdir`（make directory 的简写）如下：

```
mkdir [options] <Directory>
```

使用 `mkdir`，提供一个目录名称，它就会被为你创建：

```
pwd
/home/Simon
ls
bin Documents public_html

mkdir linuxtutorialwork
ls
bin Documents linuxtutorialwork public_html
```

在上面的示例中，我们首先检查当前位置，然后运行列表以确切知道该目录包含什么。然后我们运行 `mkdir` 命令并创建一个名为 `linuxtutorialwork` 的目录。记住，当我们在命令行中给出目录名称时，我们是在给出一个路径。

在以下示例中，我们可以看到几种创建目录的方法：

```
mkdir /home/Simon/foo
mkdir ./blah
mkdir ../dir1
mkdir ~/linuxtutorialwork/dir2
```

`mkdir` 有一些非常有用的选项。第一个是 `-p`，它告诉 `mkdir` 命令在必要时创建父目录。第二个是 `-v`，它命令 `mkdir` 告诉我们它正在做什么。

这里是使用 `-p` 选项的示例：

```
mkdir -p linuxtutorialwork/foo/bar
cd linuxtutorialwork/foo/bar
pwd
/home/Simon/linuxtutorialwork/foo/bar
```

现在让我们看看同时使用 `-v` 选项的相同示例：

```
mkdir -pv linuxtutorialwork/foo/bar
mkdir: created directory 'linuxtutorialwork/foo'
mkdir: created directory 'linuxtutorialwork/foo/bar'
cd linuxtutorialwork/foo/bar
pwd
/home/Simon/linuxtutorialwork/foo/bar
```

## 删除目录

创建新目录很容易，删除一个目录也非常容易。请记住，在 Linux 上使用命令行删除某物时没有撤销选项。所以要小心，并养成在删除之前仔细检查一切的习惯。我们用来删除目录的命令是 `rmdir`（remove directory 的简写）：

```
rmdir [options] <Directory>
```

这里有几点需要注意 – 首先，`rmdir` 支持 `-p` 和 `-v` 选项；其次，目录必须在删除之前为空。

```
rmdir linuxtutorialwork/foo/bar
ls linuxtutorialwork/foo
```

## 创建空文件

许多涉及数据操作的命令的一个特性是，如果我们引用一个尚不存在的目录，它们会为我们创建它。我们可以利用这一点使用名为 `touch` 的命令来创建空文件：

```
touch [options] <filename>
```

例如：

```
pwd
/home/Simon/linuxtutorialwork
ls
foo
touch example1
ls
example1 foo
```

`touch` 命令用于修改文件的修改时间和访问时间。它并不总是需要的，但如果你正在测试一个依赖于文件修改时间或文件访问时间的系统，使用它会很有帮助。正如我之前所说，重要的是，如果你接触（touch）一个不存在的文件或目录，它会被为你创建。

我们在 Linux 中做的很多事情不能自动完成，但当你知道某个命令的行为以及系统的一些深层方面时，你可以创造性地使用命令来获得你期望的结果。

## 复制文件或目录

有时你可能想复制一个目录或文件，例如，如果你即将对其进行更改，并希望有一个备份，以便如果事情出错，一切并非全完！用于此操作的命令是 `cp`（copy 的简写）：

```
cp [options] <source> <destination>
```

这个命令有几个选项，我现在将演示其中一个：

```
ls
example1 foo

cp example1 barney

ls
barney example1 foo
```

你注意到源和目标都是路径了吗？这些可以使用相对路径和绝对路径来引用，如下例所示：

```
cp /home/Simon/linuxtutorialwork/example2 example3
cp example2 ../../backups
cp example2 ../../backups/example4
cp /home/Simon/linuxtutorialwork/example2 /otherdir/foo/example5
```

当你使用 `cp` 命令时，它可以是文件的路径或目录的路径。如果它是文件，源的副本将被创建，并将被指定在目标路径中的文件名称命名。如果路径指向一个目录，文件将被复制到该目录中，并保留与源相同的名称。

默认情况下，`cp` 只复制文件。如果我们使用代表递归（Recursive）的选项 `-r`，我们可以复制目录。递归意味着你希望查看一个目录，并希望查看其中包含的所有文件和目录。对于子目录，只需进入它们并重复该命令，依此类推：

```
ls
barney example1 foo
cp foo foo2
cp: omitting directory 'foo'
cp -r foo foo2
ls
barney example1 foo foo2
```

在这个例子中，包含在名为 `foo` 的目录中的文件和目录被复制到 `foo2`。

## 移动文件或目录

如果你想移动一个目录或文件，可以使用代表 move（移动）的命令 `mv`。它的运作方式与 `cp` 几乎相同，但有一个小优点 – 我们不需要使用 `-r` 选项来移动目录：

```
mv [options] <source> <destination>
```

例如：

```
ls
barney example1 foo foo2
mkdir backups
mv foo2 backups/foo3
mv barney backups/
ls
backups example1 foo
```

让我们分解一下。在第 3 行，创建了一个名为 `backups` 的新目录。在第 4 行，名为 `foo2` 的目录被移动到新的 `backups` 目录并重命名为 `foo3`。然后，名为 `barney` 的文件被移动到名为 `backups` 的目录。因为它没有给一个新的目标名称，所以它保留了相同的名称。

## 重命名文件和目录

与 `touch` 命令一样，我们可以以稍微不同的方式使用 `mv` 命令的基本行为，从而得到不同的结果。正如你可以从上例的第 4 行看到的，我们可能需要为目录或文件提供一个新名称，当它被移动时，它会被重命名。如果你指定目标与源具有相同的目录名称，但提供不同的名称，你就使用了 `mv` 命令来更改文件或目录的名称，如下例所示：

```
ls
backups example1 foo
mv foo foo3
ls
backups example1 foo3
cd ..
mkdir linuxtutorialwork/testdir
mv linuxtutorialwork/testdir /home/Simon/linuxtutorialwork/fred
ls
backups example1 foo3 fred
```

所以首先，在第 3 行，使用相对路径将名为 `foo` 的文件重命名为 `foo3`。然后使用 `cd ..` 进入父目录，这样，在下一行中，我们可以表明即使不在其当前目录中，也可以对目录或文件运行命令。在第 8 行，使用源为相对路径，目标为绝对路径，将名为 `testdir` 的目录重命名为 `fred`。

