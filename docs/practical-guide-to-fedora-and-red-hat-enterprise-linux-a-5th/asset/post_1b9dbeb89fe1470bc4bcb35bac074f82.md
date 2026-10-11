
## Table 9-13 bash features (continued)

| Feature | Description | Syntax | Alternate syntax |
| :--- | :--- | :--- | :--- |
| history | Enable command history (on by default; page 316). | `set -o history` | |
| ignoreeof | Specifies that bash must receive ten EOF characters before it exits. Useful on noisy dial-up lines. | `set -o ignoreeof` | |
| monitor | Enables job control (on by default, page 294). | `set -o monitor` | `set -m` |
| nocaseglob | Causes ambiguous file references (page 243) to match filenames without regard to case (off by default). | `shopt -s nocaseglob` | |
| noclobber | Helps prevent overwriting files (off by default; page 235). | `set -o noclobber` | `set -C` |
| noglob | Disables pathname expansion (off by default; page 243). | `set -o noglob` | `set -f` |
| notify | With job control (page 294) enabled, reports the termination status of background jobs immediately. The default behavior is to display the status just before the next prompt. | `set -o notify` | `set -b` |
| nounset | Displays an error and exits from a shell script when you use an unset variable in an interactive shell. The default is to display a null value for an unset variable. | `set -o nounset` | `set -u` |
| nullglob | Causes bash to expand ambiguous file references (page 243) that do not match a filename to a null string. By default bash passes these file references without expanding them. | `shopt -s nullglob` | |
| posix | Runs bash in POSIX mode. | `set -o posix` | |
| verbose | Displays command lines as bash reads them. | `set -o verbose` | `set -v` |
| vi | Specifies vi editing mode for command-line editing (page 326). | `set -o vi` | |
| xpg_echo | Causes the echo builtin to expand back-slash escape sequences without the need for the -e option (page 914). | `shopt -s xpg_echo` | |
| xtrace | Turns on shell debugging (page 900). | `set -o xtrace` | `set -x` |

## Processing the Command Line

Whether you are working interactively or running a shell script, **bash** needs to read a command line before it can start processing it—**bash** always reads at least one line before processing a command. Some **bash** builtins, such as **if** and **case**, as well as functions and quoted strings, span multiple lines. When **bash** recognizes a command that covers more than one line, it reads the entire command before processing it. In interactive sessions **bash** prompts you with the secondary prompt (\$2, > by default; page 309) as you type each line of a multiline command until it recognizes the end of the command:

```bash
$ echo 'hi
> end'
hi
end
$ function hello () {
> echo hello there
> }
$
```

After reading a command line, **bash** applies history expansion and alias substitution to the line.

## HISTORY EXPANSION

“Rexecuting and Editing Commands” on page 318 discusses the commands you can give to modify and reexecute command lines from the history list. History expansion is the process that **bash** uses to turn a history command into an executable command line. For example, when you give the command !!, history expansion changes that command line so it is the same as the previous one. History expansion is turned on by default for interactive shells; **set +o histexpand** turns it off. History expansion does not apply to noninteractive shells (shell scripts).

## ALIAS SUBSTITUTION

Aliases (page 332) substitute a string for the first word of a simple command. By default aliases are turned on for interactive shells and off for noninteractive shells. Give the command **shopt -u expand_aliases** to turn aliases off.

## PARSING AND SCANNING THE COMMAND LINE

After processing history commands and aliases, **bash** does not execute the command immediately. One of the first things the shell does is to *parse* (isolate strings of characters in) the command line into tokens or words. The shell then scans each token for special characters and patterns that instruct the shell to take certain actions. These actions can involve substituting one word or words for another. When the shell parses the following command line, it breaks it into three tokens (**cp**, **~/letter**, and **.**):

```bash
$ cp ~/letter .
```

After separating tokens and before executing the command, the shell scans the tokens and performs *command-line expansion*.

