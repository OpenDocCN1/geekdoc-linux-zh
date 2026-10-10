```
$ ps -auxf | less<Enter>
```

We will discuss the command in more detail later. But for now, the system normally responds with a list of processes that are currently running. The output will probably come to more than one screenful of output. We have piped the output of the ps command and options to the less command, however, so the system will stop and wait for user input until that screenful of output is displayed. Let’s look at some of the output; see Table 12.3.

We included the `init` process in the listing here to illustrate that it is indeed the parent of all processes. Now, let’s look at PID 637, which shows us when the root user logged in. The system provided the capability to log in at 09:32, but the root user actually logged in at 12:57. We also see that root’s login bash shell automatically spawned the child process PID 694, a (default) bash shell, at 12:57. We know that the bash shell is the child of the login because of the slash mark ( \ ) that connects the bash command to `login - root`.

Moving along, we see that our user Lady Toloso logged in at 14:22, which caused the spawning of a child process bash shell, as well. Notice the same slash connection between that bash shell and Lady Toloso’s login process. Later, at 14:37, we see that Lady Toloso entered the `ps -auxf | less` command. Two child processes were spawned as a result of Lady Toloso entering that command: the ps -auxf process itself and the (piped) less process. Those two processes are children of the bash shell because each has a slash connection to it.

# **Example 12.4 Examining PIDs and PPIIDs**

Have a look now at Figure 12.3. This figure shows an illustration of Don Quixote’s login session, which we briefly discussed earlier in this chapter. Remember that the `init` process—the first process to start in a system—has a process ID number of 1. The Don logged into the system and the kernel assigned his login shell a PID of 340. To check the PID number, he could have used the `echo $` command. Incidentally, the `echo` command is one of several built-in commands; thus, when it is invoked, there is no need to create a subshell to run it.

Although Don Quixote used the special `$$` variable as an argument to `echo`, `$$` is mostly used within shell scripts to distinguish between multiple instances of the same shell script. The value of that variable changes as you move from one (current) process environment to another.

At any rate, there he is in the login shell. The PID is 340 and the parent process ID (PPID) is 1 (`init` process). To further illustrate parent-child