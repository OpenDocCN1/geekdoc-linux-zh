
# 198

# csh

A pipeline or sequence can be enclosed within parentheses ( ) to form a simple command that can be a component in a pipeline or sequence.

A sequence of pipelines can be executed asynchronously or "in the background" by appending an ampersand (&); instead of waiting for the sequence to finish before issuing a prompt, the shell displays the job number ("Job Control" on page 206) and associated IDs and prompts immediately.

Note — Quote conventions are confusing. Overriding the escape character to force variable substitutions within double quotes is counterintuitive and inconsistent with the Bourne shell.

# History Substitution

History substitution enables you to use words from previous command lines in the command line you are typing. This process simplifies spelling corrections and the repetition of complicated commands or arguments. Command lines are saved in the history list, the size of which is controlled by the history variable. The most recent command is retained in any case. History substitution begins with a ! (although you can change this with variable) and occur anywhere on the command line; history substitutions do not nest. You can escape the ! with \ to suppress its special meaning.

Input lines containing history substitutions are echoed on the terminal after being expanded by any other substitutions take place or the command gets executed.

> — The g (global) flag in history substitutions applies only to the first match in each word, instead of to all matches in all words. The common text editors consistently do the latter when given the g flag in a substitution command.

Refer to history(1) for more details.

# Event Designators

An event designator is a reference to a command-line entry in the history list.

- ! Start a history substitution, except when followed by a space character, Tab, newline, =, or (.
Refer to the previous command. By itself, this substitution repeats the previous command.
- !n Refer to the command line n.
- !-n Refer to the current command line minus n.
- !str Refer to the most recent command starting with str.
- !str Refer to the most recent command containing str.
- !?str additional Refer to the most recent command containing str, and append additional to that referenced command.
- !(command) additional Refer to the most recent command beginning with command and append additional to that referenced command.

# csh 199

^previous-word replacement^
Repeat the previous command line, replacing the string previous-word with the string replacement. This is equivalent to the history substitution: !s/previous-word/replacement/ to execute a specific previous command and make such a substitution, say, reexecuting command #6,
!:6s/previous-word/replacement./

# Word Designators

A colon (:) separates the event specification from the word designator. You can omit it if the word designator begins with a ^, $, *, or %. If the word is to be selected from previous command, you can omit the second character from the event specification. For instance, !!1 and !!1 both refer to the first word of the previous command, whereas !! and $ both refer to the last word in the previous command. Word designators include:

- # The entire command line typed so far.
- 0 The first input (command).
- n The $n-th argument.
- ^ The first argument, that is, 1.
- $ The last argument.
- % The word matched by (the most recent) ?s search.
- x-y A range of words: -y abbreviates 0-y.
- * All arguments, or a null value if there is one word in the event.
- x-^ Abbreviates x-.
- x-^ Like x-^ but omitting word $.

# Modifiers

After the optional word designator, you can add one of the following modifiers, preceded by a colon (:).

- h Remove a trailing path name component, leaving the head.
- r Remove a trailing suffix of the form .xxx leaving the basename.
- e Remove all but suffix, leaving the extension.
- s/l/r/ Substitute r for l/.
- t Remove all leading path-name components, leaving the tail.
- & Repeat the previous substitution.
- g Apply the change to the first occurrence of a match in each word by prefixing the above (for example, g&).
- p Print the new command but not execute it.
- q Quote the substituted words, escaping further substitutions.
- x- Like q, but break into words at each space character, Tab, or newline.

Note - Although it should be possible to use the : modifiers on the output of command substitution, there are two problems with : modifier usage of variable substitutions: not all of the modifiers are available, and only one modifier per substitution is allowed.

Unless preceded by a \, the modification is applied only to the first string that matches; an error results if no string matches.
The left-hand side of substitutions are not regular expressions, but character strings. You can use any character as the delimiter in place of /. A backslash quotes the character \ in the right-hand side, is replaced by the text from the left-hand side. You can escape the \ with a backslash. A rule 1 uses the previous string either from a l or from a contextual scan \ from ?. You can omit the rightmost delimiter if a newline immediately follows r; similarly, you can omit the ? in a context scan.

Without an event specification, a history reference refers to the previous command or to a previous history reference on the command line (if).

# Quick Substitution

^r is equivalent to the history substitution !:s/l/r/.

# Aliases

The C shell maintains a list of aliases that you can create, display, and modify by using the alias and unalias commands. The shell checks the first word in command to see if it matches that of an existing alias. If it does, the command is reprocessed with the alias definition replacing its name; the history substitution mechanism is made available as though command were the input line. History substitutions, escaped with a backslash in the definition, can be replaced with actual command-line arguments when you use the alias. If no history substitution is called for, the arguments remain unchanged.

You can nest aliases. That is, an alias definition can contain the name of another alias. Nested aliases are expanded before any history substitution is applied. This expansion is useful in pipelines as

```
alias lm -l !* | more
```

which when called, pipes the output of ls(1) through more(1).

Except for the first word, the name of the alias may not appear in its definition nor in any alias referred to by its definition. Such loops are detected and display an error message.

# I/O Redirection

The following metacharacters indicate that the subsequent word is the name of a file to which redirect the command's standard input, standard output, or standard error; this word is variable, command, and file-name expanded separately from the rest of the command.

```
< Redirect standard input.
```

# csh

# 201

Read the standard input, up to a line that is identical with word, and place the resulting lines in a temporary file. Unless word is escaped or quoted, perform variable and command substitutions on these lines. Then, invoke the pipeline with the temporary file as its input. word is not subjected to variable, file-name, or command substitution, and each line is compared to it before any substitutions are performed by the shell.

```
<<word
```

When set, the variable noclobber prevents destruction of existing files. It also prevents redirection to terminals and /dev/null unless you use one of the forms !. The forms redirect both standard output and the standard error (diagnostic output) to the file.

```
>> ! & &
```

```
>>> >> !
```

Append the standard output. Like, but place at the end of the file instead of overwriting it. If noclobber is set, it is an error for the file not to exist unless you use one of the forms The forms append both the standard error and standard output to the file.

> Note — Control over output after processes are started primitive; use the Sun window system if you need better output control.

The only way to direct the standard output and standard error is separately by invoking a subshell, as follows:

```
# (command) > outfile
```

# Variable Substitution

The shell maintains a set of variables, each of which is composed of a name and a value. A variable name consists of up to 20 letters and digits, and starts with a letter (the underscore is considered a letter). A variable s value is a space-separated list of zero or more words.

To refer to a variable, precede it with a dollar ($). You can use certain references (described below) to select specific words from the variable or to display information about it. You can use braces to insulate the reference from other characters in an input-line word.

Variable substitution takes place after the line is analyzed, aliases are resolved, and I/O redirections are applied. Variable references in I/O redirections and quoted strings, however, are substituted at the time the redirection is made.

You can suppress substitution by preceding the $ with a \, except within double quotes. Variable substitution is suppressed inside of single quotes. A $ is followed by a space character, Tab, or newline.

You can use the set and unset commands to create, display, or destroy variables. Some variables are maintained or used by the shell. For instance, the argv variable contains an image of the shell argument argument list. Of the variables used by the shell, a number are toggles; the shell does not care what their value is, only whether they are set or not.

You can operate on numerical values as numbers (as with the built-in command). With numeric operations, an empty value is considered to be 0; the second
