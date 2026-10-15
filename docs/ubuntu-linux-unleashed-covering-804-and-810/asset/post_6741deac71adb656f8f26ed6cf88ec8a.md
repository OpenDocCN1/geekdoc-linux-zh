
The last command to try is r, which allows you to renice—or adjust the nice value—of a process. You need to enter the PID of the process, press Enter, and enter a new nice value. Keep in mind that 19 is the lowest and -20 is the highest; anything less than 0 is considered "high" and should be used sparingly.

## Printing the Location of a Command with which

The purpose of which is to tell you the exact command that would be executed if you typed it. For example, which mkdir returns /bin/mkdir, telling you that running the command mkdir runs /bin/mkdir.

## Combining Commands

So far, we have only been using commands individually, and for the large part that is what you will be doing in practice. However, some of the real power of these commands lies in the ability to join them together to get exactly what you want. There are some extra little commands that we have not looked at that are often used as glue because they do one very simple thing that enables a more complex process to work.

All the commands we have looked at have printed their information to the screen, but this is often inflexible. There are two ways to control where output should go: piping and output redirection. A pipe is a connector between one command's output and another's input. Instead of sending its output to your terminal, a command sends that output directly to another command for input. Output redirection works in a similar way to pipes but is usually used for files. We will look at pipes first and then output redirection.

Two of the commands we have looked at so far are ps and grep: the process lister and the string matcher. We can combine the two to find out which users are playing Nethack right now:

```
ps aux | grep nethack
```

That creates a list of all the processes running right now and sends that list to the grep command, which filters out all lines that do not contain the word nethack. Ubuntu allows you to pipe as many commands as you can sanely string together. For example, we could add in the wc command, which counts the numbers of lines, words, and characters in its input, to count precisely how many times Nethack is being run:

```
ps aux | grep nethack | wc -l
```

The -l parameter to wc (lowercase L) prints only the line count.

Using pipes in this way is often preferable to using the -exec parameter to find, simply because many people consider find to be a black art and so anything that uses it less frequently is better! This is where the xargs command comes in: It converts output from one command into arguments for another.

For a good example, consider this mammoth find command from earlier:

```
find / -name "*.txt" -size +10k -user paul -not -perm -o+r -exec chmod o+r {} \;
```

That searches every directory from / onward for files matching *.txt that are greater than 10KB, are owned by user paul, and do not have read permission for others. Then it executes chmod on each of the files. It is a complex command, and people who are not familiar with the workings of find might have problems understanding it. So, what we can do is break it up into two—a call to find and a call to xargs. The conversion would look like this:

```
find / -name "*.txt" -size +10k -user paul -not -perm -o+r | xargs chmod o+r
```

That has eliminated the confusing {} \; from the end of the command, but it does the same thing, and faster, too. The speed difference between the two is because using -exec with find causes it to execute chmod once for each file. However, chmod accepts many files at a time and, because we are using the same parameter each time, we should take advantage of that. The second command, using xargs, is called once with all the output from find, and so saves many command calls. The xargs command automatically places the input at the end of the line, so the previous command might look something like this:

```
chmod o+r file1.txt file2.txt file3.txt
```

Not every command accepts multiple files, though, and if you specify the -l parameter, xargs executes its command once for each line in its input. If you want to check what it is doing, use the -p parameter to have xargs prompt you before executing each command.

For even more control, the -i parameter allows you to specify exactly where the matching lines should be placed in your command. This is important if you need the lines to appear before the end of the command or need it to appear more than once. Either way, using the -i parameter also enables the -l parameter so each line is sent to the command individually. This next command finds all files in /home/paul that are larger than 10,000KB in size (10MB) and copies them to /home/paul/archive:

```
find /home/paul -size +10000k | xargs -i cp {} /home/paul/archive
```

Using find with xargs is a unique case. All too often, people use pipes when parameters would do the job just as well. For example, these two commands are identical:

```
ps aux --sort=-%cpu | grep -v `whoami`
ps -N ux --sort=-%cpu
```

The former prints all users and processes and then pipes that to grep, which in turn filters out all lines that contain the output from the program whoami (our username). So, line one prints all processes being run by other users, sorted by CPU use. Line two does not specify the a parameter to ps, which makes it list only our processes. It then uses the -N parameter to flip that, which means it is everyone but us, without the need for grep.
