

## 10.10 存储脚本

在成功创建脚本之后，通常的做法是将它们收集到一个公共脚本目录中，并修改你的路径，以便可以从任何位置执行这些脚本。

### 示例 10.30

```
1  % mkdir ~/bin
2  % mv myscript ~/bin
3  % vi .login

（在 .login 中重置路径以添加 ~/bin。）
4    set path = (/usr/ucb /usr /usr/etc ~/bin .)

5  （在命令行）
% source .login
```

### 说明

- 1. 在你的主目录下创建一个名为 bin 的目录，或者你选择的其他名称。
- 2. 将所有无错误的脚本移动到 bin 目录中。将含有错误的脚本放在这里只会引发问题。
- 3. 进入你的 .login 文件并重置路径。
- 4. 新路径包含目录 ~/bin，shell 将在此目录中查找可执行程序。由于它位于路径的末尾附近，因此与你的脚本同名的系统程序将优先被执行。
- 5. 通过 source .login，路径更改即可生效；无需注销并重新登录。

## 10.11 内置命令

与 UNIX/Linux 命令驻留在磁盘上不同，内置命令是 C/TC shell 内部代码的一部分，并从 shell 内部执行。如果内置命令作为管道中除最后一个以外的任何组件出现，它将在子 shell 中执行。适用于 C 和 TC shell 的内置命令列表见表 10.11。有关仅适用于 TC shell 的内置命令的扩展列表，请参见第 504 页的表 9.25。

### 表 10.11 C 和 TC shell 内置命令及其含义

| 命令 | 含义 |
|---|---|
| : | 解释空命令，但不执行任何操作。 |
| alias | 命令的昵称。 |
| bg [%job] | 在后台运行当前或指定的作业。 |
| break | 跳出最内层的 foreach 或 while 循环。 |
| breaksw | 从 switch 中跳出，在 endsw 之后继续执行。 |
| case label: | switch 语句中的标签。 |
| cd [dir] chdir [dir] | 将 shell 的工作目录更改为 dir。如果未提供参数，则更改为用户的主目录。 |
| continue | 继续执行最近的外层 while 或 foreach 循环。 |
| default: | 在 switch 语句中标记默认情况。default 应放在所有 case 标签之后。 |
| dirs [-l] | 打印目录栈，最近的在左侧；显示的第一个目录是当前目录。使用 -l 参数时，输出不缩写；抑制使用 ~ 符号。 |
| echo [-n] list | 将 list 中的单词写入 shell 的标准输出，以空格字符分隔。除非使用 -n 选项，否则输出以换行符结束。 |
| eval command | 将 command 作为 shell 的标准输入运行，并执行生成的命令。这通常用于执行由命令或变量替换生成的命令，因为解析发生在这些替换之前（例如，eval `tset -s options`）。 |
| exec command | 在当前 shell 的位置执行 command，当前 shell 随之终止。 |
| exit [(expr)] | 退出 shell，使用 status 变量的值或 expr 指定的值。 |
| fg [% job] | 将当前或指定的作业带入前台。 |
| foreach var (wordlist) | 参见第 561 页的“foreach 循环”。 |
| glob wordlist | 对 wordlist 执行文件名扩展。类似 echo，但不识别转义字符（\）。输出中单词以空字符分隔。 |
| goto label | 参见第 547 页的“goto”。 |

### 表 10.11 C 和 TC shell 内置命令及其含义（续）

| 命令 | 含义 |
|---|---|
| hashstat | 打印一行统计信息，说明内部哈希表在定位命令（以及避免 exec）方面的有效性。对于路径中哈希函数指示可能命中的每个组件，以及每个不以反斜杠开头的组件，都会尝试一次 exec。 |
| history [-hr] [n] | 显示历史列表；如果给出 n，则仅显示 n 个最近的事件。- r 反转打印顺序，使最近的事件先于最旧的事件显示。- h 显示不带前导编号的历史列表。这用于生成适合使用 source 的 -h 选项进行 source 的文件。 |
| if (expr) | 参见第 535 页的“条件结构和流程控制”。 |
| else if (expr?) then | 参见第 535 页的“条件结构和流程控制”。 |
| jobs [-l] | 在作业控制下列出活动作业。- l 在正常信息之外还列出 ID。 |
| kill [-sig] [pid[%job] ...] kill -l | 默认情况下或按指定信号，向指定 ID、指定作业或当前作业发送 TERM（终止）信号。信号以数字或名称给出。没有默认值。键入 kill() 不会向当前作业发送信号。如果发送的信号是 TERM（终止）或 HUP（挂断），则还会向作业或进程发送 CONT（继续）信号。- l 列出可以发送的信号名称。 |
| limit [-h] [resource [max-use]] | 限制当前进程或其产生的任何进程的资源消耗，每个进程在指定资源上不超过 max-use。如果省略 max-use，则打印当前限制；如果省略 resource，则显示所有限制。- h 使用硬限制而不是当前限制。硬限制对当前限制的值设置了上限。只有超级用户可以提高硬限制。resource 是以下之一：cputime，每个进程的最大 CPU 秒数；filesize，允许的最大单个文件；datasize，进程的最大数据大小（包括堆栈）；stacksize，进程的最大堆栈大小；coredump，核心转储的最大大小；descriptors，文件描述符的最大值。 |
| login [username -p] | 终止登录 shell 并调用 login(1)。不处理 .logout 文件。如果省略 username，login 会提示输入用户名。- p 保留当前环境（变量）。 |
| logout | 终止登录 shell。 |

