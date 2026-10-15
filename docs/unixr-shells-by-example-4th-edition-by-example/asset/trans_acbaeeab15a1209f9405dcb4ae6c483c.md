

## 第11章 交互式Korn Shell

### 11.1 引言

使用交互式Shell时，标准输入、输出和错误都连接到终端。当你在Korn（ksh）Shell中交互式操作时，你会在ksh提示符下输入UNIX/Linux命令，然后等待响应。交互式Korn Shell结合了UNIX Bourne Shell和C Shell的优点，为你提供了大量内置命令和命令行快捷方式，例如历史记录、别名、文件和命令补全等。David Korn扩展了他的Shell，加入了更多功能，比如使用vi和emacs进行命令行编辑、新的元字符、协同处理和错误处理。Korn Shell非常流行，虽然它起源于AT&T，但已经适配到大多数操作系统中运行。

本章重点介绍如何在命令行上与ksh交互，以及如何定制你的工作环境。你将学习如何利用所有快捷方式和内置功能，以创建一个高效且有趣的工作环境。第12章将进一步深入。到那时，你将准备好编写ksh Shell脚本，通过自动化日常任务和开发复杂的脚本，进一步为自己定制工作环境；如果你是管理员，不仅为自己，也为整个用户群体这样做。

### 11.1.1 启动

在Korn Shell显示提示符之前，会先经过一系列进程。（参见图11.1.1。）第一个运行的进程叫做init，PID为1。它从名为inittab的文件（System V）获取指令，或者产生一个getty（BSD）进程。这些进程打开终端端口，提供输入来源（stdin）以及标准输出（stdout）和标准错误（stderr）的出口，并在屏幕上显示登录提示符。然后执行/bin/login程序。登录程序提示你输入密码，加密并验证密码，设置初始环境，然后启动登录Shell，即/bin/ksh，这是passwd文件中的最后一个条目。ksh程序查找系统文件/etc/profile并执行其中的命令。然后它在用户的主目录中查找名为.profile的初始化文件，以及一个环境文件，通常称为.kshrc。执行这些文件中的命令后，美元符号提示符出现在屏幕上，Korn Shell等待命令输入。

![](img/60a0b5d254bd6007403850f972cbfad8_620_0.png)
![](img/60a0b5d254bd6007403850f972cbfad8_621_0.png)

### 11.2 环境

### 11.2.1 初始化文件

在/etc/profile中的命令执行之后，会执行用户主目录中的初始化文件。首先执行.profile，然后执行ENV文件，通常称为.kshrc文件。

**/etc/profile文件。**

/etc/profile是一个系统级可读文件，由系统管理员设置，用于在用户登录且Korn Shell启动时执行任务。它对系统上所有Bourne和Korn Shell用户可用，通常执行诸如检查邮件队列中是否有新邮件、显示/etc/motd文件中的当日消息等任务。以下文本是/etc/profile的示例。关于/etc/profile每一行的完整解释，请参见第321页的第8章“Bourne Shell编程”。

**示例11.1**

```
# The profile that all logins get before using their own .profile
trap "" 2 3
export LOGNAME PATH  # Initially set by /bin/login
if [ "$TERM" = "" ]
then
    if /bin/i386
    then  # Set the terminal type
        TERM=AT386
    else
        TERM=sun
    fi
    export TERM
fi
# Login and -su shells get /etc/profile services.
# -rsh is given its environment in the .profile.
case "$0" in
-sh | -ksh | -jsh )
    if [ ! -f .hushlogin ]
    then
        /usr/sbin/quota
    fi
# Allow the user to break the Message-Of-The-Day only.
trap "trap ' ' 2" 2
/bin/cat -s /etc/motd
# Display the message of the day
trap "" 2
/bin/mail -E
case $? in
0)  # Check for new mail
echo "You have new mail."
;;
2) echo "You have mail."
;;
esac
fi
esac
umask 022
trap 2 3
```

**.profile文件。**

.profile文件是用户自定义的初始化文件，在登录时由Bourne和Korn Shell执行一次，位于你的主目录中。它使你能够自定义和修改你的工作环境。环境变量和终端设置通常在此处设置；如果某个窗口应用程序或dm需要启动，也是从这里启动的。如果.profile文件中包含一个特殊变量ENV，那么赋给该变量的文件名将接下来被执行。ENV文件是

