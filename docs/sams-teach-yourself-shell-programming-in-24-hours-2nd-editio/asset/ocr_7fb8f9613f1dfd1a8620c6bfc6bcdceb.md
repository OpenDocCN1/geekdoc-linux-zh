**exec** executes the following command, which replaces the current process instead of running it as a child process.

**exit** *n* ends the shell script with status code *n*.

**export** marks variables as environment variables, allowing them to be passed to any child processes and called programs.

**false** (ksh, bash, and zsh only) always returns an unsuccessful or logical false result.

**fg** (Korn/Bash) brings a background or suspended job to the foreground.

**fi** denotes the end of an *if* statement.

**for** executes a block of code multiple times.

```
```bash
for var in list1
 do
 list2
 done
```
```

**function** (Korn/Bash) keyword to define a function.

**getopts** a function called repeatedly in a loop to process the command-line arguments.

**if** allows conditional execution.

```
```bash
if list1 ; then
 list2 ;
elif list3 ; then
 list4 ;
...
else
 listN ;
fi
```
```

**integer** (ksh, bash and zsh only) specifies an integer variable.

**jobs** (ksh, bash, and zsh only) list the background and suspended jobs.

**kill** sends a signal to a process; often used to terminate a process or to reinitialize a daemon background process.

**let** (ksh, bash, and zsh only) performs integer arithmetic.

**pwd** prints the present working or current directory.

**read** waits for one line of standard input and saves each word in the variables specified to it as arguments. If there are more words than variables, it saves the remaining words in the last variable.

![](bbox=[0.85, 0.55, 0.98, 0.7])