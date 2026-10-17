
```
if [ -f $file ]; then
echo $file is a regular file
elif [ -d $file ]; then
echo $file is a directory
else
echo $file is not a regular file or a directory
fi
```

注意，`then`应该出现在第二行，表达式后面跟有一个分号（事实上，许多 shell 程序员习惯把`then`独占放在一行，尽管这在空间利用上并不十分高效）。

5. 在某个时刻，`if-then-else`代码可能会变得难以理解。当你有许多可能的分支时，你应该使用`case`命令。它的语法比之前的要复杂一些：

```
case string in
pattern) command-block ;
pattern) command-block ;;
esac
```

如果你正在寻找一个变量的可能值，可以使用`case`：

```
echo What do you want:
read var remainder
case $var in
house) echo The price must be very high;
car) echo The price must be high;
popsicle) echo The price must be low;
*) echo I do not know the price;
esac
```

这个`case`语句遵循一个输入请求并给用户一个大致的价格概念。`case`列表可以包含任意数量的项。注意特殊的`;`符号，它表示特定`case`语句项的结束。

这是另一个例子，一个微型文件命令：

```
case $filename in
*.gif) echo Graphics Interchange Format ;
*.jpg) echo Joint Photographic Experts Group ;;
*.png) echo Progressive Networking Group ;;
*.tif) echo Tagged Interchange Format ;
*.sox) echo Screen Capture format ;;
*) echo unknown format ${filename#*};
esac
```

在之前的两个示例中，模式匹配算法被用于通配符。还要注意在最后一个条件中使用的 bash 变量技巧，通过对文件名变量引用添加`#*.`修饰符来提取文件名后缀。要提取另一部分（仅不带后缀的文件名），你可以使用：

```
${filename%.*}
```

- 2. 这里有一个简单的 shell 脚本示例，其中`read`命令和`if`语句结合非常用：

```
echo "Delete which file? *"
read filename
if [ ! -f $filename ]; then
echo Can't delete $filename since it doesn't exist
else
echo Deleting $filename
/bin/rm $filename
fi
```

它提示输入文件名，然后在尝试调用`/bin/rm`删除文件之前，测试该文件是否存在。

有两种基本的条件表达式，以及第三种快捷方式。你可以使用`if`语句和快捷方式来测试条件并执行替代操作。你也可以使用`case`语句比较字符串并执行任意数量的操作。

## 任务 16.5：循环表达式

如果你想多次运行同一组命令，而不是每次都写一遍，那么使用循环命令会更好。循环分为两种类型：确定性循环（determinate loop）和不确定循环（indeterminate loop）。

确定性循环是指你在进入循环之前，已经确切知道要执行命令的次数。遍历文件列表就是一个很好的例子；你可能不知道文件的数量，但一旦知道了，你就可以为这些文件启动循环。

不确定循环是指你需要持续执行一个代码块，直到某个条件不再为真。你可能是在等待，或者在执行一系列修改以达到目标。

- 1. 确定性循环的常用命令是`for`命令。它具有以下语法：

```
for var in list
do
  command-block
done
```

你可以构建任何你喜欢的列表。它可以是一个数字序列，可以是命令的输出。早些时候我提到了遍历文件列表。这是通过以下循环实现的：

```
for var in `ls`
  if
    [ -f $var ]
    then
      echo $var is a regular file
  fi
```

这是分步执行的。

## 任务 16.6：bash 函数

Much of what's covered in this chapter has been what I characterize as flow control; ways to specify what command to execute in what set of conditions. What's interesting about using bash as a programmatic shell that you can actually create your own functions and use them throughout your, as if you were in a more formal (powerful) programming environment.

The greatest value of functions is that they give you the ability to specify and access parameters.

Let's get our feet wet and see how they can significantly help you develop powerful shell scripts!

- 1. Functions are defined as follows:

```
function functionname
{
  shell commands
}
```
