

# 高级 Bash 脚本指南

```bash
# Shell 提示符
#-----------

function fastprompt() {
  unset PROMPT_COMMAND
  case $TERM in
    *term | rxvt)
      PS1="[#h] \W > \u033[0;\u007[h] \w\u007";
    )
    *)
      PS1="[#h] \W > "
  esac
}
```

```bash
function powerprompt() {
  _powerprompt() {
    LOAD=$($uptime | sed -e "s/.*([^^*]*).\1/" -e "s //g")
    TIME=$(date +%H:%M)
  }
  PROMPT_COMMAND=_powerprompt
  case $TERM in
    *term | rxvt)
      PS1="$(cyan)[\TIME]NC\u033[0;\u007[h] \w\u007";
    linux)
      PS1="$(cyan)[\TIME]NC\u033[0;\u007[h] \w\u007";
    *)
      PS1="$(cyan)[\TIME]NC\u033[0;\u007[h] \w\u007";
  esac
}
powerprompt # 这是默认设置 - 可能会慢
# 如果慢，请改用 fastprompt。
```

## 别名（ALIASES）与函数
# 可以认为，这里的某些函数非常占用内存，所以
# 如果你想让它更小量，可以将这些函数转换为脚本。许多函数取自 bash-2 示例。

## 个人别名
--------------------------------------------
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
alias h='history'
alias j='jobs'
alias r='login'

## 附录 G. 示例 .bashrc 

```bash
alias ..='type -all'
alias .='cd'
alias path='echo -e ${PATH}'
alias background='- -d &'
alias vi='vim'
alias du='du -h'
alias df='df -kh'

# 'ls' 系列（假设你使用的是 GNU ls）
alias ls='--color' # 为文件类型添加颜色
alias lr='sort -r' # 按扩展名排序
alias ks='-S' # 按大小排序
alias la='-Al' # 显示隐藏文件
alias lm='-ai' # 按日期排序
alias tree='tree -Cs' # 'ls' 的良好替代方案

# 定制 'less'
alias more='less'
export PAGER='less'
export LESSOPEN='|usr/bin/lesspipe.sh' # 如果存在 lesspipe.sh 则使用
export LESS='-i -N -Z -g -e -M -X -F -P -t'

# 拼写错误 - 高度个人化
alias xs='cd'
alias vf='cd'
alias moor='more'
alias moew='more'
alias kk='less'

function {
  case $term in
    *rxvt)
      echo -ne "\033];0*"
    *)
  esac
}

# 别名...
alias top='top on $HOST &'
alias make='make $(basename $PWD)'
alias nftp='nftp'

# 函数
function man () {
  man $(basename $PWD) |tr -d .[:digit:]
  man -a "*"
}

function ll() { ls -1 "$*" | grep "^d"; ls -l "$@" 2>&1 | grep -v "^d|total"; }

function emacs() { command emacs -private 2>&1 && disown }
function te() { # emacs/gnuuser 的封装
{
  if [ "$(gnuclient -eval t 2>&1)" == "t" ]; then
    gnuclient -q "$@"
  else
    emacs "$@" &
  fi
}
```

## 文件与字符串相关函数：

```bash
function ff() { find -name '*$1*' ; } # 查找文件
function fe() { find -name '*$1*' -exec $2 \; \; } # 查找文件并在其上运行 $2
function fstr() { 在一组文件中查找字符串
if [ "@" -gt 2 ]; then
  echo "Usage: fsstr \"pattern\" [files]"
  return;
fi
SMS=$(tput rmso)
RMS=$(tput smso)
find . -type f -name "${2:-*}" -print | xargs grep -sin "$1" | \
sed "s/$1/$SMS$RMS/g"
}

function cutall() # 剪切文件中最后 n 行，默认 10 行
{
lines=${2:-10}
sed -n -e "1,\${lines}p"
}

function lowercase() { # 将文件名转换为小写
{
  for file; do
    filename=${file##*/}
    case "$filename" in
      *)
        dirname="$filename"
        if [ "$file" != "$dirname" ]; then
          echo "lowercase: $file"
        fi
    esac
  done
}

function swap() { # 交换
{
  local TMPFILE=$1
  mv $1 $2
  mv $2 $TMPFILE
}

## 进程/系统相关函数：
function my_ps() { ps -u -o cpu,$mem,command; }
function pp() { ps f; }
function kills() { # 该函数与 'kill' 大致相同，但没有等效对应
local pid=$1
if [ "$#" -lt 1 ] || [#" -gt 2 ]; then
return;
fi
kill $pid
}

function my_ip() { # 获取 IP 地址
{
MY_IP=$(sbin/ifconfig | awk '/inet/ {print $2}')
echo "$MY_IP"
}

function ii() { # 获取当前主机信息
{
MY_IP=$(sbin/ifconfig | awk '/inet/ {print $2}')
echo "$MY_IP"
}

## 杂项工具：
function repeat() { # 重复 n 次命令
local i max
max=$1; shift;
for ((i=1; i<=max; i++)); do
echo "$2"
done
}

function ask() {
echo -n "$@" [y/n]
read ans
case "$ans" in
  y*|Y*) return 0 ;;
*) return 1 ;;
esac

## 可编程补全 - 从 BASH-2.04 起
# (大部分内容取自 bash 2.05 文档)
# 如果实际上需要 bash-2.05 的某些功能
if [ "$BASH_VERSION*" != "2.05" ]; then
    echo 你需要升级到 2.05 版本使用可编程补全
    return
fi

shopt -s extglob
set -o nounset # 否则补全将失败

complete -A hostname rsh telnet rmdir ping
complete -A command nohup exec trace g gdb
complete -A type which
printenv
complete -A export local unset
complete -A variable builtin
complete -A alias unalias
complete -A function function
complete -A user su

complete -A help # 目前与 builtin 相同
complete -A short shopt
complete -A stopped -P '\%%' bg
complete -A job -P '\%%' fg jobs disown

complete -A directory mkdir rmdir
complete -A directory -o default cd

complete -f -d -X '*.gz' gzip
complete -f -o default -X '*.bz2' bzip2
complete -f -o default -X '*.gz' gunzip
complete -f -o default -X '*.bz2' bunzip2
complete -f -o default -X '*.pl*' perl perls1
complete -f -o default -X '*.ps*' gs ghostview ps2pdf ps2ascii
complete -f -o default -X '*.vi*' dvipid select dvitype
complete -f -o default -X '*.+.*' pdf2ps
complete -f -o default -X '*.+(ps)*' gv
complete -f -o default -X '*.txt*' makeinfo texi2divi texi2html texi2pdf
complete -f -o default -X '*.tex*' latex slitex
complete -f -o default -X '*.lyx*
complete -f -o default -X '*.*(jpg|gif|png|bmp)*' xv image
complete -f -o default -X '*.mp3*' mp3123
complete -f -o default -X '*.ogg*' ogg123
```
