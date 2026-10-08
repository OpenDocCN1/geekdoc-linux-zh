
# Advanced Bash-Scripting Guide

```bash
read name                     # Reads from redirected stdin ($Filename)
let echo "count += 1"
done                           # Loop reads from file $Filename because of line 20
```

# The original version of this script terminated the "while" loop with
# done <"$Filename"
# Exercise:
# Why is this unnecessary?

```bash
exec 0<&3                     # Restore old stdin.
exec 2<&-                      # Close temporary fd 3.
echo "$count names read"; echo
```

exit 0

# Example 20-7. Redirected until loop

```bash
#!/bin/bash
# Same as previous example, but with "until" loop

if [ -z "$1" ]; then
    Filename=names.data        # Default, if no filename specified
else
    Filename=$1
fi

while [ "$name" != Smith ];
until [ "$name" = Smith ];   # Change != to =
do
    read name                   # Reads from $Filename, rather than stdin.
    echo $name
done <"$Filename"          # Redirects stdin to file $Filename.
~~~~~~~~~~~~~
# Same results as with "while" loop in previous example.
```

exit 0

# Example 20-8. Redirected for loop

```bash
#!/bin/bash

if [ -z "$1" ]; then
    Filename=names.data        # Default, if no filename specified
else
    Filename=$1
fi
```

```bash
line_count=`wc $Filename | awk '{ print $1 }`
# Number of lines in target file.
#
# Very contrived and kludgy, nevertheless shows that
# it's possible to redirect stdin within a "for" loop...
# if you're clever enough.
```

# Chapter 20. I/O Redirection

# Advanced Bash-Scripting Guide

# More concise is line_count=$(wc -l < "$Filename")

```bash
for name in $(seq $line_count); # Recall that "seq" prints sequence of numbers.
while [ "$name" != Smith ]; do -- more complicated than a "while" loop
do
  read name
  echo $name
  if [ "$name" = Smith ]; # We need all this extra baggage.
  then
    break
  fi
done <"$Filename" # Redirects stdin to file $Filename.
```

exit 0

We can modify the previous example to redirect the output of the loop.

# Example 20-9. Redirected for loop (both stdin and stdout redirected)

```bash
#!/bin/bash
if [ -z "$1" ]; then
  Filename=names.data # Default, if no filename specified.
else
  Filename=$1
fi
Savefile=$Filename.new # Filename to save results in.
FinalName=Jonah # Name to terminate "read" on.
line_count=`wc $Filename | awk '{ print $1 }'` # Number of lines in target file.
for name in $(seq $line_count);
do
  read name
  echo "$name"
  if [ "$name" = "$FinalName" ];
then
    break
  fi
done < "$Filename" > "$Savefile" # Redirects stdin to file $Filename, and saves it to backup file.
exit 0
```

# Example 20-10. Redirected if/then test

```bash
#!/bin/bash
if [ -z "$1" ]; then
  Filename=names.data # Default, if no filename specified.
else
  Filename=$1
fi
```

Chapter 20. I/O Redirection

```bash
TRUE=1
if [ "$TRUE" ]; then # if and if also work.
  read name
  echo $name
fi <"$Filename"
# Reads only first line of file. 
# An "if/then" test has no way of iterating unless embedded in a loop.
exit 0

# Example 20-11. Data file names above
- Aristotle
- Arrhenius
- Belisarius
- Capablanca
- Dickens
- Euler
- Goethe
- Hegel
- Jonah
- Laplace
- Maroc
- Purcell
- Schmidt
- Schopenhauer
- Semmelweiss
- Smith
- Steinmetz
- Tukhevsky
- Turing
- Venn
- Warsawski
- Znosko
- Borowski

# This is a data file for "redir2.sh", "redir3.sh", "redir4.sh", "redir5.sh".
# Redirecting the stdout of a block has the effect of saving its output to a file.
# See Example 20-2. documents are special case of redirected blocks.

```bash
function doesOutput() {
  # Could be external command, of course.
  # Here show you can use a function as well.
  ls -al | awk '{print $5}'
}

nr=0 # We want the loop to be able to manipulate these
totalSize=0 # to be able to see the changes after 'while' finished.

while read fileName; do
  echo "$fileName is $fileSize bytes"
  let totalSize=$((totalSize+fileSize)) # Or: let totalSize+=fileSize
done<<EOF
$(doesOutput)
EOF

echo "$nr files totaling $totalSize bytes"
```

