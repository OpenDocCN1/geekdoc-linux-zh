

<Ctrl+C> 在执行此程序时。标签处的代码是一个 goto 命令，将控制转移到 onintr 中断命令，以重置代码的中断处理能力，从而有效地忽略 <Ctrl+C>。一个示例运行说明了这一点。

```
% cat onintr_demo
#!/bin/csh

# Intercept <Ctrl+C> and transfer control to the command at
# backagain:
onintr interrupt

# Set the secret code
set secretcode = agent007

# Get user input
echo "Guess the code!"
echo -n "Enter your guess: "
set yourguess = `head -1`

# As long as the user input is not the secret code (agent007 in
# this case), loop here: display a message and take user input
# gain. When the user input matches the secret code, terminate the
# loop and execute the following echo command.
while ( "$secretcode" != "$yourguess" )
 echo "Good guess but wrong. Try again!"
 echo -n "Enter your guess: "
 set yourguess = `head -1`
end
echo "Wow! You are a genius!"
exit 0
# Code executed when you press <Ctrl+C>
interrupt:
 echo "Nice try -- you cannot terminate me by <Ctrl+C>!"
 goto backagain
% ./onintr_demo
Guess the code!
Enter your guess: codecracker
Good guess but wrong. Try again!
Enter your guess: <Ctrl+C>
Nice try -- you cannot terminate me by <Ctrl+C>!
Guess the code!
Enter your guess: Lionking
Good guess but wrong. Try again!
Enter your guess: agent007
```

```
Wow! You are a genius!
%
```

在前面的脚本中使用 onintr 命令的净效果是忽略键盘中断。您可以通过使用带 - 选项的命令来实现相同的效果。因此，onintr_demo 程序中的整个中断处理代码可以用 onintr - 命令替换；在任何标签处都不需要代码，但这样当您按下 <Ctrl+C> 时，代码不会为你显示任何消息。

要终止忽略终端中断的程序，您必须使用 kill 命令。您可以通过按下 <Ctrl+Z> 挂起进程，使用 ps 命令获取进程的进程 ID（PID），然后使用 kill 命令终止它来实现。

您可以修改 onintr_demo 文件中的脚本，使其忽略键盘中断，清除显示屏并关闭回显。这样，无论您在键盘上输入什么，都不会显示。接下来，它会提示您两次输入代码词。如果您两次输入的代码词不同，它会提醒您短期记忆不好并退出。如果您输入相同的代码词，它会清除显示屏并提示您再次猜测代码词。如果您没有输入原始代码词，屏幕将被清除并提示您再次猜测。程序不会在您输入原始代码词之前终止。当您输入它时，显示屏将被清除，一条消息显示在屏幕左上角，回显被打开。由于终端中断被忽略，您无法通过按下 <Ctrl+C> 来终止程序。stty -echo 命令关闭回显。因此，当您输入原始代码词（或任何猜测）时，它不会显示在屏幕上。clear 命令清除显示屏并将光标定位在左上角。stty echo 命令打开回显。 resulting 脚本在 canleave 文件中，如以下会话所示。

```
% cat canleave
#!/bin/csh
# File Name:      ~/unix3e/CShell/canleave
# Author:         Syed Mansoor Sarwar
# Written:        August 18, 2004
# Modified:       May 8, 2004, September 15, 2014
# Purpose:        To allow a user to leave his/her terminal for a
#                 short duration of time by locking the terminal
#                 after taking a code from the user. Terminal is
#                 unlocked only when the user re-enters the same
#                 code. Ignores command line arguments. Does not
#                 terminate with <Ctrl+C>.
# Brief Description:
#                 Clear screen and turn off echo (i.e., do not
#                 display what the user types at the keyboard).
#                 Take user code, save it, and ask the user
```