## COMMAND-LINE EXPANSION

In both interactive and noninteractive use, the shell transforms the command line using *command-line expansion* before passing the command line to the program being called. You can use a shell without knowing much about command-line expansion, but you can use what a shell has to offer to a better advantage with an understanding of this topic. This section covers Bourne Again Shell command-line expansion.

The Bourne Again Shell scans each token for the various types of expansion and substitution in the following order. Most of these processes expand a word into a single word. Only brace expansion, word splitting, and pathname expansion can change the number of words in a command (except for the expansion of the variable "$@"—page 932).

- 1. Brace expansion (page 344)
- 2. Tilde expansion (page 345)
- 3. Parameter and variable expansion (page 346)
- 4. Arithmetic expansion (page 346)
- 5. Command substitution (page 348)
- 6. Word splitting (page 349)
- 7. Pathname expansion (page 349)
- 8. Process substitution (page 351)

> After **bash** finishes with the preceding list, it removes from the command line single quotation marks, double quotation marks, and backslashes that are not a result of an expansion. This process is called *quote removal*.

### ORDER OF EXPANSION

The order in which **bash** carries out these steps affects the interpretation of commands. For example, if you set a variable to a value that looks like the instruction for output redirection and then enter a command that uses the variable's value to perform redirection, you might expect **bash** to redirect the output.

```bash
$ SENDIT="> /tmp/saveit"
$ echo xx $SENDIT
xxx > /tmp/saveit
$ cat /tmp/saveit
cat: /tmp/saveit: No such file or directory
```

In fact, the shell does *not* redirect the output—it recognizes input and output redirection before it evaluates variables. When it executes the command line, the shell checks for redirection and, finding none, evaluates the `SENDIT` variable. After replacing the variable with > /tmp/saveit, bash passes the arguments to echo, which dutifully copies its arguments to standard output. No /tmp/saveit file is created. The following sections provide more detailed descriptions of the steps involved in command processing. Keep in mind that double and single quotation marks cause the shell to behave differently when performing expansions. Double quotation marks permit parameter and variable expansion but suppress other types of expansion. Single quotation marks suppress all types of expansion.

## BRACE EXPANSION

Brace expansion, which originated in the C Shell, provides a convenient way to specify filenames when pathname expansion does not apply. Although brace expansion is almost always used to specify filenames, the mechanism can be used to generate arbitrary strings; the shell does not attempt to match the brace notation with the names of existing files.

Brace expansion is turned on in interactive and noninteractive shells by default; you can turn it off with set +o braceexpand. The shell also uses braces to isolate variable names (page 302).

The following example illustrates how brace expansion works. The ls command does not display any output because there are no files in the working directory. The echo builtin displays the strings that the shell generates with brace expansion. In this case the strings do not match filenames (there are no files in the working directory.)

```bash
$ ls
$ echo chap_{one, two, three}.txt
chap_one.txt chap_two.txt chap_three.txt
```

The shell expands the comma-separated strings inside the braces in the echo command into a space-separated list of strings. Each string from the list is prepended with the string chap_, called the preamble, and appended with the string .txt, called the postscript. Both the preamble and the postscript are optional. The left-to-right order of the strings within the braces is preserved in the expansion. For the shell to treat the left and right braces specially and for brace expansion to occur, at least one comma and no unquoted whitespace characters must be inside the braces. You can nest brace expansions.

Brace expansion is useful when there is a long preamble or postscript. The following example copies the four files main.c, f1.c, f2.c, and tmp.c located in the /usr/local/src/C directory to the working directory.

```bash
$ cp /usr/local/src/C/{main, f1, f2, tmp}.c .
```

You can also use brace expansion to create directories with related names:

```bash
$ ls -F
file1 file2 file3
$ mkdir vrs{A, B, C, D}
$ ls -F
file1 file2 file3 vrsA/ vrsB/ vrsC/ vrsD/ vrsE/
```
