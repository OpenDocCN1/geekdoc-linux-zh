

```
alias ll='ls -AFls'
alias la='ls -all'
alias ..='cd ..'
alias ...='cd ../..'
export HISTFILESIZE=5000      # Larger history
export CLICOLOR=1             # Use colors (if possible)
export LSCOLORS=ExGxFxdxCxDxBxBxExEx
```

## 20.2 tcsh

tcsh 和 csh 的重定向和管道（简单的 > 和 >> 与 sh 相同）：

```
# cmd >& file                # Redirect both stdout and stderr to file.
# cmd >>& file               # Append both stdout and stderr to file.
# cmd1 | cmd2                # pipe stdout to cmd2
# cmd1 |& cmd2               # pipe stdout and stderr to cmd2
```

csh/tcsh 的设置保存在 ~/.cshrc 中，使用 "source .cshrc" 重新加载。示例：

```
# in .cshrc
alias ls      'ls -aF'
alias ll      'ls -aFls'
alias la      'ls -all'
alias ..      'cd ..'
alias ...     'cd ../..'
set prompt    = "!%n%b@%m%b:%~%#"  # like user@host/path/todir>
set history   = 5000
set savehist  = ( 6000 merge )
set autolist  # Report possible completions with tab
set visiblebell               # Do not beep, inverse colors
```

```
# Bindkey and colors
bindkey -e    Select Emacs bindings   # Use emacs keys to edit the command prompt
bindkey ^k    up history-search-backward # Use up and down arrow to search
bindkey ^k    down history-search-forward
setenv CLICOLOR 1                # Use colors (if possible)
setenv LSCOLORS ExGxFxdxCxDxBxBxExEx
```

Emacs 模式允许你使用 Emacs 键快捷键来修改命令行提示符。这非常有用（不仅对于 Emacs 用户）。最常用的命令有：

- C-a    将光标移动到行首
- C-e    将光标移动到行尾
- M-b    将光标向后移动一个词
- M-f    将光标向前移动一个词
- M-d    剪切下一个词
- C-w    剪切上一个词
- C-u    剪切光标前所有内容
- C-k    剪切光标后所有内容（行的剩余部分）
- C-y    粘贴最后一次剪切的内容（直接粘贴）
- C-_    撤销

注意：C- 表示按住 Control 键，M- 表示按住 Meta 键（通常是 Alt 或 Esc 键）。

## 21 脚本

基础（第52页） | 脚本示例（第53页） | awk（第53页） | sed（第53页） | 正则表达式（第53页） | 常用命令（第54页）

Bourne shell（/bin/sh）存在于所有 Unix 安装中，用该语言编写的脚本（相当）可移植；man 1 sh 是一个很好的参考。

### 21.1 基础

#### 变量和参数

使用 variable=value 进行赋值，使用 $variable 获取内容。

```
MESSAGE="Hello World"          # Assign a string
PI=3.1415                        # Assign a decimal number
N=8
TWON=`expr $N * 2`               # Arithmetic expression (only integers)
TWON=$(($N * 2))                 # Other syntax
TWOP1=`echo "$PI * 2" | bc -l`  # Use bc for floating point operations
ZERO=`echo "c($PI/4)-sqrt(2)/2" | bc -l`
```

命令行参数如下：

```
$0, $1, $2, ...                  # $0 is the command itself
$#                               # The number of arguments
$*                               # All arguments (also $0)
```

#### 特殊变量

```
$$                               # The current process ID
$?                               # exit status of last command
command
if [ $? != 0 ]; then
    echo "command failed"
fi
mypath=`pwd`
mypath=$mypath//file.txt
echo ${mypath##*/}                # Display the filename only
echo ${mypath%.*}                 # Full path without extension
var2=${var:=string}               # Use var if set, otherwise use string
                                 # assign string to var and then to var2.
```

#### 结构

```
for file in `ls`
do
    echo $file
done

count=0
while [ $count -lt 5 ]; do
    echo $count
    sleep 1
    count=$(($count + 1))
done

myfunction() {
    find . -type f -name "*,$1" -print   # $1 is first argument of the function
}
myfunction "txt"
```

#### 生成文件

```
MYHOME=/home/colin
cat > testhome.sh << _EOF
# All of this goes into the file testhome.sh
if [ -d "$MYHOME" ]; then
    echo $MYHOME exists
else
    echo $MYHOME does not exist
fi
_EOF
sh testhome.sh
```

