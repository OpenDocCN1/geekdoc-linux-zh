After you press Enter, the ispell command searches the system dictionary and displays matching words. On the other hand, the spell command is designed to display words in a given text file or stream that do not match. You can use the spell command interactively like this:

```
```
$ spell
giraffe
<EOT>
```
```

In this example, after you press Enter, the word giraffe is typed. After pressing Enter, type a Ctrl+d (the end-of-text marker), and the spell command will respond with:

```
```
giraffe
```
```

This indicates that the word is either misspelled or not in the system dictionary. If no word is echoed, the word is correct. As you can see, the spell command returns non-matching words. For example, to check the contents of a document such as linumpr.txt, you can use the spell command on the command-line with input redirection and other commands in a pipe like this:

```
```
$ spell < linumpr.txt | sort | uniq >misspelled.txt
```
```

This command line pipes the output stream of misspelled words in the document through the sort and uniq commands and saves the result in a file named misspelled.txt. You can then use the sed command or a text editor to fix the file. Spell checking documents interactively and fixing errors in context is, however, a much easier way to correct misspelling. That is the job of the ispell command, discussed next.

![](bbox=[0.04, 0.73, 0.12, 0.85])

> SuSE Linux includes the ispell command, but does not provide a spell command. However, you can use the ispell command to emulate spell. Create a shell script containing these lines:
> ```
> #!/bin/sh
> exec ispell -1 $*
> ```
> Save the file with the name spell, then use the chmod +x command to make the script executable and save it under the /usr/bin directory.

# ### Using ispell

The ispell, or International Ispell command, is an interactive spell-check program for Linux and a number of UNIX operating systems. This program is included