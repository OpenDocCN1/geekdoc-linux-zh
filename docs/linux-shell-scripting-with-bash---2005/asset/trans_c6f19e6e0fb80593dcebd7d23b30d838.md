
# 列表 14.9 	 polling.sh

```bash
#!/bin/bash
#
# polling.sh: a daemon using polling to check for new files

shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -rx INCOMING_FTP_DIR="/home/ftp/ftp_incoming"
declare -rx PROCESSING_DIR="/home/ftp/processing"
declare -rx statftime="/usr/bin/statftime"
declare FILE
declare FILES
declare NEW_FILE

printf "$SCRIPT started at %s\n" "$(date)"

# Sanity checks

if test ! -r "$INCOMING_FTP_DIR" ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to read the incoming directory - aborted" >&1
    exit 1
fi
if test ! -x "$PROCESSING_DIR" ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to read the incoming directory - aborted" >&1
    exit 1
fi
if test ! -r "$statftime" ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to find or execute $statftime - aborted" >&1
    exit 1
fi

# Poll for new FTP files

cd $INCOMING_FTP_DIR
while true; do

    # Check for new files more than 30 minutes unchanged
FILES=`find . -type f -mmin +30 -print`

# If new files exist, move them to the processing directory

if [ ! -z "$FILES" ] ; then
    printf "$SCRIPT: new files have arrived at %s\n" "$(date)"
    printf "\n" "$FILES" | {
        while read FILE ; do
            # Remove leading "./"
            FILE="${FILE#./}"
            # Rename the file with the current time
            NEW_FILE="$STATFTIME -f "%L_%T.dat" "$FILE""
            if [ -z "$NEW_FILE" ] ; then
                printf "\n" "$SCRIPT:$LINENO: statftime failed to create a new filename - skipping"
            else
                # Move the file to the processing directory
                printf "\n" "$SCRIPT: moved $FILE to $PROCESSING_DIR/$NEW_FILE"
                mv "$FILE" "$PROCESSING_DIR/$NEW_FILE"
            fi
        done
    }
    sleep 30
done

printf "$SCRIPT finished unexpectedly at %s\n" "$(date)"
exit 1
```

该脚本可以使用*阻塞*代替轮询。通过用 `suspend` 命令替换 `sleep` 命令，脚本将无限期休眠，直到通过 `kill -SIGCONT` 命令唤醒。当一个脚本依赖另一个脚本时，这非常有用。

守护脚本会一直运行，直到它被 `suspend` 或 `kill` 命令停止。它可以启动为在后台运行并自动重启自身：

```bash
$ { ( while true ; do nohup bash polling.sh ; done ; ) \
>/dev/null 2>&1 </dev/null & } &
```

此命令行创建两个进程。外层进程将标准输入、输出和错误重定向到 `/dev/null`，因为它们不再适用。内层进程在 `while` 循环中重复 bash 脚本。当命令提示符返回时，使用 `ps` 命令可以看到 `polling.sh` 脚本正在运行。（可以通过使用 `exec` 在 `while` 循环前关闭标准输入、输出和错误，从而消除其中一个命令分组。）

## Shell 函数

函数是将小型子脚本嵌入 Bash 脚本中的方法，无需将它们保存在单独的文件中。由于它们嵌入在脚本中，因此使用时无需加载。这反过来使它们比单独的脚本运行得更快。像单独的脚本一样，函数可用于将复杂脚本分解为单独的、命名的任务，以提高可读性。

Shell 函数与其他编程语言中的函数不同之处在于，它们返回状态码而不是返回值。由于没有返回值，它们不能用于表达式中。

与变量一样，函数必须在使用之前声明。函数使用 *function* 命令而不是 *declare* 命令进行声明。每个函数都有一个名称，组成函数的语句用花括号包围。参见列表 14.10。

# 列表 14.10 function.sh

```bash
#!/bin/bash
#
# function.sh - A simple function example

declare -rx SCRIPT=${0##*/}
declare -rx TMP="/tmp/temp.$$"
declare -rx TRASH_DIR="$HOME/.trash"

# $TRASH_TMP
#
# Move the TMP file to the trash directory

function trash_tmp {

  if test ! -d "$TRASH_DIR" ; then
    printf "%s\n" "$SCRIPT:$FUNCNAME:$LINENO: trash directory \
$TRASH_DIR is missing" >&2
    exit 1
  fi
  if test -f "$TMP" ; then
    mv $TMP "$TRASH_DIR/."
  fi
}

readonly -f trash_tmp
declare -t trash_tmp

printf "This is a function test\n" > $TMP
trash_tmp

exit 0
```

