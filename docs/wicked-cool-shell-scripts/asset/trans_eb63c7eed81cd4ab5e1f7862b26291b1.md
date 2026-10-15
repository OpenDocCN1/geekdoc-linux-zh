

![](img/4ffb1cc24a1b24b49254839643abedb2_376_0.png)

# B
# BONUS SCRIPTS

因为我们拒绝不了这些宝物！在开发这第二版时，我们为备份目的又写了几个脚本。事实证明我们并不需要这些备用脚本，但我们不想把我们的秘方藏着掖着不让读者知道。

前两个奖励脚本是给那些系统管理员用的，他们必须处理移动或处理大量文件。最后一个脚本是给那些总在寻找下一个急需被改写成 shell 脚本的网络服务的网络用户；我们将抓取一个网站来帮助我们追踪月相！

## #102 Bulk-Renaming Files

系统管理员经常被要求将大量文件从一个系统移动到另一个系统，而且新系统中的文件通常需要完全不同的命名方案。对于少数几个文件，手动重命名很简单，但当重命名数百或数千个文件时，它立刻就变成更适合用 shell 脚本处理的任务。

### The Code

Listing B-1 中的简单脚本接受两个参数作为要匹配和替换的文本，以及一个参数列表指定你想要重命名的文件（可以用通配符方便使用）。

```
#!/bin/bash
# bulkrename--Renames specified files by replacing text in the filename

printHelp()
{
  echo "Usage: $0 -f find -r replace FILES_TO_RENAME*"
  echo -e "\t-f The text to find in the filename"
  echo -e "\t-r The replacement text for the new filename"
  exit 1
}

while getopts "f:r:" opt
do
  case "$opt" in
    r ) replace="$OPTARG"  ;;
    f ) match="$OPTARG"    ;;
    ? ) printHelp           ;;
  esac
done

shift $(($OPTIND - 1))

if [ -z $replace ] || [ -z $match ]
then
  echo "You need to supply a string to find and a string to replace";
  printHelp
fi

for i in $@
do
  newname=$(echo $i | sed "s/$match/$replace/")
  mv $i $newname
  && echo "Renamed file $i to $newname"
done
```

Listing B-1: The bulkrename script

### How It Works

我们首先定义一个 printHelp() 函数 ①，它会打印所需参数和脚本用途，然后退出。在定义新函数之后，代码使用 getopts ② 遍历传递给脚本的参数，如之前脚本中所做的那样，当指定其参数时，将值赋给 replace 和 match 变量。

脚本随后检查我们是否已为稍后使用的变量提供值。如果 replace ③ 和 match ④ 变量的长度为零，脚本会打印错误信息，告诉用户他们需要提供要查找的字符串和要替换的字符串。脚本随后打印 printHelp 文本并退出。

在验证 match 和 replace 有值之后，脚本开始遍历其余指定的参数 ⑤，这些参数应该是要重命名的文件。我们使用 sed ⑥ 将文件名中的 match 字符串替换为 replace 字符串，并将新文件名存储在 bash 变量中。存储新文件名后，我们使用 mv 命令将文件移动到新文件名，然后打印一条消息告诉用户文件已被重命名。

### Running the Script

bulkrename shell 脚本接受两个字符串参数和要重命名的文件（可以用通配符方便使用；否则逐个列出）。如果指定了无效参数，会打印友好的帮助信息，如 Listing B-2 所示。

### The Results

```
$ ls "~/tmp/bulk"
1_dave 2_dave 3_dave 4_dave
$ bulkrename
You need to supply a string to find and a string to replace
Usage: bulkrename -f find -r replace FILES_TO_RENAME*
-f The text to find in the filename
-r The replacement text for the new filename
$ bulkrename -f dave -r brandon "~/tmp/bulk/*"
Renamed file /Users/bperry/tmp/bulk/1_dave to /Users/bperry/tmp/bulk/1_brandon
Renamed file /Users/bperry/tmp/bulk/2_dave to /Users/bperry/tmp/bulk/2_brandon
Renamed file /Users/bperry/tmp/bulk/3_dave to /Users/bperry/tmp/bulk/3_brandon
Renamed file /Users/bperry/tmp/bulk/4_dave to /Users/bperry/tmp/bulk/4_brandon
$ ls "~/tmp/bulk"
1_brandon 2_brandon 3_brandon 4_brandon
```

Listing B.2: Running the bulkrename script

你可以单独列出要重命名的文件，也可以在文件路径中使用星号 (*) 对它们进行通配，就像我们在 ① 处做的那样。移动后，每个重命名后的文件都会连同其新名称一起打印到屏幕上，以向用户保证文件已按预期重命名。

