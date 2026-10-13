As mentioned earlier, the init program runs programs similar to getty for networked connections. For example, sshd, telnetd, and rlogind answer connection requests via ssh, telnet, and rlogin, respectively. Instead of being tied directly to a specific, physical terminal or modem line, these programs connect users’ shells to pseudo-ttys. You can see this whether you’re logged in to your system over a network, on an X Windows screen, or through a networked terminal connection program with the who command:

```
```text
$ who
phw       pts/0    Jul 20 17:37        Logged in with nlogin
$
```
```

# Typing Commands to the Shell

When the shell starts up, it displays a command prompt—typically a dollar sign $—at your terminal and then waits for you to type in a command (Figure 2.6, Steps 1 and 2). Each time you type in a command and press the Enter key (Step 3), the shell analyzes what you typed and proceeds to carry out your request (Step 4).

If you ask the shell to invoke a particular program, it searches the disk, stepping through all the directories you’ve specified in your PATH until it finds the named program. When the program is found, the shell creates a clone of itself (known as a subshell) and asks the kernel to replace the subshell with the specified program; then the login shell “goes to sleep” until the program has finished (Step 5). The kernel copies the specified program into memory and begins its execution. This copied program is called a process; in this way, the distinction is made between a program that is kept in a file on the disk and a process that is in memory and being executed, line by line.

If the program writes output to standard output, that output will appear at your terminal unless redirected or piped into another command. Similarly, if the program reads input from standard input, it will wait for you to type in that input unless redirected from a file or piped from another command (Step 6).

When the command finishes execution, it vanishes and control once again returns to the login shell, which prompts for your next command (Steps 7 and 8).

![](bbox=[0.143, 0.693, 0.646, 0.944])