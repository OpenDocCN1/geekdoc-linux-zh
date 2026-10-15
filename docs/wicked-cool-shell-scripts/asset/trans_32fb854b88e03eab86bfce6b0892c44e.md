

# 现在重新压缩所有内容。

if [ ! -z "$zlist" ] ; then
eval $Z $zlist
fi
if [ ! -z "$gzlist" ] ; then
eval $gz $gzlist
fi
if [ ! -z "$bzlist" ] ; then
eval $bz $bzlist
fi

# 完成！

exit 0

清单 4-15：zcat/zmore/zgrep 脚本

## 工作原理

对于任何给定的后缀，需要三个步骤：解压缩文件，将文件名重命名以去掉后缀，并在脚本末尾将其添加到重新压缩的文件列表中。通过保留三个独立的列表，每个压缩程序一个，该脚本还允许你轻松地在不同压缩工具压缩的文件中进行 grep。

最重要的一点是重新压缩文件时使用 eval 指令 ① ② ③。这是为了确保包含空格的文件名能够得到正确处理。当 zlist、gzlist 和 bzlist 变量被实例化时，每个参数都被引号包围，因此一个典型的取值可能是 "sample.c" "test.pl" "penny.jar"。由于列表中包含嵌套引号，像 cat $zlist 这样的命令会让 cat 抱怨找不到文件 "sample.c"。为了强制 shell 像在命令行中输入命令一样行事（其中引号在参数解析后会被去掉），使用 eval，一切就会按预期工作。

## 运行脚本

要正常工作，该脚本应有三个名称。在 Linux 中如何做到这一点？很简单：链接。你可以使用符号链接，这是一种存储链接目标名称的特殊文件，或硬链接，这实际上与链接文件分配了相同的 inode。我们更喜欢符号链接。这些可以很容易地创建（这里脚本已命名为 zcat），如清单 4-16 所示。

```
$ ln -s zcat zmore
$ ln -s zcat zgrep
```

清单 4-16：将 zcat 脚本符号链接到 zmore 和 zgrep 命令

完成之后，你就有了三个新的命令，它们具有相同的实际（共享）内容，每个命令都接受要处理的文件列表，并在处理完毕后对其进行解压缩然后重新压缩。

## 结果

无处不在的 compress 实用程序迅速压缩了 ragged.txt 并为其添加了 .Z 后缀：

```
$ compress ragged.txt
```

在 ragged.txt 处于压缩状态下，我们可以使用 zcat 查看文件，如清单 4-17 所述。

```
$ zcat ragged.txt.Z
So she sat on, with closed eyes, and half believed herself in Wonderland, though she knew she had but to open them again, and all would change to dull reality--the grass would be only rustling in the wind, and the pool rippling to the waving of the reeds--the rattling teacups would change to tinkling sheep-bells, and the Queen's shrill cries to the voice of the shepherd boy--and the sneeze of the baby, the shriek of the Gryphon, and all the other queer noises, would change (she knew) to the confused clamour of the busy farm-yard--while the lowing of the cattle in the distance would take the place of the Mock Turtle's heavy sobs.
```

清单 4-17. 使用 zcat 打印压缩的文本文件

然后再次搜索 teacup。

```
$ zgrep teacup ragged.txt.Z
rattling teacups would change to tinkling sheep-bells, and the
```

在此期间，文件在开始和结束时都保持其原始的压缩状态，如清单 4-18 所示。

```
$ ls -l ragged.txt*
-rw-r--r-- 1 taylor staff 443 Jul 7 16:07 ragged.txt.Z
```

清单 4-18：ls 的结果，显示只有压缩文件存在

## 修改脚本

这个脚本最大的弱点可能是如果在中途取消，文件不保证会被重新压缩。 一个不错的改进是利用 trap 能力并使用一个进行错误检查的 recompress 函数来修复这个问题。

## #34 确保文件最大程度压缩

如第 109 页脚本 #53 所强调的那样，大多数 Linux 实现包含不止一种压缩方法，但用户必须自行判断哪一种对给定文件压缩效果最好。因此，用户通常只学会使用一种压缩程序，而没有意识到使用另一种程序可以获得更好的结果。更令人困惑的是，有些文件用一种算法压缩效果更好，而另一种则更差，而且没有办法在不进行实验的情况下知道哪一种更好。

逻辑上的解决方案是编写一个脚本，使用每种工具压缩文件，然后选择结果最小的文件作为最佳文件。这正是 bestcompress 所做的，如清单 4-19 所示！

## 代码

```
#!/bin/bash

# bestcompress--Given a file, tries compressing it with all the available
# compression tools and keeps the compressed file that's smallest,
# reporting the result to the user. If -a isn't specified, bestcompress
# skips compressed files in the input stream.

Z="compress"  gz="gzip"  bz="bzip2"
Zout="/tmp/bestcompress.$$.Z"
gzout="/tmp/bestcompress.$$.gz"
bzout="/tmp/bestcompress.$$.bz"
skipcompressed=1

if [ "$1" = "-a" ] ; then
  skipcompressed=0 ; shift
fi

if [ $# -eq 0 ] ; then
  echo "Usage: $0 [-a] file or files to optimally compress" >&2
  exit 1
fi

trap "/bin/rm -f $Zout $gzout $bzout" EXIT

for name in "$@"
do
  if [ ! -f "$name" ] ; then
    echo "$0: file $name not found. Skipped." >&2
    continue
  fi

  if [ "$(echo $name | egrep '(\.[Z$]\|\.gz$\|\.bz2$)' )" != "" ] ; then
    if [ $skipcompressed -eq 1 ] ; then
      echo "Skipped file ${name}: It's already compressed."
      continue
```

