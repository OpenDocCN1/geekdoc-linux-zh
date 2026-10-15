

# 附录 B • Shell 比较

| Feature | Bourne | Bash | Korn |
|---|---|---|---|
| Metacharacters for Filename Expansion (continued): |  |  |  |
| `*` | `[A-Z]` (sh) | `[ ]` | `abc?z(19)1` |
| `?` matches zero or more characters in the set |  |  |  |
| `[...]` matches any one character in the set. Parentheses, the vertical bar, and braces represent an OR condition. |  |  |  |
| `[...]` matches zero or more characters in the set. |  |  |  |
| `?` matches any one character. |  |  |  |
| `@(pattern)` |  |  |  |
| `?(pattern)` |  |  |  |
| `*(pattern)` |  |  |  |
| `+(pattern)` |  |  |  |
| `!(pattern)` |  |  |  |
| `abc?z(19)1` |  |  |  |

| Feature | Bourne | Bash | Korn |
|---|---|---|---|
| **I/O Redirection and Pipes:** |  |  |  |
| Command output redirected to a file | `cmd > file` | `cmd > file` | `cmd > file` |
| Command output appended to a file | `cmd >> file` | `cmd >> file` | `cmd >> file` |
| Command input redirected from a file | `cmd < file` | `cmd < file` | `cmd < file` |
| Command errors redirected | `(cmd > /dev/tty) 2>errors` | `cmd 2> file` | `cmd 2> errors` |
| Output and errors redirected to a file | `cmd > file 2>&1` | `cmd &> file or cmd > file 2>&1` | `cmd > file 2>&1` |

| Feature | C / TC | Bourne | Bash | Korn |
|---|---|---|---|---|
| I/O Redirection and Pipes (continued): |  |  |  |  |
| Assign output and ignore noblocker | cmd > file | N/A | cmd > file | cmd > file |
| here document | cmd < EOF\ninput\nEOF | cmd < EOF\ninput\nEOF | cmd << EOF\ninput\nEOF | cmd << EOF\ninput\nEOF |
| Pipe output of one command to input of another | cmd | cmd | cmd | cmd | cmd |
| Pipe output and error to a command | cmd | & cmd | N/A | N/A | (See coprocesses) |
| Coprocess | N/A | N/A | N/A | command | &\n cmd && cmd\n cmd || cmd |
| Conditional statement | cmd && cmd\n cmd || cmd | cmd && cmd\n cmd || cmd | cmd && cmd\n cmd || cmd | cmd && cmd\n cmd || cmd |
| Reading from the Keyboard: |  |  |  |  |
| Read a line of input and store into variable(s) | set var = $k\n set var1 = "line" | read var\n read var1 var2... | read var\n read var1 var2...\n read -p prompt | read var\n read var1 var2...\n read var"Enter value" |
| Arithmetic: |  |  |  |  |
| Perform calculation | @ var = 3 + 1 | var = expr 5 + 1 | (( var = 5 + 1 ))\n let var=5+1 | (( var = 5 + 1 ))\n let var=5+1 |

| Feature | C/TC | Bourne | Bash | Korn |
|---|---|---|---|---|
| Tilde Expansion: |  |  |  |  |
| Represent home directory of user | ~username | N/A | ~username | ~username |
| Represent home directory | - | N/A | , | , |
| Represent present working directory | N/A | N/A | † | † |
| Represent previous working directory | N/A | N/A | ; | : |
| working directory |  |  |  |  |
| Aliases: |  |  |  |  |
| Create an alias | alias m more | N/A | alias m more | alias m more |
| List aliases | alias | N/A | alias, alias -p | alias, alias -t |
| Remove an alias | unalias m | N/A | unalias m | unalias m |
| History: |  |  |  |  |
| Set history | set history = 25 | N/A | automatic or HISTSIZE=25 | automatic or HISTSIZE=25 |
| Display numbered history list | history | N/A | history, fc -l | history, fc -l |
| Display portion of history list selected by number | history 5 | N/A | history 5 | history 5 |
|  |  |  | history -5 | history -5 |
| Re-execute a command | !! (last command) |  | !! (last command) | r (last command) |
|  | !5 (5th command) |  | !5 (5th command) | !5 (5th command) |
|  | !v (last command starting with v) |  | !v (last command starting with v) | !v (last command starting with v) |
| Set interactive editor | N/A (vi) | N/A | set -o vi | set -o vi |
|  | bindkey -v |  | set -o emacs | set -o emacs |
|  | or bindkey -e (tcsh) |  |  |  |

| Feature | C/TC | Bourne | Bash | Korn |
|---|---|---|---|---|
| Signals: Command | onintr | trap | trap | trap |
| Initialization Files: |  |  |  |  |
| Executed at login | .login | .profile | .bash_profile | .profile |
| Executed every time the shell is invoked | .cshrc | N/A | Bash_2. bashrc (or other filename) ENV=.bashrc | ENV=.kshrc (or other filename) |
| Functions: |  |  |  |  |
| Define a function | N/A | fun() { commands; } | function fun { commands; } | function fun { commands; } |
| Call a function | N/A | fun\nfun param? ... | fun\nfun param? ... | fun\nfun param? ... |
| Programming Constructs: |  |  |  |  |
| If conditional | if ( expression ) then\ncommands\nendif | if [ expression ]\nthen\ncommands\nfi | if [[ string expression ]]\nthen\ncommands\nfi | if [[ string expression ]]\nthen\ncommands\nfi |
| if ( command ) then\ncommands\nendif | if command\nthen\ncommands\nfi | if (( numeric expression ))\nthen\ncommands\nfi | if (( numeric expression ))\nthen\ncommands\nfi |
| if/else conditional | if ( expression ) then\ncommands\nelse\ncommands\nendif | if command\nthen\ncommands\nelse\ncommands\nfi | if command\nthen\ncommands\nelse\ncommands\nfi | if command\nthen\ncommands\nelse\ncommands\nfi |

