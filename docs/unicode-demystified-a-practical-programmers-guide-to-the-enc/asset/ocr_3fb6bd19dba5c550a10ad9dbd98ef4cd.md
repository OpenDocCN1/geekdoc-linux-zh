# Chapter 10 The vim Editor

![](bbox=[0.315, 0.055, 0.795, 0.303])

Figure 10-2 Starting vim without a filename

+   - builtin_vt320
- builtin_vt52
- builtin_xterm-ansi
- builtin_iris_debug
- builtin_dumb
- defaulting to 'ansi'

If you want to reset your terminal type, press ESCAPE, and give the following command to exit vim and get the shell prompt back:

```
:q!
```

When you enter the colon (;), vim moves the cursor to the bottom line of the screen. The characters q tell vim to quit without saving your work. (You will not ordinarily exit from vim this way you typically want to save your work.) You must press RETURN after you give this command. Once you get the prompt back, refer to “Specifying Your Terminal” on page 1402, and start vim again.

If you start it without a filename, vim assumes you are a novice and tells you how to get started (Figure 10-2).

Continuing with the practice file example: The practice file is new, so it contains no text. The vim editor displays a message similar to the one shown in Figure 10-1 on the status (bottom) line of terminal to show that you are creating and editing a new file. Your version of vim may display a different message. When you edit an existing file, vim displays the first few lines of the file and gives status information about the file on the status (bottom) line.

# Command and Input Modes

Two of the vim editor's modes of operation are Command mode and Input mode (Figure 10-3). While vim is in Command mode, you can give vim commands. For example, in Command mode you can delete text or exit from vim. You can also