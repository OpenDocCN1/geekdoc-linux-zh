# command `ps`

# Syntax:

```
ps [-al] [-u user]
```

Display running processes with their characteristics. Without options, only the user's own processes running in the current shell are displayed.

Important options:

+   - `-a` display all processes assigned to any terminal (tty)
+   - `-l` long format display. Additional information about owner, parent process etc.
+   - `-u` display all processes which are owned by a specific user.

# Example:

```
wegner@arber:~ > ps
  PID TTY       TIME CMD
21733 pts/4    00:00:00 bash
22197 pts/4    00:00:00 xterm
22198 pts/5    00:00:00 bash
22212 pts/4    00:00:00 ps
wegner@arber:~ >
```

# Exercise:

*View all current processes within your shell!*

# command `kill`

# Syntax:

```
kill [-9] PID
```

Terminates the process with number PID. Can be executed only by the owner of the process or by *root*.

Important option:

+   - `-9` for ‘obstinate’ processes which cannot be terminated by a normal kill.

# Example:

```
wegner@arber:~ > ps
  PID TTY       TIME CMD
21733 pts/4    00:00:00 bash
22197 pts/4    00:00:00 xterm
22198 pts/5    00:00:00 bash
22212 pts/4    00:00:00 ps
wegner@arber:~ > kill 22197
wegner@arber:~ > ps
  PID TTY       TIME CMD
21733 pts/4    00:00:00 bash
22214 pts/4    00:00:00 ps
[1]+  Exit 15  xterm
wegner@arber:~ >
```

# Exercise:

*Terminate eyes via kill!*