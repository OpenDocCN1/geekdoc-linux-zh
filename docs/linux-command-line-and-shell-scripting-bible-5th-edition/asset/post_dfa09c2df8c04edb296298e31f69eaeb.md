
The script assigns the value to a variable, which is then used as part of a filename. The file itself contains the redirected output (discussed later in the “Redirecting Input and Output” section) of a directory listing. After running the script, you should see a new file in your directory:

```
-rw-r--r-- 1 user user 769 Jun 01 16:15 log.250601
```

The log file appears in the directory using the value of the $today variable as part of the filename. The contents of the log file are the directory listing from the /usr/bin directory. If the script is run the next day, the log filename will be log.250602, thus creating a new file for the new day.

> **WARNING**
> Command substitution creates what’s called a subshell to run the enclosed command. A subshell is a separate child shell generated from the shell that’s running the script. Because of that, any variables that you create in the script won’t be available to commands running in the subshell.
>
> Subshells are also created if you run a command from the command prompt using the . / path, but they aren’t created if you just run the command without a path. However, if you use a built-in shell command, that doesn’t generate a subshell. Be careful when running scripts from the command prompt!

# Redirecting Input and Output

There are times when you’d like to save the output from a command instead of just having it displayed on the monitor. The Bash shell provides a few different operators that allow you to redirect the output of a command to an alternative location (such as a file). Redirection can be used for input as well as output, redirecting a file to a command for input. This section describes what you need to do to use redirection in your shell scripts.

## Output redirection

The most basic type of redirection is sending output from a command to a file. The Bash shell uses the greater-than symbol (>) for this:

```
command > outputfile
```

Anything that would appear on the monitor from the command instead is stored in the output file specified:

```
$ date > test6
$ ls -l test6
-rw-r--r-- 1 user user 29 Jun 01 16:56 test6
$ cat test6
Sun Jun 01 16:56:58 EDT 2025
$
```

The redirect operator created the test6 file (using the default umask settings) and redirected the output from the date command to the test6 file. If the output file already exists, the redirect operator overwrites the existing file with the new file data:

![](img/0798d50a0e5dbf1265fbda3832b3e015_276_0.png)

```
$ who > test6
$ cat test6
rich pts/0 Jun 01 16:55
$
```

Now the contents of the test6 file contain the output from the who command.

Sometimes, instead of overwriting the file's contents, you may need to append output from a command to an existing file—for example, if you're creating a log file to document an action on the system. In this situation, you can use the double greater-than symbol (>>) to append data:

```
$ date >> test6
$ cat test6
rich pts/0 Jun 01 16:55
Sun Jun 01 17:02:14 EDT 2025
$
```

The test6 file still contains the original data from the who command processed earlier—plus now it contains the new output from the date command.

## Input redirection

Input redirection is the opposite of output redirection. Instead of taking the output of a command and redirecting it to a file, input redirection takes the contents of a file and redirects it to a command.

The input redirection symbol is the less-than symbol (<):

```
command < inputfile
```

The easy way to remember this is that the command is always listed first in the command line, and the redirection symbol “points” to the way the data is flowing. The less-than symbol indicates that the data is flowing from the input file to the command.

Here’s an example of using input redirection with the wc command:

```
$ wc < test6
2 11 60
$
```

The wc command provides a count of text in the data. By default, it produces three values:

- The number of lines in the text
- The number of words in the text
- The number of bytes in the text

By redirecting a text file to the wc command, you can get a quick count of the lines, words, and bytes in the file. The example shows that there are 2 lines, 11 words, and 60 bytes in the test6 file.

There’s another method of input redirection, called inline input redirection. This method allows you to specify the data for input redirection on the command line instead of in a file. This may seem somewhat odd at first, but there are a few applications for this process (such as those shown in the “Performing Math” section later).

The inline input redirection symbol is the double less-than symbol (`<<`). Besides this symbol, you must specify a text marker that delineates the beginning and end of the data used for input. You can use any string value for the text marker, but it must be the same at the beginning of the data and at the end of the data:

```
command << marker

data
marker
```

