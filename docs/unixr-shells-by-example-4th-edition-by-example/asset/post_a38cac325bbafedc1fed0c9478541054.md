
```ksh
% set -o noglob        # or set -f
% print -r -- [?] $LOGNAME
% ?? [] /home/jody/ellie/ellie
% set +o noglob        # or set +f
```

## EXPLANATION

- 1. The noglob variable is set. It turns off the special meaning of the wildcards for file-name expansion. You can use the -f option to set the command to achieve the same results.
- 2. The filename expansion metacharacters are displayed as themselves without any interpretation. Note that the tilde and the dollar sign are still expanded.
- 3. The noglob option is reset. Filename metacharacters will be expanded.

## 11.9 Variables

### 11.9.1 Local Variables

Local variables are given values that are known only to the shell in which they are created. Variable names must begin with an alphabetic or underscore character. The remaining characters can be alphabetic, decimal digits zero to nine, or an underscore character. Any other characters mark the termination of the variable name.

**Setting and Referencing Local Variables.** When assigning a value to a variable, there can be no whitespace surrounding the equal sign. To set the variable to null, the equal sign is followed by nothing. If more than one word is assigned to a variable, it must be quoted to protect the characters; otherwise, the shell prints an error message and the variable is undefined.

If a dollar sign is prepended to the variable name, the value assigned to that variable can be referenced. If other characters are attached to a variable name, curly braces are used to shield the name of the variable from the extra characters.

## EXAMPLE 11.34

```ksh
1  $ state=Cal
   $ echo $state
   Cal
2  $ name="Peter Piper"
   $ echo $name
   Peter Piper
```

## EXAMPLE 11.34 (CONTINUED)

```
3  $ x=
$ echo $x

# Blank line appears when a variable is either unset or set to null
$
4  $ state=Ca
$ print ${state}ifornia
California
```

## EXPLANATION

- 1 The variable state is assigned the value Cal. When the shell encounters the dollar sign preceding a variable name, it performs variable substitution. The value of the variable is displayed.
- 2 The variable name is assigned the value "Peter Piper". The quotes are needed to hide the whitespace so that the shell will not split the string into separate words when it parses the command line. The value of the variable is displayed.
- 3 The variable x is not assigned a value. It will be assigned a null string. The null value, an empty string, is displayed. The same output would be displayed if the variable had not been set at all.
- 4 The variable state is assigned the value Ca. The variable is enclosed in curly braces to shield it from the characters that are appended. The value of the variable Ca is displayed with ifornia appended.

### The Scope of Local Variables.

A local variable is known only to the shell in which it was created. It is not passed on to subshells. The $$ variable is a special variable containing the PID of the current shell.

## EXAMPLE 11.35

```
1  $ echo $$
1313
2  $ round=world
$ echo $round
world
3  $ ksh   # Start a subshell
4  $ echo $$
1326
5  $ echo $round
6  $ exit   # Exits this shell, returns to parent shell
7  $ echo $$
1313
8  $ echo $round
world
```

## EXPLANATION

- 1 The value of the $$ variable evaluates to the PID of the current shell. The PID of this shell is 1313.
- 2 The local variable round is assigned the string value world and the value of the variable is displayed.
- 3 A new Korn shell is invoked. This is called a subshell, or child shell.
- 4 The PID of this shell is 1326. The parent shell's PID is 1313.
- 5 The variable round is not defined in this shell.
- 6 The exit command terminates this shell and returns to the parent shell. If the ignoreeof option is not set, Ctrl-D will also exit this shell.
- 7 The parent shell returns. Its PID is displayed.
- 8 The value of the variable is displayed.

### Setting Read-Only Variables.

A read-only variable cannot be redefined or unset. It can be set with the readonly or typeset -r built-in commands. You may want to set variables to readonly for security reasons when running in privileged mode.

## EXAMPLE 11.36

```
1 $ readonly name=Tom
$ print $name
Tom
2 $ unset name
ksh: name: is read only
3 $ name=Joe
ksh: name: is read only
4 $ typeset -r PATH
$ PATH=${PATH}:/usr/local/bin
ksh: PATH: is read only
```

## EXPLANATION

- 1 The readonly local variable name is assigned the value Tom.
- 2 A readonly variable cannot be unset.
- 3 A readonly variable cannot be redefined.
- 4 The PATH variable is set to be readonly. Any effort to unset or change the variable will produce an error message.

### 11.9.2 Environment Variables

Environment variables are available to the shell in which they are created and any subshells or processes spawned from that shell. By convention, environment variables are capitalized.
