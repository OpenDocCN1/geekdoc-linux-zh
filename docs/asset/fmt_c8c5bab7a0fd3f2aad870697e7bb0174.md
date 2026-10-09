
# 第 4 部分 命令

# 高级 Bash 脚本指南

## 附录：常用命令列表

- `readelf`
- `readlink`
- `readonly`
- `reboot`
- `recode`
- `renice`
- `reset`
- `resize`
- `restore`
- `rev`
- `rlogin`
- `rm`
- `rmdir`
- `rmod`
- `route`
- `rpm`
- `rpm2cpio`
- `rsh`
- `rsync`
- `runlevel`
- `run-parts`
- `rx`
- `rz`
- `sat`
- `scp`
- `script`
- `diff`
- `sed`
- `seq`
- `service`
- `set`
- `setfacl`
- `setquota`
- `setserial`
- `setter`
- `sha1sum`
- `shar`
- `shopt`
- `shred`
- `shutdown`
- `size`
- `skill`
- `sleep`
- `slocate`
- `snice`
- `sort`
- `source`
- `sox`
- `split`
- `sq`
- `ssh`
- `stat`
- `strace`
- `strings`
- `strip`
- `stv`
- `su`
- `sudo`
- `sum`
- `suspend`
- `swapoff`
- `swapon`
- `sx`
- `sync`
- `sz`
- `tac`
- `tail`
- `tar`
- `tbl`
- `tcpdump`
- `tee`
- `telinit`
- `telnet`
- `Tex`
- `texexec`
- `time`
- `times`
- `tmpwatch`
- `top`
- `touch`
- `tput`
- `tr`
- `traceroute`
- `true`
- `tset`
- `tsort`
- `tty`
- `tune2fs`
- `type`
- `typeset`
- `ulimit`
- `umask`
- `umount`
- `uname`
- `umarc`
- `unari`
- `uncompress`
- `unexpand`
- `uniq`
- `units`
- `ulzma`
- `unrar`
- `unset`
- `unsq`
- `unzip`
- `uptime`
- `usmodules`
- `useradd`
- `userdel`
- `userm`
- `users`
- `usleep`
- `uucp`
- `uudecode`
- `uuencode`
- `uux`
- `vacation`
- `vdir`
- `vmstat`
- `vrfy`
- `w`
- `wait`
- `wall`
- `watch`
- `wc`
- `wget`
- `whatis`
- `whereis`
- `which`
- `who`
- `whoami`
- `whois`
- `write`
- `xargs`
- `xrandr`
- `xz`
- `yacc`
- `yes`
- `zcat`
- `zdiff`
- `zgrep`
- `zfgrep`
- `zgrep`
- `zip`

# 目录

- 15. 内部命令与内置命令
  - 15.1 作业控制命令
- 16. 外部过滤器、程序与命令
  - 16.1 基础命令
  - 16.2 复杂命令
  - 16.3 时间/日期命令
  - 16.4 文本处理命令
  - 16.5 文件与压缩命令
  - 16.6 通信命令
  - 16.7 终端控制命令
  - 16.8 数学命令
  - 16.9 杂项命令
- 17. 系统命令
  - 17.1 系统命令

# 高级 Bash 脚本指南

旧版本的 `Bash` 可能不支持 `printf`。

## 示例 15-2. `printf` 的实际应用

```bash
#!/bin/bash
# printf demo

declare -r PI=31.4159265358979  # 只读变量，即常量。
declare -r DecimalConstant=31373

Message1="Greetings,"
Message2="Earthling."
echo

printf "PI to 2 decimal places = %1.2f" $PI
echo
printf "PI to 9 decimal places = %1.9f" $PI  # 它能正确进行四舍五入。

printf "\n"                          # 打印换行符，
                              # 等于 'echo' . .

printf "Constant = %t\d" $DecimalConstant  # 插入制表符 (\t)。

printf "%s %s \n" $Message1 $Message2
echo
===============================================
# 模拟 C 函数 sprintf().
# 使用格式化字符串加载变量。
echo
PI2=$(printf "%1.12f" $PI)
echo "PI to 12 decimal places = $PI2"  # 舍入误差！
Msg=$(printf "%s %s \n" $Message1 $Message2
echo $Msg; echo $Msg

# 恰好，'sprintf' 函数现在可以作为
#+ 可加载模块到 Bash 中访问，
#+ 但这不是可移植的。

exit 0
```

