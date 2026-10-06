# Line Length and File Size

The vim editor operates on any format file, provided the length of a single “line"
(that is, the characters between two NEWLINE characters) can fit into available memory.
The total length of the file is limited only by available disk space and memory.

# Windows

The vim editor allows you to open, close, and hide multiple windows each editing a ndifferent file. Most of the window commands are CONTROL-w followed by another letter. For example, CONTROL-w opens a second window (splits the screen) editing the same file. CONTROL-w opens a second window that is editing an empty file. CONTROL-w moves the cursor between windows, and CONTROL-w q (or q) quits (closes) a window. If you give a Quit command and have not written out the text you have entered/changed, vim will prompt you to do so. The command :help windows for a complete list of windows commands.

# File Locks

When you edit an existing file, vim displays the first few lines of the file, gives status information about the file on the status line, and locks the file. A user attempting to edit the file at the same time as you does (assuming proper permissions) will see a message similar to the one shown in Figure 10-7.

Although it is advisable to follow the instructions that vim displays, the second user can edit the file and write it out with a different filename. Refer to the next section.

![](bbox=[0.344, 0.606, 0.773, 0.856])

Figure 10-7 Attempting to open a locked file