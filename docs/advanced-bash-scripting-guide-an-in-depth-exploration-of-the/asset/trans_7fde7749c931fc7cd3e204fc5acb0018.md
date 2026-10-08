

# 第 3 部分 基础之外

## 目录

- 9. 变量的重新认识
- 9.1. 内部变量
- 9.2. 变量类型：声明或类型化
- 9.3. $RANDOM：生成随机整数
- 10 变量操作
- 10.1. 字符串操作
- 10.2. 参数替换
- 11 循环与分支
- 11.1. 循环
- 11.2. 嵌套循环
- 11.3 循环控制
- 11.4. 测试与分支
- 12 命令替换
- 13 算术扩展
- 14 休息时间

# 第 9 章 变量的重新认识

使用得当的变量可以增加脚本的威力和灵活性。这需要学习它们的细微之处和差别。

## 9.1. 内部变量

内置变量：
影响 bash 脚本行为的变量

$BASH
Bash 二进制文件本身的路径

```bash
bash$ echo $BASH
/bin/bash
```

$BASH_ENV
一个环境变量，指向在脚本被调用时读取的 Bash 启动文件。

$BASH_SUBSHELL
一个表示子壳层级的变量。这是 Bash 3 版本中新增的变量。

用法请参见示例 21-1。

$BASHPID
当前 Bash 实例的进程 ID（PID）。这与 $$变量不同，但通常给出相同的结果。

```bash
bash4$ echo $$
11015

bash4$ echo $BASHPID
11015

bash4$ ps ax | grep bash4
11015 pts/2	R	0:00 bash4
```

但是...
!/bin/bash

```bash
echo "$ outside of subshell = $"	# 9602
echo "$BASH_SUBSHELL outside of subshell = $BASH_SUBSHELL" # 0
echo "$BASHPID inside of subshell = $BASHPID" # 9602
```

$echo
一个包含 6 个元素的数组，包含有关安装的 Bash 版本的信息。这是 $BASH_VERSION，但更详细一些。

```bash
echo "$ outside of subshell = $"	# 9602
echo "$BASH_SUBSHELL inside of subshell = $BASH_SUBSHELL" # 1
echo "$BASHPID inside of subshell = $BASHPID" # 9603
# 注意 $ 返回的是父进程的 PID。
```

$BASH_INFO[n]

```bash
# Bash 版本信息：
for n in 0 1 2 3 4 5
do
  echo "BASH_INFO[$n] = ${BASH_INFO[$n]}"
done
```

```bash
# BASH_INFO[0] = 3 # 主版本号。
# BASH_INFO[1] = 00 # 小版本号。
# BASH_INFO[2] = 14 # 补丁级别。
# BASH_INFO[3] = 1 # 构建版本号。
# BASH_INFO[4] = release # 发布状态。
# BASH_INFO[5] = 1386-redhat-linux-gnu # 架构
# (与 $MACHYPE 相同)
```

$BASH_VERSION
系统中安装的 bash 版本

```bash
bash$ echo $BASH_VERSION
3.2.25(1)-release
```

```bash
tcsh$ echo $BASH_VERSION
BASH_VERSION: Undefined variable.
```

检查 $BASH_VERSION 是确定正在运行哪个 shell 的良好方法。SHELL 不一定能给出正确答案。

$CDPATH
一个用冒号分隔的搜索路径列表，供 cd 命令使用，功能与用于二进制文件的 PATH 变量类似。$CDPATH 变量可能在 ~/.bashrc 文件中设置。

```bash
bash$ cd bash-doc
bash: bash-doc: No such file or directory
```

```bash
bash$ CDPATH=/usr/share/doc
bash$ cd bash-doc
/usr/share/doc
```

```bash
bash$ echo $PWD
/usr/share/bash-doc
```

$DIRSTACK
目录栈中的值（受 pushd 和 popd 影响）。此内置变量对应 dirs 命令，显示目录栈的所有内容。

$EDITOR
脚本调用的默认编辑器，通常是 vi 或 emacs。

$UID
当前用户的标识数字。UID 并不与 SUID 相同。

