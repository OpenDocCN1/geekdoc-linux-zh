
It may be more efficient to do only one step as follows:

```
export HISTSIZE=1000
```

To display the current value of an environment variable, use the `echo` command:

```
echo $HISTSIZE
```

You can access these variables from within a C program using the `getenv` function.

## Piping and Redirection

Piping and redirection are such powerful tools that it's frustrating to find yourself on a system that either doesn't handle pipes or handles them badly. Most Unix–like operating systems handle both pipes and redirection similarly.

### Piping

When you execute a command in Linux, it has three streams opened for it. The first is for input and is called Standard In (stdin). The next is for output and is called Standard Out (stdout). The last is the error stream and is called Standard Error (stderr).

Piping is the practice of passing the first program's stdout into the stdin of another program. You do this by listing the first command followed by a pipe ( | ) and then the command where the first command's output is being sent. For example, if your task is to back up certain files on your system, you can funnel the file listing that is output from a find command into stdin of the cpio command, prompting cpio to store only the listed files on your tape:

```
# find /home/user | cpio -ocvB /dev/st0
```

The output of the find command would look something like this:

```
/home/user
/home/user/calendar
/home/user/linus.au
/home/user/.bash_logout
/home/user/.bash_profile
/home/user/.bashrc
```

When this output is piped into the cpio command, each of these files is added to the archive and written to the tape drive specified as /dev/st0 (the first SCSI tape drive).

If you want to exclude all sound files with the extension .au, you could pipe the find command through a grep command and then into the cpio command. The command would then look something like this:

```
# find /home/user | grep -v ".au" | cpio -ocvB /dev/st0
```

In this case, the file list output by the find command would be filtered to exclude all of the files that end in the extension .au, and only the remaining files would be added to the archive.

### Redirection

*Redirection* is the practice of changing where the stream comes from or is written to. One common use is to route the system log to a vacant console and update it as messages are added. You do this by listing the tail command followed by an output redirection character ( > ) and then the device where the output is to be sent. If you wanted the output of the command to go to the console device designated by /dev/tty9 rather than to stdout, you would enter this:

```
# tail -f /var/log/messages > /dev/tty9
```

When you execute this command, the output of the tail command will be redirected to console 9, causing the system log (/var/log/messages) to be displayed there and, since the -f argument is present, appending new output as it is written to the system log.

Sometimes you want to take input from somewhere other than stdin. This is also redirection, and you can use the same principle illustrated above. Simply follow the command that requires input with the input redirection character ( < ) and the file that contains the data to be input. Let's say that a file contains a list of names to be sorted in a particular order. By changing the stdin for the sort command, we can make it take the names from the file, reorder them, and write them to stdout. The command would look like this:

```
# sort < namelist
```

You can use the two redirection operators in the same command sequence when you need to take stdin from one file and send stdout to another. A common use of this is to sort the lines in a file and output the sorted lines into a new file. With redirection it would look like this:

```
# sort < namelist > sortedlist
```

Another common use of redirection is to send both stdout and stderr to a file in order to save the data for examination. This is a very useful tool for tracking down a problem. This can be done for any two I/O streams and not just stdout and stderr. You need to know that standard input is considered the first stream and numbered 0; standard output numbered 1, and standard error is numbered 2, since the numeric representation is used in redirection. Using stdout and stderr, the command would look like this:

```
# backup > backup.log 2>&1
```

**Note** The 2>&1 means to route stderr (2) wherever stdout (1) goes. The ampersand (&) often relates to memory location or addresses. Redirection as above causes backup.log to write over any file previously known as backup.log. If you want to append the output from a command to backup.log instead of writing over it, you'd use the >> symbol. This is especially good for log keeping. The command would look like this:

```
# backup >> backup.log 2>&1
```

## Wildcards

Bash, like most other Unix shells, allows the use of special characters called *wildcards* to reference more than one file at a time. DOS and Windows, of course, also offer wildcards, but the difference is that in Linux, these special characters are expanded by the Bash shell and not by the program itself. That is, if you launch a program that has special characters in its argument string, the program does not need to know how to handle them; they are translated by the Bash shell before being passed to the application. Instead of the wildcard characters, for instance, the program would receive a space-delimited list of all files matching the wildcard construct. The user may restrict this capability if the wildcard characters are intended to be interpreted by the program rather than the shell. There are three wildcard characters frequently used in Linux, each interpreted differently by the Bash shell: the asterisk, the question mark, and the bracket pair.

The asterisk is often called the “splat”; the string b*.bmp might be pronounced as “b–splat–dot–bmp.” Its purpose is to replace a string of any number of characters in sequence. Thus b*.bmp matches with any file whose name begins with b and has the .bmp extension. The files blue.bmp, barney.bmp, bermuda.bmp, and before_you_go_away.bmp would all match.

The string *.* matches all files that contain a period; be certain that you really mean to act on all files in the directory when you use this string. The string .* matches any dot file.

Many a user has deleted important files by specifying an incorrect wildcard string as an argument to the rm command. The “joke” that is often played is trying to get the new guy to run rm –rf * from the root directory. This is a forced removal of all files and directories. It’s ugly if you have no backup.

The question mark represents any one character. The string file_? would match all of the following: file_1, file_2, file_A, or file_b. The string file.??? would match any file named file that has a three-character extension.

The bracket pair is used to define a list or range of characters to be matched. The string file[0–9] would match file0, file1, file9. The string [a–zA–Z] would match any single alphabetical character. The string [a–zA–Z0–9] would match any alpha or numeric character.

## Quoting

As you’ve seen, shell commands assign special meanings to ordinary alphanumeric characters, so when these characters are used within strings literally, there needs to be some way to prevent the shell from interpreting the characters. In the Bash shell, quoting is the basic technique for this. There are three quoting mechanisms: the escape character, single quotes, and double quotes:

- The backslash (\) is the Bash escape character. It causes the next character to be taken literally.
- Single quotes preserve the literal value of each character within the quotes. A single quote may not occur between single quotes, since the enclosed quote would be interpreted as the closing single quote.
- Double quotes protect the literal value of all characters contained within, except for the dollar sign ($), the backtick (`), the double quote ("), and the backslash (\). If a quoted string contains an environment variable that is to be expanded, double quotes allow this. Single quotes prevent the expansion.

## The Tilde

The tilde can save you several keystrokes every day. If a pathname/file combination begins with a tilde, everything preceding the first / is treated as a possible login name. In the case of ~/user/some_files, the ~/user would be replaced by the home directory of user. In most cases, this would be expanded to /home/user/some_files. If the resulting login name is a null string, as in ~/myfile, the tilde is replaced by the username of the user who executed the command.

If the tilde is followed by a plus sign, the ~+ is replaced by the present working directory. If the plus
