illustrated, depending on which editor you want the changes to be implemented in. If you put a vim-specific behavior-changing option in the .exrc file, when you run vi, you will probably get a warning message in vi, but not a fatal error message.

You can modify any of several environment options to customize the behavior of the vi, vim, and gvim editors, either when you are in the editor at a given time, or for every editor session. These options include, for example, specifying maximum line length and automatically wrapping the cursor to the next line, displaying line numbers as you edit a file, and displaying the mode that the editor is in. You can use full or abbreviated names for most of the options. Some of the most important and useful options and their abbreviations are summarized in Table 3.8. Also see Table 3.9 for a summary of the use of the set command.

The set command in Last Line mode changes environmental options. There are two types of environmental options that can be modified with the set command: toggle options, which are either "on" or "off," and options that require the use of an argument.

For example, after typing :set showmode, you have toggled the mode display "on," and the editor displays the current mode at the bottom of the screen. If you then type :set noshowmode, you have toggled the mode display "off." Similarly, after typing :set nu, vi displays the line numbers for all the lines in the file. To turn "off" the line number display, type :set nonu. When the :set ai command has been executed, the next line is aligned with the beginning of the previous line. This useful feature allows you to easily indent source codes that you compose with vi. Pressing <Ctrl+D> on a new line moves the cursor to the previous indentation level.

# TABLE 3.8 Important Environmental Options for Vi, Vim, and Gvim

| Option | Abbreviation | Purpose |
|---|---|---|
| autoindent | ai | Aligns the new line with the beginning of the previous line. |
| ignorecase | ic | Ignores the case of a letter during the search process (with a / or the ? command). |
| list | list | Displays invisible characters, such as ^I for <Tab> and a $ for end-of-line characters. |
| nolist | nolist | Turns off the display of invisible characters. |
| noignorecase | noic | Instructs cases to be case sensitive. |
| number | nu | Displays line numbers when a file is being edited; line numbers are not saved as part of the file. |
| nonumber | nonu | Hides line numbers. |
| scroll |  | Sets the number of lines to scroll when the <Ctrl+D> command is used to scroll the vi screen up. |
| set |  | Displays all the vi variables that are set. |
| all |  | Displays all set vi variables and their current values. |
| showmode | smd | Displays the current vi mode in the bottom right corner of the screen. |
| noshowmode | nosmd | Turns off the mode of operation display. |
| wrapmargin | wm | Sets the wrap margin in terms of the number of characters from the end of the line, assuming a line length of 80 characters. |