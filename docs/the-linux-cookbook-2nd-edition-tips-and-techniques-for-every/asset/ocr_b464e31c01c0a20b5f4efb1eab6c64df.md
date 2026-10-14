A list of other recommended shells is given at Recipe 3.9.5 [Using Other Shells], page 92. For more information on using Bash beyond what this chapter provides, consult the Info documentation for bash (see Recipe 2.8.5 [Reading an Info Manual], page 48).

# 3.1 Typing at the Command Line

In Recipe 2.4 [Running a Command], page 36, you learned how to run commands by typing them in at the shell prompt. The line where you type in a command at a shell prompt is called the command line (it's also called the input line). The process of writing a command on the command line is called command line editing.

The following sections describe some important features of command line editing, such as quoting special characters and strings, letting the shell complete your typing, re-running commands, and running multiple commands.

NOTES: For more information on Bash's command line editing features, consult the Info documentation for bash (see Recipe 2.8.5 [Reading an Info Manual], page 48).

# 3.1.1 Using Basic Command Line Editing Keys

There are special keystrokes for moving about the input line and editing the line you are typing; the following table describes them.

| Typing Commands | |
|---|---|
| text | Insert text at the point where the cursor is; any text already existing to the right of the cursor is shifted further right to accommodate the new text. |
| RET | Send the command line to Bash for execution (in other words, it runs the command typed at the shell prompt). You don't have to be at the far right end of the command line to type RET; you can type it when the cursor is anywhere on the command line. |
| Cutting and Pasting | |
| BKSP or CTRL-H | Delete the character to the left of the cursor. |
| DEL or CTRL-D | Delete the character the cursor is underneath. |