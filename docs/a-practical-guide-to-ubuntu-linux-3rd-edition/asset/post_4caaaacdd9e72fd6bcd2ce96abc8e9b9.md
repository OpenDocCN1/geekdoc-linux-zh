
## cat: DISPLAYS A TEXT FILE

  cat utility displays the contents of a text file. The name of the command is derived from catenate, which means to join together, one after the other. (Figure 7-8 on page 247 shows how to use cat to string together the contents of three files.)

A convenient way to display the contents of a file to the screen is by giving the command cat, followed by a SPACE and the name of the file. Figure 5-1 shows cat displaying the contents of practice. This figure shows the difference between the ls and cat utilities: The ls utility displays the name of a file, whereas cat displays the contents of a file.

## rm: DELETES A FILE

The rm (remove) utility deletes a file. Figure 5-1 shows rm deleting the file named practice. After rm deletes the file, ls and cat show that practice is no longer in the directory. The ls utility does not list its filename, and cat says that no such file exists. Use rm carefully.

### A safer way of removing files

> tip You can use the interactive form of rm to make sure that you delete only the file(s) you intend to delete. When you follow rm with the -i option (see page 139 for a tip on options) and the name of the file you want to delete, rm displays the name of the file and then waits for you to respond with y (yes) before it deletes the file. It does not delete the file if you respond with a string that begins with a character other than y.

```
$ rm -i toollist
rm: remove regular file 'toollist'? y
```

**Optional:** You can create an alias (page 346) for `rm -i` and put it in your startup file (page 204) so that rm always runs in interactive mode.

## less Is more: DISPLAY A TEXT FILE ONE SCREEN AT A TIME

**Pagers** When you want to view a file that is longer than one screen, you can use either the less utility or the more utility. Each of these utilities pauses after displaying a screen of text; press the SPACE bar to display the next screen of text. Because these utilities show one page at a time, they are called pagers. Although less and more are very similar, they have subtle differences. At the end of the file, for example, less displays an END message and waits for you to press q before returning you to the shell. In contrast, more returns you directly to the shell. While using both utilities you can press h to display a Help screen that lists commands you can use while paging through a file. Give the commands less practice and more practice in place of the cat command in Figure 5-1 to see how these commands work. Use the command less /etc/adduser.conf instead if you want to experiment with a longer file. Refer to the less and more man pages for more information.

## hostname: DISPLAYS THE SYSTEM NAME

The hostname utility displays the name of the system you are working on. Use this utility if you are not sure that you are logged in on the right machine.

```
$ hostname
bravo.example.com
```

## WORKING WITH FILES

This section describes utilities that copy, move, print, search through, display, sort, and compare files.

### Filename completion

After you enter one or more letters of a filename (following a command) on a command line, press TAB and the Bourne Again Shell will complete as much of the filename as it can. When only one filename starts with the characters you entered, the shell completes the filename and places a SPACE after it. You can keep typing or you can press RETURN to execute the command at this point. When the characters you entered do not uniquely identify a filename, the shell completes what it can and waits for more input. When pressing TAB does not change the display, press TAB again to display a list of possible completions. For more information refer to “Pathname Completion” on page 342.

### cp: COPIES A FILE

The cp (copy) utility (Figure 5-2) makes a copy of a file. This utility can copy any file, including text and executable program (binary) files. You can use cp to make a backup copy of a file or a copy to experiment with.

The cp command line uses the following syntax to specify source and destination files:

```
cp source-file destination-file
```

The *source-file* is the name of the file that cp will copy. The *destination-file* is the name that cp assigns to the resulting (new) copy of the file.

![](img/2344fc4a798f29dca9e8b5ed7288171a_213_0.png)

**Figure 5-2** cp copies a file

The `cp` command line in Figure 5–2 copies the file named **memo** to **memo.copy**. The period is part of the filename—just another character. The initial `ls` command shows that **memo** is the only file in the directory. After the `cp` command, a second `ls` shows two files in the directory, **memo** and **memo.copy**.

Sometimes it is useful to incorporate the date in the name of a copy of a file. The following example includes the date January 30 (**0130**) in the copied file:

```
$ cp memo memo.0130
```

Although it has no significance to Linux, the date can help you find a version of a file you created on a certain date. Including the date can also help you avoid overwriting existing files by providing a unique filename each day. For more information refer to “File names” on page 201.

Use `scp` (page 667) or `ftp` (page 687) when you need to copy a file from one system to another on a common network.

### cp can destroy a file

If the *destination-file* exists *before* you give a `cp` command, `cp` overwrites it. Because `cp` overwrites (and destroys the contents of) an existing *destination-file* without warning, you must take care not to cause `cp` to overwrite a file that you need. The `cp -i` (interactive) option prompts you before it overwrites a file. See page 139 for a tip on options.

The following example assumes that the file named **orange_2** exists before you give the `cp` command. The user answers **y** to overwrite the file:

```
$ cp -i orange orange.2
cp: overwrite 'orange.2'? y
```

### mv: CHANGES THE NAME OF A FILE

The `mv` (move) utility can rename a file without making a copy of it. The `mv` command line specifies an existing file and a new filename using the same syntax as `cp`:

```
mv existing-filename new-filename
```

The command line in Figure 5–3 changes the name of the file **memo** to **memo.0130**. The initial `ls` command shows that **memo** is the only file in the directory. After you give the `mv` command, **memo.0130** is the only file in the directory. Compare this result to that of the `cp` example in Figure 5–2.

The `mv` utility can be used for more than changing the name of a file. Refer to “mv, cp: Move or Copy Files” on page 212. See the `mv` info page for more information.

### mv can destroy a file

Just as `cp` can destroy a file, so can `mv`. Also like `cp`, `mv` has a `-i` (interactive) option. See the caution box labeled “cp can destroy a file.”

```
$ ls
memo
$ mv memo memo.0130
$ ls
memo.0130
```

**Figure 5-3** mv renames a file

## lpr: PRINTS A FILE

The **lpr** (line printer) utility places one or more files in a print queue for printing. Linux provides print queues so that only one job is printed on a given printer at a time. A queue allows several people or jobs to send output simultaneously to a single printer with the expected results. On systems that have access to more than one printer, you can use **lpstat -p** to display a list of available printers. Use the **-P** option to instruct **lpr** to place the file in the queue for a specific printer—even one that is connected to another system on the network. The following command prints the file named **report**:

```
$ lpr report
```

Because this command does not specify a printer, the output goes to the default printer, which is *the* printer when you have only one printer.

The next command line prints the same file on the printer named **mailroom**:

```
$ lpr -P mailroom report
```

You can see which jobs are in the print queue by giving an **lpstat -o** command or by using the **lpq** utility:

```
$ lpq
lp is ready and printing
Rank Owner Job Files Total Size
active max 86 (standard input) 954061 bytes
```

In this example, Max has one job that is being printed; no other jobs are in the queue. You can use the job number (86 in this case) with the **lprm** utility to remove the job from the print queue and stop it from printing:

```
$ lprm 86
```

You can send more than one file to the printer with a single command. The following command line prints three files on the printer named **laser1**:

```
$ lpr -P laser1 05.txt 108.txt 12.txt
```

Refer to Chapter 14 for information on setting up a printer and defining the default printer.
