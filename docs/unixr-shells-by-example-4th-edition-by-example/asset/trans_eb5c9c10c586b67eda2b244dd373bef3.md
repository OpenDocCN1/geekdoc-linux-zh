

# 可执行语句和 Bourne Shell 构造。

Bourne shell 程序由 UNIX 命令、Bourne shell 命令、编程构造和注释的组合构成。

## 使脚本可执行。

当你创建文件时，它不会被赋予执行权限。你需要此权限来运行脚本。使用 chmod 命令打开执行权限。

### EXAMPLE 8.1

```
1  $ chmod +x myscript
2  $ ls -lF myscript
-rwxr-xr-x  1 ellie  0 Jul 13:00 myscript*
```

### EXPLANATION

- 1 chmod 命令用于为用户、组和其他人打开执行权限。
- 2 ls 命令的输出表明所有用户对 myscript 文件都有执行权限。文件名末尾的星号也表明这是一个可执行程序。

## 脚本会话。

在以下示例中，用户在编辑器中创建脚本。保存文件后，执行权限被打开，然后执行脚本。如果程序中有错误，shell 会立即响应。

### EXAMPLE 8.2

```
(The Script)
1  #!/bin/sh
2  # Scriptname: greetings
# Written by: Barbara Born
# This is the first Bourne shell program of the day.
3  echo "Hello $LOGNAME, it's nice talking to you."
4  echo "Your present working directory is `pwd`."
   echo "You are working on a machine called `uname -n`."
   echo "Here is a list of your files."
5  ls      # List files in the present working directory
6  echo "Bye for now $LOGNAME. The time is `date +%T`!"

(The Command Line)
7  $ chmod +x greetings
   $ greetings
3  Hello barbara, it's nice talking to you.
```

### EXAMPLE 8.3

(The Script)

```
#!/bin/sh
# Scriptname: nosy
echo "Are you happy? \c"
1 read answer
echo "$answer is the right response."
echo "What is your full name? \c"
2 read first middle last
echo "Hello $first"
```

(The Output)

```
Are you happy? Yes
1 Yes is the right response.
2 What is your full name? Jon Jake Jones
Hello Jon
```

### EXPLANATION

- 1. read 命令接受一行用户输入并将输入分配给变量 answer。
- 2. read 命令从用户接受输入并将输入的第一个词分配给变量 first，第二个词分配给变量 middle，其余所有词直到行尾分配给变量 last。

### EXAMPLE 8.4

(The Script)

```
#!/bin/sh
# Scriptname: printer_check
# Script to clear a hung up printer for SVR4
1 if [ $LOGNAME != root ]
then
    echo "Must have root privileges to run this program"
    exit 1
fi
2 cat << EOF
Warning: All jobs in the printer queue will be removed.
Please turn off the printer now. Press Enter when you
are ready to continue. Otherwise press Ctrl-C.
EOF
3 read ANYTHING    # Wait until the user turns off the printer
echo
4 /etc/init.d/lp stop    # Stop the printer
```

```
5  rm -f /var/spool/lp/SCHEDLOCK /var/spool/lp/temp
   echo
   echo "Please turn the printer on now."
6  echo "Press Enter to continue"
7  read ANYTHING        # Stall until the user turns the printer back on
   echo                # A blank line is printed
8  /etc/init.d/lp start  # Start the printer
```

### EXPLANATION

- 1. 检查用户是否为 root。如果不是，则发送错误并退出。
- 2. 创建一个 here 文档。警告信息显示在屏幕上。
- 3. read 命令等待用户输入。当用户按下 Enter 时，变量 ANYTHING 接受所键入的内容。该变量未用于任何用途。此处的 read 用于等待用户关闭打印机，返回后按下 Enter。
- 4. lp 程序停止打印机守护进程。
- 5. 在调度程序重新启动之前，必须删除 SCHEDLOCK 文件，以及 /var/spool/lp 中的临时文件。
- 6. 提示用户在准备好时按下 Enter。
- 7. 用户键入的任何内容都被读入变量 ANYTHING，并在按下 Enter 后程序将恢复执行。
- 8. lp 程序启动打印守护进程。

## 8.3  算术

算术并未内置于 Bourne shell。如果需要执行简单的整数算术计算，UNIX expr 命令在 Bourne shell 脚本中最常用。对于浮点算术，可以使用 awk 或 bc 程序。由于算术未内置，shell 在循环迭代多次时的性能会下降。每次在循环机制中递增或递减计数器时，都需要 fork 另一个进程来处理算术。

### 8.3.1  整数算术和 expr 命令

expr 命令是一个表达式处理程序。当用于计算算术表达式时，它可以执行简单的整数运算（参见表 8.2）。其每个参数必须用空格分隔。支持 +, −, *, /, 和 % 运算符，并且正常的编程结合性和优先级规则适用。

