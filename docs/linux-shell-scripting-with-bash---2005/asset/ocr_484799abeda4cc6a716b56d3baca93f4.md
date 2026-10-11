+   OSTYPE—The name of the operating system.

+   PATH—Colon-separated list of search paths to find a command to execute.

+   PPID—The process ID of the shell's parent process.

+   PROMPT_COMMAND—Command to execute before the setting of the PS1 primary prompt string.

+   PS1—The primary prompt string.

+   PS2—The secondary prompt string.

+   PS3—The select command prompt string.

+   PS4—The trace command output prefix string.

+   PWD—The current working directory (as set by the cd command).

+   RANDOM—Returns a random number between 0 and 32767 each time it is referenced.

+   SHELL—The preferred shell to use; for programs that start a shell for you.

+   TERM—The terminal emulation type (for example, console).

Linux distributions define additional variables. The presence of these variables depends on your particular distribution. Many are declared for the use of applications.

+   DISPLAY is the X Window display server.

+   EDITOR is your default editor. Historically, this was used to indicate a line editor to use when a visual editor was not available (see VISUAL).

+   ORGANIZATION is the name of your organization (usually the contents of /etc/organization).

+   TERM is the terminal emulation (for example, xterm for an xterm session, or linux for the Linux console) .

+   VISUAL is your default editor, usually the same as EDITOR.

+   WINDOWMANAGER is the path to your current X Windows window manager.

A complete list appears in the reference section at the end of this chapter.

# # The Effect of Quotations

Those people familiar with other computer languages might be confused by the way Bash uses quotation marks. Single and double quotes are not used to delineate strings or characters, but to control how the shell groups characters and interprets special characters within a string. Bash calls this process *word splitting*.

```
$ COST=0
$ COST="0"
```