

# 高级 Bash 脚本编写指南

```bash
echo
echo "Simple page creator"
echo "Author: Mendel Cooper"
echo "License: GPL3"
echo; echo; echo
}
```

```bash
prohame () 
{
    echo -n "Program name? "
    read name

    echo -n "Manpage section? [按回车键默认值 ("1")] "
    read section
    if [ -z "$section" ]
    then
        section=1 # 大多数 man页都在第 1 部分。
    fi

    if [ -n "$name" ]
    then
        savefile="$name".$section" # 文件名后缀 - section。
        echo -n "$1" >>$savefile
        name=$(echo "$name" | tr a-z A-Z) # 转换为大写，
        echo -n "$name" >>$savefile # 根据 man页命名规范。
    else
        echo "Error! No input." # 强制输入。
        exit $E_NOINPUT # 关键！
        # 练习：如果没有文件名输入就中止脚本有点笨拙。
        # 重写这部分以使用默认文件名
    fi

    echo -n "\$name\">>$savefile # 追加，始终追加。

    echo -n "Version? " 
    read ver
    echo -n "\Version \$ver>>$savefile

    echo -n "简短描述 [0 5 个单词]" 
    read dsdesc
    echo "$NameHeader">>$savefile
    echo "$BOLD "$name">>$savefile
    echo "-\$dsdesc>>$savefile
}
```

```bash
fill_in () {
    # 这个函数或或少是从 "pad.sh" 脚本复制的。
    echo -n "$2? " # 获取用户输入。
    read var
    # # 可以粘贴（仅限单行！）来填充字段。
    if [ -n "$var" ]
    then
        echo "$1 " >>$savefile
        echo -n "$var" >>$savefile
    else
        # # 不要向文件添加空字段。
        return $E_NOINPUT # 这里不关键。
    fi
}
```
```

附录 A. 贡献脚本

```bash
echo >>$savefile
}
end() {
    clear
    echo -n "你是否想查看保存的 man 页 (y/n)? "
    read ans
    if [ "$ans" = "n" -o "$ans" = "N" ]; then exit; fi
    exec less "$savefile" # 退出脚本并将控制权移交给 "less" ... 它将对 man 页源码进行格式化。
}
```

```bash
# #######################################################
start
programme "$TopHeader" "Synopsis"
fill "$DesHeader" "Long description"
# 可以传入“单行”文本。
fill "$OptHeader" "Options"
fill "$FilesHeader" "Files"
fill "$AuthHeader" "Author"
fill "$BugsHeader" "Bugs"
fill "$AlsoHeader" "See also"
# 根据需要传入 "$OtherHeader" ...
end
# 不需要退出。
```

- # 注意，生成的 man 页通常
## 需要使用文本编辑器进行手动微调。
## 然而，与从头开始编写 man 源相比，
## 即使编辑空白的 man 页模板，
## 也是显著的改进。

- # 脚本的主要缺陷是它允许
## 在输入字段中只粘贴单行文本。
## 这可能是一个很长的连接在一起的行，它会自动换行并连字符。
## 但是，如果你想要多个（由换行符分隔的）参数，
## 必须在脚本生成的 man 页上
## 通过 man 编辑来插入。
## 练习（困难）：修复此！

- # 这个脚本并不像全功能的
## "manedit" 软件包那样复杂。
## http://freshmeat.net/projects/manedit/
## 但用起来简单得多。

## 示例 A-40，花瓣

```bash
#!/bin/bash -i
# petals.sh
```

```bash
# #######################################################
# 玫瑰花瓣
## 版本 0.1 Sergey Rodin 创建
## 版本 0.2 由 ABS 修改
```

附录 A. 贡献脚本

```bash
# Advanced Bash 编写指南

# 许可证: GPL3
# 在 ABS 指中使用。
# ###########################
hits=0      # 正确次数。
WIN=6       # 赢了。
ALMOST=5   # 差。
EXIT=$     # 脚本生成的随机种子。

