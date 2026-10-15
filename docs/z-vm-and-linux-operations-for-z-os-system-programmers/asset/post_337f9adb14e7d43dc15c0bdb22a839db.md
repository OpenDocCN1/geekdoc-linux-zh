
To move a block of lines, enter the double character MM in the prefix area of both the first and last lines to be moved. The first and last lines to be moved, and the destination line, can all be on different screens. You can use PF selections to scroll the screen before pressing Enter.

z/OS analogy: In z/OS (ISPF editor), the M(ove) command is identical, but line command A(fter) is used instead of F(ollowing), and B(efore) instead of P(receeding).

## Copying lines

The procedure for copying lines is the same as for moving lines, except that you enter a C or CC prefix subcommand instead of M or MM. The copy operation leaves the original lines in place but makes a copy at the destination line, which is indicated by F or P.

z/OS analogy: In z/OS (ISPF editor), the C(opy) command is identical, with the same exceptions as stated for the M(ove) command previously

## Canceling prefix subcommands

If you entered one or more prefix subcommands that created a pending status, you can cancel all of them by entering the following subcommand on the command line:

```
====> reset
```

After you press Enter, all prefix subcommands disappear from the display and the prefix areas are restored with equal signs, numbers, or blank characters, depending on your particular XEDIT configuration.

If you have typed any prefix subcommands (even those that do not cause a pending status) but have not yet pressed Enter, you can clear your screen to remove them. If you have only typed a few characters, it is also be sufficient to simply type over them with blank characters.

## Moving through a file

XEDIT lets you move backward, forward, up, down, and to the top and bottom in a file. You have already seen that the PF7 and PF8 selections are set to the BACKWARD and FORWARD subcommands, which scroll one full window backward or forward. You may also enter the BACKWARD and FORWARD subcommands in the command line. The format of these subcommands is:

```
BAckwardn
FOrwardn
```

Here n is the number of window displays to scroll. This is like pressing PF7 or PF8 n times. If you omit n, the editor scrolls one window backward or forward.

If you enter a BACKWARD subcommand when the current line is the Top of File line, the editor wraps around the file, making the last line of the file the new current line. Similarly, if you enter a FORWARD subcommand when the current line is the End of File line, the editor makes the first line of the file the new current line.

Suppose the file is many screens long and the current screen display is somewhere in the middle of the file. To return to the beginning of the file, you could enter multiple BACKWARD subcommands, or you can enter the TOP subcommand.

The TOP subcommand makes the Top of File line the new current line. Enter the TOP subcommand as shown:

```
====> top
```

The BOTTOM subcommand makes the last line of the file the new current line. Enter the BOTTOM subcommand as shown:

```
====> bottom
```

These subcommands are useful when you want to insert new lines either at the beginning or end of a file.

Suppose that you want to move the file up or down a few lines instead of a whole window. Use the DOWN subcommand to advance the line pointer one or more lines toward the end of a file. The line pointed to becomes the new current line. For example, the following command causes the fifth line down from the current line to be the new current line:

```
====> down 5
```

If you omit the number, then 1 (one line) is assumed. The UP subcommand moves the line pointer toward the beginning of the file. The line pointed to becomes the new current line. For example, the following command causes the fifth line up from the current line to be the new current line.

```
====> up 5
```

Again, if you omit the number, then 1 (one line) is assumed.

z/OS analogy: In z/OS (ISPF editor), these commands are identical.

## Searching within a file

Searching for a particular word or phrase is a very important part of text editing on any platform, and is especially important when using CMS to edit various configuration files. When using XEDIT, you can search by using the forward slash (/) on the command line, as shown:

```
====> /target_search_string
```

After pressing Enter, XEDIT moves to the first line it finds that matches your search phrase. XEDIT searches in the direction of the current line toward the end of the file. To move to the next occurrence, reenter the command:

```
====> /target_search_string
```

A more convenient solution is to prefix the search command with the ampersand (&) character:

```
====> &/target_search_string
```

Even easier is to enter equals (=) on the command line.

After pressing Enter, XEDIT moves to the first line it finds that matches your search phrase. Each time you press Enter again, XEDIT moves to the next match in the file.

This can be a very powerful way to move through files, but you can also search in reverse. The search is performed from the current line moving toward the top of the file. To search in reverse, prefix the search command with the minus sign (-), for example:

```
====> -/target (reverse search)
```

In some cases highlighting all occurrences of a phrase within a file can be useful. To accomplish this task, XEDIT provides the ALL command:

```
====> all /target
```

From the XEDIT command line, the ALL command lists all lines that contain instances of the target search phrase. To return to normal editing mode, issue the ALL command with no search phrase as shown:

```
====> all
```

> z/OS analogy: In z/OS, this is similar to the F 'txt' (Find) primary command of ISPF editor.
