

## 示例 9.52（续）

```
8   % echo $PERSON
    Joe Jr.
9   % setenv PERSON "Nelly Nerd"
10  % echo $PERSON
    % Nelly Nerd
11  % exit              # Exit the subshell
12  % echo $$
    206
13  % echo $PERSON      # Back in parent shell
    Joe Jr.
```

## 解释

- 1. shell 环境变量 TERM 被设置为 wyse 终端。
- 2. 用户自定义变量 PERSON 被设置为 Joe Jr.。引号用于保护空格。
- 3. 加在变量名前面的美元符号（$）允许 shell 计算变量的内容，称为变量替换。
- 4. 环境变量 PERSON 的值被打印出来。
- 5. $$ 变量包含当前 shell 的 PID。PID 为 206。
- 6. csh 命令启动了一个新的 C shell，称为子 shell。
- 7. 当前 shell 的 PID 被打印出来。因为这是一个新的 C shell，所以它有不同的 PID 号。PID 为 211。
- 8. 环境变量 PERSON 被新 shell 继承。
- 9. PERSON 变量被重置为 Nelly Nerd。此变量将被从该 shell 启动的任何 shell 继承。
- 10. PERSON 变量的新值被打印出来。
- 11. 此 C shell 已退出。
- 12. 原始 C shell 正在运行；为此，PID 206 被打印出来。它与子 shell 启动前相同。
- 13. PERSON 变量包含其原始值。

**打印环境变量。** printenv（BSD）和 env（SVR4）命令（两者在 Linux 中都可用）打印为此 shell 及其子 shell 设置的所有环境变量。setenv 命令在 BSD 和 SVR4 版本的 C shell 上打印变量及其值。

## 示例 9.3

```
(Linux/tcsh Example)

> env or printenv or setenv
USERNAME=root
COLORTERM=rxvt-xpm
HISTSIZE=1000
HOSTNAME=homebound
LOGNAME=ellie
HISTFILESIZE=1000
MAIL=/var/spool/mail/ellie
MACHTYPE=i386
COLORFGBG=default;15
TERM=xterm
HOSTTYPE=i386-linux
PATH=/usr/sbin:/sbin:/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin:/home/ellie/bin:/root/bash-2.03:/usr/X11R6/bin
HOME=/root
SHELL=/bin/bash
PS1=[\u@\h \W]\$ 
USER=ellie
VENDOR=intel
GROUP=ellie
HOSTDISPLAY=homebound:0.0
DISPLAY=:0.0
HOST=homebound
OSTYPE=linux
WINDOWID=37748738
PWD=/home/ellie
SHLVL=6
_= /usr/bin/env
```

## 解释

环境变量为此会话设置，并由从此 shell 启动的所有进程显示，使用以下内置命令之一：env 或 printenv。许多应用程序需要设置环境变量。例如，mail 命令有一个 MAIL 变量设置为用户邮件 spooler 的位置，而 xterm 程序有一个 DISPLAY 变量决定使用哪个位图显示终端。当执行其中任何一个程序时，它们各自变量中的值会被传递给它们。

## 示例 9.34

(UNIX/Solaris/csh Example)

```
% env
FONTPATH=/usr/local/OW3/lib/fonts
HELPPATH=/usr/local/OW3/lib/locale:/usr/local/OW3/lib/help
HOME=/home/jody/ellie
LD_LIBRARY_PATH=/usr/local/OW3/lib
LOGNAME=ellie
MANPATH=/usr/local/man:/usr/local/man:/usr/local/doctools/man:/usr/man
NOSVIEW=0
OPENWINHOME=/usr/local/OW3
PATH=/bin:/usr/local/usr:/usr/bin:/usr/etc:/home/sbin:/usr/doctools:/usr::
PWD=/home/jody/ellie
SHELL=/bin/csh
TERM=sun-cmd
USER=ellie
WINDOW_PARENT=/dev/win0
WINDOW_TTYPARMS=
WNCR_ENV_PLACEHOLDER=/dev/win3
```

### 9.10.4 数组

在 C shell 中，数组只是一个由空格或制表符分隔并用括号括起来的单词列表。数组的元素由从 1 开始的子脚本编号。如果子脚本没有对应的数组元素，则会显示 Subscript out of range 消息。命令替换也会创建数组。如果 $# 记法置于数组名称之前，则会显示数组中元素的数量。

## 示例 9.53

```
1 % set fruit = ( apples pears peaches plums )
2 % echo $fruit
apples pears peaches plums
3 % echo $fruit[1]    # Subscripts start at 1
apples
4 % echo $fruit[2:4]  # Prints the 2nd, 3rd, and 4th elements
pears peaches plums
5 % echo $fruit[6]
Subscript out of range.
6 % echo $fruit[*]    # Prints all elements of the array
apples pears peaches plums
7 % echo $#fruit      # Prints the number of elements
4
```

