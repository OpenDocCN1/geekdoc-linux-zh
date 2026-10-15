# Table 9.25  `tcsh` Built-In Commands and Their Meanings (continued)

| Command | Meaning |
|---|---|
| `eval arg ...` | Treats the arguments as input to the shell and executes the resulting command(s) in the context of the current shell. This is usually used to execute commands generated as the result of command or variable substitution, as parsing occurs before these substitutions. |
| `eval command` | Runs command as standard input to the shell and executes the resulting commands. This is usually used to execute commands generated as the result of command or variable substitution, as parsing occurs before these substitutions (e.g., `eval 'tset -s options'`). |
| `exec command` | Executes command in place of the current shell, which terminates. |
| `exit [(expr)]` | Exits the shell, either with the value of the status variable or with the value specified by expr. |
| `fg [%job]`<br>`%job` | Brings the current or specified job into the foreground. A synonym for the `fg` built-in command. |
| `filetest -op file ...` | Applies op (which is a file inquiry operator) to each file and returns the results as a space-separated list. |
| `foreach name (wordlist)`<br>`end` | See “Looping Control Commands” on page 566. |
| `foreach var (wordlist)` | See “The foreach Loop” on page 561. |
| `getspath` | Prints the system execution path. |
| `getxvers` | Prints the experimental version prefix. |
| `glob wordlist` | Performs filename expansion on wordlist. Like echo, but no escapes (\) are recognized. Words are delimited by null characters in the output. |
| `goto label` | See “The goto” on page 547. |
| `goto word` | word is filename and command-substituted to yield a string of the form “label.” The shell rewinds its input as much as possible, searches for a line of the form “label:”, possibly preceded by blanks or tabs, and continues execution after that line. |
| `hashstat` | Prints statistics line indicating how effective the internal hash table has been at locating commands (and avoiding execs). An exec is attempted for each component of the path where the hash function indicates a possible hit, and in each component that does not begin with a backslash. |