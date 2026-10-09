
## Table 9-13 bash features (continued)

| Feature | Description | Syntax | Alternate syntax |
| :-- | :-- | :-- | :-- |
| **histappend** | Causes **bash** to append the history list to the file named by **HISTFILE** (page 377) when the shell exits (default is off [bash overwrites this file]). | **shopt** -s histappend | |
| **histexpand** | Turns on the history mechanism (which uses exclamation points by default; page 381). Turn this feature off to turn off history expansion (default is on). | **set** -o histexpand | **set** -H |
| **history** | Enables command history (default is on; page 376). | **set** -o history | |
| **huponexit** | Specifies that **bash** send a SIGHUP signal to all jobs when an interactive login shell exits (default is **off**). | **shopt** -s huponexit | |
| **ignoreeof** | Specifies that **bash** must receive ten EOF characters before it exits. Useful on noisy dial-up lines (default is off). | **set** -o ignoreeof | |
| **monitor** | Enables job control (default is on; page 346). | **set** -o monitor | **set** -m |
| **nocaseglob** | Causes ambiguous file references (page 165) to match filenames without regard to case (default is off). | **shopt** -s nocaseglob | |
| **noclobber** | Helps prevent overwriting files (default is off; page 156). | **set** -o noclobber | **set** -C |
| **noglob** | Disables pathname expansion (default is off; page 165). | **set** -o noglob | **set** -f |
| **notify** | With job control (page 346) enabled, reports the termination status of background jobs immediately (default is off: **bash** displays the status just before the next prompt). | **set** -o notify | **set** -b |
| **nounset** | Displays an error when the shell tries to expand an unset variable; **bash** exits from a script but not from an interactive shell (default is off: **bash** substitutes a null value for an unset variable). | **set** -o nounset | **set** -u |
| **nullglob** | Causes **bash** to substitute a null string for ambiguous file references (page 165) that do not match a filename (default is off; **bash** passes these file references as is). | **shopt** -s nullglob | |
| **pipefail** | Sets the exit status of a pipeline to the exit status of the last (rightmost) simple command that failed (returned a nonzero exit status) in the pipeline; if no command failed, exit status is set to zero (default is off). **bash** sets the exit status of a pipeline to the exit status of the final command in the pipeline. | **set** -o pipefail | |
| **posix** | Runs **bash** in POSIX mode (default is off). | **set** -o posix | |
| **verbose** | Displays each command line after **bash** reads it but before **bash** expands it (default is off). See also **xtrace**. | **set** -o verbose | **set** -v |
| **vi** | Specifies **vi** editing mode for command-line editing (default is off; page 386). | **set** -o vi | |
| **xpg_echo** | Causes the **echo** builtin to expand backslash escape sequences without the need for the **-e** option (default is off; page 1009). | **shopt** -s xpg_echo | |
| **xtrace** | Turns on shell debugging: Displays the value of **PS4** (page 363) followed by each input line after the shell reads and expands it (default is off; see page 994 for a discussion). See also **verbose**. | **set** -o xtrace | **set** -x |

## PROCESSING THE COMMAND LINE

Whether you are working interactively or running a shell script, `bash` needs to read a command line before it can start processing it—`bash` always reads at least one line before processing a command. Some `bash` builtins, such as `if` and `case`, as well as functions and quoted strings, span multiple lines. When `bash` recognizes a command that covers more than one line, it reads the entire command before processing it. In interactive sessions, `bash` prompts with the secondary prompt (PS2, `>` by default; page 362) as you type each line of a multiline command until it recognizes the end of the command:

```
$ ps -ef |
> grep emacs
zach          26880   24579   1 14:42 pts/10    00:00:00 emacs notes
zach          26890   24579   0 14:42 pts/10    00:00:00 grep emacs

$ function hello () {
> echo hello there
> }
$
```

For more information refer to "Implicit Command-Line Continuation" on page 1063. After reading a command line, **bash** applies history expansion and alias substitution to the command line.

