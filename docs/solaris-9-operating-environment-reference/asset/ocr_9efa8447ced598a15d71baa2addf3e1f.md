# echo

# 287

The following example shows that the 3-digit syntax produces the correct results.
$ echo "\00337\" | od -xc
0000000  1b37  0a00
         033  7 \n
000003 $

For the octal sequences of each character, see ascii(5).

# Usage

Portable applications should not use -n(as the first argument) or escape sequences.
The printf(1) command can be used portably to emulate any of the traditional behaviors of
t echo command as follows.
The Solaris 2.x /usr/bin/echo is equivalent to:
printf "%b\n" "$*",

```
The /usr/ucb/echo is equivalent to:
if ["X$1" = "X-n"]
then
  shift
  printf "%s" "$*"
else
  printf "%s\n" "$*"
fi
```

New applications are encouraged to use printf instead of echo.

# Examples

You can use the echo command to display the value for a variable by preceding the
variable name with a dollar sign ($). The following example displays the values for the
PATH environment variable.

```
castle$ echo $PATH
/usr/overwin/bin:/usr/dt:/bin:/bin:/usr/bin:/usr/sbin:/usr/ucb:/etc:/usr
/proc/bin:/opt/hnp/bin:/usr/local/games:
caste$
```

The following example shows how you can use the echo command in combination
with tr and wc commands to determine how many subdirectories are between the
root directory (/) and your current directory. The example has the following parts:

+   * Echo the full path of your current working directory.
* Pipe the output through tr to translate the path's embedded slash characters into
space characters.
* Pipe that output through wc -w for a count of the names in your path.

```
castle$ /usr/bin/echo tr '/' ' ' | wc -w
3ncaste$
```

See tr(1) and wc(1) for their functionality.