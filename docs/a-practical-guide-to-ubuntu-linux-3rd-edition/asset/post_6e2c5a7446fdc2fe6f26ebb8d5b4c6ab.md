
## Table 9-13 bash features

| Feature | Description | Syntax | Alternate syntax |
| :--- | :--- | :--- | :--- |
| allexport | Automatically exports all variables and functions you create or modify after giving this command. | `set -o allexport` | `set -a` |
| braceexpand | Causes bash to perform brace expansion (the default; page 358). | `set -o braceexpand` | `set -B` |
| cdspell | Corrects minor spelling errors in directory names used as arguments to cd. | `shopt -s cdspell` | |
| cmdhist | Saves all lines of a multiline command in the same history entry, adding semicolons as needed. | `shopt -s cmdhist` | |
| dotglob | Causes shell special characters (wildcards; page 256) in an ambiguous file reference to match a leading period in a filename. By default special characters do not match a leading period. You must always specify the filenames . and .. explicitly because no pattern ever matches them. | `shopt -s dotglob` | |
| emacs | Specifies emacs editing mode for command-line editing (the default; page 341). | `set -o emacs` | |
| errxit | Causes bash to exit when a simple command (not a control structure) fails. | `set -o errxit` | `set -e` |
| execfail | Causes a shell script to continue running when it cannot find the file that is given as an argument to exec. By default a script terminates when exec cannot find the file that is given as its argument. | `shopt -s execfail` | |
| expand_aliases | Causes aliases (page 346) to be expanded (by default it is on for interactive shells and off for noninteractive shells). | `shopt -s expand_aliases` | |
| hashall | Causes bash to remember where commands it has found using PATH (page 319) are located (default). | `set -o hashall` | `set -h` |
| histappend | Causes bash to append the history list to the file named by HISTFILE (page 330) when the shell exits. By default bash overwrites this file. | `shopt -s histappend` | |
| histexpand | Turns on the history mechanism (which uses exclamation points by default; page 335). Turn this feature off to turn off history expansion. | `set -o histexpand` | `set -H` |
| history | Enables command history (on by default; page 330). | `set -o history` | |
| huponexit | Specifies that bash send a SIGHUP signal to all jobs when an interactive login shell exits. | `shopt -s huponexit` | |
| ignoreeof | Specifies that bash must receive ten EOF characters before it exits. Useful on noisy dial-up lines. | `set -o ignoreeof` | |
| monitor | Enables job control (on by default, page 307). | `set -o monitor` | `set -m` |
| nocaseglob | Causes ambiguous file references (page 256) to match filenames without regard to case (off by default). | `shopt -s nocaseglob` | |
| noclobber | Helps prevent overwriting files (off by default; page 248). | `set -o noclobber` | `set -C` |
| noglob | Disables pathname expansion (off by default; page 256). | `set -o noglob` | `set -f` |
| notify | With job control (page 307) enabled, reports the termination status of background jobs immediately. The default behavior is to display the status just before the next prompt. | `set -o notify` | `set -b` |
| nounset | Displays an error and exits from a shell script when you use an unset variable in an interactive shell. The default is to display a null value for an unset variable. | `set -o nounset` | `set -u` |
| nullglob | Causes bash to expand ambiguous file references (page 256) that do not match a filename to a null string. By default bash passes these file references without expanding them. | `shopt -s nullglob` | |
| posix | Runs bash in POSIX mode. | `set -o posix` | |
| verbose | Displays command lines as bash reads them. | `set -o verbose` | `set -v` |
| vi | Specifies vi editing mode for command-line editing (page 340). | `set -o vi` | |
| xpg_echo | Causes the echo builtin to expand backslash escape sequences without the need for the -e option (page 980). | `shopt -s xpg_echo` | |
| xtrace | Turns on shell debugging (page 966). | `set -o xtrace` | `set -x` |

## PROCESSING THE COMMAND LINE

Whether you are working interactively or running a shell script, **bash** needs to read a command line before it can start processing it—**bash** always reads at least one line before processing a command. Some **bash** builtins, such as **if** and **case**, as well as functions and quoted strings, span multiple lines. When **bash** recognizes a command that covers more than one line, it reads the entire command before processing it. In interactive sessions, **bash** prompts you with the secondary prompt (**PS2**, **>** by default; page 322) as you type each line of a multiline command until it recognizes the end of the command:

```bash
$ echo 'hi
> end'
hi
end
$ function hello () {
>  echo hello there
> }
$
```

After reading a command line, **bash** applies history expansion and alias substitution to the line.

## HISTORY EXPANSION

“Rerexecuting and Editing Commands” on page 332 discusses the commands you can give to modify and reexecute command lines from the history list. History expansion is the process that **bash** uses to turn a history command into an executable command line. For example, when you give the command **!!**, history expansion changes that command line so it is the same as the previous one. History expansion is turned on by default for interactive shells; **set +o histexpand** turns it off. History expansion does not apply to noninteractive shells (shell scripts).

## ALIAS SUBSTITUTION

Aliases (page 346) substitute a string for the first word of a simple command. By default aliases are turned on for interactive shells and off for noninteractive shells. Give the command **shopt -u expand_aliases** to turn aliases off.

## PARSING AND SCANNING THE COMMAND LINE

After processing history commands and aliases, **bash** does not execute the command immediately. One of the first things the shell does is to *parse* (isolate strings of characters in) the command line into tokens or words. The shell then scans each token for special characters and patterns that instruct the shell to take certain actions. These actions can involve substituting one word or words for another. When the shell parses the following command line, it breaks it into three tokens (**cp**, **~/letter**, and **.**):

```bash
$ cp ~/letter .
```

After separating tokens and before executing the command, the shell scans the tokens and performs *command-line expansion*.

## COMMAND-LINE EXPANSION

Both interactive and noninteractive shells transform the command line using *command-line expansion* before passing the command line to the program being called. You can use a shell without knowing much about command-line expansion, but you can use what a shell has to offer to a better advantage with an understanding of this topic. This section covers Bourne Again Shell command-line expansion.

The Bourne Again Shell scans each token for the various types of expansion and substitution in the following order. Most of these processes expand a word into a single word. Only brace expansion, word splitting, and pathname expansion can change the number of words in a command (except for the expansion of the variable "$@"—see page 1000).

- 1. Brace expansion (page 358)
- 2. Tilde expansion (page 359)
- 3. Parameter and variable expansion (page 360)
- 4. Arithmetic expansion (page 360)
- 5. Command substitution (page 362)
- 6. Word splitting (page 363)
- 7. Pathname expansion (page 363)
- 8. Process substitution (page 365)

After **bash** finishes with the preceding list, it removes from the command line single quotation marks, double quotation marks, and backslashes that are not a result of an expansion. This process is called *quote removal*.

### ORDER OF EXPANSION

The order in which **bash** carries out these steps affects the interpretation of commands. For example, if you set a variable to a value that looks like the instruction for output redirection and then enter a command that uses the variable's value to perform redirection, you might expect **bash** to redirect the output.

```bash
$ SENDIT="> /tmp/saveit"
$ echo xxx $SENDIT
xxx > /tmp/saveit
$ cat /tmp/saveit
cat: /tmp/saveit: No such file or directory
```

In fact, the shell does *not* redirect the output—it recognizes input and output redirection before it evaluates variables. When it executes the command line, the shell checks for redirection and, finding none, evaluates the SENDIT variable. After