格式化错误信息是一个非常有用的 `printf` 用例。

```bash
E_BADDIR=85
var=nonexistent_directory
error() {
    printf "$$" >&2
    # 格式化传递的位置参数，并将其发送到标准错误 (stderr)。
    echo
    exit $E_BADDIR
}
cd $var || error "Can't cd to %s." "$var"
```

# 第 15 章 内部命令与内置命令

## 高级 Bash 脚本指南

感谢 S.C.。

另见示例 36-17。

读取变量 `stdin` 的值，即从键盘交互式获取输入。

`-r` 允许获取数组变量（参见示例 27-6）。

## 示例 15-3. 使用 `read` 进行变量赋值

```bash
#!/bin/bash
# "读取" 变量

echo -n "Enter the value of variable 'var1':"
# -n 选项抑制换行符。

read var1
# 注意 var1 前面没有 '$'，因为它 正在被赋值。

echo "var = $var1"

echo

# 单个 'read' 语句可以设置多个变量。
echo -n "Enter the values of variables 'var2' and 'var3'"
echo -n "(separated by a space or tab):"
read var2 var3
echo var2=$var2 var3=$var3
# 如果你只输入了一个值，
#+ 其他变量将保持保持未设置状态（空）。

exit 0
```

没有赋值变量的 `read` 会将输入存到专用的 `$REPLY` 中。

## 示例 15-4. 当 `read` 没有变量时会发生什么

```bash
#!/bin/bash
# read-novar.sh
echo

#-
echo -n "Enter a value:"
read var
echo "$var" = "$var"
# 这里都是符合预期的。
#-

echo

#-
echo -n "Enter another value:"
read # 为 'read' 未提供变量，因此...
#+ 输入到 'read' 被赋值给默认变量 $REPLY
var=$REPLY
echo "$var" = "$var"
# 这等同于第一个代码块。
```

# 第 15 章 内部命令与内置命令

## 高级 Bash 脚本指南

```bash
echo
echo "================"
echo

# 这个示例与 "reply.sh" 脚本类似。
# 然而，这个示例显示即使在以常规方式向变量
#+ 读取后，$REPLY 仍然可用。

# 在某些情况下，你可能希望丢弃第一个读取的值。
# 在这种情况下，只需忽略 $REPLY 变量即可。

# 代码块。
read          # 第 1 行，将被丢弃。
read line2    # 第 2 行，保存在变量中。
echo "$REPLY"
echo "Line 2 of this script is:"
echo "$line2"      # read-novar.sh
echo                  # /bin/bash 行被丢弃。

# 参见 soundcard-on.sh 脚本。
```

通常情况下，输入 `\` 在 `read` 期间抑制换行符。`-r` 选项允许输入的 `\` 被字面解释。

## 示例 15-5. `read` 的多行输入

```bash
#!/bin/bash
echo
echo "Enter a string terminated by a \ , then press <ENTER>."
echo "Then, enter a second string (no \ this time), and again press <ENTER>"
read -r var1      # 当读取 $var1 时，\ 抑制了换行符。
                  # 第一行 \
                  # 第二行
echo var1 = "$var1"
          # 第一行第二行

# 对于每一行以 \ 结尾的行
#+ 你会在下一行获得一个提示，以继续向 var1 输入字符。
echo; echo
echo "Enter another string terminated by a \ , then press <ENTER>."
read -r var2  # -r 选项导致 "\" 被字面读取。
              # 第一行 \
echo var2 = "$var2"
      # 第一行
```

# 第 15 章 内部命令与内置命令

## 高级 Bash 脚本指南

`read` 命令有一些有趣的选项，允许回显提示并读取按键。

- `-s`: 意味着不显示输入。
- `-n`: 仅接受 `N` 个字符的输入。
- `-p`: 在读取输入之前显示以下提示。

使用这些选项很微妙，因为它们需要处于正确的顺序。`read` 的 `-n` 选项还允许检测箭头键和某些不寻常键。

### 示例 15-6. 检测箭头键

```bash
#!/bin/bash
# arrow-detect.sh: 检测箭头键以及其他几个键。
# 感谢 Magi 向我展示。
------------------------------------
# 键位生成的字符代码。
arrowup='A'
arrowdown='B'
arrowright='C'
arrowleft='D'
insert='Z'
delete='3'
------------------------------------

SUCCESS=0
OTHER=65

echo -n "Press a key..." # 如果按了未列出的键，可能需要按 ENTER。
read -n 3 key # 读取 3 个字符。

