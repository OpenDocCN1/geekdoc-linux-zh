# Parameters and Variables 587

```
$ echo $$\n5209
$ ps
PID TTY             TIME CMD
5209 pts/1         00:00:00 bash
6015 pts/1         00:00:00 ps
```

The echo builtin keeps the shell from creating another process when you give it an echo command. The results are the same whether echo is a builtin or not, because the shell substitutes the value of $$ before it forks a new process. In the following example, the shell substitutes the value of $$ and passes that value to cp as a prefix for a new filename:

```
$ echo $$\n8232
$ cp memo $$.memo
$ ls
8232.memo memo
```

This technique is useful for creating unique filenames when the meanings of the names do not matter; it is often used in shell shell scripts for creating names of temporary files. When two people are running the same shell script, these unique filenames keep them from inadvertently sharing the same temporary file.

The following example demonstrates that the shell creates a new process when it runs a shell script. The id2 script displays the PID numbers of the process running it (not the process that called it; the substitution for $$ is performed by the shell that is forked to run id2):

```
$ cat id2
echo "$0 PID= $$"
$ echo $$
8232
$ id2
id2 PID~ 8362
$ echo $$
8232
```

The first echo in the preceding example displays the PID number of the login shell. Then id2 displays its name ($0) and the PID of the subshell that it is running in. The last echo shows that the current process is the login shell.

The Bourne and Z Shell store the value of the PID number of the last process that you ran in the background in $!. The following example executes sleep as a background task and then uses echo to display the value of $$:

```
$ sleep 60 &
8376
$ echo !$
8376
```