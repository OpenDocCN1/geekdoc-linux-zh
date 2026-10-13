
![](img/3def70414996f811615f713b2077a154_476_0.png)

## 附录 D

### Shell 函数库

本附录包含第 21 章“使用函数解决问题”中的完整 shell 函数库。库可通过以下 URL 下载：

http://www.csua.berkeley.edu/~ranga/downloads/tysp2/libtysp2.sh

### LISTING D.1 库 libTYP S2.sh 的列表

```sh
# Name: printError
# Desc: prints an error message to STDERR
# Args: $0 -> message to print

printError () {
  echo "ERROR: $0" 1>&2
}

# Name: printWarning
# Desc: prints a message to STDERR
# Args: $0 -> message to print

printWarning () {
  echo "WARNING: $0" 1>&2
}
```

### LISTING D.1 继续

```sh
# Name: promptYESNO
# Desc: Asks a yes/no question
# Args: $1 -> The prompt
#       $2 -> The default answer (optional)
# Global: YESNO -> set to the users response y for yes, n for no

promptYESNO () {
    YESNO=""

    if [ "${1:-t}" ] ; then
        return 1
    fi

    _YNPROMPT="$1 (y/n)? "
    _YNDEFANS=""

    case "$2" in
        [yY][eE][sS] ) _YNDEFANS="y" ;;
        [nN][oO] ) _YNDEFANS="n" ;;
    esac

    _YNPROMPT="$_YNPROMPT[${_YNDEFANS:-[${_YNDEFANS}]}] "

    while :
    do
        printf " $_YNPROMPT"
        read YESNO
        case "${YESNO:-${_YNDEFANS}}" in
            [yY][eE][sS] )
                YESNO="y"
                break
                ;;
            [nN][oO] )
                YESNO="n"
                break
                ;;
            * ) YESNO="" ;;
        esac
    done

    unset _YNPROMPT _YNDEFANS
    export YESNO
    return 0
}

# Name: promptRESPONSE
# Desc: Asks a question
# Args: $1 -> The prompt
```

### LISTING D.1 继续

```bash
# $2 -> The default answer (optional)
# Globals: RESPONSE -> set to the users response

promptRESPONSE () {
    RESPONSE=""

    if [ $# -lt 1 ] ; then
        return 1
    fi
    _RDEFANS="${2:2:$2}"
    _RPROMPT="${1} [${_RDEFANS}:${_RDEFANS}] "

    while :
    do
        printf '%s' "$_RPROMPT"
        read RESPONSE
        RESPONSE="${RESPONSE:-$_RDEFANS}"
        if [ -n "$RESPONSE" ] ; then
            break
        fi
    RESPONSE=""
    done
    unset _RDEFANS _RPROMPT
    export RESPONSE
    return 0
}

# Name: getSpaceFree
# Desc: Outputs the space avail for a directory
# Args: $1 -> The directory to check

getSpaceFree () {
    if [ $# -ge 1 ] ; then
        df -k "$1" 2>/dev/null | awk 'NR != 1 { print $4; }'
        return 0
    fi
    return 1
}

# Name: getSpaceUsed
# Desc: output the space used for a directory
# Args: $1 -> The directory to check

getSpaceUsed () {
    if [ -d "$1" ] ; then
        du -sk "$1" | awk '{ print $1; }'
```

### LISTING D.1 继续

```sh
return $?
return 1
}
# Name: getPID
# Desc: Outputs a list of process id matching $1
# Args: $1 -> the command name to look for
getPID() {
    if [ $# -lt 1 ]; then
        return 1
    fi
    PSOPTS="-ef"
    /bin/ps $PSOPTS | grep "$1" | grep -v grep | awk '{ print $2; }'
}
# Name: getUID
# Desc: outputs a numeric user id
# Args: $1 -> a user name (optional)
getUID() {
    id $1 | sed -e 's/(.*// ' -e 's/^uid=//'
}
# Name: toLower
# Desc: changes an input string to lower case
# Args: $0 -> string to change
toLower() {
    echo $0 | tr '[A-Z]' '[a-z]' ;
}
# Name: toUpper
# Desc: changes an input string to upper case
# Args: $0 -> string to change
toUpper() {
    echo $0 | tr '[a-z]' '[A-Z]'
}
```

![](img/3def70414996f811615f713b2077a154_480_0.png)

## 索引

### 符号

