
to preface the variable name.

These variables exist in two domains—the first is local to the shell and the other is part of a global environment common to this process and all child processes. Local variables are inherited only by child shells. The global environment is outside of the shell and is inherited by any kind of process started by the shell. The shell looks for a variable definition first in the local environment and then in the global environment. Some of the shell variables are automatically set by the shell, others are set through explicit commands. All global variables are set through explicit commands.

For example, every time a child process completes execution, the C shell variable accessed as $status is set to indicate success or failure of that process. (The Bourne shell addresses this status variable as $?.) The shell variable notify is explicitly set by a command in the shell start-up file. The global variable HOSTNAME has the value grieg.seaslug.org on my system.

## Control of execution

Most shells provide methods to control the order of execution. In this respect, they are considered to support a proper programming language.

### Sequencing and Grouping

To begin with, these shells use a special token, usually “;”, to separate multiple commands on a single command line. The semantics are that the command to the left of the “;” is executed and then the command to the right of the “;” is executed. Parenthesis can be used to group commands so that they are treated as a single command by other parts of the command line.

For example, when the example on page 41 is decoded, date sees its own name as the only argument and echo sees its own name as the initial argument and “hello world” as the next argument. Neither command sees the parenthesis nor the redirection as any part of its arguments. The parentheses tell the shell that the redirection is to be applied to each of the commands.

Other tokens, described below, not only separate commands on a line, but describe additional actions to be performed by the shell.

### Parallel Execution

Another separator, "&", directs that the proceeding command is started as before, but the shell does not wait for that command to finish before starting the subsequent command. The proceeding command is said to be running in the background.

If nothing special is done, the output of both commands are intermingled on the display and both commands can attempt to read data from the keyboard. This potential problem is solved through the use of redirection described earlier on page 43. One can, for instance, issue the command

```
command1 > result1 & command2 > result2
```

and not have to worry about intermingled results.

### Coordinated Parallel Execution

When two commands are separated by the "|" token, they are executed in parallel. The output of the first command is passed through a pipe to become the input to the second command.

The implementation of the pipe involves an internal buffer and, as long as the rate of the production and consumption of data are matched, both commands run at full speed. If the producer gets ahead, the buffer fills and the producer is blocked until some of the data have been read. If the consumer empties the buffer, it is blocked until more data are written.

Because of this buffering, one can string together programs that generate or operate on potentially infinite streams of text. For instance, in this command

```
$ monitor my_device | uniq | timestamp.pl
```

the first process continuously shows the status of a device, a second process filters out all but lines which differ from the previous line, and the last process will prefix them with a timestamp. Figure 3.1 shows the timestamp.pl program. (If the pipeline buffer was implemented with a file which had to close before the consumer could start, the consumer might never start. If the pipeline buffer had to fill before the consumer started, the operation would stutter. Neither problem occurs in Linux.)

```
#!/usr/bin/perl
# this is the file named "timestamp.pl"
while (<>) {
    $stamp = `/bin/date +"a %b %d %T %Z %Y"`;
    chop($stamp);
    print $stamp, " ", $_;
}
```

![](img/bd9544b8c1ad3b1347c84630c5d698e1_70_0.png)

Processes can also co-ordinate their efforts with the use of named pipes and semaphores. These are discussed further in Sections 5.3.3 and 5.2.4 respectively.

## Selection

From our knowledge of ordinary programming languages, we know that there are a multitude of ways to express conditional execution. We further know that there are many ways of expressing the same algorithmic construct using alternative syntactic forms. For instance

```
if ( condition ) then action
if ( not condition ) then alternate_action
```

can be recast as

```
if ( condition )
    then action
    else alternate_action
end if
```

or

```
condition ? action : alternate_action
```

## Bourne Shell

Conditional statements differ in syntactic details among the shells, but in all cases they offer fundamentally the same capability. The most widely known shell, the “Bourne shell” (sh), has a conditional statement which relies on the status value returned by all Linux commands. The syntax of the basic conditional command is

```
if list; then list; fi
```

where `list` represents a list of `;` separated commands. The status of the last command in the first list is used to determine if the second list is to be executed. The “Korn shell” (ksh) and the “Bourne again shell” (bash) provide strictly upwardly compatible extensions to the Bourne shell.

The command

```
if false; true; then date; fi
```

first executes **false** and then executes **true**. (The external commands **true** and **false** are provided by the system.) As a result of the **true** command returning success, the conditional command executes `date`. In contrast, the command

```
if true; false; then date; fi
```

first executes **true** and then executes **false**. As a result of the **false** command returning failure, the `date` command is not executed.

## C Shell

The C shell (csh) has a slightly different approach to evaluating the predicate of the conditional statement. Instead of executing a list of commands, the C shell evaluates an expression using the C-like syntax:

```
if ( expression ) command
```

or

```
if( expression ) then
 commands
 endif
```

The expression which executes the command within “{” and “}” returns a 1 if the command was successful. (Both csh and its descendant tcsh require that there be whitespace between the brackets and the command. Whitespace is optional on either side of the parenthesis.) The commands

```
if(1)date
```

and

```
if({ true })date
```

have the same results.

All these advanced shells have two additional forms of conditional statements. The separator token “&&”, read as “and then”, means that the second command is to be executed only if the first command returned success. The separator token “||”, read as “or else”, means that the second command is to be executed only if the first command returned failure.

Some of these advanced shells have some form of case or switch command. The selectors in these commands generally apply to patterns rather than integer values. This makes these commands useful for parsing command line options in a shell script.

## Iteration

The last necessary language feature is used to repeat commands. All these advanced shells have two forms of iteration command. The first iterates over a list and the second iterates while some condition is met.

## Bourne Shell

The Bourne shell and its descendants use the syntax:

```
for name do list ;done
for name in wordlist ;do list ;done
while list;do list;done
```

The first form iterates over all the arguments to the shell—which is most useful when the shell is processing a shell script. The second form is useful both in shell scripts and when used as an interactive command. The elements of the list do not have to be entered individually. It is possible to use file name expansion (wild cards) and variable substitution (both described earlier) to build the list. For example

```
for name in *; do echo $name ;done
```

writes a list of all the files in the current working directory.

The third form iterates as long as the last command in the first list returns success.

## C Shell

The C shell and its descendants have the syntax:

```
foreach name(wordlist)
  commands
end
```

```
while(expression)
  commands
end
```

Again you can see that the C shell relies on expressions rather than the results of command execution. It also requires that these commands be presented in a multi-line format. When commands are entered via the keyboard, the shell will present a secondary prompt to ask for the rest of the command.

Appendix E has additional shell syntax.

> You can circumvent the multi-line requirement if you trick the keystroke processing to permit a Control-J to appear where you would type <RETURN> or <ENTER>. Control-J is the code for <LINE FEED>, also called <NEWLINE>, so this effort causes the shell to see the end-of-line it wants, but the screen isn’t cluttered with the extra lines.
