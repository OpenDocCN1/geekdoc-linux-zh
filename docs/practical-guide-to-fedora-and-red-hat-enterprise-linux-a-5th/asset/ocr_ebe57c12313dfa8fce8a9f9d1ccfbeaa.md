The read builtin returns an exit status of 0 if it successfully reads any data. It has a nonzero exit status when it reaches the EOF (end of file). The following example runs a while loop from the command line. It takes its input from the names file and terminates after reading the last line from names.

```
$ cat names
Alice Jones
Robert Smith
Alice Paulson
John Q. Public
```

```
$ while read first rest
> do
> echo $rest, $first
> done < names
Jones, Alice
Smith, Robert
Paulson, Alice
Q. Public, John
$
```

The placement of the redirection symbol (<) for the while structure is critical. It is important that you place the redirection symbol at the done statement and not at the call to read.

> optional Each time you redirect input, the shell opens the input file and repositions the read pointer at the start of the file:
> $ read line1 < names; echo $line1; read line2 < names; echo $line2
> Alice Jones
> Alice Jones
> Here each read opens names and starts at the beginning of the names file. In the following example, names is opened once, as standard input of the subshell created by the parentheses. Each read then reads successive lines of standard input.
> $ (read line1; echo $line1; read line2; echo $line2) < names
> Alice Jones
> Robert Smith
> Another way to get the same effect is to open the input file with exec and hold it open (refer to “File Descriptors” on page 921):
> $ exec 3< names
> $ read -u3 line1; echo $line1; read -u3 line2; echo $line2
> Alice Jones
> Robert Smith
> $ exec 3<&-

# exec: Executes a Command

The exec builtin has two primary purposes: to run a command without creating a new process and to redirect a file descriptor—including standard input, output, or error—of a shell script from within the script (page 921). When the shell executes a