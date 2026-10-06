
# Advanced Bash–Scripting Guide

```
command1 2>& | command2 # Also futile.

Thanks, S.C.
```

Using Bash version2+ functionality may cause a bailout with error messages. Older Linux machines have version 1.XX of Bash as the default installation.

```bash
#!/bin/bash

minimum_version=2
# Since Chet Ramey is constantly adding features to Bash,
# you may set $minimum_version to 2.XX, or whatever is appropriate.
SE_BAD_VERSION=80

if [ "$BASH_VERSION" -lt "$minimum_version" ];
then
  echo "This script works only with Bash, version $minimum_version or greater.
  echo "Upgrade strongly recommended."
  exit $SE_BAD_VERSION
fi
```

Using Bash-specific functionality in a Bourne script (#bin/sh) on a non-Linux machine may cause unexpected behavior. A Linux system usually aliases sh to bash, which does not necessarily hold true for a generic UNIX machine.

A script with DOS-type newlines (\r) will fail to execute, since #/bin/bash\r is not recognized, not the same as the #/bin/bash. The fix is to convert the script to UNIX-style newlines.

A shell script headed #!/bin/sh may not run in Bash-compatibility mode. Bash-specific functions might be disabled. Scripts that need complete access to all the Bash-specific extensions should start with #!bin/bash.

A script may not export variables to its parent process, the shell, or the environment. Just as learned in biology, a child process can inherit from a parent, but not vice versa.

```
WHATEVER=/home/bozo
export WHATEVER
exit 0
bash$WHATEVER
bash$
```

Sure enough, back at the command prompt, $WHATEVER remains unset.

Setting and manipulating variables in a shell, attempting to use those same variables outside the scope of the shell will result in an unpleasant surprise.

# Example 32–1. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell.
```

outer_variable=outer

Chapter 32. Gotchas

# Advanced Bash–Scripting Guide

```bash
echo
echo "outer_variable = $outer_variable"
echo
(
# Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
out_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"
# End subshell
)
echo
echo "inner_variable outside subshell = $inner_variable" # Unset
echo "outer_variable outside subshell = $outer_variable" # Unchanged.
echo
```

Using "suid" commands in scripts is risky, as it may compromise system security. [61]

Using shell scripts for CGI programming may be problematic. Shell script variables are not "typesafe", and this can cause undesirable behavior as far as CGI is concerned. Moreover, it is difficult to "cracker-proof" shell scripts.

> Danger is near thee --
>
> Beware, beware, beware, beware.
>
> Many brave hearts are asleep in the deep.
>
> So beware --
>
> Beware.
> AJ. Lamb and H.W. Petrie

# Chapter 33. Scripting With Style

Get into the habit of writing shell scripts in a structured and systematic manner. Even "on–the-fly" and "written on the back of an envelope" scripts will benefit if you take a few minutes to plan and organize your thoughts before sitting down coding.

Herewith a few stylistic guidelines. This is not intended as an Official Shell Scripting Stylesheet.

# 33.1. Unofficial Shell Scripting Stylesheet

- Comment your code. This makes it easier to understand (and appreciate), and easier for you to maintain.
- PASS="$PASSES(MATRIX:$($RANDOM$(#MATRIX))):):1"
- It made perfect sense when you wrote it last year, but now it's a complete mystery.
- (From Anton Sawicki's "pw.sh" script.)

Add descriptive headers to your scripts and functions.

```bash
#!/bin/bash

****************************************************
# xyz.sh
# written by Bozo Bozman
# July 05, 2001

# Clean up project files.
****************************************************

BADDIR=65      # No such directory.
projectdir=/home/bozo/projects  # Directory to clean up.

####################################################
cleanup_files() {
# Removes all files in designated directory
# Parameter: $target_directory
# Returns: 0 on success, $BADDIR if something went wrong.
####################################################
cleanup_files() {
  if [ ! -d "$1" ]; # Test if target directory exists.
  then
    echo "$1 is not a directory."
    return $BADDIR
  fi

  rm -f "$1"*      # Success.
  return 0
}

cleanup_files $projectdir

exit 0
```

Be sure to put the #!/bin/bash at the beginning of the first line of the script, preceding any comment headers.

- Avoid using "magic numbers", [62] that is, "hard-wired" literal constants. Using meaningful variable names instead. This makes the script easier to edit and permits making changes and updates without breaking the application.

```bash
if [ -f /var/log/messages ]
then
fi
# A year later, you decide to change the script to check /var/log/syslog.
# It is now necessary to change the script, instance by instance,
# and hope nothing breaks.

# A better way:
LOGFILE=/var/log/messages # Only line that needs to be changed.
if [ -f "$LOGFILE" ]
then
fi
```

- Choose descriptive names for variables and functions.

```bash
fl='ls -al $dirname # Cryptic.
file_listing='ls -al $dirname # Better.

MAXVAL=10 # All caps used for a script constant.
while [ "$index" -le "$MAXVAL" ]
...

E_NOTFOUND=75 # Uppercase for an errorcode,
# and name begins with "E_"
if [ ! -e "$filename" ]
then
echo "File $filename not found."
exit $E_NOTFOUND
fi
```

```bash
MAIL_DIRECTORY=/var/spool/mail/bozo # Uppercase for environmental.
export MAIL_DIRECTORY
```

```bash
GetAnswer ()
{
prompt=$n
read answer
}
```

```bash
GetAnswer "What is your favorite number? "
favorite_number=$?
```

- It's better to start with underscore.

- Use exit codes in a systematic way.

```bash
E_WRONG_ARGS=65
...
exit $E_WRONG_ARGS
```

Chapter 33. Scripting With Style

309

See Appendix C.

- Break complex scripts into simpler modules. Use functions where appropriate. See Example 35–4.
- Don't use a complex construct where a simpler one will do.

```bash
if COMMAND
...
# Redundant and non-intuitive.
```

# Chapter 34. Miscellany

> Nobody really knows what the Bourne's grammar is. Even examination of the source code is little help.

Tom Duff

# 34.1. Interactive and non-interactive shells

An *interactive* shell reads commands from user input on a *tty*. Among other things, such as a shell reads startup files on activation, directs a prompt, and enables job control by default. The user can *interact* with the shell.

A shell running a script is always a non-interactive shell. All the same, the script can still access its *tty*. It is possible to eliminate an interactive shell in a script.

```bash
#!/bin/bash
MY_PROMPT='$'
while
  echo -n "$MY_PROMPT"
  read line
  eval "$LINE"
done
```

This example script, and much of the above explanation supplied by
# Stephanie Chazelas (thanks again).

Let us consider an interactive script script one that requires input from the user, usually with [read] statements (see Example 11-2). "Real life is actually a bit messy than that. For now, assume an interactive script is bound to a tty that a user has invoked from the console or an xterm.

Input start scripts are necessarily non-interactive, they must run without human intervention. Many administrative and system maintenance scripts are likewise non-interactive. Repetitive tasks cry out for automation by non-interactive scripts.

Non-interactive scripts can run in the background, but otherwise one hang, waiting for input that never comes. Handle that by having an *expect* script or embedded [here document] feed input to an interactive script running as a background job. In the simplest case, redirect a file to supply to the *read* statement (*read variable*).

If a script needs to test whether it is running in an interactive shell, it is simply a matter of finding whether the prompt variable, [PS1] is set.

```bash
if [ -z $PS1 ]; then no prompt?
then
```
316
