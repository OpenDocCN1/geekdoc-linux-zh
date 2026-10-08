
# Part 3. Beyond the Basics

## Table of Contents

- 9. Another Look at Variables
- 9.1. Internal Variables
- 9.2. Typing variables: declare or typeset
- 9.3. $RANDOM: generate random integer
- 10 Manipulating Variables
- 10.1. Manipulating Strings
- 10.2. Parameter Substitution
- 11 Loops and Branches
- 11.1. Loops
- 11.2. Nested Loops
- 11.3. Loop Control
- 11.4. Testing and Branching
- 12 Command Substitution
- 13 Arithmetic Expansion
- 14 Recess Time

# Chapter 9. Another Look at Variables

Used properly, variables can add power and flexibility to scripts. This requires learning their subtleties and nuances.

## 9.1. Internal Variables

Builtin variables:
variables affecting bash script behavior

$BASH
The path to the Bash binary itself

```bash
bash$ echo $BASH
/bin/bash
```

$BASH_ENV
an environmental variable pointing to a Bash startup file to be read when a script is invoked

$BASH_SUBSHELL
A variable indicating the subshell level. This is a new addition to Bash, version 3.

See Example 21-1 for usage.

$BASHPID
Process ID of the current instance of Bash. This is not the same as the $$ variable, but often gives the same result.

```bash
bash4$ echo $$
11015

bash4$ echo $BASHPID
11015

bash4$ ps ax | grep bash4
11015 pts/2	R	0:00 bash4
```

But...
!/bin/bash

```bash
echo "$ outside of subshell = $"	# 9602
echo "$BASH_SUBSHELL outside of subshell = $BASH_SUBSHELL" # 0
echo "$BASHPID inside of subshell = $BASHPID" # 9602
```

