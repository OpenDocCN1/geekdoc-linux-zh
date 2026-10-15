
``` 
$ zcat ragged.txt.Z
So she sat on, with closed eyes, and half believed herself in Wonderland, though she knew she had but to open them again, and all would change to dull reality--the grass would be only rustling in the wind, and the pool rippling to the waving of the reeds--the rattling teacups would change to tinkling sheep-bells, and the Queen's shrill cries to the voice of the shepherd boy--and the sneeze of the baby, the shriek of the Gryphon, and all the other queer noises, would change (she knew) to the confused clamour of the busy farm-yard--while the lowing of the cattle in the distance would take the place of the Mock Turtle's heavy sobs.
```

清单 4-17. 使用 `zcat` 打印压缩的文本文件

然后再次搜索 `teacup`。

```
$ zgrep teacup ragged.txt.Z
rattling teacups would change to tinkling sheep-bells, and the
```

在此期间，文件在开始和结束时都保持其原始的压缩状态，如清单 4-18 所示。

```
$ ls -l ragged.txt*
-rw-r--r-- 1 taylor staff 443 Jul 7 16:07 ragged.txt.Z
```

清单 4-18：`ls` 的结果，显示只有压缩文件存在

## 修改脚本

这个脚本最大的弱点可能是如果在中途取消，文件不保证会被重新压缩。 一个不错的改进是利用 `trap` 能力并使用一个进行错误检查的 `recompress` 函数来修复这个问题。

## 确保文件最大程度压缩

如第 109 页脚本 #53 所强调的那样，大多数 Linux 实现包含不止一种压缩方法，但用户必须自行判断哪一种对给定文件压缩效果最好。因此，用户通常只学会使用一种压缩程序，而没有意识到使用另一种程序可以获得更好的结果。更令人困惑的是，有些文件用一种算法压缩效果更好，而另一种则更差，而且没有办法在不进行实验的情况下知道哪一种更好。

逻辑上的解决方案是编写一个脚本，使用每种工具压缩文件，然后选择结果最小的文件作为最佳文件。这正是 `bestcompress` 所做的，如清单 4-19 所示！

### 代码

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

```
else
    echo "Warning: Trying to double-compress $name"
fi

# Try compressing all three files in parallel.
$Z < "$name" > $Zout &
$gz < "$name" > $gzout &
$bz < "$name" > $bzout &

wait # Wait until all compressions are done.

# Figure out which compressed best.
smallest="$(ls -l "$name" $Zout $gzout $bzout | \ awk '{"print $5"NR}' | sort -n | cut -d= -f2 | head -1)"

case "$smallest" in
    1 ) echo "No space savings by compressing $name. Left as is." ;;
    2 ) echo Best compression is with compress. File renamed $(name).Z
        mv $Zout "${name}.Z" ; rm -f "$name"
        ;;
    3 ) echo Best compression is with gzip. File renamed $(name).gz
        mv $gzout "${name}.gz" ; rm -f "$name"
        ;;
    4 ) echo Best compression is with bzip2. File renamed $(name).bz2
        mv $bzout "${name}.bz2" ; rm -f "$name"
esac

done

exit 0
```

Listing 4-19: The `bestcompress` script

### How It Works

The most interesting line in this script is at ②. This line has `ls` output the size of each file (the original and the three compressed files, in a known order), chops out just the file sizes with `awk`, sorts these numerically, and ends up with the line number of the smallest resultant file. If the compressed versions are all bigger than the original file, the result is 1, and an appropriate message is printed out ①. Otherwise, `smallest` will indicate which of `compress`, `gzip`, or `bzip2` did the best job. Then it’s just a matter of moving the appropriate file into the current directory and removing the original file.
