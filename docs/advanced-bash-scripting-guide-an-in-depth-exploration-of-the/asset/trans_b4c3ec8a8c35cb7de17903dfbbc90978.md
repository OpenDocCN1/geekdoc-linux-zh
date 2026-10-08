

# 高级 Bash 脚本指南

```bash
do
echo -n "$number 
done
echo
exit 0
```

这里是一个使用命令替换来创建[列表]的稍微复杂一点示例：

# 示例 11-8. 针对二进制文件的 grep 替代方案

```bash
#!/bin/bash
# bin-grep.sh: 在二进制文件中查找匹配的字符串。

# 一个针对二进制文件的 "grep" 替代方案。
# 效果类似于 "grep -a"

E_BADARGS=65
E_NOFILE=66

if [ $# -ne 2 ];
then
    echo "Usage: $0 basename search_string filename"
    exit $E_BADARGS
fi

if [ ! -f "$2" ];
then
    echo "File \$2" does not exist.\n    exit $E_NOFILE
fi

IFS=$'\01'
# 根据 Anton Filippov 的建议。
# 原为：IFS=$'\' | grep "$1"
for word in $strings; do
    echo "$2" | grep "$1"
    do
    echo $word
done

# "strings" 命令列出二进制文件中的字符串。
# 输出通过给 "grep"，用于测试所需的结果。

# 正如 S.C. 指出的，第 23 - 30 行可以用更简单的替换
strings "$2" | grep "$1" | tr -s "$IFS" '[\n*]'
```

# 示例 11-9. 列出系统上的所有用户

```bash
#!/bin/bash
# userlist.sh

PASSWORD_FILE=/etc/passwd
```

尝试运行类似 "./bin-grep.sh /bin/ls" 命令
# 以练习此脚本。

exit 0
更多类似的内容。

第 11 章 循环与分支

# 高级 Bash 脚本指南

```bash
n=1 # 用户编号
for name in $(awk 'BEGIN[FS=":"]{print $1}' < "$PASSWORD_FILE")
# 字段分隔符 = =
^^^^^^
# 打印第一个字段
^^^^^^^
# 从密码文件 /etc/passwd 获取输入 ^^^^^^^^^^^^^^^^^^
do
  echo "USER $n = $name"
  let n += 1
done

# USER #1 = root
# USER #2 = bin
# USER #3 = daemon
#...
# USER #33 = bozo
```

exit?

# 讨论：
# 为什么普通用户或由其运行的脚本
# 可以读取 /etc/passwd（提示：检查 /etc/passwd 文件权限）。
这是一个安全漏洞吗？为什么或者为什么不是？
另一个由命令替换产生的[列表]示例。

# 示例 11-10. 检查目录中所有二进制文件的所有者

```bash
#!/bin/bash
# findstring.sh
# 在指定目录的二进制文件中查找特定字符串
directory=/usr/bin/
fstring="Free Software Foundation" # 查看哪些文件来自 FSF。

for file in $(find $directory -type f -name '*' | sort)
do
  strings = $file | grep "$fstring" | sed -e "s/$directory%%"
  # 在 "sed" 表达式中，
  #+ 有必要替换普通的 "/"分隔符
  # 因为 / 恰好是被过滤掉的字符之一。
  # 未替换会导致错误信息。（试一下。）
done
```

exit?
# 练习（简单）：
#----
# 将此脚本转换为接收命令行参数
#+ 用于 $directory 和 $fstring。
这是[列表] / 命令替换的最后一个示例，但这次“命令”是一个函数。

```bash
generate_list ()
{
  echo "one two"
}
for word in $(generate_list) # 让 "word" 获取函数的输出。
```

```bash
do
echo "$word"
done
# one
# two
# three
```

for 循环的输出可以传递给一个或多个命令。

# 示例 11-11. 列出目录中的符号链接

```bash
#!/bin/bash
# symlinks.sh: 列出目录中的符号链接。

directory=${1:-pwd}
# 默认值为当前工作目录，
+# 除非另有指定。
+# 等同于下面的代码块。
#-
# ARGS=1
# 期望一个命令行参数。

if [ $ -ne "$ARGS" ]; then # 如果参数不是 1...
then
  directory=$(pwd) # 当前工作目录
else
  directory=$$1
fi
```

```bash
echo "symbolic links in directory \$(find $directory -type 1)" # -type 1 = 符号链接
for file in \$(find $directory -type 1)
do
  echo "$file"
d | sort
# 严格来说，这里并不需要循环，
# 因为 "find" 命令的输出会被展开为单行。
# 然而，这样做易于理解且具有说明性。
```

> 正如 Dominik "Aeneas" Schnitzer 指出的，
## 未引用 $ (find $directory -type 1)
## 会导致包含空格的文件名崩溃。
# 包含空格。

exit 0

```bash
echo "symbolic links in directory \$directory*"
# 备份当前的 IFS。越审慎越好。
OLDIFS=$IFS
IFS=' 	
'
```

```bash
for file in $ (find $directory -type 1 -printf "%p\n$IFS")
do
#
```

# 第 11 章 循环与分支

# 高级 Bash 脚本指南

```bash
echo "$file"
done | sort

# 使用逗号运算符计数 10。
# 标准语法。
for a in 1 2 3 4 5 6 7 8 9 10
done

echo; echo
# ============================

# 使用 "seq" ...
for a in `seq 10`
do
    echo -n "$a "
done
```

```
# ============================

# 使用花括号扩展 ...
for a in {1..10}
do
    echo -n "$a "
done
```

```
# ============================

# 现在，让我们使用双括号来完成相同操作。
```bash
LIMIT=10
for ((a=1; a<=LIMIT; a++))
do
    echo -n "$a "
done
```

```
# ============================

# 让我们使用逗号运算符来增加两个变量。
```bash
for ((a=1, b=1; a<=LIMIT; a++, b++))
do
    # 逗号连接了操作。
    echo -n "$a-$b "
done
```

```
# ============================

# 最后，执行工作。
```
```bash
exit
```

