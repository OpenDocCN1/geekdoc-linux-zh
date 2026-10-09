# cat: DISPLAYS A TEXT FILE

The cat utility displays the contents of a text file. The name of the command is derived from catenate, which means to join together, one after the other. (Figure 7-8 on page 247 shows how to use cat to string together the contents of three files.)

A convenient way to display the contents of a file to the screen is by giving the command cat, followed by a SPACE and the name of the file. Figure 5-1 shows cat displaying the contents of practice. This figure shows the difference between the ls and cat utilities: The ls utility displays the name of a file, whereas cat displays the contents of a file.

# rm: DELETES A FILE

The rm (remove) utility deletes a file. Figure 5-1 shows rm deleting the file named practice. After rm deletes the file, ls and cat show that practice is no longer in the directory. The ls utility does not list its filename, and cat says that no such file exists. Use rm carefully.

# A safer way of removing files

> tip You can use the interactive form of rm to make sure that you delete only the file(s) you intend to delete. When you follow rm with the -i option (see page 139 for a tip on options) and the name of the file you want to delete, rm displays the name of the file and then waits for you to respond with y (yes) before it deletes the file. It does not delete the file if you respond with a string that begins with a character other than y.

```
$ rm -i toollist
rm: remove regular file 'toollist'? y
```

**Optional:** You can create an alias (page 346) for `rm -i` and put it in your startup file (page 204) so that rm always runs in interactive mode.

# less Is more: DISPLAY A TEXT FILE ONE SCREEN AT A TIME

**Pagers** When you want to view a file that is longer than one screen, you can use either the less utility or the more utility. Each of these utilities pauses after displaying a screen of text; press the SPACE bar to display the next screen of text. Because these utilities show one page at a time, they are called pagers. Although less and more are very similar, they have subtle differences. At the end of the file, for example, less displays an END message and waits for you to press q before returning you to the shell. In contrast, more returns you directly to the shell. While using both utilities you can press h to display a Help screen that lists commands you can use while paging through a file. Give the commands less practice and more practice in place of the cat command in Figure 5-1 to see how these commands work. Use the command less /etc/adduser.conf instead if you want to experiment with a longer file. Refer to the less and more man pages for more information.