```bash
#!/bin/bash
# logevents.sh
# Author: Stephane Chelas.
# Used with permission.

# Event logging to a file.
# Must be run as root (for write access in /var/log).

ROOT_UID=0 # Only users with UID 0 have root privileges.
E_NOTROOT=1 # Non-root error.

if [ "$UID" -ne "$ROOT_UID" ]; then
    echo "Must be root to run this script."
    exit $E_NOTROOT
fi

FD_DEBUG=1
FD_DEBUG=2
FD_DEBUG=3

# --- Uncomment one of the lines below to activate script ---
# LOG_EVENTS=1
# LOG_VAR=1

log() { # Writes time and date to log file.
{
  echo "$(date)" >&7 # This appends the date to the file.
  # command substitution
  # See below.
}
```

```bash
case $LOG_LEVEL in
1) exec 3>&2 4>/dev/null 5>/dev/null
2) exec 3>&2 5>/dev/null;
3) exec 3>&2 4>&2 5>&2;
*) exec 3 >dev/null 4 >dev/null 5>/dev/null;
esac

FD_LOG_VARS=6
if [[ $LOG_VARS ]]; then 
    exec 6>> /var/log/vars.log # Bury output.
else 
    exec 6 >/dev/null
fi

FD_LOG_EVENTS=7
if [[ $LOG_EVENTS ]]; then 
    # exec 7 >(awk '{print strftime(), $0}') >> # Above line fails in versions of Bash more recent than 2.04. Why?
    exec 7>> /var/log/event.log # Append to "event.log"
    log # Write time and date.
    # Bury output.
else 
    exec 7 >/dev/null
fi

echo "DEBUG3: beginning" >${FD_DEBUG3}
ls -1 >5 2>&4 # command1 >5 2>&4
echo "Done" # command2
echo "sending mail" >&${FD_LOG_EVENTS} # Writes "sending mail" to file descriptor #7.
```

exit 0

# Chapter 21. Subshells

Running a script launches a new process, a *subshell*.

**Subshell**: A subshell is a child process launched by a shell (or shell script) -- the shell that gives you the prompt at the console or in an xterm window. As your commands are interpreted as the command-line prompt, similarly does a script batch-process a list of commands. Each shell script running is, in effect, a subprocess (child process) of the parent shell.

A shell script can launch itself subprocesses. These *subshells* let the script do parallel processing, in effect executing multiple tasks simultaneously.

```bash
#!/bin/bash
# subshell-test.sh
(
  # Inside parentheses, and therefore a subshell
  while [ "$name" != Smith ]; do
    read name
    echo $name
  done <"$Filename"
)
```

# **List Command within Parentheses**

A command list between parentheses runs as a subshell. Variables in a subshell are not visible outside the block. They are not accessible to the shell that launched the subshell. These are, in fact, variables local to the child process.

# Example 21-1. Variable scope in a subshell

```bash
#!/bin/bash
# subshell.sh
echo
echo "We are outside the subshell."
echo "Subshell level OUTSIDE subshell = $BASH_SUBSLL"

echo

outer_variable=Outer
global_variable=
# Define global variable for "storage" of
# value of subshell variable.
(
echo "We are inside the subshell."
echo "Subshell level INSIDE subshell = $BASH_SUBSLL"
inner_variable=Inner

echo "From inside subshell, \inner_variable\" = $inner_variable"
echo "From inside subshell, \"outer\" = $outer_variable"

global_variable="$inner_variable"    # This will allow "exporting"
# a subshell variable?
)
echo
echo "We are outside the subshell."
echo "Subshell level OUTSIDE subshell = $BASH_SUBSLL"

if [ -z "$inner_variable" ]; then
    echo "inner_variable undefined in main body of shell"
else
    echo "inner_variable defined in main body of shell"
fi

echo "From main body of shell, \inner_variable\" = $inner_Variable"
# $inner_variable will show as blank (uninitialized)
# because variables defined in a subshell are "local variables".
# Is there a remedy for this?
echo "global_variable = \$global_variable*"" # Why doesn't this work?
echo
```
