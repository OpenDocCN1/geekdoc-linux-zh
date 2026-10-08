# Advanced Bash-Scripting Guide

$FUNCNAME
Name of the current function

```
xyz23 ()
{
  echo "$FUNCNAME now executing."  # xyz23 now executing.
}
xyz23

echo "$FUNCNAME = $FUNCNAME"
  # Null value outside a function.
```

See also Example A-50.
$GLOBIGNOREnA list of filename patterns to be excluded from matching in globbing.

$GROUPS
Groups current user belongs to

This is a list (array) of the group id numbers for current user, as recorded in /etc/passwd and /etc/group.

```
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
The hostname command assigns the system host name at bootrap in an init script. However, the gethostname() function sets the Bash internal variable $HOSTNAME. Also see Example 10-7.

$HOSTTYPE
host type
Like $MACHTYPE, identifies the system hardware.

```
bash$ echo $HOSTTYPE
i3686
```

$IFS
internal field separator
This variable determines how Bash recognizes fields, or word boundaries, when it interprets character strings.

$IFS defaults to whitespace (space, tab, and newline), but may be changed, for example, to parse a comma-separated data file. Note that $* uses the first character held in $IFS. See Example 5-1.

Chapter 9. Another Look at Variables