you wish (use quotes so that bash processes the options and arguments correctly). If you type alias without an argument, you see a list of all the aliases you have defined, if there are any.

*See also unaliases.*

# **EXAMPLES**

**This Command**
`alias bigfiles='ls -Shl'`

`alias newfiles='ls -tl'`

`alias oldfiles='ls -Rtlr'`

**Does the Following**

Lists files sorted by size, showing the largest files first.

Lists files sorted by the time of the last modification, showing most recently modified files first.

Using reverse chronological order (oldest files first), lists all the files in the current directory and all associated subdirectories.

# **bash**

`bash [ option ] [ filename ]`

Starts the bash shell. If you specify a filename, bash reads commands from the specified file.

# **OPTIONS**

**Use This Option** | **To Do This**
---
`-c string` | Read commands from the specified string.
`-i` | Start bash as an interactive shell
`-login` | Start bash by reading all the startup files that are consulted when bash is started after you log in
`-nobraceexpansion` | Disable brace expansion
`-nolineediting` | Disable line editing
`-noprofile` | Do not execute the login startup files