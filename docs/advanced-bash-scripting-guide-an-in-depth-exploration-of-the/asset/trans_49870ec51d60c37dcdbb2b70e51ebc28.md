

# 高级 Bash 脚本指南

```bash
# shift _=n $i=$i_"
# 列表中的下一个参数。
if (( n == LIMIT ));
then
  echo $*
  return
fi
for i; do
  echo "-n=$n $i-"
  # "i" 设置为 "@", $n 的原有值。
  (( i > n )) && break
  # 优化。
  (( n % i )) && continue
  # 使用取模运算符过滤掉非素数。
  Primes $n
  # 循环内的递归。
  return
  # 循环外的递归。
  # 连续累积
  # "$8" 是素数的累积列表。
  Primes $n $0 $n
done
```

Primes 1
exit $?

# 将脚本输出管道到 'fmt' 以进行更美的打印。
#比较此生成素数算法与埃拉托尼筛法 (ex68.sh) 的速度。

# 练习：在不递归的情况下重写此脚本。

Rick Boivie 对 Jordi Sanfeliu 树脚本的修订。

# 示例 A-16：显示目录树

```bash
#!/bin/bash
# tree.sh
# 由 Rick Boivie 编写。
# 经许可。
# 这是由 Jordi Sanfeliu（原作者）编写并由 Ian Kjos 补丁的修订和简化版本。
# 此脚本替换了《高级 Bash 脚本指南》之前版本中使用的版本。
# 版权所有 (c) 2002, Jordi Sanfeliu, Rick Boivie, and Ian Kjos.

# 本作者添加的注释。

search () {
  for dir in $(echo '*');
    # --> 列出当前工作目录下的所有文件，
    # --> 不换行。
```

附录 A. 贡献脚本

```bash
# == 与 dir in * 效果类似
# == 但在 dir `echo *` 中无法处理包含空格的文件名。
if [ -d"$dir" ]; then # 如果是一个目录 (-d)...
  # == 临时变量，用于跟踪
  zz=0

  while [ $zz -eq 1 ]; do
    # 跟踪内部嵌套循环。
    echo -n ""
    # == 显示垂直连接符号，
    # == 带有2个空格且无换行
    # 以进行缩进。
    zz=$(expr $zz + 1)
    if [ -L"$dir" ]; then # 如果是一个符号链接...
      echo "$dir" -ls -1 | sed 's/.*$dir //'
      # == 显示水平连接并列出目录名，但...
      # == 删除长列表中的日期/时间部分。
    else
      echo "$dir" -- # 显示水平符号，
      # == 并打印目录名。
      numdirs=$(expr $numdirs + 1) # == 计数加。
      if cd "$dir"; then # 如果可以移动子目录...
        search expr $1 + 1 # == 使用递归调用自身。
        cd ..
      fi
    fi
  done
fi

if [ $# -eq 0 ]; then
  cd "$1" # 移动指定的目录。
else # 留在当前目录
  :
fi
```

echo "初始目录 = `pwd`"
numdirs=0
echo "目录目录 = $numdirs"

exit 0

Patsie 版本的目录树脚本。

# 示例 A-172：交替目录树脚本

```bash
#!/bin/bash
tree2.sh

# 为 ABS Guide 作者进行了微调/格式调整。
# 经脚本作者许可包含在 ABS Guide 中（感谢！）。

## Patsie 编写的递归文件/大小检查脚本
# 此脚本构建文件/目录及其大小列表 (du -akx)
# 并将此列表处理为人类可读的树状。
# 'du -akx' 的效果取决于所有者拥有的权限。
# 因此应以 root 身份运行以获得最佳结果，或仅用于

附录 A. 贡献脚本

## 你具有读取权限的目录。你无法
# ## 读取的不在列表中。

# ABS Guide 建议在以 root 身份运行脚本时要小心：

########## 此处可配置 ##########

```bash
TOP=5 # 最大的前 5 个（子）目录。
MAXRECURS=5 # 最大 5 层子目录/递归深度。
E_BL=80 # 已返回空行。
E_DIR=81 # 未指定目录。
```

########## 不要修改此行以下的任何内容 #

```bash
PID=$$ # 我们的进程 ID。
SELF=$(basename $0) # 我们的程序名。
TMP=$(tmp/$(SELF)).$(PID).tmp # 临时 'du' 结果。
```

```bash
# 将数字转换为千。
function dot { echo $1 | sed -a 's/\.[0-9]*\([0-9]\{3}\)/\1,\2/' | tail -c 12; }
```

```bash
# 用法: tree <递归> <缩进前缀> <最小大小> <目录>
function tree {
  curs=$1 # 我们嵌套了多深？
  prefix=$2 # 在文件/目录名之前显示什么？
  minsize=$3 # 最小文件/目录大小是多少？
  dirname=$4 # 我们创建哪个目录？
}
```

```bash
# 从 TMP 文件获取 (TOP) 最大的子目录/子文件。
LIST=$(grep '^[[:space:]]*$(dirname)/.*' "$TMP" | awk '{if($1)}print $0}' | sort -nr | head -$TOP)
[ -z "$LIST" ] && return 4 # 列表为空，返回。
```

```bash
cnt=0
um=$(echo "$LIST" | wc -l) # 列表中有多少条项。
```

```bash
# 主循环
echo "$LIST" | while read dirname; do
  ((cnt++)) # 计数计数。
  basename=$(basename "$") # 我们只需要项的基本名称。
  [ -d "$basename" ] && basename="$basename/" # 如果是目录，添加斜杠。
  echo "dot $basename" # 显示结果。
```

```bash
# 如果是目录且递归深度未达到太深 $(MAXRECURS)，则也递归调用。
# 递归向上增加：$(curs+1)
# 前缀在是最后一项时获得空格，
# 如果有更多项则获得管道符。
# 最小文件/目录大小变为 $(((minsize/10))).
# 最后一个参数是完整的目录名。
if [ -d "$dirname" ] && [ $curs -lt $MAXRECURS ]; then
  tree "$dirname" "$prefix|" "$((minsize/10))" $((curs+1))
fi
#
Primes $n
done
}
Primes 1
