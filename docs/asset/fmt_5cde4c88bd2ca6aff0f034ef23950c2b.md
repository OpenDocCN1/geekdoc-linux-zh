
## Comments

- 1. 程序目前存在的问题是，它在从休眠中唤醒之前不会响应任何按键。你无法让它提前唤醒。它将休眠指定的时间，任凭风雨。这意味着反应快的用户会对这个解决方案感到不满意。从本质上讲，这是一种适用于所有用户的、使程序对用户响应速率做出反应的解决方案。从本质上讲，这是一种轮询解决方案，因为它只是反复检查用户。一种替代方案是 somehow 让程序在用户实际做点什么之前休眠。

- 2. 程序的另一个问题是，如果它被异常终止，例如当用户输入 `Ctrl-C` 时，它将没有机会将终端恢复到原始设置。例如，如果程序关闭了规范输入和回显，并且在主程序中恢复终端的指令执行前就被杀掉，那么当 shell 在程序非正常死亡后恢复执行时，终端仍将处于非规范模式且无回显。幸运的是，对于当今的 UNIX 程序员来说，像 `bash` 和 `tcsh` 这样的现代 shell 会在从 shell 调用的进程被杀掉时自动重置终端，因此这些用户不会看到这种情况发生。

- 3. 然而，即使 shell 能够重置终端，当程序打开非阻塞 I/O 时，它仍然不一定能免疫由此产生的问题。如果程序打开了非阻塞读取然后随后被杀掉，很有可能 shell 也会被杀掉。这是因为，当程序从 shell 调用时，它会与其父 shell 共享文件描述符。换句话说，程序中的文件描述符 0 指向

2 一些 shell 看起来也修复了这个“bug”。如果一个派生进程在标准输入上留下 `O_NONBLOCK` 标志，它们会清除它。

to the same file structure in the kernel as it does in the shell. Suppose that the program turns on the `O_NONBLOCK` flag on the standard input connection. It is actually modifying the connection that its parent, i.e., the shell, uses as well. In fact, this standard input connection is shared by all related processes – siblings, cousins, and so on. Any process that is sharing this file connection can potentially make changes that affect all other processes that use this terminal. Once the changes are made, unless they are undone before the process terminates, the shell’s connection has those changed properties.

Now think about the shell for a moment. A shell is basically running a loop of the form

```
while ( not end of input ) {

    display the shell prompt

    read the user’s command line

    carry out the instruction

}
```

Thus, if the program turns on non-blocking reads and is killed before turning it off, when the shell resumes, it executes a read command. Usually the shell is in blocking input mode, so when it tries to read input but none is there, it enters a blocked state waiting for the user to press the Enter key, which sends input to the shell process. Since non-blocking input is still on, instead of waiting for the user’s input, it receives an EOF from the function call that it uses to retrieve the input. This EOF may cause the shell itself to terminate because most shells are killed by the EOF character. You should set `ignoreeof` to prevent this. In `bash`, you add the line

```
set -o ignoreeof
```

in your `.bashrc` to do this. Anyway, the result is that your shell is killed, and if this is a login shell, you will be logged out. On my host machine, `bash` gets caught in a segmentation fault, which should not happen.

4. The problem with non-blocking reads causing the shell to exit can also be solved by opening a new file connection to the terminal instead of using standard input. In the demo program, explore the effect of replacing the line

```
fp = stdin;
```

by

```
fp = fopen(ctermid(NULL), "r");
```
