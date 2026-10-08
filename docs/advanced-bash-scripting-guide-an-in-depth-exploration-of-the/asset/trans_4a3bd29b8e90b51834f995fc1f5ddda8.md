

# 高级 Bash 脚本指南

```bash
clear
echo -e '\E[31;47m' # 红色前景。'\E[34;47m' 为蓝色。
cat <<INSTRUCTION1

QUACKEY 是 Perquay [TM] 的一个变体。
规则相同，但计分方式经过简化，允许使用之前出现过的单词的复数形式。
*易受攻击* 模式尚未实现，但在其他功能上已完备。

游戏开始时，玩家将获得 10 个字母。
目标是从字母集中构造出长度至少 3 个字母的有效字典单词。
单词长度分类：
-- 3 字母、4 字母、5 字母、...
当分类被录入单词填满后，
将不再接受该分类中的其他单词。

单词过短（2 个字母）、重复、无法构造以及
无效（不在字典中）的单词惩罚分为 -200。尝试在已满的分类中输入单词
也适用相同的惩罚。

```
INSTRUCTION1
echo -n "按回车键查看说明页。 "; read
cat <<INSTRUCTION2

计分方式大部分对应 Perquay：
第一个 3 字母单词得 60 分，后续每个额外加 60 分。
第一个 4 字母单词得 120 分，后续每个加 20 分。
第一个 5 字母单词得 200 分，后续每个加 50 分。
第一个 6 字母单词得 300 分，后续每个加 100 分。
第一个 7 字母单词得 500 分，后续每个加 150 分。
第一个 8 字母单词得 750 分，后续每个加 250 分。
第一个 9 字母单词得 1000 分，后续每个加 500 分。
第一个 10 字母单词得 2000 分，后续每个加 2000 分。

分类完成奖金：
3 字母单词 100 分
4 字母单词 200 分
5 字母单词 400 分
6 字母单词 800 分
7 字母单词 2000 分
8 字母单词 10000 分
这是对极其荒诞且复杂的 Perquay 奖金计分系统的简化。

```
INSTRUCTION2
echo -n "按回车键查看最后的说明页。 "; read
cat <<INSTRUCTION3

仅单词输入的时间限制最长为 10 秒。
*** 输入超时将结束游戏。***
除此外，游戏是不限时的。

附录 A. 贡献的脚本

游戏统计数据将自动保存到文件中。

对于竞技（“重复”）对战，可以通过重复脚本的随机种子（命令行参数 $1）来复制先的字母集。
例如，`qky 7633` 指定了字母集为
cadifrhusk...

```bash
IN3
echo -n "按回车键开始游戏."; read
	echo -e "\033[0m" # 关闭红色。
	fi

clear
}
```

```bash
seed_random() {
	if [ -n "$randomseed" ]; # 可以指定随机种子。
	then # 用于竞技模式。
	RANDOM="$randomseed"
	echo "RANDOM set to $randomseed"
	else
	randomseed="$$" # 或从进程 ID 获取随机种子。
	echo "RANDOM seed not specified, set to Process ID of script ($$)"
	fi
}

RANDOM="$randomseed"
echo
}
```

```bash
get_letset() {
	element=0
	echo -n "Letterset"
	for letset in $(seq $NVLET)
	do # 选取字母填满字母集。
	LS[element]=${letters[$((RANDOM%numelements))]}
		((element++))
	done
	echo
	echo "${LS[0]}"
}
```

附录 A. 贡献的脚本

```bash
Status[3]=""
Status[4]=""

while [ "${Words[idx]}" != '' ]
do
  if [ "${Words[idx]}" = "$wrd" ];
  then
    Status[3]=Duplicate-word-PENALTY
    let Score[0]= - PENALTY
    let Score[1]=$PENALTY
    return
  fi

  ((idx++))
done

Words[idx]="$wrd"
get_score
}

get_score() {
  local wlen=0
  local score=0
  local bonus=0
  local first_word=0
  local add_word=0
  local numwords=0

  wlen=$(wrd)
  numwords=$(Score[wlen])
  Score[2]=0
  Status[4]="" # 将 "bonus" 初始化为 0。

  case $wlen in
    3) first_word=60;
     add_word=0;
    4) first_word=120;
     add_word=20;
    5) first_word=200;
     add_word=50;
    6) first_word=300;
     add_word=100;
    7) first_word=500;
     add_word=150;
    8) first_word=750;
     add_word=250;
    9) first_word=1000;
     add_word=500;
    10) first_word=2000;
     add_word=2000;
  esac

  Category complete bonuses:
  3-letter words 100
  4-letter words 200
  5-letter words 400
  6-letter words 800
  7-letter words 2000
  8-letter words 10000
  这是对极其荒诞且复杂的 Perquay 奖金计分系统的简化。

```