## HISTORY EXPANSION

"Reexecuting and Editing Commands" on page 378 discusses the commands you can give to modify and reexecute command lines from the history list. History expansion is the process **bash** uses to turn a history command into an executable command line. For example, when you enter the command `!!`, history expansion changes that command line so it is the same as the previous one. History expansion is turned on by default for interactive shells; **set +o histexpand** turns it off. History expansion does not apply to noninteractive shells (shell scripts).

![](img/243613168ac865b539f12460d966088e_460_0.png)

## ALIAS SUBSTITUTION

Aliases (page 392) substitute a string for the first word of a simple command. By default, alias substitution is turned on for interactive shells and off for noninteractive shells; **shopt -u expand_aliases** turns it off.

## PARSING AND SCANNING THE COMMAND LINE

After processing history commands and aliases, **bash** does not execute the command immediately. One of the first things the shell does is to *parse* (isolate strings of characters in) the command line into tokens (words). After separating tokens and before executing the command, the shell scans the tokens and performs *command-line expansion*.

## COMMAND-LINE EXPANSION

Both interactive and noninteractive shells transform the command line using *command-line expansion* before passing the command line to the program being called. You can use a shell without knowing much about command-line expansion, but you can use what a shell has to offer to a better advantage with an understanding of this topic. This section covers Bourne Again Shell command-line expansion.

The Bourne Again Shell scans each token for the various types of expansion and substitution in the following order. Most of these processes expand a word into a single word. Only brace expansion, word splitting, and pathname expansion can change the number of words in a command (except for the expansion of the variable "$@" --- see page 1026).

1. Brace expansion (next page)
2. Tilde expansion (page 407)
3. Parameter and variable expansion (page 408)
4. Arithmetic expansion (page 408)
5. Command substitution (page 410)
6. Word splitting (page 411)
7. Pathname expansion (page 412)
8. Process substitution (page 413)
9. Quote removal (page 413)

## ORDER OF EXPANSION

The order in which *bash* carries out these steps affects the interpretation of commands. For example, if you set a variable to a value that looks like the instruction for output redirection and then enter a command that uses the variable’s value to perform redirection, you might expect *bash* to redirect the output.

```
$ SENDIT="> /tmp/saveit"
$ echo xxx $SENDIT
xxx > /tmp/saveit
$ cat /tmp/saveit
cat: /tmp/saveit: No such file or directory
```

In fact, the shell does *not* redirect the output—it recognizes input and output redirection before it evaluates variables. When it executes the command line, the shell checks for redirection and, finding none, evaluates the *SENDIT* variable. After replacing the variable with "> /tmp/saveit", *bash* passes the arguments to *echo*, which dutifully copies its arguments to standard output. No /tmp/saveit file is created.

### Quotation marks can alter expansion

> Double and single quotation marks cause the shell to behave differently when performing expansions. Double quotation marks permit parameter and variable expansion but suppress other types of expansion. Single quotation marks suppress all types of expansion.

## BRACE EXPANSION

*Brace expansion*, which originated in the C Shell, provides a convenient way to specify a series of strings or numbers. Although brace expansion is frequently used to specify filenames, the mechanism can be used to generate arbitrary strings; the shell does not attempt to match the brace notation with the names of existing files. Brace expansion is turned on in interactive and noninteractive shells by default; you can turn it off using *set +o braceexpand*. The shell also uses braces to isolate variable names (page 355).

The following example illustrates how brace expansion works. The *ls* command does not display any output because there are no files in the working directory. The *echo* builtin displays the strings the shell generates using brace expansion.

```
$ ls
$ echo chap_{one,two,three}.txt
chap_one.txt  chap_two.txt  chap_three.txt
```

The shell expands the comma-separated strings inside the braces on the command line into a *space*-separated list of strings. Each string from the list is prepended with the string *chap_*, called the *preamble*, and appended with the string *.txt*, called the
