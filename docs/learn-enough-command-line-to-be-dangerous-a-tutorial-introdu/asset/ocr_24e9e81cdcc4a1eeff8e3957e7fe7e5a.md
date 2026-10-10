| Command | Description | Example |
|---|---|---|
| `curl` | Interact with URLs | `$ curl -O example.com` |
| `which` | Locate a program on the path | `$ which curl` |
| `head <file>` | Display first part of file | `$ head foo` |
| `tail <file>` | Display last part of file | `$ tail bar` |
| `wc <file>` | Count lines, words, bytes | `$ wc foo` |
| `cmd1 | cmd2` | Pipe cmd1 to cmd2 | `$ head foo | wc` |
| `less <file>` | View file contents interactively | `$ less foo` |
| `grep <string> <file>` | Find string in file | `$ grep foo bar.txt` |
| `grep -i <string> <file>` | Find case-insensitively | `$ grep -i foo bar.txt` |
| `ps` | Show processes | `$ ps aux` |
| `top` | Show processes (sorted) | `$ top` |
| `kill -15 <pid>` | Kill a process | `$ kill -9 24601` |
| `pkill -15 -f <name>` | Kill matching processes | `$ pkill -9 -f spring` |

Table 4: Important commands from Section 3.

This is because there is one line that contains both “Rose” and “rose”, and thus shows up in both `grep rose` and `grep -i rose`. Write a command confirming that the number of lines matching “Rose” but not matching “rose” is equal to the expected 2. Hint: Pipe the result of `grep` to `grep -v`, and then pipe that result to `wc`. (What does `-v` do? Read the man page for `grep` (Box 5.))

# ## 3.5 Summary

Important commands from this section are summarized in Table 4.

# ### Exercises

+   1. The `history` command prints the history of commands in a particular terminal shell (subject to some limit, which is typically large). Pipe `history` to `less` to examine your command history. What was your 17th command?

+   2. By piping the output of `history` to `wc`, count how many commands