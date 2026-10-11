```
kali@kali:~$ [CTRL-R]c
(reverse-i-search)`ca': cat /etc/lsb-release
Listing 37 - Exploring the reverse-i-search facility
```

# 3.1.3.2  Exercises

+   1. Inspect your bash history and use *history expansion* to re-run a command from it.
+   2. Execute different commands of your choice and experiment browsing the history through the shortcuts as well as the *reverse-i-search* facility.

# 3.2  Piping and Redirection

Every program run from the command line has three data streams connected to it that serve as communication channels with the external environment. These streams are defined as follows:

| Stream Name | Description |
| Standard Input (STDIN) | Data fed into the program |
| Standard Output (STDOUT) | Output from the program (defaults to terminal) |
| Standard Error (STDERR) | Error messages (defaults to terminal) |

Table 3 - Streams connected to command line programs

Piping (using the `|` operator) and redirection (using the `>` and `<` operators) connects these streams between programs and files to accommodate a near infinite number of possible use cases.

# 3.2.1  Redirecting to a New File

In the previous command examples, the output was printed to the screen. This is convenient most of the time, but we can use the `>` operator to save the output to a file to keep it for future reference or manipulation:

```
kali@kali:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

kali@kali:~$ echo "test"
test

kali@kali:~$ echo "test" > redirection_test.txt

kali@kali:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  redirection_test.txt  Template

kali@kali:~$ cat redirection_test.txt
test

kali@kali:~$ echo "Kali Linux is an open source project" > redirection_test.txt

kali@kali:~$ cat redirection_test.txt
Kali Linux is an open source project
Listing 38 - Redirecting the output to a file
```