

## 表 9.25 `tcsh` 内建命令及其含义（续）

| 命令 | 含义 |
|---|---|
| `eval arg ...` | 将参数视为 shell 的输入并在当前 shell 的上下文中执行由此产生的命令(组)。这通常用于执行作为命令或变量替换结果而生成的命令，因为解析在这些替换之前发生。 |
| `eval command` | 将 command 作为 shell 的标准输入运行并执行由此产生的命令。这通常用于执行作为命令或变量替换结果而生成的命令，因为解析在这些替换之前发生（例如，`eval 'tset -s options'`）。 |
| `exec command` | 代替当前 shell 执行 command，当前 shell 终止。 |
| `exit [(expr)]` | 退出 shell，使用状态变量的值或 expr 指定的值退出。 |
| `fg [%job]`<br>`%job` | 将当前或指定的作业带到前台。`fg` 内建命令的同义词。 |
| `filetest -op file ...` | 对每个文件应用 op（即文件查询操作符）并以空格分隔的列表形式返回结果。 |
| `foreach name (wordlist)`<br>`end` | 参见第 566 页的“循环控制命令”。 |
| `foreach var (wordlist)` | 参见第 561 页的“The foreach Loop”。 |
| `getspath` | 打印系统执行路径。 |
| `getxvers` | 打印实验版本前缀。 |
| `glob wordlist` | 对 wordlist 执行文件名展开。与 echo 类似，但不识别转义（\）。单词在输出中以空字符分隔。 |
| `goto label` | 参见第 547 页的“The goto”。 |
| `goto word` | word 是文件名并经过命令替换以产生形如“label”的字符串。shell 尽可能回绕其输入，搜索形如“label:”的行，可能前面有空格或制表符，并在该行之后继续执行。 |
| `hashstat` | 打印统计行，指示内部哈希表在定位命令（并避免 exec）方面的有效性。会在哈希函数指示可能命中以及每个不以反斜杠开头的路径组件中尝试 exec。 |
| `limit [ -h ] [ resource [ max-use ] ]` | 限制当前进程或其派生的任何进程的消耗，使其不超过指定资源上的 max-use。若省略 max-use，则打印当前限制；若省略 resource，则显示所有限制。加上 -h 时，使用硬限制而非当前限制。硬限制对当前限制的值施加上限。只有超级用户可以提高硬限制。Resource 为以下之一：cputime，每进程最大 CPU 秒数；filesize，允许的最大单个文件大小；datasize，进程的最大数据大小（包括栈）；stacksize，进程的最大栈大小；coredump，核心转储的最大大小；以及 descriptors，文件描述符的最大值。 |
| `log` | 打印 watch shell 变量并报告 watch 中指示的每个已登录用户，无论他们何时登录。另见 watchlog。 |
| `login` | 终止登录 shell，用 /bin/login 的实例替换它。 |
| `login [ username -p ]` | 终止登录 shell 并调用 login(1)。不处理 .logout 文件。若省略 username，login 会提示输入用户名。加上 -p 时，保留当前环境（变量）。 |
| `logout` | 终止登录 shell。 |
| `ls-F [-switch ...] [file ...]` | 像 ls -F 一样列出文件但速度更快。它用特殊字符标识列表中每种特殊文件类型：/ 目录 * 可执行文件 # 块设备 % 字符设备 | 命名管道（仅有命名管道的系统） = 套接字（仅有套接字的系统） @ 符号链接（仅有符号链接的系统） + 隐藏目录（仅 AIX）或上下文相关（仅 HP-UX） : 网络特殊设备（仅 HP-UX） 若设置了 listlinks shell 变量，则符号链接会被更详细地标识（当然，仅在有符号链接的系统上）：@ 指向非目录的符号链接 > 指向目录的符号链接 & 指向无处的符号链接 ls-F 内建命令可以根据文件类型或扩展名使用不同颜色列出文件。 |

