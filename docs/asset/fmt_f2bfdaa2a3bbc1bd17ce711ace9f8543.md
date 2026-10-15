
```
grep -n $word $filename
sed -e 's/^/' -e "s/$word$boldonword$boldoff/"
echo -n "ignore, quit, or type replacement: "
read fix
if [ "$fix" = "q" -o "$fix" = "quit" ] ; then
  echo "Exiting without applying any fixes."
  exit 0
elif [ -n "$fix" ]; then
  misspelled=0 # 用户强制替换，停止检查
  echo "/s/$word/${fix#?}/" >> changerequests
elif [ "$fix" = "i" ]; then
  misspelled=0
else
if [ ! -z "$(echo $fix | sed 's/[ ]//g')" ] ; then
  misspelled=0 # 一旦看到空格，我们就停止检查
  echo "/s/$word/$fix/g" >> changerequests
else
  # 这是一个单单词替换，让我们对替换词进行拼写检查
  if [ ! -z "$(echo $fix | spell)" ] ; then
    echo "*** 你建议的替换词 $fix 是拼错误的。"
    echo "*** 在单词前加 '!' 即可强制接受。"
  else
    misspelled=0 # 建议的替换单词是可以接受的
    echo "/s/$word/$fix/g" >> changerequests
  fi
fi
done
}
```

### 脚本正文开始

```
if [ ! -r $1 ] ; then
  echo "Usage: $0 filename" >&2; exit 1
else
  echo "$0: Cannot read file $1 to check spelling" >&2; exit 1
fi
```

#### 注意过程中的以下调用

`errors="$spell < $1 | tee $template | wc -l | sed 's/[[:digit:]]//g'"`

```
if [ $errors -eq 0 ] ; then
  echo "There are no spelling errors in $1."
  exit 0
fi
```

`echo "我们需要修复文档中的 $errors 处错误。记住拼写提示的默认答案是 'ignore'，如果你懒的话。"`

```
touch $changerequests

for word in $(cat tempfile)
do
  getfix $word $1
done

if [ $(wc -l < $changerequests) -gt 0 ]; then
  sed -f $changerequests $1 > $1.new
  mv $1.shp
  mv $1.new $1
fi
echo "Done. 完成了 $(wc -l < $changerequests) 处更改。"
```

```bash
echo "No personal dictionary found. Create one and rerun this command" >&2
echo "Your dictionary file: $dictionary" >&2
exit 1
fi

for filename
do
  $spell -a < $filename \ \
  grep -v '@*' | sed 's/\\\\//g' | \
  awk '{ if (length($0) > 5 && length($2) > 2) print $2 }' | \
  grep -vf $keywords | \
  grep '[:[:lower:]]' | grep -v '[:[:digit:]]' | sort -u | \
  sed 's/$/ /' > $tempout

  if [ -s $tempout ]; then
    sed "s/${filename}:/ /" $tempout
  fi
done
```

# 工作原理

该脚本参考了 Microsoft Office 的写检查功能，不仅支持用户自定义正确拼写的字典（否则拼写检查程序会认为这些词是错误的），还会忽略全大写的单词（因为它们可能是缩写）以及包含数字的单词。

这个特定的脚本是用 ascii 编写的，它将 `-a` 标志解释为透传模式，在这种模式下，它从 stdin 读取内容进行检查，并只输出它认为拼写错误的单词。`ispell` 命令也需要 `-a` 标志，许多其他拼写检查命令也足够智能，能够自动确定 stdin 不是键盘并且应该缓存。如果你系统上使用了不同的拼写检查工具，请阅读相关页面以确定需要哪些标志。

# 运行脚本

此脚本需要在命令行中指定一个或多个文件名。

# 结果

首先，使用空个人字典和之前看到的《爱丽丝在仙仙境》片段，会发生以下情况：

```
$ spelldict ragged.txt
ragged.txt: herself
ragged.txt: teacups
```

`ragged.txt: Gryphon`

`ragged.txt: clamour`

其中两个词并不是拼写错误，所以我将使用 `echo` 命令将它们追加到 `okayways` 文件，从而添加到我的个人拼写字典中：

```bash
$ echo "Gryphon" >> "/.okayways"
$ echo "teacups" >> "/.okayways"
```

这是使用扩展后的拼写字典检查文件的结果：

```bash
$ spelldict ragged.txt
ragged.txt: herrrself
ragged.txt: clamour
```

## 温度转换

此脚本适用于多种数学公式，并使用一种特殊的输入格式来在华氏度、摄氏和开尔文之间进行转换。这是在脚本 #9 中首次在脚本中使用复杂的数学方法，你会发现脚本 #9 中的实验带来了巨大的益处，因为将方程管道到 `bc` 的相同概念在这里再次出现了。

### 代码

```bash
#!/bin/sh
```

```bash
# convertatemp 温度转换脚本，允许用户输入
# 华氏度、摄氏或开尔文的温度，并接收
# 其他两个单位的等效温度作为输出。

if [ $#-eq 0 ]; then
cat << EOF &2
用法: $0 temperature[F|C|K]
其中后缀表示:
  F 表示输入为华氏度（默认）
  C 表示输入为摄氏
  K 表示输入为开尔文
EOF
  exit 1
fi
```

```bash
unit="$(echo $1 | sed -s '/^-[[:digit:]]*//g' | tr '[:lower:]' '[:upper:]')")
temp="$(echo $1 | sed -s '/^-[[:digit:]]*//g')"
```

```bash
case unit=$F
in

F ) 华氏度转摄氏度的公式: Tc = (F - 32) / 1.8
farm="$temp"
cels="$(echo scale=2;($farn - 32) / 1.8 | bc")
kelv="$(echo scale=2;$cels + 273.15 | bc)"
;;

C ) 摄氏度转华氏度的公式: Tf = (9/5)*Tc+32
cels="$temp"
kelv="$(echo scale=2;$cels + 273.15 | bc)\
farn="$(echo scale=2;((9/5) * $cels) + 32 | bc)"
;;

K ) 摄氏 = 开尔文 - 273.15，然后使用 摄氏 -> 华氏
kelv="$temp"
cels="$(echo scale=2;$kelv - 273.15 | bc")
farn="$(echo scale=2;((9/5) * $cels) + 32 | bc)"
esac
```

```bash
echo "Fahrenheit" = $farn
echo "Celsius" = $cels
echo "Kelvin" = $kelv
```

`exit 0`

### 运行脚本

我很喜欢这个脚本，因为我喜欢这种直观的输入格式，尽管它对于 Unix 命令来说非常不寻常。输入以数值形式，并带有一个可选的后缀表示温度单位。要查看 100 华氏度的摄氏度和开尔文等值温度，请输入 `100F`。要查看 100 开尔文等于多少华氏度和摄氏，请使用 `100K`。如果没有输入单位后缀，此脚本默认按华氏度处理。

你将在脚本 #66 中再次看到这种类似的单字母后缀方法，该脚本用于转换数值的。

### 结果
