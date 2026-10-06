# 14 | Master of Linux Commands

# Shell

Shell is taking place between the user and kernel tasks, interprets commands from the user to communicate with the kernel. Kernel and shell's interaction happens through with the system calls.

There are many shells are used in Linux systems but the most preferred programs are BASH shell program. To learn using shell program in our system, we can use the echo $SHELL command.

```
root@kemal:~# echo $SHELL
/bin/bash
root@kemal:~# 
```

The console commented our order and sent us an outcome. We said it would also reviewed the commands issued from the console, but it will be interpreted according to what? That point, environmental variables come play into concept.

# Environment Variables

We will use the following command and check what command try to explain to us to get the subject. The command we will use is echo $ PATH command

```
root@kemal:~# echo PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/bin
root@kemal:~# 
```

§