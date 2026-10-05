
# This is the top of the INFO tree

This (the Directory node) gives a menu of major topics.
Ting 'q' exits, '?' lists all Info commands, 'd' returns here,
'b' gives a primer for first timers.
Emacs-<Return> visits the Emacs topic, etc.

In Emacs, you can click button 2 on a menu item or reference

to select it.

- Menu
- Archiving
- Cpio (cpio): Copy-in/copy-out archive to tar or disk.
- Tar (tar): Making tape (or disk) archives.
- Basics
- Common options: Common options.
- Coreutils (coreutils): Get GNU (file, text, shell) utilities.
- Date format (coreutils) Date input format.
- File permissions (coreutils) File permissions.
- Finding files (find): Operation on files matching criteria.
- Edit (ed): The GNU Line Editor.

Figure 4.1: pinfo document viewer, directory tree

Info documentation is comprehensive and hyperlinked. It is possible to insert info pages into multiple formats. By contrast, man pages are optimized for printed output. The Info format is more flexible than man pages, allowing discussion of complex commands and concepts. Man pages, Info nodes are read from the command line, using the pinfo command.

A typical page has a small amount of content focusing on one particular topic, command, tool, or file. The Info documentation is a comprehensive document. Info provides the following improvements:

- One single document for a large system containing all the necessary information for that system
- Hyperlinks
- A complete browsable document index
- A full text search of the entire document

Some commands and utilities have both man pages and info documentation; usually, the Info documentation is more in depth. Compare the differences in the tar documentation using man and pinfo:

```
[user@host ~] man tar
[user@host ~] pinfo tar
```

The pinfo reader is more than the original info command. To browse a specific topic, use the pinfo topic command. The pinfo command without an argument opens the top directory. New documentation becomes available in pinfo when their software packages are installed.

> NOTE: If no info topic exists in the system for a particular entry that you requested, Info will look for a matching man page and display that instead.

# COMPARING GNU INFO AND MAN PAGE NAVIGATION

The pinfo command and the man command use slightly different navigational keystrokes. The following table compares the navigational keystrokes for both commands:

pinfo and man, key binding comparison

| NAVIGATION | PINFO | MAN |
| --- | --- | --- |
| Scroll forward (down) one screen | PageDown or Space | PageDown or Space |
| Scroll backward (up) one screen | PageUp or b | PageUp or b |
| Display the directory of topics | D | - |
| Scroll forward (down) one half-screen | - | D |
| Display the parent node of a topic | U | - |
| Display the top (up) of a topic | HOME | G |
| Scroll backward (up) one half-screen | - | U |
| Scroll forward (down) to next hyperlink | DownArrow | - |
| Open topic at cursor location | Enter | - |
| Scroll forward (down) one line | - | DownArrow or Enter |
| Scroll backward (up) to previous hyperlink | UpArrow | - |
| Scroll backward (up) one line | - | UpArrow |
| Search for a pattern | /string | /string |
| Display next node (chapter) in topic | N | - |
| Repeat previous search forward (down) | / then Enter | n |
| Display previous node (chapter) in topic | P | - |
| Repeat previous search backward (up) | - | ShiftN |
| Quit the program | Q | Q |

> REFERENCES
pinfo info (Info: An Introduction)
npinfo pinfo (Documentation for pinfo)

The GNU Project
http://www.gnu.org/gnu/thegnuproject.html
npinfo(1) and info(1) man pages

# GUIDED EXERCISE

# READING INFO DOCUMENTATION

In this exercise, you will look up information stored in GNU Info documents by navigating those documents with command-line tools.

# OUTCOMES

You should be able to navigate GNU Info documentation with command-line tools.

# BEFORE YOU BEGIN

Log in to workstation as student using student as the password.

On workstation, run the lab help-info start command.

```
[student@workstation ~$ lab help-info start
```

- 1. On workstation launch info without any arguments.

```
[student@workstation ~$ info
```

- 2. Navigate to the Common options topic.
Use UpArrow or DownArrow until (coreutils) Common options is highlighted.

- Basics
- Bash: (bash). The GNU Bourne-Again Shell.
- Common options: (coreutils)Common options.

> Figure 4.2: Bash documentation

- 3. Press Enter to view this topic.

```
File: coreutils.info, Mode: Common options, Next: Output of entries file, Prev: Introduction, Up: Top
Common options
```

Certain options are available in all of these programs. Rather than writing descriptions for each of the programs, they are described here. (In fact, every GNU program accepts (or should accept) these options).
Normally options and operands appear in any order, and programs act as all the options appear before any operands. For example, 'sort -t :' likes 'sort -r -t :', since 'i' is an option of '-t'. However, if the 'POSIX_COR' environment variable is set, options must appear before operands, unless otherwise specified for a particular command.

> Figure 4.3: Common options info topic

- 4. Browse through this Info topic. Whether long-style options can be abbreviated.

Use PageUp and PageDown to navigate through the topic. Yes, many programs allow long
options to be abbreviated.

- 5. Determine the symbols -- signify when used as a command argument.
The symbols -- signify the end of command options and the start of command arguments
in complex commands where the shell's command-line parser might not correctly make the
distinction.

- 6. Without exiting pinfo, move to the GNU Coreutils node.
Press U to move to the top node of the topic.

- 7. Return to the top level topic.
Press U. Observe when positioned at the top of a topic node, moving returns to
the directory of topics. Alternately, pressing D from any level or topic moves directly to
the directory of topics.

- 8. Search for the pattern coreutils and select it.
- 9. Select the topic. Press by the search for "coreutils".
- 10. Move up two levels to return to the directory of topics.
- 11. Press Q to quit pinfo.
- 12. Use the pinfo command again, specifying coreutils as the command line.

```
[student@workstation ~$ pinfo coreutils
```

- 13. Select the Disk usage topic.
Press DownArrow to highlight Disk usage, then press Enter to select this topic.

- 14. View your PostScript file using the various evince options you researched. Close your document file when you are finished.

# Finish

On workstation, run the lab help-info finish to complete this exercise.

```
[student@workstation ~$ lab help-info finish
```

This concludes the guided exercise.

# GETTING HELP IN RED HAT ENTERPRISE

PERFORMANCE CHECKLIST
In this lab, you will look up information to help you complete tasks in man pages and GNU Info documents.

OUTCOMES
You should be able to:

- Locate relevant commands by searching man pages and Info nodes.
- Learn new options for commonly used commands.
- Use appropriate tools to view and print documentation and other non-text formatted files.

BEFORE YOU BEGIN
Log in to workstation as student using student as the password.
On workstation, run the lab help-review start.

```
[student@workstation ~$ lab help-review start
```

- 1. On workstation, determine how to prepare a man page for printing. Specifically, find what format or rendering language is used for printing.

- 2. Create a formatted output file of the password man page. Call the file password.ps. Determine the file content format. Inspect the contents of the password.ps file.

> NOTE
Created output of the password man page using the following command:

[student@workstation $] man -t password > password.ps

The symbol redirects the contents of the man page to the password.ps file. This command is taught in more detail in a following chapter.

- 3. Using man, learn the commands used for viewing and printing PostScript files.

- 4. Learn how to use the evince() viewer in preview mode. Also, determine how to open a document starting on a specific page.

- 5. View your PostScript file using the various evince options you researched. Close your document file when you are finished.
