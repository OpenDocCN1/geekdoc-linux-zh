The log file appears in the directory using the value of the $today variable as part of the file name. The contents of the log file are the directory listing from the /usr/bin directory. If the script is run the next day, the log filename will be log.081104, thus creating a new file for the new day.

# Redirecting Input and Output

There are times when you'd like to save the output from a command instead of just having it display on the monitor. The bash shell provides a few different operators for allowing you to redirect the output of a command to an alterative location (such as a file). Redirection can also be used to input and output, redirecting a file to a command for input. This section describes what you need in order to use redirection in your shell scripts.

# Output Redirection

The most basic type of redirection is sending output from a command to a file. The bash shell uses the greater-than symbol for this:

```
command > outputfile
```

Anything that would appear on the monitor from the command is stored in the output file specified instead:

```
$ date > test6
$ ls -l test6
-rw-r--r-- 1 rich rich 29 2008-11-04 17:56 test6
$ cat test6
Tue Nov 4 17:56:58 EDT 2008
$
```

The redirect operator created the file test6 and redirected the output from the date command to the test6 file. If the output file already exists, the redirect operator overwrites the existing file with the new file data:

```
$ who > test6
$ cat test6
rich pts/0 Nov 4 17:55
$
```

Now the contents of the test6 file contain the output from the who command.

Sometimes, instead of overwriting the file contents you may need to append output from a command to an existing file—for instance, if you're creating a log file to document an action on the system. For this situation, you can use the double greater-than symbol (>>) to append data:

```
$ date >> test6
$ cat test6
rich pts/0 Nov 4 17:55
Tue Nov 4 18:02:14 EDT 2008
$
```

The test6 file still contains the original data from the who command processed earlier, and now it contains the new output from the date command.