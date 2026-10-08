# Chapter 11: Using Command-Line Tools

list. When you find the command that you want to re-execute, you can simply press Return to re-execute it or edit that command using Emacs commands (by default) such as Ctrl-B to move backward one character in that command, Ctrl+F to move forward in that one character, the Backspace and Delete keys to delete the previous and current characters, and so on.

Obviously, if the command you want to re-execute is far back in your command history list, scrolling back through a few hundred commands can be a bit tedious. In this case, you can use the exclamation point to identify a particular command from the history list in either of the following ways:

+   - Identifying a command by its sequence number: Each command in the history list is preceded by its sequence number in your command history. If you've displayed the history list and can see the command that you want to execute, you can re-execute a specific command by typing an exclamation mark followed by its sequence number. for example, using the history output displayed earlier in this section, the command !236 would re-execute the vi ~/.bashrc.
- Identifying a command by name: You can re-execute the most recently executed command that begins with a certain command name by typing an exclamation mark followed by the command that you want to re-execute. For example, using the history output displayed earlier in this section, the command !vi would re-execute the vi ~/.bashrc command.

# Tip

If you want to re-display a previous command and edit it before re-executing it, you can use the history mechanism's : modifier to simply print the command without executing it. You can then type Ctrl+P to display that command, edit it however you wish, and then press Return to execute the modified command. ■

If you've already executed several similar commands, you can narrow down the list of those shown by the command history | grep vi uses displaying commands that contain a substring. For example, the command history | grep vi uses a pipe and the grep command to display only lines of output from the history order that contain the string vi. (see the section, "Pipes and Input Output-Direction" for more information about connecting different commands in this way.)

The shell's command-line history mechanism is extremely powerful, and this discussion only scratches the surface of the myriad ways that you can save yourself by recalling and updating previously executed commands. For all the gory details on the shell's command-line history mechanism, use the info bash command to display the current online help for the bash command.

# Using Command and Filename Completion

As you've seen throughout this chapter, the command line provides a very powerful, flexible mechanism for executing commands, but one of the goals of all UNIX and Linux developers seems to have to allowed all users to type as few characters as possible to execute commands.