函数 `trash_tmp` 将 `TMP` 文件移动到用户主目录中名为 `trash` 的目录。函数由 `function` 命令创建，但直到在程序中明确命名才会执行。

`readonly` 命令防止函数被重新定义。该命令将在本章后面详细讨论。

通常，函数不会执行 `DEBUG` 陷阱。`declare -t` 开启函数中的调试陷阱执行。

与脚本类似，函数可以有参数。虽然参数 `$0` 保留脚本的路径名，但其他参数是提供给函数的参数，`$#` 指示参数的数量。当函数完成时，参数变量恢复为之前的值。

`FUNCNAME` 变量在函数执行期间包含函数的名称。在报告错误时使用 `$SCRIPT:$FUNCNAME:` 可以识别发生错误的脚本和函数。

因为函数不是子脚本，函数返回状态码的方式以及声明变量的方式不同。

在脚本中，`exit` 命令返回状态码。在函数中，`exit` 命令退出包含该函数的脚本。要在不退出脚本的情况下返回状态码，函数使用 `return` 命令代替。`return` 语句的使用方式与 `exit` 语句相同。

### 局部变量

在函数内部声明的变量仅在函数持续期间存在。这些被称为*局部变量*。当函数完成时，变量会被丢弃，就像子脚本丢弃变量一样。参见列表 14.11。

# 列表 14.11 function2.sh

```bash
#!/bin/bash
#
# function2.sh: A simple function example with local variables
#
shopt -s -o nounset

declare -rx SCRIPT=$0##*/
declare -rx TMP=/tmp/temp.$$*

# TRASH FILE
#
# Move the specified file to the trash directory
# The first parameter is the file to move

function trash_file {
declare -r TRASH_DIR="$HOME/.trash"

if test ! -d "$TRASH_DIR" ; then
printf "%s\n" "$SCRIPT:$FUNCNAME:$LINENO: trash \
directory $TRASH_DIR is missing" >&2
return 1
fi
if test -f "$1" ; then
mv $1 "$TRASH_DIR"/
fi
return 0
}
readonly -f trash_file
declare -t trash_file

printf "This is a function test\n" > $TMP
trash_file $TMP
if [ $? -ne 0 ] ; then
printf "%s\n" "$SCRIPT:$LINENO: unable to trash $TMP--aborting" >&2
exit 1
fi

exit 0
```

在 function2.sh 中，变量 TRASH_DIR 仅存在于函数 trash_file 内部。当发生错误时，函数不会退出脚本，而是返回一个状态码来指示其是否成功，从而让主脚本决定是否应该退出。

`local` 命令也可以在函数内部声明局部变量并分配初始值。然而，`local` 缺少 `declare` 命令使用的其他开关。因此，最好使用 `declare` 命令代替。

如果未明确声明新变量，当函数完成时，它们不会被丢弃。这种行为是为了与 Bourne shell 保持向后兼容，但可能导致变量意外残留。

```bash
$ function f { COMPANY="NightLight Inc." ; } 
$ f
$ printf "%s\n" "$COMPANY"
NightLight Inc.
```

在此示例中，变量 COMPANY 在微小的 f 函数结束时没有被丢弃，因为它未在 f 内部正式声明。

```bash
$ function f { declare COMPANY="Nightlight Inc." ; }
$ f
$ printf "$a\n" "$COMPANY"
$
```

## 递归和嵌套函数

在 Bash 中，函数可以嵌套或递归使用。局部变量与嵌套函数共享。参见列表 14.12。

# 列表 14.12 factorial.sh

```bash
#!/bin/bash
#
# factorial.sh: A recursive function example
#
shopt -s -o nounset

declare -rx SCRIPT=$0##*/
declare -i REPLY

# FACTORIAL : compute a factorial
#
# $1 is the number to compute the factorial for

function factorial {
	declare -i RESULT=1			# shared with factorial1

	function factorial1 {
		declare -i FACT=$1		# the current number
		let "FACT--"			# deduct one
		if [ $FACT -gt 1 ] ; then
			factorial1 $FACT	# repeat
			let "RESULT=RESULT*FACT"	# and multiply in result
		else
			RESULT=1			# factorial of 1 is 1
		fi
		return				# leave function
	}
}
```

