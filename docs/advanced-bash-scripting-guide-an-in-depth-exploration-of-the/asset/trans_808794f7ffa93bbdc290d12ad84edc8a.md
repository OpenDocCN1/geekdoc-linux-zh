
```bash
repeat = "$spaces1"
echo -n "*"
repeat = "$spaces2"
echo -n "*"
repeat = "$spaces2"
echo -n "|"
```

```bash
sequence=$(echo $seq 0 $disks | tac)
for disk in $sequence; do
  for rod in {1..3}; do
    eval empty=$(( (Rods)[$disk] / 2 ))
    eval fill=$(Rods)[$disk]
    repeat = "Empty"
    test $fill -ne 0 && echo $fill || echo -n "|"
    repeat = "Empty"
  done
done
repeat = "$basewidth " # 在柱子下方打印“底部”。
echo
```

```bash
display() {
  echo
  PrintRods
}

# 获取柱子编号、顶部元素和重量
first=$(FromRod $1)
eval Rod$(first[0])=${first[1]}=0

# 获取柱子编号和空闲位置
second=$(ToRod ${first[2]} '$2')
eval Rod$(second[0])=${second[1]}=${first[2]}

echo; echo
if [ "${Rods[3][last_move]}" -eq 1 ];
then
  # 是最后一步吗？如果是，则显示最终位置。
  echo "+ Final Position: $Moves moves"; echo
  PrintRods
fi
```

# 从这里开始，与原始 (hanoi.bash) 脚本几乎相同。

dohanoi() {
  # 递归函数。
  case $1 in
    0)
      return;
      )
    *)
      dohanoi "$($1-1))" $2 $4 $3
      if [ "$Moves" -ne 0 ];
      then
        echo "+ Position after move $Moves"
      fi
      ((Moves++))
      echo -n "  Next move will be: "
      echo $2 "--" $3
  esac
}

setup_arrays ()
{
  local dim n elem

  let diml=$1 - 1
  elem=$diml

  for n in $(seq 0 $diml)
  do
    let "Rod1[$elem] = 2 * $n + 1"
    Rod2[$n]=0
    Rod3[$n]=0
    ((elem--))
  done
}
```

### Main DISKS
setup_arrays $DISKS
echo echo "+ Start Position"
case $# in
1) case $(($1>0)) in
1) # 必须至少有一个盘子
  disks=$1
  dohanoi 1 3 2
  Total moves = 2^n - 1, 其中 n = 盘子的数量。
  echo
  exit 0
;;
*)
  echo "$0: Illegal value for number of disks"
  exit $E_BADPARAM
;;
esac
;;
*
clear
echo "usage: $0 N"
echo " Where \N" 是盘子的数量。"
exit $E_NOPARAM
;;
esac
```

# Note：
# 将脚本输出重定向到文件，否则它会超出屏幕。

## Example A-49. 汉诺塔，交替图形版本

Appendix A. Contributed Scripts

# 高级 Bash 脚本指南

```bash
#! /bin/bash
# 汉诺塔
# 原始脚本 (hanoi.bash) 版权 (C) 2000 Amit Singh.
# 保留所有权利。
# http://hanoi.kernelthread.com

（注：后续部分已根据逻辑清理去除了 OCR 产生的重复碎片）
