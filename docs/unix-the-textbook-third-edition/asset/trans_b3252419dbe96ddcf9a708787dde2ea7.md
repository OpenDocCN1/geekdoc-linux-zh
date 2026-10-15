

C shell 不支持使用文件描述符进行 I/O 和错误重定向。此外，将命令的标准输出和标准错误重定向到不同文件的方式在 C shell 中与其它 shell 的指定方式不同。

FIFO，也称为命名管道，允许系统上的相关或不相关进程进行通信。与管道不同，管道是内存缓冲区，而 FIFO 是在二级存储设备上创建的文件。对于命令行使用，你可以使用 mkfifo 命令创建 FIFO。mknod() 系统调用或 mkfifo() 库调用可用于在进程内部创建 FIFO。当你不再需要 FIFO 时，可以使用运行中的程序（进程）内的 unlink() 系统调用或命令行上的 rm 命令将其删除。我们在第 18 章至第 21 章关于 UNIX 系统编程中讨论与管道和 FIFO 相关的 UNIX 系统调用和库调用。

## QUESTIONS AND PROBLEMS

- 1. 什么是标准文件？请列出它们并说明其用途。
- 2. 简要描述输入、输出和错误重定向。写出各两种命令以展示重定向操作符的简单使用和组合使用。
- 3. UNIX 中的文件描述符是什么？标准文件的文件描述符是什么？如何在 Bourne、Korn、Bash 和 POSIX shell 中将 I/O 和错误重定向操作符与标准文件的文件描述符结合使用以执行重定向？
- 4. 对文件 data1 进行排序并将排序后的文件放入名为 data1.sorted 的文件中。给出使用输入和输出重定向的命令。
- 5. 给出使用管道和输出重定向完成问题 4 任务的命令。
- 6. 给出一组等价于命令 ls -l | grep "sarwar" > output.p3 的命令，该命令仅使用 I/O 重定向操作符。给出的命令与你的命令序列的性能如何比较？解释原因。
- 7. tee 命令的用途是什么？给出一个等价于问题 6 中的命令的命令，该命令使用 tee 命令。
- 8. 编写 UNIX shell 命令以完成以下任务。
  a. 统计名为 data1 的文件中的字符数、单词数和行数，并在显示屏上显示输出。
  b. 统计 ls -l 命令输出中的字符数、单词数和行数，并在显示屏上显示输出。
  c. 与 b 部分相同，但将输出重定向到名为 data1.stats 的文件。

9. 给出搜索文件 datafile 中字符串 “Internet” 的命令，将命令的输出发送到名为 Internet.freq 的文件，并将任何错误消息发送到文件 error.log。绘制该命令的图表，类似于本章中所示的图表，以说明其语义。

10. 给出完成问题 9 任务的命令，但命令的输出和任何错误消息都进入名为 datafile 的文件。

11. 给出搜索 /etc/passwd 中包含字符串 “sarwar” 的行的命令。

12. 将命令的输出存储在当前目录中名为 passwd.sarwar 的文件中。如果命令失败，错误消息也必须进入同一文件。

13. UNIX 管道是什么？管道与输出重定向有何不同？举例说明你的答案。

14. 在 Bourne shell 下，以下命令做什么？
  a. cat 1> letter 2> save 0< memo
  b. cat 2> save 0< memo 1> letter
  c. cat 1> letter 0< memo 2>&1
  d. cat 0< memo | sort 1> letter 2> /dev/null
  e. cat 2> save 0< memo | sort 1> letter 2> /dev/null

15. 在 Bourne shell 下考虑以下命令。
  a. cat memo letter 2> communication 1>&2
  b. cat memo letter 1>&2 2> communication
在每种情况下，如果
  a. 两个文件（memo 和 letter）都存在于当前工作目录中，且
  b. 两个文件之一不存在于当前工作目录中，
cat 命令的输出和错误消息会去哪里？

16. 使用 mail 命令向 doe@domain.com 发送电子邮件消息。假设消息在名为 greetings 的文件中。给出一条使用输入重定向的命令和一条使用管道的命令。任何错误消息应追加到文件 mail.error。

17. 在你的 UNIX 系统上执行以下命令时会发生什么？为什么这些命令会产生它们产生的结果？
  a. cat letter >> letter
  b. cat letter > letter

