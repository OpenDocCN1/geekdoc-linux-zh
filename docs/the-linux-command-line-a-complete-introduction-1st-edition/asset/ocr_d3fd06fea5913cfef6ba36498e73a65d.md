**Note:** *If your system does not include the xlogo program, try using gedit or kwrite instead.*

We can verify that xlogo is running by resizing its window. If the logo is redrawn in the new size, the program is running.

Notice how our shell prompt has not returned? This is because the shell is waiting for the program to finish, just like all the other programs we have used so far. If we close the xlogo window, the prompt returns.

# Interrupting a Process

Let’s observe what happens when we run xlogo again. First, enter the xlogo command and verify that the program is running. Next, return to the terminal window and press CTRL-C.

```
```bash
[me@linuxbox ~]$ xlogo
[me@linuxbox ~]$
```
```

In a terminal, pressing CTRL-C interrupts a program. This means that we politely asked the program to terminate. After we pressed CTRL-C, the xlogo window closed and the shell prompt returned.

Many (but not all) command-line programs can be interrupted by using this technique.

# Putting a Process in the Background

Let’s say we wanted to get the shell prompt back without terminating the xlogo program. We’ll do this by placing the program in the *background*. Think of the terminal as having a *foreground* (with stuff visible on the surface, like the shell prompt) and a background (with hidden stuff below the surface). To launch a program so that it is immediately placed in the background, we follow the command with an ampersand character (&):

```
```bash
[me@linuxbox ~]$ xlogo &
[1] 28236
[me@linuxbox ~]$
```
```

After the command was entered, the xlogo window appeared and the shell prompt returned, but some funny numbers were printed too. This message is part of a shell feature called *job control*. With this message, the shell is telling us that we have started job number 1 ([1]) and that it has PID 28236. If we run ps, we can see our process:

```
```text
[me@linuxbox ~]$ ps
  PID TTY          TIME CMD
10603 pts/1    00:00:00 bash
28236 pts/1    00:00:00 xlogo
28239 pts/1    00:00:00 ps
```
```