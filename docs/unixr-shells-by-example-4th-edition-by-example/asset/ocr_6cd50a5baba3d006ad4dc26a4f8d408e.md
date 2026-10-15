# Table 15.13 The shopt Command Options (continued)

| Option | Meaning |
|---|---|
| huponexit | If set, bash will send SIGHUP (hangup signal) to all jobs when an interactive login shell exits. |
| interactive_comments | Allows a word beginning with # to cause that word and all remaining characters on that line to be ignored in an interactive shell. Enabled by default. |
| lithist | If enabled, and the cmdhist option is enabled, multiline commands are saved to the history with embedded newlines rather than using semicolon separators where possible. |
| mailwarn | If set, and a file that bash is checking for mail has been accessed since the last time it was checked, the message The mail in mailfile has been read is displayed. |
| nocaseglob | If set, bash matches filenames in a case-insensitive fashion when performing filename expansion. |
| nullglob | If set, bash allows filename patterns that match no files to expand to a null string, rather than themselves. |
| promptvars | If set, prompt strings undergo variable and parameter expansion after being expanded. Enabled by default. |
| restricted_shell | The shell sets this option if it is started in restricted mode. The value may not be changed. This is not reset when the startup files are executed, allowing the startup files to discover whether or not a shell is restricted. |
| shift_verbose | If this is set, the shift built-in prints an error message when the shift count exceeds the number of positional parameters. |
| sourcepath | If set, the source built-in uses the value of PATH to find the directory containing the file supplied as an argument. Enabled by default. |
| source | A synonym for dot (.). |

# 15.6 Summary

Now that we have covered the major UNIX and Linux shells, you can start reading, writing, and maintaining scripts. Remember, a lot of time is spent debugging scripts. So often, you’ll have a successful script, but you’ll want to make it better. So, back in the editor you’ll go make a few changes, try to run the program, and whoops! It’s broken! With what you’ve learned in this chapter, you’ll be able to keep these surprises to a minimum. If you are a system administrator and want to learn more about how the shells interact with the system, the next chapter will shed some light on topics that typically apply to the way the shells are used for system administration.