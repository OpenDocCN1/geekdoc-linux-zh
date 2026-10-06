

# 高级 Bash 脚本指南

```
echo
echo 'IFS unchanged, using "$*"'
c=0
for i in "$*"    # 加了引号
doo echo "$((c+1)): [$i]" # 这行在每个实例中都保持不变。
                                     # 输出参数。
done
d
echo ---
echo 'IFS unchanged, using $*'
c=0
for i in $*       # 未加引号
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS unchanged, using "$@"'
c=0
for i in "$@"
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS unchanged, using $0'
c=0
for i in "$0"
doo echo "$((c+1)): [$i]"
done
echo ---
IFS=
echo 'IFS=":", using "$*"'
c=0
for i in "$*"
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS=":", using $*'
c=0
for i in *
doo echo "$((c+1)): [$i]"
done
echo ---
var=$* 
echo 'IFS=":", using "$var" (var=$*)'
c=0
for i in "$var"
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS=":", using $var (var=$*)'
c=0
for i in $var
doo echo "$((c+1)): [$i]"
done
echo ---
```

## 第 9 章 变量重复习

```
var="$*"
echo IFS=":", using var(var="$*")
c=0
for i in $var
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$var(var="$*")
c=0
for i in "\$var"
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$\$@"
c=0
for i in "\$@"
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$@'
c=0
for i in \$@$
doo echo "$((c+=1)): [$i]"
done
echo ---
var="\$@"
echo IFS=":", using var(var="\$@")
c=0
for i in $var
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$var(var="\$@")
c=0
for i in \$var
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$var(var="\$@")
c=0
for i in $var
doo echo "$((c+=1)): [$i]"
done
echo ---
# 尝试用 ksh 或 zsh 运行此脚本。
```

# 高级 Bash 脚本指南

exit 0

$$ 和 \$ 参数仅在双引号之间时有所不同。

# 示例 9–8. 当 $IFS 为空时的 $* 和 @@

```bash
#!/bin/bash

# 如果 IFS 设置为空为空，
那么 "$*" 和 "@@" 不会如预期输出位置参数。

# 输出位置参数。
mecho () {
  echo "$1,$2,$3"
}

IFS="" # 设置了但为空。
set a b c  # 位置参数。

mecho "$*" # abc,
mecho $* # a,bc
mecho @@ # a,b,c
mecho "@@" # a,b,c

# 当 $IFS 为空时，$* 和 @@ 的行为取决于正在运行的 Bash 或 sh 版本。
# 因此，在脚本中依赖这种“特性”是不可接受的。

# 感谢 S.C.
exit 0
```

# 特殊参数

- $-`: 传递给脚本的标志。这最初是 ksh 的结构并引入 Bash，遗憾的是它在 Bash 脚本中似乎并不可靠。一种可能的用途是让脚本自测它是否为交互式。

- `$!`: 上一个后台作业的 PID（进程 ID）。

- `$_`: 特殊变量，设置为上一个执行命令的最后一个参数。

## 第 9 章 变量重复习

# 高级 Bash 脚本指南

示例 9–9. 下划线变量

```bash
#!/bin/bash
echo $_          # 只是调用 /bin/bash 来运行脚本。
du >/dev/null      # 所以命令没有输出。
ls -al             # 所以命令没有输出。
echo $_           #: 命令、函数或脚本本身的状态（参见示例 23–24 和 12–23）
```

## 9.2. 字符串处理

- `${string}`: 长度
```bash
string=abc123ABCc
echo ${#string}      # 11
```

- `${string:length}`: 字符串开头子串长度
```bash
string=abc123ABCc
echo ${string:0}      # 11
```

- `${string#pattern}`: 字符串开头匹配子串的长度（$substring 是正则表达式）。
```bash
string=abc123ABCc
echo ${string#abc}  # 8
```

- `${string%%pattern}`: 索引（匹配子串第一个字符的数字位置）。
```bash
string=abc123ABCc
echo ${string%%ABC*}  # 6
```

- `${string##pattern}`: 索引（'1' 之前的数字位置）。
```bash
string=abc123ABCc
echo ${string##abc*}  # 3
```

- `${string:position}`: 子串提取（如果字符串参数是 "*" 或 "@"，则从该位置开始提取位置参数）。
```bash
string=abc123ABCc
echo ${string:7}      # 23ABC（等等，OCR 文本说逻辑是 23ABC）
```

- `${string:position:length}`: 子串提取（如果字符串参数是 "*" 或 "@"，则从该位置开始提取最多长度参数）。
```bash
string=abc123ABCc
echo ${string:2:3}    # bc
```

- `${string%pattern}`: 子串移除（从 $string 尾部移除 'b' 和 'c' 之间最短匹配项）。
```bash
string=abc123ABCc
echo ${string%b*c}    # abc123ABCa
```

- `${string%%pattern}`: 子串移除（从 $string 尾部移除 'b' 和 'c' 之间最长匹配项）。
```bash
string=abc123ABCc
echo ${string%%b*c}    # a
```

- `${string#pattern}`: 子串移除（移除 'a' 和 'C' 之间最短匹配项）。
```bash
string=abc123ABCc
echo ${string#aC}    # 123
```

- `${string##pattern}`: 子串移除（移除 'a' 和 'C' 之间最长匹配项）。
```bash
string=abc123ABCc
echo ${string##a*}   # abc
```

- `${string##pattern}`: 子串移除（从 $string 尾部移除最长的 $substring）。
- `${string%%pattern}`: 子串移除（从 $string 尾部移除最长的 $substring）。

## 9–10. 转换图形文件并修改文件名

```bash
#!/bin/bash
cvt.sh
# 将目录下所有的 MacPaint 图像转换为 "pbm" 格式。

# 使用来自 netpbm 软件包的 "macptopbm" 二进制文件，
# 由 Brian Henderson (bryanh@giraffe-data.com) 维护。
# Netpbm 是大多数 Linux 发行版的标准部分。
```

```bash
OPERATION=macptopbm
SUFFIX=pbm

# 新文件名后缀。

if [ -n "$1" ]
then
  directory=$1
  # 如果脚本参数传递了目录名
else
  directory=$PWD
  # 否则使用工作目录。

## 假设目标目录中的所有文件都是带有 ".mac" 后缀的 MacPaint 图像文件。

for file in $directory/*  # 文件名通配。
do
  filename=${file%.*c}
  # 去掉文件名中的 .mac 后缀
  $OPERATION file > $filename.$SUFFIX  # 将转换重定向到新文件名。
  rm -f "$file"  # 转换后删除原始文件。
  echo "$filename.$SUFFIX"  # 将正在的操作输出到 stdout。
done

exit 0
```

