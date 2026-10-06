
```bash
# numbers.sh: let oct = 081: value too great for base (error token "081")
# Octal numbers use only digits in the range of 0 - 7.

exit 0
# Thanks, Rich Bartell and Stephane Chazelas, for clarification.
```

# Part 3. Beyond the Basics

+ Table of Contents
9. Variables Revisited
  9.1. Manipulating Strings
  9.2. Parameter Substitution
  9.3. Typing variables: declare or typeset
  9.4. Indirect References to Variables
  9.5. SRAND: generate random integer
  9.6. The Double Parentheses Construct
10. Loops and Branches
  10.1. Loops
  10.2. Nested Loops
  10.3. Loop Control
  10.4. Testing and Branching
11. Internal Commands and Builtins
  11.1. Job Control
12. External Filters, Programs and Commands
  12.1. Basic Commands
  12.2. Complex Commands
  12.3. Time / Commands
  12.4. Text Processing Commands
  12.5. File and Archiving Commands
  12.6. Communications Commands
  12.7. Terminal Commands
  12.8. Math Commands
  12.9. Miscellaneous Commands
13. System and Administrative Commands
14. Command Substitution
15. Arithmetic Expansion
16. I/O Redirection
  16.1. Using exec
  16.2. Redirecting Code Blocks
  16.3. Applications
17. Here Documents
18. Time

## Chapter 9. Variables Revisited

Used properly, variables can add power and flexibility to scripts. This requires learning their subtleties and nuances.

### 9.1. Internal Variables

Built-in variables affecting bash behavior:

```bash
$BASH
the path to the Bash binary, usually /bin/bash
```

```bash
$BASH_ENV
an environmental variable pointing to a Bash startup file to be read when a script is invoked
```

```bash
$BASH_VERSINFO[n]
an array containing version information about the installed release of Bash. This is similar to $BASH_VERSION, below, but a bit more detailed.
```

```bash
# Bash version:
for n in 0 1 2 3 4 5; do
  echo "${BASH_VERSINFO[$n]}"
done
# BASH_VERSINFO[0] = 2 # Major version no.
# BASH_VERSINFO[1] = 0 # Minor version no.
# BASH_VERSINFO[2] = 1 # Patch level.
# BASH_VERSINFO[3] = 1 # Build version.
# BASH_VERSINFO[4] = release # Release status.
# BASH_VERSINFO[5] = 13-redhat-gnu # Architecture (same as $HOSTNAME).
```

```bash
$BASH_VERSION
the version of Bash installed on the system
```

```bash
bash$ echo $BASH_VERSION
2.0.4
```

```bash
tcsh% echo $BASH_VERSION
BASH_VERSION: Undefined variable.
```

Checking $BASH_VERSION is a good method of determining which shell is running. Shell does not necessarily give the correct answer.

$DIRSTACK
the top value in the directory stack. pushd and popd correspond to the dirs command, however dirs shows the entire contents of the directory stack.

$EDITOR
the default editor invoked by a script, usually vi or emacs.

$EUID
"effective" user id number of whatever the current user has assumed, perhaps by su. The $EUID is not necessarily the same as $SUID.

$FUNCN
name of the current function

```bash
xyz2 () {
  echo "$FUNCN now executing."
}
xyz2
echo "$FUNCN" # Null value outside a function.
xyz2
echo "$FUNCN" # Name of function.
```

$GLOBIGNORE
A list of filename patterns excluded from matching in glob.

$GROUPS
groups current user belongs to is a listing (array) of group ids for current user, recorded in /etc/passwd.

```bash
root$ echo $GROUPS
0
root$ echo ${GROUPS[1]}
1
root$ echo ${GROUPS[5]}
6
```

$HOME
home directory of the user, usually /home/username (see Example 9–12).

$HOSTNAME
The hostname assigns the system name at bootup in an init script. However, the hostname () function sets the Bash variable $HOSTNAME. See also Example 9–12.

$HOSTTYPE
host type Like $MACHTYPE, identifies the system hardware.

```bash
bash$ echo $HOSTTYPE
```

$IFS
input field separator. This defaults to whitespace (space, tab, and newline), but may be changed, for example, to parse a comma-separated data file. Note that $* uses the first character in $IFS. See Example 6–1.

```bash
bash$ echo $IFS | cat -v
bash$ bash -c 'set w y z; IFS=";"; echo "$*"'
w:y:z
```

$IFS does not handle whitespace the same as it does characters. Example 9, $IFS and whitespace

```bash
#!/bin/bash
# $IFS treats whitespace differently than other characters.

output_args_per_line() {
  for arg; do
    echo "[$arg]"
  done
}
echo; echo "$IFS=$*"
echo "----------------"
```

Chapter 9. Variables Revisited

```bash
IFS=" "
var=" a b c "
output_args_per_line $var # output_args_per_line "echo a b c ""

# [a]
# [b]
# [c]

echo; echo IFS=:
echo ""

IFS=:
var=:a::b:: # Same as above, substitute ":" for "
output_args_per_line $var
# [a]
# [b]
# [c]

# The same thing happens with the "FS" field separator in awk.

# Thank you, Stephane Chazelas.
# exit 0
```

(Thanks, S. C., for clarification and examples.)

$IGNOREEOF
ignore EOF: how many end–of–files (control–D) the shell will ignore before logging out.

$LC_COLLATE
Often set in .bashrc or /etc/profile files, this variable controls collation order in filename expansion and pattern matching. If mishandled, LC_COLLATE can cause unexpected results in filename globbing.

![](img/1ce1edffaa3e4f698a85430e71c6d3b_71_0.png)

As of version 2.05 of Bash, filename globbing no longer distinguishes lowercase and uppercase letters in a character range between brackets. For example, b [A-M]* would match File1.txt and file1.txt. To revert the custom behavior of bracket matching, set LC_COLLATE to C by an export LC_COLLATE=C in /etc/profile and/or ~/.bashrc.

$LC_CTYPE
This internal variable controls character interpretation in globbing and pattern matching.

$LINENO
This variable is the line number of the shell script in which this variable appears. It has significance only within the script in which it appears, and is chiefly useful for debugging purposes.

```bash
last_cmd_arg=$# Save it.
echo "At line number $LINENO, v1 = $v1"
echo "Last command argument processed = $last_cmd_arg"
```

$MACHCTYPE
machine type Identifies the shell hardware.

```bash
bash$ echo $MACHCTYPE
```

$OLDPWD
old working directory (previous directory you were in)

$OSTYPE
operating system type

```bash
bash$ echo $OSTYPE
```

$PATH
path to binaries, usually /bin/, /usr/local/bin/, etc. When given a command, the shell automatically does a search on the directories listed in $PATH. The system stores the $PATH definition in /etc/profile and/or ~/.bashrc. It may be expedient to temporarily add a directory to the path in this way. When a script exits, it restores the original $PATH (a child process, such as a script, may not change the environment of the parent process, the shell).

![](img/1ce1edffaa3e4f698a85430e71c6d3b_72_0.png)

The current "working directory". is omitted from the $PATH as a security measure.

$PIPETYPE
Exit status of last executed pipe. Interestingly enough, this does not give the same result as the exit status of the last executed command.

```bash
bash$ echo $PIPSTATUS
0

bash$ ls -al | bogus_command
bash: bogus_command: command not found
bash$ echo $PIPSTATUS
141

bash$ ls -al | bogus_command
bash: bogus_command: command not found
bash$ echo $?
127
```
