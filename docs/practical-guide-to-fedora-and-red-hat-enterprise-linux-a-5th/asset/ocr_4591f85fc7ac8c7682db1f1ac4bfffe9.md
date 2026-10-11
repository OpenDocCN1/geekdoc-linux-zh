with the pipe (|) symbol or how complex they are. The Bourne Again Shell shows only one process placed in the background:

```
`$ d | e | f &
[1] 14295`
```

# **optional** () GROUPS COMMANDS

You can use parentheses to group commands. The shell creates a copy of itself, called a *subshell*, for each group. It treats each group of commands as a job and creates a new process to execute each command (refer to “Process Structure” on page 314 for more information on creating subshells). Each subshell (job) has its own environment, meaning that it has its own set of variables with values that can differ from those of other subshells.

The following command line executes commands **a** and **b** sequentially in the background while executing **c** in the background. The shell prompt returns immediately.

```
`$ (a ; b) & c &
[1] 15520
[2] 15521`
```

The preceding example differs from the earlier example **d** & **c** & **f** & in that tasks **a** and **b** are initiated sequentially, not concurrently.

Similarly the following command line executes **a** and **b** sequentially in the background, and, at the same time, executes **c** and **d** sequentially in the background. The subshell running **a** and **b** and the subshell running **c** and **d** run concurrently. The prompt returns immediately.

```
`$ (a ; b) & (c ; d) &
[1] 15528
[2] 15529`
```

The next script copies one directory to another. The second pair of parentheses creates a subshell to run the commands following the pipe. Because of these parentheses, the output of the first tar command is available for the second tar command despite the intervening cd command. Without the parentheses, the output of the first tar command would be sent to cd and lost because cd does not process input from standard input. The shell variables $1 and $2 represent the first and second command-line arguments (page 931), respectively. The first pair of parentheses, which creates a subshell to run the first two commands, allows users to call cpdir with relative pathnames. Without them the first cd command would change the working directory of the script (and consequently the working directory of the second cd command). With them only the working directory of the subshell is changed.

```
`$ cat cpdir
(cd $1 ; tar -cf - .) | (cd $2 ; tar -xvf - )
$ cpdir home/alex/sources /home/alex/memo/biblio`
```

The *cpdir* command line copies the files and directories in the */home/alex/sources* directory to the directory named */home/alex/memo/biblio*. This shell script is almost the same as using cp with the -r option. Refer to the cp and tar man pages for more information.