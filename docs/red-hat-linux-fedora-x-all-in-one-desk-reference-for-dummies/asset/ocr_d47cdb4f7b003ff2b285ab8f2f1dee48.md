# Typing less with automatic command completion

Many commands take a filename as an argument. To view the contents of the /etc/modprobe.conf text file, for example, type the following command:

```
cat /etc/modprobe.conf
```

The cat command displays the /etc/modprobe.conf file. For any command that takes a filename as an argument, use a Bash feature to avoid typing the whole file. All you have to do is bare minimum—just the first few characters to uniquely identify the file in its directory.

To see an example, type cat /etc/mod but not press Enter; press Tab instead. Bash automatically completes the filename, so the command becomes /etc/modprobe.conf. Now press Enter to run the command.

![](bbox=[0.153, 0.401, 0.209, 0.473])

Whenever you type a filename, press Tab after the first few characters of the filename. Bash probably can complete the filename so that you don't have to type the entire name. If you don't enter enough characters to uniquely identify it, Bash beep. Just type a few characters and press Tab again.

# Going wild with asterisks and question marks

You can avoid typing long filenames another way. (After all, making less work for users is the idea of computers, isn't it?)

This particular trick involves the asterisk (*) and question mark (?) and a few more tricks. These special characters are wildcards that match zero or more characters in a line of text.

If you know MS-DOS, you may have used commands such as COPY *, A: to copy all files from the current directory to the A drive. Bash accepts similar wildcards in filenames. As you'd expect, Bash provides more options than the MS-DOS command interpreter does.

You can use three types of wildcards in Bash:

+   * The asterisk (*) matches zero or more characters in a filename. That means * denotes all files in a directory.

+   * The question mark (?) matches any single character. If you type test?, it matches any five-character text that begins with test.

+   * A set of characters in brackets matches any single character from that set. The string [aB]*, for example, matches any filename that starts with a or B.