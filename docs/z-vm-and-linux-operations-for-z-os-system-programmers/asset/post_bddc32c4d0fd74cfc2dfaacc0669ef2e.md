
> Note: When using the ALL command or the search (/) command, you can set your current line to be one of the lines of output. This enables you to exit the search results and to directly edit the file at the location you want.

## Setting tabs

You might want to place information in specific columns. The PF4 key functions like a Tab key on a keyboard. Each time you press the PF4 key, the cursor is positioned at the next tab column, where you can enter data. The editor defines initial tab settings according to file type; you can display them by using the following subcommand:

```
====> query tabs
```

You can change these settings one or more times during an editing session with the SET TABS subcommand:

```
====> set tabs 10 20 30
```

Using the example, the first time you press PF4, the cursor moves to column 10 in the window. The second time, it moves to column 20, and so forth. You can use PF4 for tabbing in regular XEDIT input mode, but not all other advanced XEDIT modes. To change the tab settings, enter another SET TABS subcommand. To view the current tab settings before changing them, use the following subcommand:

```
====> modify tabs
```

This displays the current SET TABS subcommand in the command line; you can type over the numbers and press Enter to define new tabs.

## Inserting an external file

The GET subcommand inserts all or part of another file into the file you are editing, after the current line. A file that you get is not destroyed; a copy of that file is inserted.

Before you enter the GET subcommand, make the current line be the line preceding where you want to insert data. That way, the file will be inserted immediately under the current line.

To insert another file at the end of your file, use the BOTTOM subcommand to make the last line current. To insert another file somewhere in the middle of your file, use the UP or DOWN subcommands to make the desired line current.

> z/OS analogy: This is similar to the COPY primary command of ISPF editor in z/OS.

## Inserting all of another file

To insert an entire file into the file you are editing, use the command:

```
====> get filename filetype
```

For example, if you are editing FILE1 and want to insert all of FILE2 SCRIPT A at the end of FILE1, move the line pointer to the end of the file by issuing the following command:

```
====> bottom
```

With the line pointer at the end of the current file, import the entire external file by issuing the following command:

```
====> get file2 script
```

When the entire second file has been inserted, the editor displays the message:

```
EOF reached
```

## Inserting a portion of another file

Sometimes, importing an entire file is unnecessary; instead, you might want only a portion of an external file. Use the GET command with additional optional arguments to insert a portion of another file.

The first additional parameter specifies the line number of the first line to import. The second additional parameter indicates the number of successive lines to insert. For example, to insert the first 10 lines of a second file:

```
====> get file2 data 1 10
```

## Powertyping

If you have to type a substantial amount of text continuously, without worrying about line numbers or word length, enter the command POWERINP. This places XEDIT in a mode called power input or powertyping mode. The shortest command abbreviation for POWERINP is POW.

When you are in powertyping mode, a *** Power Typing*** banner is displayed across the top of the window. Any time you want to leave powertyping mode, press the Enter key. Your text is formatted to fit the correct line width in a normal XEDIT session.

Combining the TOP or BOTTOM commands with POWERINP provides an easy method for prepending or appending to a file.

z/OS analogy: POW is similar to ISPF TextEntry (TE).

## Autosaving

To minimize the risk of losing your data, XEDIT provides the SET AUTOSAVE subcommand. This subcommand causes your file to be automatically written to disk after you have typed in or changed a certain number of lines. The syntax is:

```
SET AUTOSAVE n
```

The n specifies the number of typed-in or changed lines. For example, to write the file to disk or SFS directory every time you have changed 10 lines, enter:

```
====> set autosave 10
```

The number of alterations you have made to your file since the last AUTOSAVE is displayed as the alteration count (Alt=n) in the file identification line. When the alteration count is equal to the AUTOSAVE setting, and the file contains at least one record, the file is saved on disk or SFS directory and the alteration count is reset to zero (0).

You can enter the SET AUTOSAVE subcommand at any time during an editing session, but good practice would be to enter it right after you enter an XEDIT command to create a new file or to call an existing file from disk or SFS directory.

When a file is automatically saved, it is written to a new file that has a number for a file name and that has a file type of AUTOSAVE. If the system malfunctions during an editing session, you can recover all changes made up to the time of the last automatic save.

To do this, replace the original file with the AUTOSAVE file by using the CMS COPYFILE command with the REPLACE option. If you enter a SET AUTOSAVE subcommand while you are creating a new file or revising an existing file, and then enter a QUIT subcommand, the new or revised file is not saved, but the AUTOSAVE file is available from disk.

> z/OS analogy: This feature is similar to the RECOVERY ON command in the ISPF editor, except you cannot set the number of lines between each save. Pressing Enter or a PF key causes editing changes to be saved in a separate data set. If the editing session is terminated, you are prompted to recover the next time you edit the particular data set.

## Ending an editing session

You can end an editing session by using FILE or QUIT. When you use the XEDIT command to create a new file, the file is created in virtual storage. When you make changes to an existing file, those changes are made to a copy of the file that is brought into virtual storage (when the XEDIT command is entered).