$echo
( 6-element array containing version information about the installed release of Bash. This is $BASH_VERSION, but a bit more detailed.

```bash
echo "$ outside of subshell = $"	# 9602
echo "$BASH_SUBSHELL inside of subshell = $BASH_SUBSHELL" # 1
echo "$BASHPID inside of subshell = $BASHPID" # 9603
# Note that $ returns PID of parent process.
```

$BASH_INFO[n]

```bash
# Bash version info:
for n in 0 1 2 3 4 5
do
  echo "BASH_INFO[$n] = ${BASH_INFO[$n]}"
done
```

```bash
# BASH_INFO[0] = 3 # Major version no.
# BASH_INFO[1] = 00 # Minor version no.
# BASH_INFO[2] = 14 # Patch level.
# BASH_INFO[3] = 1 # Build version.
# BASH_INFO[4] = release # Release status.
# BASH_INFO[5] = 1386-redhat-linux-gnu # Architecture
# (same as $MACHYPE)
```

$BASH_VERSION
The version of bash installed on the system

```bash
bash$ echo $BASH_VERSION
3.2.25(1)-release
```

```bash
tcsh$ echo $BASH_VERSION
BASH_VERSION: Undefined variable.
```

Checking $BASH_VERSION is a good method of determining which shell is running. SHELL does not necessarily give the correct answer.

$CDPATH
A colon-separated list of search paths available to the cd command, similar in function to the PATH variable for binaries. $CDPATH variable may be set in the local ~/.bashrc file.

```bash
bash$ cd bash-doc
bash: bash-doc: No such file or directory
```

```bash
bash$ CDPATH=/usr/share/doc
bash$ cd bash-doc
/usr/share/doc/bash-doc
```

```bash
bash$ echo $PWD
/usr/share/doc/bash-doc
```

$DIRSTACK
The value in the directory stack (affected by pushd and popd). This builtin variable corresponds to dirs command, however shows the entire contents of the directory stack.

$EDITOR
The default editor invoked by a script, usually vi or emacs.

$UID
Identification number of the current user has assumed, perhaps by su. The UID is not necessarily the same as SUID.

$FUNAME
Name of the current function

```bash
xyz()() {
  echo "$FUNAME now executing."
}
xyz()
echo "$FUNAME" # Null value outside a function.
```

$GLOBIGNORE
list of filename patterns be excluded from matching in globbing.

$GROUPS
Groups current user belongs to (array) of numbers recorded in /etc/passwd.

```bash
root# echo $GROUPS
0
root# echo ${GROUPS[1]}
1
root# echo ${GROUPS[5]}
6
```

$HOME
Home directory of the user, /home/username (see Example 10-7).

$HOSTNAME
The hostname command assigns the system host at boot in init script. However, hostname() function sets $HOSTNAME. Also see Example 10-7.

$HOSTTYPE
host type Like $MACHTYPE identifies the hardware.

$IFS
internal field separator. This variable determines how Bash recognizes fields, or word boundaries, when interprets strings. $IFS defaults to (space, tab, and newline), but be changed, for example to parse comma-separated data. Note that $* uses the first character held in $IFS. See Example 5-1.

```bash
bash$ echo "$IFS"
With $IFS set to default, a blank line displays.)bash$ echo "$IFS" | cat -v
(Show whitespace: here a single space, horizontal tab, and newline, and display at end-of-line.)
```

$IFS=$(printf '\n\t') # Per David Wheeler. Set whitespace in path. $IFS does not handle whitespace same as other characters.

```bash
#!/bin/bash
# ifs.sh

var1="a b"
var2="d e"
var3="g h"

IFS+= # The plus sign will be interpreted as a separator.
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h
```

IFS="-" # The minus sign reverts to default interpretation. The minus sign will be interpreted as a separator.
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h

```

IFS="," # The comma will be interpreted as a separator. The minus sign reverts to default interpretation.
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h

```

IFS=" " # The space character will be interpreted as a separator. The comma reverts to default interpretation.
echo $var1 # a b
echo $var2 # d e
echo $var3 # g h

############################################
# However $IFS treats whitespace differently than other characters.

output_args_one_per_line() {
  for arg in "$arg"
  do
    echo "[$arg]"
  done # Embed within brackets, for your pleasure. thanks, Stéphane Chazelas, for clarification and above examples.) See also Example 16-41, Example 11-8, and Example 19-14 for instructive examples of using $IFS.

$IGNOREEOF:how many end-of-files (control-D) the shell will ignore before logging out.

$LC_COLLATE
Often set in the .bashrc or /etc/profile files, these variables control collation order in filename expansion and pattern matching. LC_COLLATE can cause unexpected results in filename globbing. As version 2.05 of Bash, filename no longer distinguishes between lowercase and uppercase letters in a character range. For example, ls [A-M] would match File1.txt and file.txt. To revert to the customary behavior of matching, set LC_COLLATE to C by export LC_COLLATE=C in /etc/profile and/or ~/.bashrc.

$LC_CTYPE

$LINENO This variable controls character interpretation in globbing and pattern matching. This variable is the line number of the shell script in which variable appears only within the script in which it appears, and is useful for debugging purposes.

```bash
### BEGIN DEBUG BLOCK ***
last_cmd_arg=$ Save it.
echo "At line number $LINENO, variable \"v1\" = $v1"
echo "Last command argument processed = $last_cmd_arg"
### END DEBUG BLOCK ***
```

$MACHTYPE
machine type identifies the hardware.

```bash
bash$ $MACHTYPE
i686
```

$OLDPWD
Old working directory "OLD-Print-Working-Directory", previous directory you were in.

$OSTYPE
operating system type

```bash
bash$ $OSTYPE
linux
```

$PATH Path to binaries, usually /usr/bin/, /usr/X1R6/bin/, /usr/local/bin/, etc. When a command is called, the shell automatically does a hash search on the directories listed in the path. The path is stored in the environmental variable, PATH, a list of directories. Normally, the system uses $PATH definition in /etc/profile and/or ~/.bashrc (Appendix H).

```bash
bash$ $PATH
/bin:/usr/bin:/usr/local/bin:/usr/X1R6/bin:/sbin:/usr/sbin
```
