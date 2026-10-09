The next script copies one directory to another. The second pair of parentheses creates a subshell to run the commands following the pipe. Because of these parentheses, the output of the first tar command is available for the second tar command despite the intervening cd command. Without the parentheses, the output of the first tar command would be sent to cd and lost because cd does not process input from standard input. The shell variables $1 and $2 represent the first and second command-line arguments (page 997), respectively. The first pair of parentheses, which creates a subshell to run the first two commands, allows users to call cpd1r with relative pathnames. Without them, the first cd command would change the working directory of the script (and consequently the working directory of the second cd command). With them, only the working directory of the subshell is changed.

```
```
$ cat cpd1r
(cd $1 ; tar -cf - . ) | (cd $2 ; tar -xvf - )
$ . /cpd1r /home/max/sources /home/max/memo/biblio
```
```

The cpd1r command line copies the files and directories in the /home/max/sources directory to the directory named /home/max/memo/biblio. This shell script is almost the same as using cp with the -r option. Refer to the cp and tar man pages for more information.

# JOB CONTROL

A job is a command pipeline. You run a simple job whenever you give the shell a command. For example, if you type date on the command line and press RETURN, you have run a job. You can also create several jobs with multiple commands on a single command line:

```
```
$ find . -print | sort | lpr & grep -l max /tmp/* > maxfiles &
[1] 18839
[2] 18876
```
```

The portion of the command line up to the first & is one job consisting of three processes connected by pipes: find, sort (page 168), and lpr (page 165). The second job is a single process running grep. The trailing & characters put each job in the background, so bash does not wait for them to complete before displaying a prompt.

Using job control you can move commands from the foreground to the background (and vice versa), stop commands temporarily, and list all commands that are running in the background or stopped.

# jobs: LISTS JOBS

The jobs builtin lists all background jobs. Following, the sleep command runs in the background and creates a background job that jobs reports on:

```
```
$ sleep 60 &
[1] 7809
$ jobs
[1] + Running s1eep 60 &
```
```