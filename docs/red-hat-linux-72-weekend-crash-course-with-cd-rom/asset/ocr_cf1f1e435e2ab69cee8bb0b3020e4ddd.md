The wildcard specification s.*s* denotes all filenames that meet these criteria. Thus, you can perform the search with the following command:

```
grep "*typeef struct*" /usr/include/s*.h
```

The string contains a space (you want the grep command to find, so you have to enclose that string in quotation marks (")). This method ensures that Bash does not try to interpret each word in the string as a separate command-line argument.

Although the asterisk (*) matches any number of characters, the question mark (?) matches a single character. Suppose you have four files—image1.pcx, image2.pcx, image3.pcx, and image4.pcx—in the current directory. To copy these files to the /mnt/floppy directory, use the following command:

```
cp image?.pcx /mnt/floppy
```

Bash replaces the single question mark with any single character and copies the four files to /mnt.

The third wildcard format ([...] ) matches a single character from a specific set. You may want to combine this format with other wildcards to narrow down the matching file-names to a smaller set. To see a list of all filenames in the /etc/X11/Xdm directory that start with x or X, type the following command:

```
ls /etc/X11/Xdm/[xX]*
```

![](bbox=[0.08, 0.52, 0.15, 0.58])

> If Bash does not find any filenames matching the [...] wildcard format when expanding it, Bash leaves the wildcard specification intact.

# **Looking at the command history**

To make it easy for you to repeat long commands, Bash stores up to 500 (the default) previously executed commands. This feature is called a **command history** (a list of old commands). To see the command history, type **history**. Bash displays a numbered list of the old commands, including those that you entered during previous logins. That list may resemble the following:

```
1  cd
2  ls -a
3  more /etc/X11/XF86Config
4  history
```

If the command list is too long, you may choose to see only the last few commands. To see the last 10 commands only, type this command:

```
history 10
```

To repeat a command from the list that the **history** command shows, simply type an exclamation point (!), followed by that command's number. To repeat command number **3**, type **!3**.