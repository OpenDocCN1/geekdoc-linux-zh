# Adding or Changing Variables

After you’ve poked around in your environment, you might determine that you want to set a variable that’s currently not available or change one to make it better meet your needs. In general, you won’t randomly specify variables; you’ll do it because a certain program requires a specific variable in order to run.

# Variables You Can Mess With

The following table includes some of the variables you can safely change. Keep in mind that the shell itself might not use a specific variable, like NTP SERVER, while programs running under the shell might. Sometimes shells assign default variables, while in other cases, you’ll have to manually set the value.

| Zsh, Bash, and ksh | Csh | Description |
|---|---|---|
| CDPATH | c dpath | Specifies the search path for directories specified by cd. This is similar to PATH. |
| COLUMNS |  | Specifies width of the edit window in characters. |
| EDITOR |  | Specifies the default editor. |
| ENV |  | Specifies where to look for configuration files. |
| HISTFILE |  | Specifies the name of the file containing the command history. |
| HISTFILESIZE | savehist | Specifies the maximum number of lines to keep in the history file. |
| HISTSIZE | history | Specifies the number of commands to keep in the command history. |
| HOSTFILE |  | Specifies the name of the file containing host name aliases for expansion. |
| IGNOREEOF | ignoreeof | Specifies that Ctrl-D should not log out of the shell. Use IGNOREEOF=-. |
| LINES |  | Specifies the number of lines on the screen. |
| MAIL | mail | Specifies the location of incoming mail so bash can notify you of mail arrival. |
| MAILCHECK | mail | Specifies how often (in seconds) bash checks for mail. |
| MAIL_WARNING |  | Specifies the message to be displayed if you have read mail but not unread mail. |
| noclobber | noclobber | Specifies that the shell should not overwrite an existing file when redirecting output. |
| PATH | path | Specifies the search path for commands, including multiple paths separated by colons. |
| PROMPT_COMMAND |  | Specifies the command to be run before displaying each primary prompt (does not apply to ksh). |
| PS1 | prompt | Specifies the primary prompt. |
| PS2 |  | Specifies the default second-level prompt. |
| PS3 |  | Specifies the prompt for the select command in scripts. |
| PS4 |  | Specifies the prompt used when tracing execution of a script. |
| TMOUT |  | Specifies time in seconds to wait for input before closing the shell. |
| VISUAL |  | Specifies the default visual editor—usually the same as EDITOR, but referenced by different programs. |