

# 高级 Bash 脚本指南

```bash
read name                     # 从重定向的 stdin 读取 ($Filename)
let echo "count += 1"
done                           # 因为第 20 行，循环从文件 $Filename 读取
```

# 此脚本的原始版本通过
# done <"$Filename" 终止了 "while" 循环。
# 练习：
# 为什么这是不必要的？

```bash
exec 0<&3                     # 恢复旧 stdin。
exec 2<&-                      # 关闭临时文件符 3。
echo "$count names read"; echo
```

exit 0

# 示例 20-7. 重定向的 until 循环

```bash
#!/bin/bash
# 与之前的示例相同，但使用了 "until" 循环

if [ -z "$1" ]; then
    Filename=names.data        # 如果未指定文件名，使用默认值
else
    Filename=$1
fi

while [ "$name" != Smith ];
until [ "$name" = Smith ];   # 将 != 改为 =
do
    read name                   # 从 $Filename 读取，而不是 stdin。
    echo $name
done <"$Filename"          # 将 stdin 重定向到文件 $Filename。
~~~~~~~~~~~~~
# 结果与之前示例中的 "while" 循环相同。
```

exit 0

# 示例 20-8. 重定向的 for 循环

```bash
#!/bin/bash

if [ -z "$1" ]; then
    Filename=names.data        # 如果未指定文件名，使用默认值
else
    Filename=$1
fi
```

```bash
line_count=`wc $Filename | awk '{ print $1 }`
# 目标文件的行数。
#
# 尽管这非常牵强且笨拙，但它表明
# 在 "for" 循环内部重定向 stdin 是可能的...
# 只要你足够聪明。
```

# 第 20 章. I/O 重定向

# 高级 Bash 脚本指南

# 更简洁的写法是 line_count=$(wc -l < "$Filename")

```bash
for name in $(seq $line_count); # 回忆 "seq" 会打印数字序列。
while [ "$name" != Smith ]; do -- 比 "while" 循环更复杂
do
  read name
  echo $name
  if [ "$name" = Smith ]; # 我们需要这些额外的负担。
  then
    break
  fi
done <"$Filename" # 将 stdin 重定向到文件 $Filename。
```

exit 0

我们可以修改上一个示例来重定向循环的输出。

# 示例 20-9. 重定向的 for 循环（stdin 和 stdout 都重定向）

```bash
#!/bin/bash
if [ -z "$1" ]; then
  Filename=names.data # 如果未指定文件名，使用默认值。
else
  Filename=$1
fi
Savefile=$Filename.new # 用于保存结果的文件名。
FinalName=Jonah # 用于终止 "read" 的名称。
line_count=`wc $Filename | awk '{ print $1 }'` # 目标文件的行数。
for name in $(seq $line_count);
do
  read name
  echo "$name"
  if [ "$name" = "$FinalName" ];
then
    break
  fi
done < "$Filename" > "$Savefile" # 将 stdin 重定向到文件 $Filename，并保存到备份文件。
exit 0
```

# 示例 20-10. 重定向的 if/then 测试

```bash
#!/bin/bash
if [ -z "$1" ]; then
  Filename=names.data # 如果未指定文件名，使用默认值。
else
  Filename=$1
fi
```

第 20 章. I/O 重定向

```bash
TRUE=1
if [ "$TRUE" ]; then # if 和 if 也可以用。
  read name
  echo $name
fi <"$Filename"
# 只读取文件的第一行。 
# "if/then" 测试没有办法进行迭代，除非嵌入循环中。
exit 0

# 示例 20-11. 上述数据文件名
- Aristotle
- Arrhenius
- Belisarius
- Capablanca
- Dickens
- Euler
- Goethe
- Hegel
- Jonah
- Laplace
- Maroc
- Purcell
- Schmidt
- Schopenhauer
- Semmelweiss
- Smith
- Steinmetz
- Tukhevsky
- Turing
- Venn
- Warsawski
- Znosko
- Borowski

# 这是一个用于 "redir2.sh", "redir3.sh", "redir4.sh", "redir5.sh" 的文件。
# 重定向块的 stdout 效果将其输出保存到文件中。
# 参见示例 20-2。documents 是重定向块的特殊例。

```bash
function doesOutput() {
  # 当然，可以是外部命令。
  # 这里显示你也可以使用函数。
  ls -al | awk '{print $5}'
}

nr=0 # 我们希望循环能够操作这些
totalSize=0 # 以便在 'while' 结束后能够看到变化。

while read fileName; do
  echo "$fileName is $fileSize bytes"
  let totalSize=$((totalSize+fileSize)) # 或者：let totalSize+=fileSize
done<<EOF
$(doesOutput)
EOF

echo "$nr files totaling $totalSize bytes"
```

```bash
#!/bin/bash
# logevents.sh
# 作者: Stephane Chelas.
# 经许可使用。

# 将事件记录到文件。
# 必须以 root 身份运行（为了在 /var/log 中写入权限）。

ROOT_UID=0 # 具有 root 权限。
E_NOTROOT=1 # 非 root 权限。

if [ "$UID" -ne 0 ]; then
    echo "This must be run as root."
    exit 1
fi

# 这里的逻辑可能根据具体需求有所调整
# 示例仅用于结构展示
```