$FUNAME
当前函数的名称

```bash
xyz() {
  echo "$FUNAME now executing."
}
xyz()
echo "$FUNAME" # 函数外部的值
```

$GLOBIGNORE
在通配符匹配中排除的文件模式列表。

$GROUPS
当前用户所属的组（数组），记录在 /etc/passwd 中。

```bash
root# echo $GROUPS
0
root# echo ${GROUPS[1]}
1
root# echo ${GROUPS[5]}
6
```

$HOME
用户的家目录，/home/username（见示例 10-7）。

$HOSTNAME
hostname 在启动时分配系统主机。hostname() 函数设置 $HOSTNAME。另见示例 10-7。

$HOSTTYPE
主机类型，类似于 $MACHTYPE，标识硬件。

$IFS
内部字段分隔符。此变量决定 Bash 解析字符串时识别字段或单词边界的方式。,IFS 默认值为空格、制表符和换行符，但可以更改以解析逗号分隔的数据。注意 $* 使用 $IFS 中持有的第一个字符。见示例 5-1。

```bash
bash$ echo "$IFS"
With $IFS set to default, a blank line displays.)bash$ echo "$IFS" | cat -v
(显示空白：这里的空格、水平制表符和换行符。）

$IFS=$(printf '\n\t') # 根据 David Wheeler 设置路径中的空白。,IFS 不像其他字符那样处理空白。

```bash
#!/bin/bash
# ifs.sh

var1="a b"
var2="d e"
var3="g h"

IFS+= # 加号将被解释为分隔符。
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h
```

IFS="-" # 减号恢复为默认解释。减号将被解释为分隔符。
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h

```

IFS="," # 逗号将被解释为分隔符。减号恢复为默认解释。
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h

```

IFS=" " # 空格字符将被解释为分隔符。逗号恢复为默认解释。
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h

############################################
# 然而 $IFS 处理空白的方式与其他字符不同。

output_args_one_per_line() {
  for arg in "$arg"
  do
    echo "[$arg]"
  done # 嵌入括号内供你参考。感谢 Stéphane Chazelas 的澄清和上述示例。）使用 $IFS 的教学示例见 16-41、11-8 和 19-14。

$IGNOREEOF
注销 shell 忽略的文件结束（control-D）数量。

$LC_COLLATE
通常在 .bashrc 或 /etc/profile 中设置，这些变量控制文件名扩展和模式匹配中的排序顺序。LC_COLLATE 可能导致文件名通配符出现意外结果。从 Bash 2.05 版本开始，文件名不再区分字符范围内的大小写字母。例如，ls [A-M] 会匹配 File1.txt 和 file.txt。要恢复习惯的匹配行为，请在 /etc/profile 和/or ~/.bashrc 中通过 export LC_COLLATE=C 将其设置为 C。

$LC_CTYPE

$LINENO 此变量控制通配符和模式匹配中的字符解释。此变量是变量所在的 shell 脚本的行号，且仅出现在变量所在的脚本内，常用于调试。

```bash
### BEGIN DEBUG BLOCK ***
last_cmd_arg=$ 保存它。
echo "At line number $LINENO, variable \"v1\" = $v1"
echo "Last command argument processed = $last_cmd_arg"
### END DEBUG BLOCK ***
```

$MACHTYPE
机器类型标识硬件。

```bash
bash$ $MACHTYPE
i686
```

$OLDPWD
旧工作目录“OLD-Print-Working-Directory”，你之前所在的目录。

$OSTYPE
操作系统类型

```bash
bash$ $OSTYPE
linux
```

$PATH 二进制文件的路径，通常为 /usr/bin/、/usr/X1R6/bin/、/usr/local/bin/ 等。当调用命令时，shell 会对路径中列出的目录进行哈希搜索。路径存储在环境变量 PATH 中，这是一个目录列表。通常，系统使用 /etc/profile 和/or ~/.bashrc 中的 $PATH 定义（见附录 H）。

```bash
bash$ $PATH
/bin:/usr/bin:/usr/local/bin:/usr/X1R6/bin:/sbin:/usr/sbin
```

