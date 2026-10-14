pattern. To move to the next file, press N; to move to the previous file, press P.

⇒ To page through all of the UNIX FAQ files in /usr/doc/FAQ, type:

```
$ less /usr/doc/FAQ/unix-faq-part* RET
```

This command starts less, which then opens all of the files that match the given pattern /usr/doc/FAQ/unix-faq-part*, and begins displaying the first one, as in Figure 9-1.

# METHOD #2

Another method is to use cat to concatenate all the files together, and pipe that output to less. There will be no indicator to mark where one file ends and another begins, but you can scroll through the entire text cleanly without pressing buttons to move from file to file.

⇒ To page through all of the UNIX FAQ files in /usr/doc/FAQ all at once, type:

```
$ cat /usr/doc/FAQ/unix-faq-part* | less RET
```

There is no indicator when one file ends and the next begins, but rather, all are treated as one long file in the order given. (In this case, where the wildcard character was used, they are displayed in the order in which the shell expands the "*" to all of their names.)

# 9.2 Displaying Text

The simplest way to view text is to send it to the standard output. This is useful for displaying part of a text, or for passing part of a text to other tools in a command line.

Many people still use cat to view a text file, especially if it is a very small file. To output all of a file's contents on the screen, use cat and give the file name as an argument.

⇒ To output the contents of the file notes, type:

```
$ cat notes RET
```

If you have a small text file that you want to look at, you just cat it to the screen. It's quick, it gets the job done, you don't have to think about it. But while it is useful for concatenating text (see Recipe 10.6 [Concatenating Text], page 256), it isn't always the best way to peruse or read text—a very large text will scroll off the top of the screen, for example.