When you use inline input redirection on the command line, the shell will prompt for data using the secondary prompt, defined in the `PS2` environment variable (see Chapter 6). Here’s how this looks when you use it:

```
$ wc << EOF
> test string 1
> test string 2
> test string 3
> EOF
     3     9    42
$ 
```

The secondary prompt continues to prompt for more data until you enter the string value for the text marker. The `wc` command performs the line, word, and byte counts of the data supplied by the inline input redirection.

## Employing Pipes

There are times when you need to send the output of one command to the input of another command. This is possible using redirection, but somewhat clunky:

```
$ rpm -qa > rpm.list
$ sort < rpm.list
aaajohan-comfortaa-fonts-3.001-10.el9.noarch
aardvark-dns-1.12.2-1.el9_5.x86_64
abattis-cantarell-fonts-0.301-4.el9.noarch
accountsservice-0.6.55-10.el9.x86_64
accountsservice-libs-0.6.55-10.el9.x86_64
acl-2.3.1-4.el9.x86_64
adcli-0.9.2-1.el9.x86_64
adobe-mappings-cmap-20171205-12.el9.noarch
adobe-mappings-cmap-deprecated-20171205-12.el9.noarch
adobe-mappings-pdf-20180407-10.el9.noarch
adobe-source-code-pro-fonts-2.030.1.050-12.el9.1.noarch
...
```

The `rpm` command manages the software packages installed on systems using the Red Hat Package Management system (RPM), such as the Rocky system, as shown. When used with the `-qa` parameters, it produces a list of the existing packages installed, but not necessarily in any specific order. If you’re looking for a specific package or group of packages, it can be difficult to find this using the output of the `rpm` command.

Using the standard output redirection, the output was redirected from the `rpm` command to a file called `rpm.list`. After the command finished, the `rpm.list` file contained a list of all the installed software packages on this system. Next, input redirection was used to send the contents of the `rpm.list` file to the `sort` command to sort the package names alphabetically.

That was useful, but again, a somewhat clunky way of producing the information. Instead of redirecting the output of a command to a file, you can redirect the output to another command. This process is called *piping*.

Like the command substitution backtick (`` ` ``, the symbol for piping is not used often outside of shell scripting. The symbol is two vertical lines, one above the other. However, the pipe symbol often looks like a single vertical line in print (`|`). On a U.S. keyboard, it is usually on the same key as the backslash (`\`). The pipe is put between the commands to redirect the output from one to the other:

```
command1 | command2
```

Don't think of piping as running two commands back to back. The Linux system actually runs both commands at the same time, linking them together internally in the system. As the first command produces output, it's sent immediately to the second command. No intermediate files or buffer areas are used to transfer the data.

Now, using piping you can easily pipe the output of the `rpm` command directly to the `sort` command to produce your results:

```
$ rpm -qa | sort
asojohan-comfortaa-fonts-3.001-10.el9.noarch
aardvark-dns-1.12.2-1.el9_5.x86_64
abattis-cantarell-fonts-0.301-4.el9.noarch
accountsservice-0.6.55-10.el9.x86_64
accountsservice-libs-0.6.55-10.el9.x86_64
acl-2.3.1-4.el9.x86_64
adcli-0.9.2-1.el9.x86_64
adobe-mappings-cmap-20171205-12.el9.noarch
adobe-mappings-pdf-deprecated-20171205-12.el9.noarch
adobe-mappings-pdf-20180407-10.el9.noarch
adobe-source-code-pro-fonts-2.030.1.050-12.el9.1.noarch
...
```

Unless you're a (very) quick reader, you probably couldn't keep up with the output generated by this command. Because the piping feature operates in real time, as soon as the `rpm` command produces data, the `sort` command gets busy sorting it. By the time the `rpm` command finishes outputting the data, the `sort` command already has the data sorted and starts displaying it on the monitor.

There's no limit to the number of pipes you can use in a command. You can continue piping the output of commands to other commands to refine your operation.

In this case, because the output of the `sort` command zooms by so quickly, you can use one of the text-paging commands (such as `less` or `more`) to force the output to stop at every screen of data:

```
$ rpm -qa | sort | more
```