echo -n "$key" | grep "$arrowup" # 检查是否检测到字符代码。
if [ "$key" -eq $SUCCESS ]; then
    echo "Up-arrow key pressed."
    exit $SUCCESS
fi

echo -n "$key" | grep "$arrowdown"
if [ "$key" -eq $SUCCESS ]; then
    echo "Down-arrow key pressed."
    exit $SUCCESS
fi

echo -n "$key" | grep "$arrowright"
if [ "$key" -eq $SUCCESS ]; then
    echo "Right-arrow key pressed."
    exit $SUCCESS
fi

echo -n "$key" | grep "$arrowleft"
if [ "$key" -eq $SUCCESS ]; then
    echo "Left-arrow key pressed."
    exit $SUCCESS
fi

echo -n "$key" | grep "$insert"
if [ "$key" -eq $SUCCESS ]; then
    echo "Insert key pressed."
    exit $SUCCESS
fi

echo -n "$key" | grep "$delete"
if [ "$key" -eq $SUCCESS ]; then
    echo "Delete key pressed."
    exit $SUCCESS
fi

echo "Some other key pressed."
exit $OTHER

# ==========================================
# Alexander 提出了上述脚本的简化版本（感谢！）。
# 它消除了对 grep 的需要。
```

```bash
#!/bin/bash

uparrow='[A'

downarrow='[B'

leftarrow='[D'

rightarrow='[C'

read -s -n 3 p "Hit arrow key: " x

case $x in

$uparrow)

    echo "You pressed up-arrow"

    ;;

$downarrow)

    echo "You pressed down-arrow"

    ;;

$leftarrow)

    echo "You pressed left-arrow"

    ;;

$rightarrow)

    echo "You pressed right-arrow"

    ;;

esac

exit $?
```

`Antonio Macchi` 有更简单的替代方案。

```bash
#!/bin/bash

while true

do

    read -snl a

    test "$a" == 'echo -e' || continue

    read -snl a

    test "$a" == "[" || continue

    read -snl a

    case "$a" in

        A) echo "up";

        B) echo "down";

        C) echo "right";

        D) echo "left";

    esac

done
```

```
# ==================================================

# 练习：
- 1) 添加对“Home”、“End”、“PgUp 和 PgDn”键的检测。
- `read` 的 `-r` 选项不会检测 ENTER 键。
- `read` 的 `-t` 选项用于超时输入（参见示例 9-4 和 A-41）。
- `-u` 选项接收目标文件的描述符。
- `read` 命令可以从重定向到 `stdin` 的文件中赋值值。如果文件包含多行，只有第一行会被赋值给变量。如果 `read` 有多个参数，则这些变量中的每个将获得一个连续的空格分隔字符串。

注意！
```

## 示例 15-7. 使用重定向使用 `read`

```bash
#!/bin/bash

read var1 <data-file

echo var1 = $var1

# var1 被赋值为输入文件 "data-file" 的整个第一行

read var2 <data-file

echo var2 = $var2 var3 = $var3

# 注意 "read" 不符合直觉的行为

# 1) 回置到输入文件的开头。

# 2) 每个变量现在被赋值一个相应的由空格分隔的字符串，

#   而不是整行文本。
```

# 高级 Bash 脚本指南

## 追加内容

```bash
# 3) 最后一个变量获取行的剩余部分。

# 4) 如果需要设置的变量比文件第一行中空白分隔的字符串

#   多，则多余的变量将保持为空。

echo "----------------------------------------------------------------------"
```

```bash
# 如何使用循环解决上述问题：

while read line; do

  echo "$line"

done <data-file

# Heiner Steven 指出这一点。

echo "----------------------------------------------------------------------"
```

```bash
# 使用 IFS（内部字段分隔符变量）来将输入行拆分

# 给 "read" 命令，如果你不希望默认使用空白作为分隔符。

echo "所有用户列表"

IFS=$IFS; IFS=":" # /etc/passwd 使用 ":" 作为字段分隔符。

while read name passwd uid fullname ignore; do

  echo "$name ($fullname)"

done </etc/passwd  # I/O 重定向。

IFS=$IFS  # 恢复原始的 $IFS。

# 此代码段由 Heiner Steven 增加。
```

```bash
# 在循环内部设置 $IFS 变量

## 就可以消除了将原始 $IFS 存储

## 在临时变量中的需要。

# Dim Segebart 指出这一点。
```