& (ampersand), 后台进程, 106
&& 和复合运算符, 273
-atime 选项, find 命令, 301
` (backquote), 命令替换, 143
\ (反斜杠)
echo 命令转义序列, 155-156
换行字符, 154
引用, 148-149
tr 命令, 239
#| bin/sh, 404
{ } (大括号), while 语句, 286
-c 选项, uniq 命令, 242

$ 字符, 10
; 字符, 12
: 字符, 24
shell 命令, 294-296
if 语句, 295
while 语句, 295-296
/ 字符, 53
# 字符, 注释, 30
- 字符, getopts 命令, 206
+ 字符, shell 跟踪, 333
: (冒号), 420
;; 命令, case 语句, 175
. 命令, 在其他文件中包含函数和变量定义, 409
--ftime 选项, find 命令, 301

$ (美元符号)
字段运算符, 269
换行字符, 153
使用双引号进行引用, 151
" (双引号), 引用, 150
-exec 操作, find 命令, 303-304
-f 选项, tail 命令, 234
-i 选项, grep 命令, 236
-k 选项, sort 命令, 243
-l 选项, grep 命令, 238
[>] (小于号), 引用, 150
^M (回车) 从文件中删除, 415-416

-m 选项, uname 命令, 393
$ (元字符), 252
* (元字符), 252
. (元字符), 252
\ (元字符), 252
-mtime 选项, find 命令, 301
-n 选项, 328
find 命令, 300
grep 命令, 327
sort 命令, 242-243
$? 变量, 198
^ (否定运算符), 254
! 运算符, 171
until 循环, 187
>> 运算符, here 文档, 80
|= 运算符, test 命令, 169
|| 运算符, 171, 408
&& 运算符, 171, 408
|| (或) 复合运算符, 273
% (百分号), 作业编号前缀, 109
. (句点), 39, 420
-print 操作, find 命令, 303
-r 选项
sort 命令, 242-243
uname 命令, 393
-s 选项, tr 命令, 240
[<>] (重定向符号), eval 命令, 294
; (分号), 148
awk 命令, 269

! 符号, find 命令, 303
' (单引号), 过滤, 244
-size 选项, find 命令, 302
-type 选项, find 命令, 300
$USAGE 变量, 202
-v 选项, 351
grep 命令, 236-237
$? 变量, 198
$# 变量, 198, 203
$* 变量, 198
$@ 变量, 198
与 $* @ 相比, 204
$0 变量, 198-199, 404
用法语句, 199-200
$? 变量, 198
$@ 变量, 198
与 $* 相比, 204
变量值, 124
* 通配符
basename 命令, 202
通配, 136
* 通配符, 通配, 139
? 通配符, 通配, 138
常见错误, 138-139
-x 选项, 332

### A

a- 选项, 39
绝对路径名, 56
find 命令, 299
抽象, 可移植性, 397-400
账户, 14

操作 (find 命令)
-exec, 303-304
-print, 303
适应性, init 脚本, 372-373
addperson 脚本, 378-379
地址簿, 373-374
添加人员, 377-380
删除人员, 380-383
交互模式, 377
列出人员, 375-377
非交互模式, 377
ALARM 信号, 处理函数, 321
alias 命令, 217
别名, 217, 420
C shell, 16
显示路径名, 206
函数, 比较, 217-218
unalias, 218
ampersand (&), 后台进程, 106
锚定, 正则表达式, 254-256
and-and 运算符 (&&), 273
将输出追加到文件, 78
参数, 200
basename 命令, 201
模拟, 202
cd 命令, 59
逐一考虑, 409
示例, 201
转发到另一个命令, 410

函数, 执行, 215-216
mkdir 命令, 63
使用 xargs 命令将参数传递给命令, 304
shell 跟踪, 335
故障排除, 203-205
算术
be 命令, 307
expr 命令, 306
算术表达式, 425
算术替换, 144
常见错误, 145-146
运算符, 144-145
优先级, 145
数组变量, 121-127, 427
数组
访问值, 127-128
索引, 126
表示法, 126
支持数组, 427
为变量赋值, awk, 276
赋值运算符, 数值表达式, 278-279
将文件与文件描述符关联, 82-83
AT&T System V UNIX
参见 System V UNIX
awk
调用语法, 250
操作, 250-251
与 sed 对比, 250

awk 命令, 268-269
比较运算符, 271-272
复合表达式, 273
next 命令, 273-274
字段编辑, 269-270
流程控制, 283
do 语句, 286
for 语句, 286-288
if 语句, 284-285
while 语句, 285
使用其格式化地址簿, 375
FS, 282
数值变量, 277
特定模式操作, 270-271
STDIN 作为输入, 274-275
变量, 276
数值表达式, 276-283

### B

后台进程, 106-107
fg 命令, 110
需要输入, 107-108
将前台进程移至, 108-110
防止终止, 110
等待, 111

backquote (`), 命令替换, 143
backslash (\), 148-149
echo 命令转义序列, 155-156
换行字符, 154
backslash 字符 (\), tr 命令, 239
basename 命令, 201-202, 412
bash (Bourne Again shell), 17, 15
导出变量, 130
初始化, 25
在线资源, 34
Bash shell
整数表达式, 425
支持数组, 427
通配符, 430

bc 命令, 307-308
蜂鸣, 使用 sleep 命令发出一系列, 297
BEGIN 模式, 数值表达式, 279-280
Berkeley Software Distribution (BSD), 390
bg, 420
bg 命令, 109
位桶, 405
块特殊文件, 94
Bourne Again shell (bash), 17
数组, 125
初始化, 25
在线资源, 34
通配符, 430
