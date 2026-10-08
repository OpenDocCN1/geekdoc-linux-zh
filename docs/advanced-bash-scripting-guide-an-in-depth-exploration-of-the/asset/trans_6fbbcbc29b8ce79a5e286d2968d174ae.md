

# 高级 Bash 脚本指南

```
echo $BLANK80
done

# 将前景颜色设置为黑色。
echo -ne '\E[30m'
tput cup 5 0

# 绘制围栏。
echo "----------------------------------------"
echo "----------------------------------------"
tput cup 15 0
echo "----------------------------------------"
echo "----------------------------------------"

# 将前景色和背景色设置为白色。
echo -ne '\E[37;47m'

# 绘制三条白线。
for n in `seq 3`; do
    echo $BLANK80
done

# 将前景颜色设置为黑色。
echo -ne '\E[30m'

# 创建 9 个文件来存储障碍分值。
for n in `seq 10 7 68`; do
    touch $n
done

# 设置第一种将绘制的“马”脚本类型。
HORSE_TYPE=2

# 为每匹“马”创建位置文件和赔率文件。
# 在这些文件中，存储马的当前位置、
# 类型和赔率。
for HN in `seq 9`; do
    touch horse_${HN}_position
    touch odds_${HN}
    echo -1 > horse_${HN}
    echo $HORSE_TYPE >> horse_${HN}
    # 为马定义随机障碍分值。
    HANDICAP=$(random_1_9)
    # 检查 random_1 是否返回了有效值。
    while $HANDICAP [1-9] & /dev/null; do
        HANDICAP=$(random_1_9)
    done
    # 定义马的最后的障碍位置。
    LHP=$(expr $HANDICAP * 7 + 3)
    for FILE in `seq 10 7 $LHP`; do
        echo $HN >> $FILE
    done

    # 计算赔率。
    case $HANDICAP in
        1) ODDS=`echo $HANDICAP * 0.25 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        2) ODDS=`echo $HANDICAP * 0.40 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        4 | 5) ODDS=`echo $HANDICAP * 0.55 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        7 | 8) ODDS=`echo $HANDICAP * 0.75 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        9) ODDS=`echo $HANDICAP * 0.90 + 1.25 | bc`
           echo $ODDS > odds_${HN}
    esac
done
```

```bash
# 打印赔率。
print_odds() {
    tput cup 6 0
    echo -ne '\E[30;42m'
    for HN in seq 9; do
        echo "#$HN odds_${HN}"
    done
}
```

```bash
# 在起始线画马。
draw_horses() {
    tput cup 6 0
    echo -ne '\E[30;42m'
    for HN in seq 9; do
        echo "\\"
    done
}
```

```bash
print_odds
echo -ne '\E[47m'
# 等待按下回车键开始比赛。
# 转义序列 '\E[25l' 会禁用光标。
tput cup 17 0
echo -e "\E[25l]按下任意键开始比赛..."
read -s
```

```bash
# 禁用终端的正常回显显示。
# 这避免了在比赛期间按键可能会“污染”屏幕的情况。

# 开始比赛。
draw_horses
echo -ne '\E[37;47m'
move_and_echo 18 1 $BLANK80
echo -ne '\E[30m'
move_and_echo 18 1 Starting...
sleep 1

# 设置终点线的列。
WINNING_POS=74

# 定义比赛开始的时间。
START_TIME=`date +s`

# 后续 "while" 结构需要的 COL 变量。
COL=0

while [ $COL -lt $WINNING_POS ]; do
  MOVE_HORSE=0

  # 检查 random_1_9 函数是否返回了有效值。
  while echo $MOVE_HORSE | grep [1-9] & /dev/null; do
    MOVE_HORSE=$(random_1_9)
  done

  # 定义“随机马”的旧类型和位置。
  HORSE_TYPE=$(cat horse_${MOVE_HORSE}_position | tail -n 1)
  COL=$(expr `cat horse_${MOVE_HORSE}_position | head -n 1`)

  ADD_POS=1
  # 检查当前位置是否为障碍位置。
  if seq 10 7 6 | grep -w $COL & /dev/null; then
    if grep -w $MOVE_HORSE $COL > /dev/null; then
      ADD_POS=0
      grep -w $MOVE_HORSE $COL > ${COL}_new
      rm -f ${COL}_new
    else
      ADD_POS=1
    fi
  else
    ADD_POS=1
  fi
  COL=$(expr $COL + $ADD_POS)
  echo $COL > horse_${MOVE_HORSE}_position # 存储位置。

  # 选择要绘制的马的类型。
  case $HORSE_TYPE in
    1) HORSE_TYPE=2; DRAW_horse=draw_two
    2) HORSE_TYPE=1; DRAW_horse=draw_one
  esac
  echo $HORSE_TYPE >> horse_${MOVE_HORSE}_position # 存储当前类型。

  # 将前景设置为黑色，背景设置为绿色。
  echo -ne '\E[30;42m'

  # 将光标移动到下一个马的位置。
  tput cup $(expr $MOVE_HORSE + 5)
  cat horse_${MOVE_HORSE}_position | head -n 1
  # 画马。
  $DRAW_horse
  sleep 1

  # 当所有马都超过第 15 行时，重新打印赔率。
  touch field15
  if [ $COL -eq 15 ]; then
    echo $MOVE_HORSE >> field15
  fi
  if [ `wc -l` -eq 9 ]; then
    print_odds
    rm field15
  fi

  # 获取冠军。
  HIGHEST_POS=$(cat field15 | sort -n | head -n 1)

  # 定义比赛结束的时间。
  FINISH_TIME=$(date +s)

  # 输出时间和耗时。
  echo "Winner: $HIGHEST_POS"
  echo "Time: $(expr $FINISH_TIME - $START_TIME) seconds"
done

# 清理临时文件。
rm -f horse_*
```