# 骨架 (ASCII)
bone[1]="   O"
bone[2]="   O"
bone[3]="   O"
bone[4]="   O"
bone[5]="   O"
bone[6]="   O"
bone*="----------"

# 函数
instructions () {
  clear
  echo -n "你需要说明吗？ (y/n) "; read ans
  if [ "$ans" = "y" || "$ans" = "Y" ]; then
    clear
    echo -e '\e[34;47m' # 蓝色。
    echo <<INSTRUCTIONS
游戏名为 Petals Around Rose（玫瑰花瓣），这是有意义的。
每次掷骰是零或偶数。
在你猜测之后，你会得到骰子的答案，但这就是你获得的所有信息。
连续六次猜测将让你进入玫瑰协会。
INSTRUCTIONS
    echo -e "\e[0m" # 关闭。
  else
    fi
}
```

附录 A. 贡献脚本

```bash
fortune () {
  RANGE=7
  FLOOR=0
  while [ "$number" -le $FLOOR ];
  do
    number=$RANDOM
    let "number %= $RANGE" # 1-6。
  done
  return $number
}
```

```bash
throw () { # 计算每个骰子。
    fortune; B1=$?
    fortune; B2=$?
    fortune; B3=$?
    fortune; B4=$?
    fortune; B5=$?

calc () { # 嵌套函数！
    case "$1" in
      3) rose=2;
      5) rose=4;
      *) rose=0;
    esac
    # 简化算法。
    # 并没有触及核心。
    return $rose
}
```

```bash
answer=$0
calc "$B1"; answer=$((expr answer + $(echo))
calc "$B2"; answer=$((expr answer + $(echo))
calc "$B3"; answer=$((expr answer + $(echo))
calc "$B4"; answer=$((expr answer + $(echo))
calc "$B5"; answer=$((expr answer + $(echo))
```

```bash
game () {
  # 生成骰子的图形显示。
  throw
  echo -e "\e33[1m" # 粗体。
  echo -e "\n"
  echo -e "$bone$bone$bone"
  echo -e "$bone[$B1]bone[$B2]bone[$B3]bone[$B4]bone[$B5]"
  echo -e "_"
  echo -e "$bone[$B1]bone[$B2]bone[$B3]bone[$B4]bone[$B5]"
  echo -e "_"
  echo -e "$bone[$B1]bone[$B2]bone[$B3]bone[$B4]bone[$B5]"
  echo -e "$bone$bone$bone"
  echo -e "\n\n\n"
  echo -e "\e33[0m" # 关闭粗体。
}
```

# 附录 A. 贡献脚本

```bash
echo -n "玫瑰周围有多少花瓣？ " 
}
```

# ====================================================================

instructions
while [ "$petal" != "$EXIT" ] # 主循环。
do
  game
  read petal
  echo "$petal" | grep [0-9] /dev/null # 过滤数字响应。

  if [ "$?" -eq 0 ]; then # if循环 #1
  then
    if [ "$petal" == "$answer" ]; then # if循环 #2
      echo -e "\n正确。玫瑰周围有 $petal 片花瓣。\n"
      (( hits++))

      if [ "$hits" -eq "WIN" ]; then # if循环 #3
        echo -e "\e[31;47m"      # 红色。
        echo -e "\e[03l1m"                        # 粗体。
        echo "你解开了花瓣的秘密！"
        echo "你解开了花瓣的秘密！"
        echo -e "\e[0m" # 关闭。
        break
      else
        echo -e "\n零或偶数。
        在你猜测之后，你会得到骰子的答案，但这就是你获得的所有信息。
        连续六次猜测将让你进入玫瑰协会。
        echo -e "\e[0m" # 关闭。
      fi
    else
      echo -e "\n错误。玫瑰周围有 $petal 片花瓣。\n"
    fi
  fi
done
```

