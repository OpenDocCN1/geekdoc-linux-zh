
# cat: DISPLAYS A TEXT FILE

The cat utility displays the contents of a text file. The name of the command is derived from catenate, which means to join together, one after the other (Figure 7-8 on page 247 shows how to use cat to strip the contents of three files.)

A convenient way to display the contents of a file is by giving the command cat, followed by a SPACE and the name of the file. Figure 5-1 shows how cat displaying the contents of practice. This figure shows the difference between the ls and cat utilities: The ls displays the name of a file, whereas cat displays the contents of a file.

# rm: DELETES A FILE

The rm (remove) utility deletes a file. Figure 5-1 shows rm deleting the file named practice. After rm deletes the file, ls and cat show that practice is no longer in the directory. The ls utility does not list its filename, and cat says that no such file exists. Use carefully.

# A safer way of removing files

You can use the interactive form of rm to make sure that you delete only the file(s) you intend to. When you follow rm with the -i option (see page 139 for it options) and the name of the file you want to delete, rm displays the name of the file and waits for you to respond with y (yes) before deletes the file. It does not delete the file if you respond with a string that has a character other than y.

```
rm -i toolist
rm: remove regular file 'toollist'? y
```

Optional: You can create an alias (page 346) for rm -i and put it in your startup file (page 204) so that rm always runs in interactive mode.

# less: DISPLAY A TEXT FILE ONE AT A TIME

When you want to view a file that is longer than one screen, you can use either the less utility or the more utility. Each of these utilities allows displaying a screen of text; press the SPACE bar to display the next screen of text. Because these utilities show one page at a time, they are called pagers. Although less and more are similar, they have subtle differences. At the end of the file, for example, less displays an END message and waits for you to press q before returning to the shell. In contrast, more returns you directly to the shell. While using less displays a Help screen that lists commands you can use paging through a file. Give the commands less practice and more practice in place of the cat command in Figure 5-1 to see how these commands work. Use the command /etc/adduser.conf instead if you want to experiment with a longer file. Refer to the less and more pages for more information.

# hostname: DISPLAYS THE SYSTEM NAME

The hostname displays the name of the system you are working on. Use this utility if you are not sure that you are logged in on the right machine.

```
$ hostname
bravo.example.com
```

# WORKING WITH FILES

This section describes utilities that copy, move, print, search through, display, sort, and compare files.

# Filename completion

- * tip After you enter one or more letters of a filename (following a command) on a command line, press TAB and the Bourne Again Shell will complete as much of it as it can. When only one filename starts with the characters you entered, the shell completes the filename and places a SPACE after it. You can keep typing or you can press RETURN to execute the command at this point. When the characters you entered do not uniquely identify a filename, the shell completes and waits for more input. When pressing TAB does not change the display, TAB again to display a list of possible completions. For more information refer to "Pathname Completion" page 342.

# cp: COPIES A FILE

cp (copy) utility (Figure 5-2) makes a copy of a file. This utility can copy any file, including text and executable program (binary) files. You can use cp to make a backup copy of a file or a copy to experiment with.

The cp command line uses the following syntax to specify source and destination files:

```
cp source-file destination-file
```

The source-file is the name of the file that cp will copy. The destination-file is the name that cp assigns to the resulting (new) copy of the file.

```
$ ls
memo
$ cp memo memo.copy
$ ls
memo memo.copy
```

Figure 5-2 cp copies a file

The cp command line in Figure 5-2 copies the file named memo to memo.copy. The period is of the filename—just another character. The initial ls shows that memo is the only file in the directory. After the cp command, a second ls shows two files in the directory, memo and memo.copy.

Sometimes it is useful to incorporate the date in the name of a copy of a file. The following example includes the date January 30 (0130) in the copied file:

```
$ cp memo memo.0130
```

Although it has no significance to Linux, the date can help you find a version of a file you created on a certain date. Including the date can also help you avoid writing files by providing a unique filename each day. For more information refer to "Filenames" on page 201.

Use cp (page 667) or ftp (page 687) when you need to copy a file from one system to another on a common network.

# cp destroy a file

If the destination-file exists before you give a cp command, it overwrites it. Because cp overwrites (and destroys the file), use the -i option to be prompted. The following example shows how the interactive mode works:

```
$ cp -i memo memo.copy
cp: overwrite 'memo.copy'? y
```

# mv: CHANGES THE NAME OF A FILE

The mv (move) utility can rename a file. Figure 5-3 shows mv changing the name of memo to memo.0130. The initial ls shows that memo is the only file in the directory. After the mv command, a second ls shows that memo.0130 is in the directory.

The mv command line uses the following syntax:

```
mv source-file destination-file
```

The source-file is the name of the file that mv will move. The destination-file is the name that mv assigns to the resulting file.

```
$ ls
memo
$ mv memo memo.0130
$ ls
memo.0130
```

Sometimes it is useful to incorporate the date in the name of a copy of a file. The following example includes the date January 30 (0130) in the copied file:

```
$ cp memo memo.0130
```

Although it has no significance to Linux, the date can help you find a version of a file you created on a certain date. Including the date can also help you avoid overwriting files by providing a unique filename each day. For more information refer to "Filenames" on page 201.

Use cp (page 667) or ftp (page 687) when you need to copy a file from one system to another on a common network.

# cp destroy a file

If the destination-file exists before you give a cp command, it overwrites it. Because cp overwrites (and destroys the file), use the -i option to be prompted. The following example shows how the interactive mode works:

```
$ cp -i memo memo.copy
cp: overwrite 'memo.copy'? y
```

# lpr: PRINTS A FILE

```
$ lpr memo
$ mv memo memo.0130
$ lpr memo.0130
```

Figure 5-3 mv copies a file

The lpr (printer) utility uses one or more files in a printer for printing. Linux provides print queues so that only one job is printed on a printer at a time. A queue allows several people or jobs to send output simultaneously to a printer. Systems that have access to more than one printer, can use lpstat -p to display a list of available printers. Use the -P option to instruct lpr to place the file in the queue for a specific printer—even one that is connected to another system.
